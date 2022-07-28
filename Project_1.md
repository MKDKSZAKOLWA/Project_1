# PROJECT 1 - LAMP STACK IMPLEMENTATION

## STEP 1 - INSTALLING APACHE AND UPDATING THE FIREWALL.

Install Apache using Ubuntu package manager 'apt'

Update a list of packages in package manager.

`sudo apt update`



![sudo apt update](./Images/sudo%20apt%20update.PNG)

Run apache2 package installation.

`sudo apt install apache2`

![Install Apache2](./Images/Install%20Apache2.PNG)

Verify that apache 2 is running as a Service in our OS.

`sudo systemctl status apache2`

![apache2 running check](./Images/apache2%20running%20check.PNG)

Check how server can be accessed locally in Ubuntu shell. Run below command.

`curl http://localhost:80`

![server access locally](./Images/server%20access%20locally.PNG)


Open a web browser and try to access below url. This is public address that can be copied from the details section of the instance.

http://3.145.203.85:80

![apache2 ubuntu default page](./Images/apache2%20ubuntu%20default%20page.PNG)


## STEP 2 - INSTALLING MYSQL

Run the command below to aquire and install MySQL.

`sudo apt install mysql-server`

![MySQL Installation](./Images/MySQL%20Installation.PNG)

Log into MySQL Console by typing the command below.

`sudo mysql`

![MySQL Console](./Images/MySQL%20Console.PNG)

Change the password of the root user to PassWord.1 using the command below.

`ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';`

![MySQL Root Password Change](./Images/MySQL%20Root%20Password%20Change.PNG)

Exit MySQL shell by typing the code below.

`exit`

![Exit MySQL](./Images/apache2%20ubuntu%20default%20page.PNG)

Start the interactive script by running the syntax below.

`sudo mysql_secure_installation`

![MySQL Secure Installation](./Images/MySQL%20Installation.PNG)

Test if you are able to login into MySQL console by using the code below.

`sudo mysql -p`

![MySQL Login Test](./Images/MySQL%20Installation.PNG)

Exit MySQL by typing the code below.

`exit`

![Exit MySQL2](./Images/Exit%20MySQL2.PNG)


## STEP 3 - INSTALLING PHP

Install php, php-mysql and libapache2-mod-php packages at once by running the command below.

`sudo apt install php libapache2-mod-php php-mysql`

![PHP Packages Installed](./Images/PHP%20Packages%20Installed.PNG)

Run the below command to confirm the PHP version,

`php -v`

![PHP Version](./Images/PHP%20Version.PNG)

## STEP 4 - CREATING A VIRTUAL HOST FOR THE WEBSITE USING APACHE

Create the directory for projectlamp using ‘mkdir’ command as follows:

`sudo mkdir /var/www/projectlamp`

![Projectlamp Directory](./Images/Projectlamp%20Directory.PNG)

Assign ownership of the directory with your current system user by running the command below.

`sudo chown -R $USER:$USER /var/www/projectlamp`

![Assign Ownership](./Images/Assign%20Ownership.PNG)

Create and open a new configuration file in Apache’s sites-available directory using  vi or vim.

`sudo vi /etc/apache2/sites-available/projectlamp.conf`

![New Blank File](./Images/New%20Blank%20File.PNG)

Use the ls command to show the new file in the sites-available directory.

`sudo ls /etc/apache2/sites-available`

![Show New File](./Images/Show%20New%20File.PNG)

 Use a2ensite command to enable the new virtual host. You will perform step 1 , then disable thje default website first before moving to step 2 on enabling the virtual host.

 `sudo a2ensite projectlamp`

![Enable Virtual Host Step 1](./Images/Enable%20Virtual%20Host%20Step%201.PNG)

Disable Apache’s default website using a2dissite command.

`sudo a2dissite 000-default`

![Default Website Disabled](./Images/Default%20Website%20Disabled.PNG)

Make sure the configuration file doesn’t contain syntax errors by running the command below.

`sudo apache2ctl configtest`

![Syntax Error Check](./Images/Syntax%20Error%20Check.PNG)

Finally, move to step 2 of enabling the virtual host by reloading Apache so these changes take effect by the cpmmand below.

`sudo systemctl reload apache2`

![Apache2 Reload](./Images/Apache2%20Reload.PNG)

Create an index.html file in that location so that we can test that the virtual host works as expected:

`sudo echo 'Hello LAMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectlamp/index.html`


![Index.html file](./Images/Index%2Chtml%20file.PNG)

Now go to your browser and try to open your website URL using IP address:

http://3.17.152.124:80

![Website URL Output](./Images/Website%20URL%20Output.PNG)

The website can also be accessed by public DNS name shown below. Public DNS can be found in the instance.

http://ec2-3-17-152-124.us-east-2.compute.amazonaws.com/

![Website DNS Output](./Images/Website%20URL%20Output.PNG)

## STEP 5 - ENABLE PHP ON THE WEBSITE

Edit the /etc/apache2/mods-enabled/dir.conf file and change the order in which the index.php file is listed within the DirectoryIndex directive: 

Run the command below.

`sudo vim /etc/apache2/mods-enabled/dir.conf`

Copy and paste the text below. Delete the existing text first.

```
<IfModule mod_dir.c>
        #Change this:
        #DirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm
        #To this:
        DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
</IfModule>

```



![Edit Config File](./Images/Edit%20Config%20File.PNG)

Reload Apache so the changes take effect:

`sudo systemctl reload apache2`

![Apache2 reload2](./Images/Apache2%20Reboad2.PNG)

Create a PHP script to test that PHP is correctly installed and configured on the server.

Create a new file named index.php inside your custom web root folder:

`sudo vim /var/www/projectlamp/index.php`

![New File2](./Images/New%20File2.PNG)

Go and refresh the page. The output will be shown below.

![Updated Website Output](./Images/Updated%20Website%20Output.PNG)

After checking the relevant information about the PHP server through that page, it’s best to remove the file created as it contains sensitive information about the PHP environment -and the Ubuntu server. This can be done by the command below.



`sudo rm /var/www/projectlamp/index.php`

![Remove File](./Images/Remove%20File.PNG)



         

