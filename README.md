# rpi-companion

Tested hardware:
Raspberry Pi 3B/3B+ (w/ senseHAT - optional)

Make a user account for Wordpress:

    sudo mkdir -p /local/wordpress
    sudo adduser --home /local/wordpress wordpress
    sudo chown wordpress:wordpress /local/wordpress
	
Etc:

    sudo apt-get install apache2 php mysql-server php-mysql
    cd /var/www
    sudo rm -rf html
    sudo ln -s /local/wordpress /var/www/html
    
