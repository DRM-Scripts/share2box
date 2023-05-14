1.
# Install Depedencies
sudo apt update
sudo apt -y install software-properties-common
sudo add-apt-repository ppa:ondrej/php
sudo add-apt-repository ppa:linuxuprising/java
sudo apt update


2.
# Install PHP AND NginX
sudo apt -y install oracle-java17-installer
sudo apt -y install php7.4-fpm
sudo apt -y install php7.4-sqlite3
sudo apt -y install php7.4-curl
sudo apt -y install nginx
sudo apt -y install unzip

3.
# Copy Files to Server
unzip /root/share2box-drm.zip -d /opt/share2box-drm

4.
# After Installation of Nginx
mv /etc/nginx/nginx.conf /etc/nginx/nginx.conf.bak
mv /opt/share2box-drm/nginx.conf /etc/nginx/nginx.conf

5.
# Restart Services
sudo systemctl reload nginx
sudo systemctl restart php7.4-fpm.service

6.
# Create Ramdisk
mkdir /tmp/ramdisk
chmod 777 /tmp/ramdisk
mount -t tmpfs -o size=1024M tmpfs /tmp/ramdisk

7.
# Install FFMPEG
wget https://johnvansickle.com/ffmpeg/releases/ffmpeg-release-amd64-static.tar.xz
tar -xf ffmpeg-release-amd64-static.tar.xz
cp ffmpeg-5.1.1-amd64-static/ffmpeg /usr/bin

8.
# Set Permissions
sudo chown www-data:www-data /opt/share2box-drm/channels_new.db
chgrp www-data /opt/share2box-drm/channels_new.db
chmod -R 777 /opt/

9. 
# Start Service
bash /opt/share2box-drm/shell/service.sh start

10. 
# Add Cronjob
@reboot nohup sh /opt/share2box-drm/shell/shell.events.sh > /dev/null &
@reboot sh /opt/share2box-drm/shell/restartService.sh