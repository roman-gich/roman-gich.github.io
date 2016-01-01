---
layout: post
title:  "How to backup your Ubuntu / Mint system - simple guide"
date:   2015-12-26 20:37:13 +0200
---
As we know, people can be divided into two groups: <span style="text-decoration: line-through;">those who divide people into two groups, and those who don't</span> those who backup their data and those who will do it.

I've become the last one after several crashes and if you're reading it I suppose that you've become it too.

Firstly, go to the user's folder and create a directory for the backup and also a bash script.
{% highlight bash %}cd ~
mkdir Backup
mkdir Backup/mnt
touch backup.sh{% endhighlight %}
<h3>Let's take a look at the script code now!</h3>
The script must begin with a shebang, such as #!/bin/bash. 
{% highlight bash %}#!/bin/bash

apt-get autoclean
apt-get autoremove

# you can add your own folders needed to be excluded 
excluded_folders=(
    "/proc"
    "/tmp"
    "/lost+found"
    "/mnt"
    "/media"
    "/sys"
    "/run/user"
)

for i in "${excluded_folders[@]}"; do exclude_concat+=" --exclude=$i"; done;

backup_dir=/home/$USER/Backup/
sudo su

cd /
tar -cvpzf $backup_dir/backup_$(date +"%Y-%m-%d-%H-%M-%S").tar.gz $exclude_concat /
cd $backup_dir
# if the number of backups is more than 7 - delete the oldest one
files_count=`find . -type f -name "backup_*.tar.gz" | wc -l`
if [ $files_count -gt 7 ] ; then rm `ls -v backup_*.tar.gz | head -n 1`; fi


# copy to remote server in odd-numbered days only
day=`date +"%u"`; 
if [ $((day%2)) -eq 0 ]; then exit; fi;
mount -t cifs '//pc.company.loc/backups/' $backup_dir/mnt -o user=username,pass=Passw0rD,rw,dir_mode=0777,file_mode=0777
cp `ls -vr backup_*.tar.gz | head -n 1` mnt/;
cd mnt/

# if the number of backups is more than 5 - delete the oldest one
files_count=`find . -type f -name "backup_*.tar.gz" | wc -l`
if [ $files_count -gt 5 ] ; then rm `ls -v backup_*.tar.gz | head -n 1`; fi

cd ../
umount mnt/{% endhighlight %}

For more functionality you can add it to the crontab. I hope this will help.