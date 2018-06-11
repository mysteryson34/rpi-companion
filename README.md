# rpi-companion

Tested hardware:
Raspberry Pi 3B/3B+ (w/ senseHAT - optional)

Make a user account for Wordpress:

    sudo useradd -m -r wordpress
	sudo mkdir -p /local/wordpress
	sudo chown wordpress:wordpress /local/wordpress
	
Install everything you need for Wordpress:

    sudo apt-get install apache2 php mysql-server php-mysql
	
