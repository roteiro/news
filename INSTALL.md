# Installation of this fork

Installation and updating of this fork needs to be done manually as it is not published in the app store.
The generic commands for manual installation/updating are documented in the [Nextcloud documentation](https://docs.nextcloud.com/server/stable/admin_manual/configuration_server/occ_command.html#apps-commands).
The following commands are meant as a step by step procedure. The commands assume a standard [Nextcloudpi installation](https://ownyourbits.com/nextcloudpi/). You might need to adapt the commands if your setup differs.

## Prequisites and Backup
If you have used Nextcloud News before and want to keep your feeds the easiest way is to use the opml feed export in the News web interface if you still have a working installation. Additionally you can export you unread/starred artices if you wish.

If you News installation is broken but the tables are still there in the database you'll find all your feeds in the `oc_news_feeds` table.

 You can dump the data from this table with the following commands:
```
cd /home/pi
mkdir mysql_dumps
cd mysql_dumps
sudo su
mysqldump nextcloud oc_news_feeds > dump_news_feeds.sql
```
If you want to backup all tables created by the news app continue with
```
mysqldump nextcloud oc_news_folders_ > dump_news_folders.sql
mysqldump nextcloud oc_news_items > dump_news_items.sql
```

## Installation

This procedure completely resets all news related database entries.

1. Download the newest release of this fork and unpack, e.g:
```
su pi
cd /home/pi
mkdir app_downloads
cd app_downloads
wget https://github.com/roteiro/news/releases/download/17.0.0_32-bit/news_17.0.0_32bit.tar.gz #adapt the release version
tar -xf news_17.0.0_32bit.tar.gz news/ #adapt the release version
```
2. Enable Maintenance mode and Backup old news app folder 
```
sudo -u www-data php /var/www/nextcloud/occ maintenance:mode --on
sudo su
cd /var/www/nextcloud/apps
mv news/ news_old/
```
3. Reset all News related database entries
```
mysql
use nextcloud;drop table oc_news_items;drop table oc_news_feeds;drop table oc_news_folders;DELETE  from oc_migrations where app='news';DELETE from oc_jobs where class like '%News%';DELETE from oc_appconfig where appid='news';exit;
```
4. Copy the unpacked folder to the app directory and set the correct file permissions
```
sudo su
cp -r /home/pi/app_downloads/news/ /var/www/nextcloud/apps/news/
cd /var/www/nextcloud/apps/
chown -R www-data:www-data news
```
5. Enable the app and leave maintenance mode
```
sudo -u www-data php /var/www/nextcloud/occ app:enable news
sudo -u www-data php /var/www/nextcloud/occ maintenance:mode --off
```

Go back to the web interface, check if everything is working and import you feeds.


## Preventing automatic App Store Updates
To be compatible with all clients this fork operates under the same id as the original News App. Therefore Nextcloud will offer updates from the app store which are not working on 32bit systems. The most simple way to not accidently receive those updates is to not enable auto app updates and manually update all apps but news from the appstore.

Alternatively you can use [this experimental app](https://github.com/ChristophWurst/unattended_upgrades) to auto update all apps except news. In this case you can add the following lines to your `/var/www/nextcloud/config/config.php`
```
'unattended_upgrades' => 
  array (
    'blocked' => 
    array (
      0 => 'news',
    ),
  ),
```
## Manual updating of the fork
If you wish to upgrade to a newer version of this fork repeat the procedure from the Installation section but do not reset the database.


## Building from source


```
git clone https://github.com/roteiro/news/
cd news
git checkout stable17_32bit
make clean
make no_appstore #Same as make appstore option but omits signing of the app files
```
You'll then find the app archive under `build/artifacts/no_appstore/news.tar.gz`





