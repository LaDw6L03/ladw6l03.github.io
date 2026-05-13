---
title: "Installation de Wazuh"
description: "Utilisation de PVE Helper Scripts"
pubDate: "2026/05/12"
heroImage: "/wazuh_logo.webp"
---
## Installation de Wazuh via PVE Helper Scripts :

Installation de Wazuh avec l’utilisation d’un script, cela sera un container LXC.

Je vais sur la console du pve puis je tape « menu » et je choisis l’option 6 « Proxmox VE
Helper Scripts »

![alt="proxmenux"](/proxmenux.webp)

Puis je vais rechercher « wazuh », je continue je choisis la version venant de Github

![alt="recherche de wazuh"](/search_wazuh.webp)

Je continue sur le « default install »

![alt="installation par défaut de wazuh"](/default_install_wazuh.webp)

Je retourne sur mon terminal avec un accès ssh sur le pve et je vais saisir « pct enter
« idcontainer » ainsi je vais avoir accès au container Wazuh.

Ensuie je vais modifier les informations IP et je vais suivre le chemin ci-dessous :

![alt="changement de l'ip sur le pve du conteneur de wazuh"](/lxc_change_ip_wazuh.webp)

On tape l’adresse IP « 192.168.92.4 » et on accède à Wazuh

![alt="accès à wazuh"](/login_wazuh.webp)

Ajout de l’agent Wazuh sur OPNsense, afin de faire cette ajout, il faut mettre à jour
OPNsense à la dernière en date puis d’aller chercher le plugin communautaire « os-
wazuh-agent » :

![alt="installation du plugin wazuh sur opnsense"](/install_plugin_wazuh.webp)

Ensuite je configure le plugin afin d’avoir les informations sur certains services précis :

![alt="configuration du plugin wazuh"](/configure_plugin_wazuh.webp)

Ajout de l’agent Wazuh sur Windows Server 2025 via un connexion SSH entre la fedora et
la machine windows :

![alt="installation de l'agent wazuh sur windows server 2025 via ssh"](/install_windows_agent_wazuh.webp)

Sinon on peux installer l’agent Wazuh avec une interface graphique et les configuration à
faire sois même, la version CLI étant la plus simple et rapide vu que c’est Wazuh qui
donne une commande avec les informations nécessaires.

Exemple de l’interface :

![alt="exemple de l'interface de wazuh"](/exemple_interface_wazuh.webp)

Mise en place d’un test, essaie de connexion au comptes administrateurs d’une machine
fedora et windows server :

![alt="test d'intrusion"](/intrusion_test_wazuh.webp)
