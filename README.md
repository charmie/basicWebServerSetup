# basicWebServerSetup

END STATE: Setup a basic web server in AWS Free Tier

AWS Server Specs:
1. Ubuntu 16.04.4 LTS

PRIOR INSTALLATION STEPS:

1. Get all necessary updates -- $ sudo apt-get update
INSTALL APACHE:
1. Open a terminal
2. Install apache. Run:
    $ sudo apt-get install apache2
3. Set Global ServerName > open apache2.conf > navigate to the bottom of the file then add these: ServerName server_domain_or_IP
    $ sudo nano /etc/apache2/apache2.conf
    NOTE: replace server_domain_or_IP with your server's public IP
4. Restart Apache
    $ sudo systemctl restart apache2
5. Allow traffic in your Apache
    $ sudo ufw app list
    $ sudo ufw app info "Apache Full"
    $ sudo ufw allow in "Apache Full"
    NOTE: Do spot check if this step just made your server available to public. Open a web browser and access your server: http://your_server_IP_address. You should see a default Ubuntu 16.04 Apache web page.

    
INSTALL MYSQL:
1. Run $ sudo apt-get install mysql-server to install mysql service
    NOTE: Some part of the installation will require inputs from you. Just read on and provide what is necessary (i.e. root password)
2. Run this at your own risk. But I suggest that you run it. We will run a simple security script that will remove some dangerous defaults and lock down access to our database system a little bit. 
    $ mysql_secure_installation
    NOTE: for this example, I am setting up a personal dev server hence I've answered NOs pretty much to all the queries. 


INSTALL PHP
1. Run the ff. command:
    $ sudo apt-get install php libapache2-mod-php php-mcrypt php-mysql
2. Modify the mods-enabled config file:
    $ sudo nano /etc/apache2/mods-enabled/dir.conf
    Make sure that it follows the content below. index.php is the first item after DirectoryIndex
    <IfModule mod_dir.c>
      DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
    </IfModule>
3. Restart apache2 service then check its status:
    $ sudo systemctl restart apache2
    $ sudo systemctl status apache2
    NOTE: a running apache2 service will return a result with a highlighted in bright green "active (running)
4. Optionally, if you would like to install PHP modules, you can do so:
    $ sudo apt-get install php-cli
    NOTE: php-cli is a PHP package. CLI is command-line interpreter for the PHP scripting language. 


FINAL STEPS:
1. To check if the setup is all good, let's execute the classic phpinfo.php check.
      $ sudo nano /var/www/html/info.php
      Inside info.php, provide the following scripts:
        <?php
          phpinfo();
        ?>
2. Visit your recently created file in your web browser: http://your_server_IP_address/info.php
      If you were able to see your default php configs, then CONGRATULATIONS, you just made your own web server!
      


    
