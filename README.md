# ISO 27001 Compliant Incident Management Report
<!-- hide -->

> By [@rosinni](https://github.com/rosinni) and [other contributors](https://github.com/4GeeksAcademy/deploying-wordpress-debian/graphs/contributors) at [4Geeks Academy](https://4geeksacademy.co/)

[![build by developers](https://img.shields.io/badge/build_by-Developers-blue)](https://4geeks.com)
[![build by developers](https://img.shields.io/twitter/follow/4geeksacademy?style=social&logo=twitter)](https://twitter.com/4geeksacademy)

*Estas instrucciones están [disponibles en español](https://github.com/breatheco-de/installing-kali-linux-on-virtual-machine/blob/main/README.md)*
<!-- endhide -->

<!-- hide -->

### Before Starting...

> We need you! These exercises are created and maintained in collaboration with people like you. If you find any errors or typos, please contribute and/or report them.

<!-- endhide -->

## 🌱 How to start this project?

Do not clone this repository! Just follow the instructions.

This exercise aims to teach students how to identify and report an SQL injection vulnerability using the Damn Vulnerable Web Application (DVWA). The report should be made according to ISO 27001 standards for information security incident management.

### Requirements

* VirtualBox installed on your computer.
* A Debian virtual machine installed in VirtualBox. For the purposes of this tutorial, we will use Debian.

#### Benefits of Using a Virtual Machine

* Isolation: Keeps the testing environment separate from your main operating system, protecting it from potential damage.

* Easy Restoration: You can create snapshots of your virtual machine and restore them easily if something goes wrong.

* Portability: You can move and share the virtual machine easily with others.

## 📝 Instructions

### Step 1: Create a Virtual Machine.
- [ ] Open VirtualBox and click "New".
- [ ] Name your VM (e.g., "Debian-DVWA").
- [ ] Select "Linux" as the type and "Debian (64-bit)" as the version.
- [ ] Assign at least 2 GB of RAM (recommended).
- [ ] Create a virtual hard disk with at least 20 GB of space (VDI, dynamically allocated).
- [ ] Download the Debian ISO image from the Debian website.
- [ ] Start the VM and select the downloaded Debian ISO to boot from it.
- [ ] Follow the on-screen instructions to install Debian on the virtual machine.
- [ ] In the "Network" section, select "Bridged Adapter" so that the VM is on the same network as your host.

### Step 2: Set Up the Development Environment: MySQL (MariaDB), Apache, and PHP (LAMP Stack).
- [ ] Update the package index
```sh
sudo apt-get update
```
- [ ] Install MariaDB
```sh
sudo apt-get install mariadb-server
```
- [ ] Start and enable the MariaDB service
```sh
sudo systemctl start mariadb 
sudo systemctl enable mariadb
```
- [ ] Secure the MariaDB installation
```sh
sudo mysql_secure_installation
```
- [ ] Follow the prompts to set the root password for MariaDB and configure basic security.


### Step 3: Configure Apache and PHP.
- [ ] Install Apache and PHP
```sh
sudo apt-get install apache2 
sudo apt-get install php libapache2-mod-php php-mysql
```
- [ ] Start and enable the Apache service
```sh
sudo systemctl start apache2 
sudo systemctl enable apache2
```

### Step 4: Install and Configure DVWA.
- [ ] Download DVWA
```sh
cd /var/www/html 
```
- [ ] Configure DVWA
Change to the DVWA directory and rename the configuration file
```sh
cd DVWA/config 
sudo cp config.inc.php.dist config.inc.php
```
- [ ] Edit the `config.inc.php` file to set the MariaDB credentials:
```ssh
sudo nano config.inc.php
```
> 💡 IMPORTANT: Ensure the following lines have the correct credentials:
* $_DVWA[ 'db_user' ] = 'root';
* $_DVWA[ 'db_password' ] = 'tu_contraseña_de_root'; 
* $_DVWA[ 'db_database' ] = 'dvwa';

- [ ] Configure the Database
Log in to MariaDB and create the DVWA database
```sh
sudo mysql -u root -p 
CREATE DATABASE dvwa; 
EXIT;
```
- [ ] Adjust Permissions
```sh
sudo chown -R www-data:www-data /var/www/html/DVWA/
sudo chmod -R 755 /var/www/html/DVWA/
```
- [ ] Open a browser in your VM and go to http://localhost/DVWA/setup.php
- [ ] Review the setup and click "Create / Reset Database".


### Step 5: Conduct the SQL Injection Attack.
- [ ] Open a browser in the VM and go to http://localhost/DVWA.
- [ ] Log in to DVWA:
```
*Username: admin
*Password: password
```
- [ ] Set the Security Level
Go to the "DVWA Security" tab and select the "Low" security level to facilitate exploitation.

- [ ] Execute the SQL Injection
Go to the "SQL Injection" section in DVWA
Enter a simple SQL injection attack in the provided "User ID" field, for example:
```sh
1' OR '1'='1
```
Click "Submit" and observe how DVWA processes the injection and displays the database results.
> 💡 NOTE: You should see a list of all users extracted from the database, indicating a successful SQL injection.

### Step 6: Incident Report.

- [ ] Follow the Report Structure
  * Report Title
  * Introduction
  * Incident Description
  * Reproduction Process
  * Incident Impact
  * Recommendations
  * Conclusion

 Good luck with your exercise!