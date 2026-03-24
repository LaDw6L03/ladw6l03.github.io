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

![alt="GLPI"](/vhost-glpi.png)


- **Extensive Onboarding**: Donec placerat ante eget tellus egestas, in gravida ex fermentum. Nunc ultrices consectetur erat, a pellentesque elit. Ut pellentesque varius nibh vitae dictum. Etiam tincidunt tempus elit eget mattis. Vestibulum convallis turpis sed interdum aliquet. Nam vestibulum felis in erat finibus, quis bibendum lectus blandit. Proin vel ornare justo, quis faucibus enim. In hendrerit euismod quam sit amet feugiat. Fusce in massa auctor, rutrum tellus quis, bibendum justo. Suspendisse suscipit finibus egestas. Curabitur nunc erat, lobortis at leo eget, tempus fringilla lectus. Maecenas porttitor enim vel neque pellentesque, sit amet congue ante lobortis. Curabitur sit amet sollicitudin elit. Ut nunc eros, laoreet sit amet quam sed, eleifend ullamcorper eros.

Praesent rutrum erat vitae fringilla tristique. Cras pellentesque bibendum congue. Curabitur diam nisl, elementum sit amet cursus vel, posuere in elit. Nunc lacus erat, lacinia quis cursus ut, porttitor ultricies lacus. Nulla ultricies, leo sit amet lobortis sagittis, tortor justo tincidunt ex, eu tempor elit tortor quis elit. Duis accumsan est sagittis porta pulvinar. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nullam faucibus metus id nisl viverra volutpat. Vestibulum nec sem condimentum, vulputate ex et, convallis quam. Cras maximus massa id sapien dapibus commodo. Sed varius orci velit, sed volutpat mauris mollis a. In quis tincidunt magna. Morbi nec augue metus. Nunc nec eros placerat nisl condimentum luctus.

Donec eget ipsum et sem tincidunt laoreet. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Sed sit amet metus id sem posuere porta. Maecenas lacinia, enim id suscipit faucibus, nisi neque fermentum nunc, in dictum diam tortor vitae quam. In vel turpis vitae mauris lacinia aliquam sit amet vitae nulla. Pellentesque laoreet gravida sapien. Duis a tellus eu mauris elementum lobortis. Sed eu arcu non nisl suscipit tempor. Sed aliquet felis nec egestas condimentum. Ut porttitor quam et malesuada semper. Vivamus sed nibh ac orci mollis laoreet at id ante. Nam faucibus non augue non sollicitudin. Aliquam eu ante leo. Cras sed risus non lorem porttitor sagittis. Cras non quam eu ligula gravida venenatis.

Quisque ornare, eros a dapibus posuere, sem leo pretium lorem, sit amet dignissim lacus tortor ut erat. In est purus, porta accumsan augue nec, scelerisque vestibulum elit. Nullam pellentesque quis elit vel sollicitudin. Duis vel sagittis nulla. Quisque placerat leo nec auctor laoreet. Duis eleifend, nibh quis convallis tristique, ligula nunc dapibus sapien, sit amet ultrices arcu velit id erat. Etiam lobortis mauris nec venenatis vestibulum. Integer erat justo, egestas vitae pulvinar et, ornare sed nisi. Nunc semper turpis augue. Integer et mollis erat. Etiam porttitor metus nisl, id imperdiet purus eleifend id. Integer nec erat vitae lorem egestas varius non nec est. Suspendisse urna sem, lacinia id nunc vel, tempus auctor lacus.

- **Supportive Colleagues**: Quisque ornare, eros a dapibus posuere, sem leo pretium lorem, sit amet dignissim lacus tortor ut erat. In est purus, porta accumsan augue nec, scelerisque vestibulum elit. Nullam pellentesque quis elit vel sollicitudin. Duis vel sagittis nulla. Quisque placerat leo nec auctor laoreet. Duis eleifend, nibh quis convallis tristique, ligula nunc dapibus sapien, sit amet ultrices arcu velit id erat. Etiam lobortis mauris nec venenatis vestibulum. Integer erat justo, egestas vitae pulvinar et, ornare sed nisi. Nunc semper turpis augue. Integer et mollis erat. Etiam porttitor metus nisl, id imperdiet purus eleifend id. Integer nec erat vitae lorem egestas varius non nec est. Suspendisse urna sem, lacinia id nunc vel, tempus auctor lacus.

- **Professional Communication in English**: ornare, eros a dapibus posuere, sem leo pretium lorem, sit amet dignissim lacus tortor ut erat. In est purus, porta accumsan augue nec, scelerisque vestibulum elit. Nullam pellentesque quis elit vel sollicitudin. Duis vel sagittis nulla. Quisque placerat leo nec auctor laoreet. Duis eleifend, nibh quis convallis tristique, ligula nunc dapibus sapien, sit amet ultrices arcu velit id erat. Etiam lobortis mauris nec venenatis vestibulum. Integer erat justo, egestas vitae pulvinar et, ornare sed nisi. Nunc semper turpis augue. Integer et mollis erat. Etiam porttitor metus nisl, id imperdiet purus eleifend id. Integer nec erat vitae lorem egestas varius non nec est. Suspendisse urna sem, lacinia id nunc vel, tempus auctor lacus.

![alt="yes"](/rfafinal.webp)

**Overcoming Challenges**

Quisque ornare, eros a dapibus posuere, sem leo pretium lorem, sit amet dignissim lacus tortor ut erat. In est purus, porta accumsan augue nec, scelerisque vestibulum elit. Nullam pellentesque quis elit vel sollicitudin. Duis vel sagittis nulla. Quisque placerat leo nec auctor laoreet. Duis eleifend, nibh quis convallis tristique, ligula nunc dapibus sapien, sit amet ultrices arcu velit id erat. Etiam lobortis mauris nec venenatis vestibulum. Integer erat justo, egestas vitae pulvinar et, ornare sed nisi. Nunc semper turpis augue. Integer et mollis erat. Etiam porttitor metus nisl, id imperdiet purus eleifend id. Integer nec erat vitae lorem egestas varius non nec est. Suspendisse urna sem, lacinia id nunc vel, tempus auctor lacus.

![alt="yes"](/rfafinal.webp)

**My Advice for Aspiring Interns**

- **Start Early**: Quisque ornare, eros a dapibus posuere, sem leo pretium lorem, sit amet dignissim lacus tortor ut erat. In est purus, porta accumsan augue nec, scelerisque vestibulum elit. Nullam pellentesque quis elit vel sollicitudin. Duis vel sagittis nulla. Quisque placerat leo nec auctor laoreet. Duis eleifend, nibh quis convallis tristique, ligula nunc dapibus sapien, sit amet ultrices arcu velit id erat. Etiam lobortis mauris nec venenatis vestibulum. Integer erat justo, egestas vitae pulvinar et, ornare sed nisi. Nunc semper turpis augue. Integer et mollis erat. Etiam porttitor metus nisl, id imperdiet purus eleifend id. Integer nec erat vitae lorem egestas varius non nec est. Suspendisse urna sem, lacinia id nunc vel, tempus auctor lacus.
- **Manage Expectations**: Quisque ornare, eros a dapibus posuere, sem leo pretium lorem, sit amet dignissim lacus tortor ut erat. In est purus, porta accumsan augue nec, scelerisque vestibulum elit. Nullam pellentesque quis elit vel sollicitudin. Duis vel sagittis nulla. Quisque placerat leo nec auctor laoreet. Duis eleifend, nibh quis convallis tristique, ligula nunc dapibus sapien, sit amet ultrices arcu velit id erat. Etiam lobortis mauris nec venenatis vestibulum. Integer erat justo, egestas vitae pulvinar et, ornare sed nisi. Nunc semper turpis augue. Integer et mollis erat. Etiam porttitor metus nisl, id imperdiet purus eleifend id. Integer nec erat vitae lorem egestas varius non nec est. Suspendisse urna sem, lacinia id nunc vel, tempus auctor lacus.
- **Get Out of Your Comfort Zone**: Quisque ornare, eros a dapibus posuere, sem leo pretium lorem, sit amet dignissim lacus tortor ut erat. In est purus, porta accumsan augue nec, scelerisque vestibulum elit. Nullam pellentesque quis elit vel sollicitudin. Duis vel sagittis nulla. Quisque placerat leo nec auctor laoreet. Duis eleifend, nibh quis convallis tristique, ligula nunc dapibus sapien, sit amet ultrices arcu velit id erat. Etiam lobortis mauris nec venenatis vestibulum. Integer erat justo, egestas vitae pulvinar et, ornare sed nisi. Nunc semper turpis augue. Integer et mollis erat. Etiam porttitor metus nisl, id imperdiet purus eleifend id. Integer nec erat vitae lorem egestas varius non nec est. Suspendisse urna sem, lacinia id nunc vel, tempus auctor lacus.
- **Focus on Growth**: Quisque ornare, eros a dapibus posuere, sem leo pretium lorem, sit amet dignissim lacus tortor ut erat. In est purus, porta accumsan augue nec, scelerisque vestibulum elit. Nullam pellentesque quis elit vel sollicitudin. Duis vel sagittis nulla. Quisque placerat leo nec auctor laoreet. Duis eleifend, nibh quis convallis tristique, ligula nunc dapibus sapien, sit amet ultrices arcu velit id erat. Etiam lobortis mauris nec venenatis vestibulum. Integer erat justo, egestas vitae pulvinar et, ornare sed nisi. Nunc semper turpis augue. Integer et mollis erat. Etiam porttitor metus nisl, id imperdiet purus eleifend id. Integer nec erat vitae lorem egestas varius non nec est. Suspendisse urna sem, lacinia id nunc vel, tempus auctor lacus.

**Resource Links**

Quisque ornare, eros a dapibus posuere, sem leo pretium lorem, sit amet dignissim lacus tortor ut erat. In est purus, porta accumsan augue nec, scelerisque vestibulum elit. Nullam pellentesque quis elit vel sollicitudin. Duis vel sagittis nulla. Quisque placerat leo nec auctor laoreet. Duis eleifend, nibh quis convallis tristique, ligula nunc dapibus sapien, sit amet ultrices arcu velit id erat. Etiam lobortis mauris nec venenatis vestibulum. Integer erat justo, egestas vitae pulvinar et, ornare sed nisi. Nunc semper turpis augue. Integer et mollis erat. Etiam porttitor metus nisl, id imperdiet purus eleifend id. Integer nec erat vitae lorem egestas varius non nec est. Suspendisse urna sem, lacinia id nunc vel, tempus auctor lacus.

- **Job Board**: Quisque ornare, eros a dapibus posuere, sem leo pretium lorem, sit amet dignissim lacus tortor ut erat. In est purus, porta accumsan augue nec, scelerisque vestibulum elit. Nullam pellentesque quis elit vel sollicitudin. Duis vel sagittis nulla. Quisque placerat leo nec auctor laoreet. Duis eleifend, nibh quis convallis tristique, ligula nunc dapibus sapien, sit amet ultrices arcu velit id erat. Etiam lobortis mauris nec venenatis vestibulum. Integer erat justo, egestas vitae pulvinar et, ornare sed nisi. Nunc semper turpis augue. Integer et mollis erat. Etiam porttitor metus nisl, id imperdiet purus eleifend id. Integer nec erat vitae lorem egestas varius non nec est. Suspendisse urna sem, lacinia id nunc vel, tempus auctor lacus. [Fart](https://en.wikipedia.org/wiki/Locarno_FART_railway_station). departments of companies is also Quisque ornare, eros a dapibus posuere, sem leo pretium lorem, sit amet dignissim lacus tortor ut erat. In est purus, porta accumsan augue nec, scelerisque vestibulum elit. Nullam pellentesque quis elit vel sollicitudin. Duis vel sagittis nulla. Quisque placerat leo nec auctor laoreet. Duis eleifend, nibh quis convallis tristique, ligula nunc dapibus sapien, sit amet ultrices arcu velit id erat. Etiam lobortis mauris nec venenatis vestibulum. Integer erat justo, egestas vitae pulvinar et, ornare sed nisi. Nunc semper turpis augue. Integer et mollis erat. Etiam porttitor metus nisl, id imperdiet purus eleifend id. Integer nec erat vitae lorem egestas varius non nec est. Suspendisse urna sem, lacinia id nunc vel, tempus auctor lacus.  [OFart](https://mapcarta.com/fr/N354739910).
- **Resume Format**: : [No](https://exemple.com).
- **Interview Process**: Quisque ornare, eros a dapibus posuere, sem leo pretium lorem, sit amet dignissim lacus tortor ut erat. In est purus, porta accumsan augue nec, scelerisque vestibulum elit. Nullam pellentesque quis elit vel sollicitudin. Duis vel sagittis nulla. Quisque placerat leo nec auctor laoreet. Duis eleifend, nibh quis convallis tristique, ligula nunc dapibus sapien, sit amet ultrices arcu velit id erat. Etiam lobortis mauris nec venenatis vestibulum. Integer erat justo, egestas vitae pulvinar et, ornare sed nisi. Nunc semper turpis augue. Integer et mollis erat. Etiam porttitor metus nisl, id imperdiet purus eleifend id. Integer nec erat vitae lorem egestas varius non nec est. Suspendisse urna sem, lacinia id nunc vel, tempus auctor lacus.

