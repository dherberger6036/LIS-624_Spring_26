# Install Koha

## 4/16/26

## Overview

### Install Koha to add a library management system to our online public library.

### Step 1 Create New VM and Configure

New VM created and configured with necessary tools.

No issues.


### Step 2 Add firewall rules

Firewall rules added to our cloud console to allow our VMs to access Koha through the public IP of the VM.

No issues.

### Step 3 Install Koha Repo

Installed koha repo with the following commands:

```
sudo apt install apt-transport-https ca-certificates curl
sudo mkdir -p --mode=0755 /etc/apt/keyrings
sudo curl -fsSL https://debian.koha-community.org/koha/gpg.asc -o /etc/apt/keyrings/koha.asc
```

No issues.

Next we become the root user with ```sudo su```

The following is pasted into our terminal:
``` 
ee /etc/apt/sources.list.d/koha.sources <<EOF
Types: deb
URIs: https://debian.koha-community.org/koha/
Suites: 25.05
Components: main
Signed-By: /etc/apt/keyrings/koha.asc
EOF
```

The contents were varified and we returned to the regular user account.


### Step 4

MariaDB is installed

```
udo apt update
sudo apt install mariadb-server
```

### Step 5

Koha is installed with:
```
sudo apt install koha-common
```

This took several minutes but showed no issues and the install was completed cleanly.

### Step 6

In this step we configure koha and apache to use different ports for users and admins.

We must eddit the file at ```/etc/koha/koha-sites.conf``` but first we must make a backup with:
```
sudo cp /etc/koha/koha-sites.conf /etc/koha/koha-sites.conf.backup
```

Next we use the text editor tilde to open the file and add the folloiung information in the corresponding info:
```
INTRAPORT="8080"
OPACPORT="8081"
```

### Step 7

Important apache modules are enabled for Koha to work properly.
```
sudo a2enmod rewrite cgi headers proxy_http
sudo systemctl restart apache2
```

Next we need to conifure apache to listen to certain ports by replicating what we did for the preious step but with apache config.

```
sudo cp /etc/apache2/ports.conf /etc/apache2/ports.conf.backup
```

The following is added near the top of the document:
```
Listen 8080
Listen 8081
```

No issues.

### Step 8

W ecreate a koha isntance using the following commands with no issues:
```
sudo koha-create --create-db bibliolib
sudo systemctl restart apache2
```

### Step 9

We add additional apache configurations and restart apache with no issues:
```
sudo a2dissite 000-default
sudo a2enmod deflate
sudo a2ensite bibliolib
```

### Step 10

W eprocure our koha log in information to complete the koha installation:
```
sudo koha-passwd bibliolib
```

Koha is installed on the web server using the web installer with no issues.


## This installation process allows us to manage our library system with patrons, circ info, and repository info.
