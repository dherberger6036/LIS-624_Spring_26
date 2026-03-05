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
