---
title: "Installation de GLPI"
description: "Installation de GLPI."
pubDate: "Feb 29 2026"
heroImage: "/glpi.webp"
tags: ["Debian 13","GLPI 11"]
---
**Mise à jours des paquets**

En premier temps il faut faire les mises à jours de la machine. 
``` bash
sudo apt update && apt upgrade -y
```

**Installation des paquets**

Ensuite je vais installer Apache, MariaDB et PHP qui sont nécéssaire pour le fonctionnement de GLPI.

``` bash
sudo apt install apache2 mariadb-server php -y
sudo apt install php-fpm -y
sudo apt install php-{mysql,mbstring,curl,gd,xml,intl,ldap,apcu,xmlrpc,zip,bz2,bcmath} -y
```

**Préparation de la base de donnée**

Utilisation de MariaDB précédemment installé via la commande : 

```bash
mariadb
```
``` sql
create database glpi_group;
grant all privileges on glpi_group.* to group_glpi@localhost identified by « caribou » ;
flush privileges
```

**Téléchargement et extraction de GLPI**

``` bash
cd /tmp
wget https://github.com/glpi-project/glpi/releases/download/11.0.0/glpi-11.0.0.tgz
tar -xvzf glpi-11.0.0.tgz -C /var/www/html
chown -R www-data /var/www/html
```

**Préparation du VHOST apache2**

``` bash
cd /etc/apache2/sites-available/
cp 000-default.conf glpi.conf
nano glpi.conf
```

Il faut écrire dans le fichier les informations ci-dessous, le ServerName dépend de votre configuration.


```bash
a2enmod proxy_fcgi setenvif
a2enmod rewrite
a2enconf php*-fpm
a2ensite glpi.conf
systemctl restart apache2
```

**Activation du HTTPS avec un certificat auto-signé**

```bash
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/glpi.key -out /etc/ssl/certs/glpi.crt
```

```bash
cd /etc/apache2/sites-available/
cp default-ssl.conf glpi-ssl.conf
nano glpi-ssl.conf
```
![alt="VHOST"](/glpi_apache.webp)
```bash
a2enmod ssl
a2ensite glpi-ssl.conf
systemctl restart apache2
```

**Configuration DNS**

- Entrée DNS ajoutée : `glpi.group.lan`
```bash
nano /etc/bind/db.group.lan
```
![alt="INSTALL"](/glpi_bind.webp)

**Installation via l’interface web**

- Accéder à : https://glpi.group.lan
![alt="INSTALL"](/glpi_install.webp)
- Choisir la langue : Français
- Vérification des dépendances
- Configuration de la base `glpi_group`
![alt="STEP1T"](/glpi_step1.webp)
- Choisir la base de donnée existante
![alt="STEP2"](/glpi_step2.webp)
- Initialisation de la base de donnée
![alt="STEP3"](/glpi_step3.webp)

**Identifiants par défaut**

```
Utilisateur : glpi
Mot de passe : glpi
```

