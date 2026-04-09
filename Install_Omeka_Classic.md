# Install Omeka Classic

## 4/9/2026

## Overview

The purpose of this assignment was to install omeka classic to our VM and to attach a link to our wordpress blog.
---

## Step 1

Update our VM as necessary with the sudo apt commands.

No issues and all systems up to date with needed software!
---

## Step 2

Installed imagemagick using:

'''sudo apt install imagemagick'''

Next we enabled '''mod_rewrite''' in apache using:

'''sudo a2enmod rewrite'''

This is so that apache can reqrite URLs.

No issues.
---

## Step 3

### Much of this was done "free hand" meaning done myself with help from the threads and my own toruble shooting!

Created a new user in the mysql root using '''create user 'omeka'@'localhost' identified by 'user password';'''

Created a database titled "omeka" using '''create database omeka;'''

Granted privileges to the user on the database.

Confirmed everything was good to go.
---

## Step 4

Installed latest version of omeka classic.

used the command '''sudo wget https://github.com/omeka/Omeka/releases/download/v3.2/omeka-3.2.zip'''

Unzipped the file using the sudo unzip command.

Removed the zip file and renamed the directory from omeka-3.2 to omeka.

#### This step gave me huge trpouble because I could not figure out how to download the zip file despite trying to mirror last weeks assignment. I ended up finding a youtube video that showed where I was missing a few key words and corrected my mistake.
---

## Step 5

Entered the db.ini file in tilde and added the correct user data into the fields showing "XXXXXXXXX".

Next the chmod command is used to give apache access to writeon the files '''sudo chmod -R g+w *'''
---

## Step 6

Testing of the omeka web page showed an error that mod_rewrite was not enabled.

Troubleshooting using the help thread allowed me to solve the issue.

After determining that the .htaccess file was not an issue, I turned my attention to the apache2 config file. In this file I changed the AllowOverride line from "None" to "All". Apache2 was then restarted and everything was confirmed to work!
---