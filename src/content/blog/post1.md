---
title: "Installation de GLPI | Debian 13"
description: "Installation de GLPI."
pubDate: "Feb 29 2026"
heroImage: "/glpi.webp"
tags: ["Bigbang","Fart Station"]
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

Utilisation de MariaDB précédemment installé via la commande : mariadb

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

## 5. Activation du HTTPS avec un certificat auto-signé

```bash
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/glpi.key -out /etc/ssl/certs/glpi.crt
```

```bash
cd /etc/apache2/sites-available/
cp default-ssl.conf glpi-ssl.conf
nano glpi-ssl.conf
a2enmod ssl
a2ensite glpi-ssl.conf
systemctl restart apache2
```

## 6. Configuration DNS

Entrée DNS ajoutée : `glpi.group.lan`

## 7. Installation via l’interface web

- Accéder à : https://glpi.group.lan
- Choisir la langue : Français
- Vérification des dépendances
- Configuration de la base `glpi_group`

## 8. Identifiants par défaut

```
Utilisateur : glpi
Mot de passe : glpi
```

![alt="GLPI"](/vhost-glpi.png)
