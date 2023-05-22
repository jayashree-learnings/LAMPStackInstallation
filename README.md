### Installing a LAMP stack in alpine linux  

LAMP is an acronym for Linux(OS), Apache(web sever), MySQl(DB) and 
PHP(programming language), all being open source. The LAMP stack is widely used by developers to create, host and maintain the web content.   

In this exercise, the alpine distro version of 'play with docker' is used as the linux flavour. The other installations are described below  

1)apache2   

1) Check that the repositories in /etc/apk/repositories are uncommented.
##### ![00](https://github.com/jayashree-learnings/LAMPStackInstallation/blob/main/00_includes/00_uncommentedRepos.PNG)
2) Update and upgrade packages using the command apk update && apk upgrade
##### ![01](https://github.com/jayashree-learnings/LAMPStackInstallation/blob/main/00_includes/01_apkUpdateAndUpgrade.PNG)
3) Add openrc and apache2 using the command apk add openrc apache2
##### ![02](https://github.com/jayashree-learnings/LAMPStackInstallation/blob/main/00_includes/02_addOpenrcApache2.PNG)
4) Check the run level using "rc-status". It shows the run level as sysinit
5) 'rc-update add apache2 default' adds apache2-service to default runlevel.
6) 'rc default' changes to default runlevel and in doing so, apache2 starts automatically and apache web page at port 80 can be accesses.
##### ![03a](https://github.com/jayashree-learnings/LAMPStackInstallation/blob/main/00_includes/03a_automaticSatartingApche2.PNG)
##### ![03b](https://github.com/jayashree-learnings/LAMPStackInstallation/blob/main/00_includes/03b_ItWorks.PNG)  


2)php  

1) Add php and its packages related to apache2 and mariadb using "apk add php8 php8-apache2 php8-mysqli"
##### ![04](https://github.com/jayashree-learnings/LAMPStackInstallation/blob/main/00_includes/04_phpAndRelatedPackages.PNG)

2) use vim to crete a new file at /var/www/localhost/htdocs/info.php

<?php
phpinfo();
?>

3)The apache2 server has to be stopped and started to reflect the new page info.phprc-service apache2 restart (here again we have to be at default runlevel).
##### ![05a](https://github.com/jayashree-learnings/LAMPStackInstallation/blob/main/00_includes/05a_RestartApache2.PNG)
##### ![05b](https://github.com/jayashree-learnings/LAMPStackInstallation/blob/main/00_includes/05b_phpinfopage.PNG)


3)maria-DB

1) To add mariadb server and client , use "apk add mariadb mariadb-client".Check the run level and change to default runlevel or else the command at step 2 can not be executed.
2) Before starting, run /etc/init.d/mariadb/setup to create new MySQLdatabases.Else it will throw error if prompted to start
##### ![06a](https://github.com/jayashree-learnings/LAMPStackInstallation/blob/main/00_includes/06a_initialize%20mariadb.PNG)
3) To start the service use "rc-service mariadb start".
4) To open the mariadb monitor, use "mariadb -u root".Before running this command ensure that mariadb server is up and running. 
 Else start the server first.Verify by some sql commands like
  1)show databases;
  2) create database my_database;
##### ![06b](https://github.com/jayashree-learnings/LAMPStackInstallation/blob/main/00_includes/06b_startAndConnectWithDBServer.PNG)
5) Finally to install it securely use the command "maraiadb -secure-installation". Secure the DB by going through the security-credentials-prompts 
appropriately.Restart the service.
##### ![06c](https://github.com/jayashree-learnings/LAMPStackInstallation/blob/main/00_includes/06c_SecurityConfig.PNG)
6) Add mariadb service to default mode to restart it automatically using the command 'rc-update add mariadb default'
##### ![07a](https://github.com/jayashree-learnings/LAMPStackInstallation/blob/main/00_includes/07a_AddmariaDBtoDefault.PNG)
7) Verify both apache2 and mariadb restarts when changed to default run level.
##### ![07b](https://github.com/jayashree-learnings/LAMPStackInstallation/blob/main/00_includes/07b_AutomaticStartOfApache2MariaDB.PNG)


