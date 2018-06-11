# rpi-companion

Tested hardware:
Raspberry Pi 3B/3B+ (w/ senseHAT - optional)

Make a user account for Wordpress and define its home directory. This deviates from the LAMP server instructions that are found on the Raspberry Pi web site.

    sudo mkdir -p /local/wordpress
    sudo adduser --home /local/wordpress wordpress
    sudo chown wordpress:wordpress /local/wordpress
	
Install dependencies for Wordpress, delete the html folder, then create a symbolic link from the wordpress folder in its place. We are doing this so that we can run a bash shell from wordpress in a browser.

    sudo apt-get install apache2 php mysql-server php-mysql
    cd /var/www
    sudo rm -rf html
    sudo ln -s /local/wordpress /var/www/html
    
Etc:

    cd /local/wordpress
    sudo wget http://wordpress.org/latest.tar.gz
    sudo tar xzf latest.tar.gz
    sudo mv wordpress/* .
    sudo rm -rf wordpress latest.tar.gz
    sudo chown -R www-data: .
    
