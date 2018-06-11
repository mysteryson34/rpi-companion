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
    
Install worpress into its new home directory, then give ownership of everything *inside* the directory to *www-data*

    cd /local/wordpress
    sudo wget http://wordpress.org/latest.tar.gz
    sudo tar xzf latest.tar.gz
    sudo mv wordpress/* .
    sudo rm -rf wordpress latest.tar.gz
    sudo chown -R www-data: .
    
Take care of users, groups, and permission.

    sudo usermod -aG www-data wordpress
    sudo usermod -aG wordpress www-data
    sudo usermod -aG sudo www-data
    sudo usermod -aG sudo wordpress
    sudo visudo
    
Find the matching text in your visudo file and add what you don't already have.

    # Allow members of group sudo to execute any command
    %sudo     ALL=(ALL:ALL) ALL
    www-data  ALL=(ALL) NOPASSWD: ALL
    wordpress ALL=(ALL) NOPASSWD: ALL
    
Complete your wordpress installation. If you are on a RPi, this step will enable you to set a root password if you haven't already.

    sudo mysql_secure_installation
    
Then login to and set up mysql...

    sudo mysql -uroot -p
        > create database wordpress;
	  GRANT ALL PRIVILEGES ON wordpress.* TO 'root'@'localhost' IDENTIFIED BY 'YOURPASSWORD';
	  FLUSH PRIVILEGES;
