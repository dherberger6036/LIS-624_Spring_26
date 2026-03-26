# LIS-624_Spring_26
## This will be used during the course of LIS624 during the spring semester.
This is the location used for work in the spring 26 LIS624 class.
* Topics Covered
  * Nano
  * Tilde
  * Txt editing
  * Creating Git account
  * Creating and editing public repository
  
  ## New Section
  Git edit test from VM Instance.


*Notes
 *Learned and experimented with grep and searching with grep using an uploaded .bib file.
 
 ## Update 2/23/26
 Since the last updat we have covered the yaz client, searching with grep, and updating our instances with the apt command. I believe that I am becoming better with the command line with each lesson, which is heartening.

## 2026-02-13 - Searching With Grep

Goal: To understand how to search through a large .bib file using the grep commands.
Steps: Download a .bib file containing various pieces from a larger collection and practice searching with grep.
Results: A better understanding of how to search for articles within my VM instance.
Verification: grep "^Year" scopus.bib is a command ran in the bibtex file to search for all lines that begin with "Year" which allows me to sort articles by year published.
Notes: An interesting search tool but not my first choice.

## 2026-02-18 - The yaz Client

Goal: To install yaz, connect to a library OPAC, and search that OPAC for an article.
Steps: use apt to install yaz. Connect to a library OPAC. Search the OPAC for an article(s).
Results: Searched for history of hockey articles and found 9 usable articles.
Verification: The command used to find the articles ' Z> find @and @attr 1=4 "history" @attr 1=21 "hockey" '

## 2026-2-28 Apache Web Server

## Overview

The purpose of this assignment is to understand web servers and to create our own basic server example using the apache software.

## Step 1 Update VM Instance

Updated VM instance with no issues using the typical commands:

sudo apt update
sudo apt -y upgrade

## Step 2

Install Apache using 'apt'

'apt search apache2 | head'

'sudo apt install apache2'

No issues.

## Step 3

Run 'systemctl status apache2' to confirm the server is enabled and running.

Results were satsifactory.

## Step 4 Create Web Page

'sudo apt install elinks'
'elinks 127.0.0.1'
This allows us to visit our sitee with the loopback IP address.

No issues encountered.

## Step 5

Go to the document root at cd /var/www/html/

Next we will swap our webpage root with a new document using 'sudo mc index.html index.original.html

Next we will create a new document in our text editor of choice using sudo tilde index.html

Using sudo allows to work on files outside of our home directory.

No issues.

## Step 6

Write some html to give substance to our new index.html:

<html>
<head>
<title>Myfirst web page using Apache</title>
</head>
<body>

<h1>Welcome</h1>

<p>Welcome to my website.
I created this site using the Apache HTTP server.</p>

</body>
</html>

Everything ran as intended. 

#2026-3-4 PHP

## Overview

This document is about my experience and the process of installing and configuring PHP on my VM instance.

## Environment

-Ubuntu VM hosted on Google Cloud using an apache2 web server.

## Step 1 Install PHP and Restart Apache Server

Using the 'apt install' command I installed PHP. Full command 'sudo apt install php libapache2-mod-php'. No issues were encountered.
Next I used the 'systemctl' command to restart my apache web server. This was done to essentially "refresh" the server to show that someothing had been added/updated. Full command used: 'sudo systemctl restart apache2'.
I confirmed the version installed by running 'php -v'. Everything looked normal.
Finally I checked the status of my apache server by running 'systemctl status apache2'. Everything came back good.

## Step 2 Check Installation

To check that php was correctly installed and working with apache, the following commands were run in sequence of eachother:
'''
cd /var/www/html/
sudo tilde info.php
'''
After the php file was created in tilde I added the following text:
<?php
phpinfo();
?>

This text is in the same format on the document. I saved and closed the document.

To confirm everything was working, I visted the php file from my own server's public IP address. Everything looked good, no issues.

Finally, I deleted the PHP file to hide sensitive information about my system using the command 'sudo rm /var/www/html/info.php'. This worked as intended.

## Step 3 Configuration

I enabled a link to apache through 'cd /etc/apache2/mods-available/'.
I wanted to have apache prioritize the php file so I changed the order in the index to 'DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm'
Tested the change using 'apachectl configtest'. No issues encountered.
System shows 'Syntax Ok'

##Step 4 Create index.php file

Created an index.php file using the following commands with no issues :
'''
cd /var/www/html/
sudo nano index.php
'''

Added the following HTML and PHP to the index file:
'<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Browser Detector</title>
</head>
<body>
    <h1>Browser & OS Detection</h1>
    <p>You are using the following browser to view this site:</p>

    <?php
    $user_agent = $_SERVER['HTTP_USER_AGENT'];

    // Browser Detection
    if (stripos($user_agent, 'Edg') !== false || stripos($user_agent, 'Edge') !== false) {
        $browser = 'Microsoft Edge';
    } elseif (stripos($user_agent, 'Firefox') !== false) {
        $browser = 'Mozilla Firefox';
    } elseif (stripos($user_agent, 'Chrome') !== false && stripos($user_agent, 'Chromium') === false) {
        $browser = 'Google Chrome';
    } elseif (stripos($user_agent, 'Chromium') !== false) {
        $browser = 'Chromium';
    } elseif (stripos($user_agent, 'Opera Mini') !== false) {
        $browser = 'Opera Mini';
    } elseif (stripos($user_agent, 'Opera') !== false || stripos($user_agent, 'OPR') !== false) {
        $browser = 'Opera';
    } elseif (stripos($user_agent, 'Safari') !== false && stripos($user_agent, 'Chrome') === false) {
        $browser = 'Safari';
    } else {
        $browser = 'Unknown Browser';
    }

    // OS Detection
    if (stripos($user_agent, 'Windows') !== false) {
        $os = 'Windows';
    } elseif (stripos($user_agent, 'iOS') !== false || stripos($user_agent, 'iPhone') !== false || stripos($user_agent, 'iPad') !== false) {
        $os = 'iOS';
    } elseif (stripos($user_agent, 'Android') !== false) {
        $os = 'Android';
    } elseif (stripos($user_agent, 'Mac') !== false || stripos($user_agent, 'Macintosh') !== false) {
        $os = 'Mac';
    } elseif (stripos($user_agent, 'Linux') !== false) {
        $os = 'Linux';
    } else {
        $os = 'Unknown OS';
    }

    // Output Result
    echo "<p>Your browser is <strong>$browser</strong> and your operating system is <strong>$os</strong>.</p>";
    ?>

</body>
</html>'

Saved and exited tilde text editor.

## Step 5 Test website

Tested the file on my server's public IP and everything looked normal.


### Notes
Very easy completion.
No issues encountered with errors or configuration of file.
I easily understood that apache was the entity that executed the php.


# 2026-3-13 Installing and Configuring MySQL

Ubuntu 24.04.4
Google Cloud Console
Windows 11
Tilde Text Editor

## Step 1 General Maintenance

Running the following commands to ensure our VM instance is up to date.
sudo apt update
sudo apt upgrade
sudo apt autoremove
sudo apt clean

All commands were executed without issue. Feed cleared for step 2.


## Step 2

Ran the following command:
sudo apt install mysql-server

Installed the MySQL community server without issue.

Ran the command  'MySQL --version' to check installed MySQL version. Version Ver 8.0.45 confirmed.

Ran the command 'systemctl status mysql' Confirmed everything was loaded and running.

Ran a post installation command: 'sudo mysql_secure_installation'
This allows us to set security parameters for our MySQL.


## Step 3

For this step we logged into our MySQL using the 'sudo mysql -u root' command.
This brings us to our MySQL server.

in our MySQL server I entered 'showdatabases;' and got the following:
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
4 rows in set (0.17 sec)

After confirming that everything was correct, I entered \q and returned to the BASH shell.


## Step 4

Logged back into the MySQL and entered the following promt 'create user 'opacuser'@'localhost' identified by 'XXXXXXXXX';
This created a new user with a custom password that is censored for security reasons.


## Step 5

For this step we are creating a practice database. While still logged into the MySQL, the following commands are entered in sequence:
mysql> create database opacdb default character set utf8mb4 collate utf8mb4_0900_ai_ci;
mysql> show databases;
mysql> grant all privileges on opacdb.* to 'opacuser'@'localhost';

Confirmed that the commands worked and then exited the MySQL.


## Step 6

In order to make the MySQL more informative I ran the following: tilde ~/.bashrc
This opened the client file and at the bottom of the file I added : export MYSQL_PS1="[\d]> "

Next we logged into our MySQL using the credentials we created earlier.

After logging in, we opened up the new database that we named opacdb we entered data into our table with the following:
mysql> create table books (
        id int unsigned not null auto_increment,
        author varchar(150) not null,
        title varchar(150) not null,
        copyright year not null,
        primary key (id)
);

We then added data to our table with the following commands. For the sake of the assignment , I reused the book examples already in place. No issues were encountered.

mysql> insert into books (author, title, copyright) values
('Jennifer Egan', 'The Candy House', '2022'),
('Imbolo Mbue', 'How Beautiful We Were', '2021'),
('Lydia Millet', 'A Children\'s Bible', '2020'),
('Julia Phillips', 'Disappearing Earth', '2019');

We then were able to view our data with the 'select * from books; command. The data looked as it should, according to the lecture.

A series of tests were ran using the following commands entered in sequence:
mysql> select author from books;
mysql> select copyright from books;
mysql> select author, title from books;
mysql> select author from books where author like '%millet%';
mysql> select title from books where author like '%mbue%';
mysql> select author, title from books where title not like '%e';
mysql> select * from books;
mysql> alter table books add publisher varchar(75) after title;
mysql> describe books;
mysql> update books set publisher='Simon & Schuster' where id='1';
mysql> update books set publisher='Penguin Random House' where id='2';
mysql> update books set publisher='W. W. Norton & Company' where id='3';
mysql> update books set publisher='Knopf' where id='4';
mysql> select * from books;
mysql> delete from books where author='Julia Phillips';
mysql> insert into books
       (author, title, publisher, copyright) values
       ('Emma Donoghue', 'Room', 'Little, Brown & Company', '2010'),
       ('Zadie Smith', 'White Teeth', 'Hamish Hamilton', '2000');
mysql> select * from books;
mysql> select author, publisher from books where copyright < '2011';
mysql> select author from books order by copyright;
mysql> \q

These essentially tested our database as well as allow us to practice deleting lines, adding lines, and searching for specific data based on a key word or similar data.


## Step 7

### Install PHP and MySQL Support

Installed php support in our MySQL using the 'sudo apt install php-mysql' command. Answered 'y' when prompted. No issues.

Restarted apache2 and MySQL to ensure that the system recognizes the changes. Commands used:
sudo systemctl restart apache2
sudo systemctl restart mysql
 No issues.

Created the scripts for the php:
cd /var/www
sudo touch login.php
sudo chmod 640 login.php
sudo chown :www-data login.php
ls -l login.php
sudo nano login.php

no issues when entering and executing commands.

Created a file with the following credentials in tilde editor:
<?php // login.php
$db_hostname = "localhost";
$db_database = "opacdb";
$db_username = "opacuser";
$db_password = "XXXXXXXXX";
?>

Created a new file in tilde titled "opac.php" and entered the following html:
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MySQL Server Example</title>
</head>
<body>

    <h1>A Basic OPAC</h1>
    <p>We can retrieve all the data from our database and book table using a couple of different queries.</p>

    <?php
    // Load MySQL credentials securely
    require_once '/var/www/login.php';

    // Enable detailed MySQL error reporting
    mysqli_report(MYSQLI_REPORT_ERROR | MYSQLI_REPORT_STRICT);

    // Establish database connection
    $conn = new mysqli($db_hostname, $db_username, $db_password, $db_database);

    if ($conn->connect_error) {
        die("Connection failed: " . $conn->connect_error);
    }

    echo "<h2>Query 1: Retrieving Publisher and Author Data</h2>";

    // Query using prepared statement
    $stmt = $conn->prepare("SELECT publisher, author FROM books");
    $stmt->execute();
    $result = $stmt->get_result();

    while ($row = $result->fetch_assoc()) {
        echo "<p>Publisher " . htmlspecialchars($row["publisher"]) .
             " published a book by " . htmlspecialchars($row["author"]) . ".</p>";
    }

    $stmt->close();

    echo "<h2>Query 2: Retrieving Author, Title, and Date Published Data</h2>";

    $stmt2 = $conn->prepare("SELECT author, title, copyright FROM books");
    $stmt2->execute();
    $result2 = $stmt2->get_result();

    while ($row = $result2->fetch_assoc()) {
        echo "<p>A book by " . htmlspecialchars($row["author"]) .
             " titled <em>" . htmlspecialchars($row["title"]) .
             "</em> was released in " . htmlspecialchars($row["copyright"]) . ".</p>";
    }

    $stmt2->close();
    $conn->close();
    ?>

</body>
</html>

Everything looked normal so I saved and exited tilde.

## Step 8
### Test Syntax

Entered the following commands to test how our file looked:
sudo php -f /var/www/login.php
sudo php -f /var/www/html/opac.php

No issues observed.


## Step 9

Tested the functionality of my php file in a public ip: http://34.44.65.104/opac.php

The file worked as intended.