# Install Wordpress

## 4/2/2026

## Overview

The goal of this assignment is to install wordpress and create a facade for our future library webpage.

---

## Step 1

### The goal of this first step is confirm that our Vm and the installed software is up to date to run wordpress.

Everything appears to be up to date so the next item is to install some additional PHP modules to let wordpress operate at its fullest capacity.

The command used:

'''
sudo apt install php-curl php-xml php-imagick php-mbstring php-zip php-intl
'''

No issues were encountered and apache2 as well as mysql were restarted to set the new changes.

---

## Step 2

### The goal of this step is to download the wordpress zip file and extract it in our VM.

First we must etner the /var/www/html directory to install the file from the web using:

'''
sudo wget https://wordpress.org/latest.zip
'''

The next step is extract the file but an initial run had an issue as the extract module was not installed.
he module was installed using the apt command and no issues were encountered.

The file is extracted using:

'''
sudo unzip latest.zip
'''

File unzipped without issue.

---

## Step 3

### The goal of this step is to create a database and a user for our lib page.

First we log into mysql as the root user.

In the mysql prompt we are able to create a user with a complicated password and the database for our library.

The user and the database were created with these commands:

'''
create user 'wordpress'@'localhost' identified by 'XXXXXXXXX';
create database wordpress;
'''

The user was given privileges to operate within the database with the next command:

'''
grant all privileges on wordpress.* to 'wordpress'@'localhost';
'''

No issues with this step.

---

## Step 4

### The goal of this step is to set up the wordpress config.

Inside the '/var/www/html/wordpress' directory we will rename the config file and create a text file in tilde:

'''
sudo cp wp-config-sample.php wp-config.php
sudo tilde wp-config.php
'''

Inside the php file we will enter the relevant credentials and then add the followng line at the bottom of the document to allow wordpress to write files locally:

'''
define('FS_METHOD','direct');
'''

---

## Step 5

### The name of the site was not changed.

---

## Step 6

### The URL is visited and wordpress is officially installed and confirmed running.

Edits will be made over time to the site to make it more user friendly.