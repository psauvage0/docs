---
title: 'Configurer son adresse IP en alias'
excerpt: 'Découvrez comment ajouter des Additional IP à votre configuration'
updated: 2023-06-15
---

> [!primary]
>
> Depuis le 6 octobre 2022, notre solution "IP Failover" s'appelle désormais [Additional IP](https://www.ovhcloud.com/fr/network/additional-ip/). Cela n'a pas d'impact sur ses fonctionnalités.
>

## Objectif

L'alias d'IP (*IP aliasing* en anglais) est une configuration spéciale du réseau de votre serveur dédié OVHcloud, qui vous permet d'associer plusieurs adresses IP sur une seule interface réseau.

**Ce guide vous explique comment réaliser cet ajout.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/s1qDqQ0p07Q" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

> [!warning]
>
> OVHcloud met à votre disposition des services dont la responsabilité vous revient. En effet, n’ayant aucun accès à ces machines, nous n’en sommes pas les administrateurs et ne pourrons vous fournir d'assistance. Il vous appartient de ce fait d’en assurer la gestion logicielle et la sécurisation au quotidien.
> 
> Nous mettons à votre disposition ce guide afin de vous accompagner au mieux sur des tâches courantes. Néanmoins, nous vous recommandons de faire appel à un [prestataire spécialisé](https://partner.ovhcloud.com/fr/directory/) si vous éprouvez des difficultés ou des doutes concernant l’administration, l’utilisation ou la sécurisation d’un serveur. Plus d’informations dans la section « Aller plus loin » de ce guide.
>

## Prérequis

- Posséder un [serveur dédié](https://www.ovh.com/fr/serveurs_dedies/){.external}, un [VPS](https://www.ovh.com/fr/vps/){.external} ou une [instance Public Cloud](https://www.ovh.com/fr/public-cloud/instances/){.external}.
- Avoir une ou plusieurs [Additional IP](https://www.ovhcloud.com/fr/bare-metal/ip/){.external}.
- Être connecté en SSH au serveur (accès root) ou via remote desktop pour Windows.

> [!warning]
> Cette fonctionnalité peut être indisponible ou limitée sur les [serveurs dédiés **Eco**](https://eco.ovhcloud.com/fr/about/).
>
> Consultez notre [comparatif](https://eco.ovhcloud.com/fr/compare/) pour plus d’informations.

## En pratique

> [!primary]
>  
>Si vous souhaitez utiliser une distribution récente, la procédure adéquate pour configurer votre interface réseau peut nécessiter des adaptations. Si vous rencontrez des difficultés, nous vous recommandons de consulter la documentation relative à votre système d’exploitation.

Voici les configurations pour les distributions et les systèmes d’exploitation principaux.

### Debian 10/11

#### Étape 1 : créer une sauvegarde

Il convient avant tout d'effectuer une copie du fichier source afin de pouvoir revenir en arrière à tout moment :

```sh
cp /etc/network/interfaces.d/50-cloud-init /etc/network/interfaces.d/50-cloud-init.bak
```

#### Étape 2 : éditer le fichier de configuration

> [!primary]
>
> Les noms donnés aux interfaces réseau dans ce guide peuvent différer des vôtres. Veuillez adapter les manipulations en conséquence.

Vous pouvez désormais modifier le fichier source :

```sh
editor /etc/network/interfaces.d/50-cloud-init
```

Vous devez ensuite ajouter une interface secondaire :

```bash
auto eth0:0
iface eth0:0 inet static
address ADDITIONAL_IP
netmask 255.255.255.255
```

Pour vous assurer que l’interface secondaire est activée quand l’interface `eth0` l’est aussi, vous devez ajouter la ligne suivante à la configuration de `eth0` :

```bash
post-up /sbin/ifconfig eth0:0 ADDITIONAL_IP netmask 255.255.255.255 broadcast ADDITIONAL_IP
pre-down /sbin/ifconfig eth0:0 down
```

Si vous avez deux Additional IP à configurer, le fichier `/etc/network/interfaces.d/50-cloud-init` doit ressembler à ceci :

```bash
auto eth0
iface eth0 inet dhcp

auto eth0:0
iface eth0:0 inet static
address ADDITIONAL_IP1
netmask 255.255.255.255

auto eth0:1
iface eth0:1 inet static
address ADDITIONAL_IP2
netmask 255.255.255.255
```
Ou à cela :

```bash
auto eth0
iface eth0 inet dhcp

# IP 1
post-up /sbin/ifconfig eth0:0 ADDITIONAL_IP1 netmask 255.255.255.255 broadcast ADDITIONAL_IP1
pre-down /sbin/ifconfig eth0:0 down

# IP 2
post-up /sbin/ifconfig eth0:1 ADDITIONAL_IP2 netmask 255.255.255.255 broadcast ADDITIONAL_IP2
pre-down /sbin/ifconfig eth0:1 down
```

#### Étape 3 : redémarrer l’interface

Il vous reste à redémarrer votre interface :

```sh
/etc/init.d/networking restart
```

### Debian 6/7/8 et dérivés

#### Étape 1 : créer une sauvegarde

Il convient avant tout d'effectuer une copie du fichier source afin de pouvoir revenir en arrière à tout moment :

```sh
cp /etc/network/interfaces /etc/network/interfaces.bak
```

#### Étape 2 : éditer le fichier de configuration

> [!primary]
>
> Les noms donnés aux interfaces réseau dans ce guide peuvent différer des vôtres. Veuillez adapter les manipulations en conséquence.

Vous pouvez désormais modifier le fichier source :

```sh
editor /etc/network/interfaces
```

Vous devez ensuite ajouter une interface secondaire :

```bash
auto eth0:0
iface eth0:0 inet static
address ADDITIONAL_IP
netmask 255.255.255.255
```

Pour vous assurer que l’interface secondaire est activée quand l’interface `eth0` l’est aussi, vous devez ajouter la ligne suivante à la configuration de `eth0` :

```bash
post-up /sbin/ifconfig eth0:0 ADDITIONAL_IP netmask 255.255.255.255 broadcast ADDITIONAL_IP
pre-down /sbin/ifconfig eth0:0 down
```

Si vous avez deux Additional IP à configurer, le fichier `/etc/network/interfaces` doit ressembler à ceci :

```bash
auto eth0
iface eth0 inet static
address SERVER_IP
netmask 255.255.255.0
broadcast xxx.xxx.xxx.255
gateway xxx.xxx.xxx.254

auto eth0:0
iface eth0:0 inet static
address ADDITIONAL_IP
netmask 255.255.255.255

auto eth0:1
iface eth0:1 inet static
address ADDITIONAL_IP
netmask 255.255.255.255
```
Ou à cela :

```bash
auto eth0
iface eth0 inet static
address SERVER_IP
netmask 255.255.255.0
broadcast xxx.xxx.xxx.255
gateway xxx.xxx.xxx.254

# IP 1
post-up /sbin/ifconfig eth0:0 ADDITIONAL_IP netmask 255.255.255.255 broadcast ADDITIONAL_IP
pre-down /sbin/ifconfig eth0:0 down

# IP 2
post-up /sbin/ifconfig eth0:1 IP_IP2 netmask 255.255.255.255 broadcast IP_IP2
pre-down /sbin/ifconfig eth0:1 down
```

#### Étape 3 : redémarrer l’interface

Il vous reste à redémarrer votre interface :

```sh
/etc/init.d/networking restart
```

### Debian 9+, Ubuntu 17.04+ et Arch Linux

Sur ces distributions, la dénomination des interfaces comme `eth0`, `eth1` (et ainsi de suite) est supprimée. Nous utiliserons donc désormais de manière plus générique `systemd-network`.

#### Étape 1 : créer une sauvegarde

Il convient avant tout d'effectuer une copie du fichier source afin de pouvoir revenir en arrière à tout moment :

```sh
cp /etc/systemd/network/50-default.network /etc/systemd/network/50-default.network.bak
```

#### Étape 2 : éditer le fichier de configuration

Vous pouvez désormais ajouter dans le fichier source votre Additional IP comme suit :

```sh
editor /etc/systemd/network/50-default.network
```
```sh
[Address]
Address=ADDITIONAL_IP/32
Label=failover1 # optional
```

Le label est optionnel. Il est présent pour distinguer vos différentes adresses Additional IP.

#### Étape 3 : redémarrer l’interface

Il vous reste à redémarrer votre interface :

```sh
systemctl restart systemd-networkd
```

### Fedora 36 et versions ultérieures

Fedora utilise dorénavant des fichiers clés (*keyfiles*).
Fedora utilisait auparavant des profils réseau stockés par NetworkManager au format ifcfg dans le répertoire `/etc/sysconfig/network-scripts/`.<br>
Le ifcfg étant à présent déprécié, NetworkManager ne crée plus par défaut les nouveaux profils dans ce format. Le fichier de configuration se trouve à présent dans `/etc/NetworkManager/system-connections/`.

#### Étape 1 : créer une sauvegarde

Il convient avant tout d'effectuer une copie du fichier source afin de pouvoir revenir en arrière à tout moment :

```sh
cp -r /etc/NetworkManager/system-connections/cloud-init-eno1.nmconnection /etc/NetworkManager/system-connections/cloud-init-eno1.nmconnection.bak
```

#### Étape 2 : éditer le fichier de configuration

> [!primary]
>
> Prenez en compte que le nom du fichier réseau dans notre exemple peut différer du vôtre. Veuillez adapter les commandes en fonction du nom de votre fichier. Pour obtenir le nom de votre interface réseau afin de pouvoir éditer le fichier réseau approprié, vous pouvez exécuter la commande suivante : `ip a`.
>
> Vous pouvez également vérifier l'interface connectée avec la commande suivante :
>
> `nmcli connection show`
> 

Vous pouvez maintenant ajouter votre Additional IP au fichier de configuration, comme dans l'exemple ci-dessous :

```sh
editor /etc/NetworkManager/system-connections/cloud-init-eno1.nmconnection
```

```sh
[ipv4]
method=auto
may-fail=false
address1=ADDITIONAL_IP/32
```

Si vous avez deux adresses Additional IP à configurer, le fichier de configuration devrait ressembler à ceci :

```sh
[connection]
id=cloud-init eno1
uuid=xxxxxxx-xxxx-xxxe-ba9c-6f62d69da711
type=ethernet

[user]
org.freedesktop.NetworkManager.origin=cloud-init

[ethernet]
mac-address=MA:CA:DD:RE:SS:XX

[ipv4]
method=auto
may-fail=false
address1=ADDITIONAL_IP1/32
address2=ADDITIONAL_IP2/32
```

#### Étape 3 : redémarrer l'interface

Vous devez maintenant redémarrer votre interface :

```sh
systemctl restart NetworkManager
```

### Ubuntu 17.10 et versions suivantes

Chaque adresse Additional IP aura besoin de sa propre ligne dans le fichier de configuration. Celui-ci a pour nom `50-cloud-init.yaml` et se trouve dans `/etc/netplan`.

#### Étape 1 : déterminer l’interface

```sh
ifconfig
```
Notez le nom de l'interface et son adresse MAC.

#### Étape 2 : créer le fichier de configuration

Connectez-vous à votre serveur via SSH et exécutez la commande suivante :

```sh
editor /etc/netplan/50-cloud-init.yaml
```

Ensuite, éditez le fichier avec le contenu ci-dessous, en remplaçant « INTERFACE_NAME », « MAC_ADDRESS » et « ADDITIONAL_IP » :

```sh
network:
    version: 2
    ethernets:
        INTERFACE_NAME:
            dhcp4: true
            match:
                macaddress: MAC_ADDRESS
            set-name: INTERFACE_NAME
            addresses:
            - ADDITIONAL_IP/32
```

Enregistrez et fermez le fichier. Pour tester la configuration, saisissez la commande suivante :

```sh
# netplan try
```

#### Étape 3 : appliquer le changement

Ensuite, exécutez les commandes suivantes pour appliquer la configuration :

```sh
# netplan apply
```

### CentOS, AlmaLinux (8 & 9), Rocky Linux (8 & 9), et Fedora (25 et antérieures)

#### Étape 1 : créer le fichier de configuration

Il convient avant tout de faire une copie du fichier source afin de pouvoir l’utiliser comme modèle :

```sh
cp /etc/sysconfig/network-scripts/ifcfg-eth0 /etc/sysconfig/network-scripts/ifcfg-eth0:0
```

#### Étape 2 : éditer le fichier de configuration

Vous pouvez maintenant modifier le fichier `eth0:0` afin de remplacer l'adresse IP :

```sh
editor /etc/sysconfig/network-scripts/ifcfg-eth0:0
```

Remplacez en premier le nom du `device`, puis l’adresse IP déjà existante par l’Additional IP que vous avez reçue :

```bash
DEVICE="eth0:0"
ONBOOT="yes"
BOOTPROTO="none" # For CentOS use "static"
IPADDR="ADDITIONAL_IP"
NETMASK="255.255.255.255"
BROADCAST="ADDITIONAL_IP"
```

#### Étape 3 : démarrer l'interface alias

Vous devez maintenant démarrer votre interface alias :

```sh
ifup eth0:0
```

#### Pour AlmaLinux et Rocky Linux

Vous devez redémarrer votre interface :

```sh
systemctl restart NetworkManager
```

### Gentoo

#### Étape 1 : créer une sauvegarde

Il convient avant tout d'effectuer une copie du fichier source afin de pouvoir revenir en arrière à tout moment :

```sh
cp /etc/conf.d/net /etc/conf.d/net.bak
```

#### Étape 2 : éditer le fichier de configuration

Maintenant, vous devez modifier le fichier pour ajouter l'Additional IP. Dans Gentoo, un alias est ajouté directement dans l'interface `eth0`. Vous n'avez pas besoin de créer une interface `eth0:0` comme dans Red Hat ou CentOS.

> [!warning]
>
> L’IP par défaut du serveur et `config_eth0=` doivent rester sur la même ligne. Cela permet d'assurer le bon fonctionnement de certaines opérations spécifiques à OVHcloud.
> 

Il vous suffit de faire un retour à la ligne après le masque de réseau **255.255.255.0** et d’y ajouter votre adresse Additional IP. « SERVER_IP » doit être remplacé par l’IP principale de votre serveur.

```sh
editor /etc/conf.d/net
```

Vous devez donc ajouter ceci :

```bash
config_eth0=( "SERVER_IP netmask 255.255.255.0" "ADDITIONAL_IP netmask 255.255.255.255 brd ADDITIONAL_IP" )
```

Le fichier `/etc/conf.d/net` doit contenir ce qui suit :

```bash
#This blank configuration will automatically use DHCP for any net.
# scripts in /etc/init.d. To create a more complete configuration,
# please review /etc/conf.d/net.example and save your configuration
# in /etc/conf.d/net (this file :]!).
config_eth0=( "SERVER_IP netmask 255.255.255.0"
"ADDITIONAL_IP netmask 255.255.255.255 brd ADDITIONAL_IP" )
routes_eth0=( "default gw SERVER_IP.254" )
```

Afin de pouvoir effectuer un ping sur votre Additional IP, vous devez simplement redémarrer l’interface réseau.

#### Étape 3 : redémarrer l’interface

Il vous reste à redémarrer votre interface :

```sh
/etc/init.d/net.eth0 restart
```

### openSUSE

#### Étape 1 : créer une sauvegarde

Il convient avant tout d'effectuer une copie du fichier source afin de pouvoir revenir en arrière à tout moment :

```sh
cp /etc/sysconfig/network/ifcfg-ens32 /etc/sysconfig/network/ifcfg-ens32.bak
```

#### Étape 2 : éditer le fichier de configuration

Ouvrez le fichier :

```sh
editor /etc/sysconfig/network/ifcfg-ens32
```

Ensuite, ajoutez ce qui suit :

```bash
IPADDR_1=ADDITIONAL_IP
NETMASK_1=255.255.255.255
LABEL_1=ens32:0
```

Finalement, redémarrez votre serveur pour appliquer les modifications.

### cPanel (sur CentOS 7)

#### Étape 1 : accéder à la section Gestion IP de WHM

Dans l'espace client WHM, cliquez sur `IP Functions`{.action} et sélectionnez `Add a New IP Address`{.action} dans le menu de gauche.

![Ajouter une nouvelle adresse IP](images/Cpanel-1.png){.thumbnail}

#### Étape 2 : Ajouter les informations des Additional IP

Renseignez votre adresse Additional IP sous la forme « xxx.xxx.xxx.xxx » dans le champ « New IP or IP range to add ».

Sélectionnez `255.255.255.255` comme masque de sous-réseau puis cliquez sur `Submit`{.action}.

![renseigner de nouvelles informations sur la nouvelle adresse IP](images/Cpanel-2.png){.thumbnail}

> [!warning]
>
> Attention, si vous avez plusieurs IP à configurer sur un même bloc et que vous les ajoutez toutes en même temps, le système WHM vous forcera à utiliser le masque de sous-réseau `255.255.255.0`. Il n'est pas recommandé d'utiliser cette configuration, il faut ajouter chaque IP individuellement pour pouvoir utiliser le masque de sous-réseau approprié `255.255.255.255`.
>

#### Étape 3 : Vérifier la configuration IP actuelle

De retour dans la section `IP Functions`{.action}, cliquez sur `Show or Delete Current IP Addresses`{.action} pour vérifier que l'adresse Additional IP a été correctement ajoutée.

![check configured IP](images/Cpanel-3.png){.thumbnail}

### Windows Servers

Les serveurs sous Windows sont souvent en DHCP au niveau de la configuration réseau. Si vous avez déjà paramétré une Additional IP ou passé votre configuration en IP fixe, rendez-vous directement à l’étape suivante.

Sinon, vous devez d’abord passer d’une configuration DHCP au niveau du réseau à une configuration IP fixe.

Ouvrez l’invite de commande `cmd`{.action} ou `powershell`{.action}, puis tapez la commande suivante :

```sh
ipconfig /all
```

Cela vous donnera un résultat similaire à l’exemple suivant :

![Result of "ipconfig /all" command](images/guides-network-ipaliasing-windows-2008-1.png){.thumbnail}

Identifiez et notez votre adresse IPv4, votre masque de sous-réseau, votre passerelle par défaut et le nom du contrôleur d'interface réseau (carte réseau).

Dans notre exemple, l’adresse  IP du serveur est **94.23.229.151**.

Vous pouvez effectuer les prochaines étapes via des lignes de commande ou l’interface graphique.

#### En lignes de commande (recommandé)

Dans les commandes ci-dessous, vous devez remplacer les informations suivantes :

|Commande|Valeur|
|---|---|
|NETWORK_ADAPTER| Nom de la carte réseau (dans notre exemple : « Local Area Connection »).|
|IP_ADDRESS| Adresse IP du serveur (dans notre exemple : « 94.23.229.151 »).|
|SUBNET_MASK| Masque de sous-réseau (dans notre exemple : « 255.255.255.0 »).|
|GATEWAY| Passerelle par défaut (dans notre exemple : « 94.23.229.254 »).|
|ADDITIONAL_IP| Adresse Additional IP que vous voulez ajouter.|

> [!warning]
>
> Attention, le serveur ne sera plus accessible si vous entrez des informations incorrectes. Vous devrez alors effectuer les corrections en mode WinRescue ou via le KVM.
> 

Dans l’invite de commande :

Passez en premier lieu en IP fixe :
```sh
netsh interface ipv4 set address name="NETWORK_ADAPTER" static IP_ADDRESS SUBNET_MASK GATEWAY
```
Définissez ensuite le serveur DNS :
```sh
netsh interface ipv4 set dns name="NETWORK_ADAPTER" static 213.186.33.99
```
Puis ajoutez une adresse Additional IP :
```sh
netsh interface ipv4 add address "NETWORK_ADAPTER" ADDITIONAL_IP 255.255.255.255
```

Votre Additional IP est désormais fonctionnelle.

#### Via l’interface graphique d’utilisateur

1. Allez dans le menu `Démarrer`{.action}, puis `Panneau de gestion`{.action}, `Réseau et Internet`{.action}, `Centre de réseau et Partage`{.action} et `Modifier les paramètres de la carte`{.action} dans la barre de gauche ;
2. Effectuez un clic droit sur `Connexion au réseau local`{.action} ;
3. Cliquez sur `Propriétés`{.action} ;
4. Sélectionnez `Protocole Internet Version 4 (TCP/IPv4)`{.action}, puis cliquez sur `Propriétés`{.action} ;
5. Cliquez sur `Utiliser l’adresse IP suivante`{.action} et renseignez l’IP principale de votre serveur, le masque sous-réseau et la passerelle par défaut obtenus grâce à la commande `ipconfig`{.action} ci-dessus. Dans la case « Serveur DNS Préféré », tapez « 213.186.33.99 ».

![Propriétés Protocole Internet Version 4 (TCP/IPv4)](images/guides-network-ipaliasing-windows-2008-2.png){.thumbnail}

> [!warning]
>
> Attention, le serveur ne sera plus accessible si vous entrez des informations incorrectes. Vous serez alors obligé d’effectuer les corrections en mode WinRescue ou via le KVM.
> 

Ensuite, cliquez sur `Avancé`{.action} en étant toujours positionné dans les `Paramètres TCP/IP`{.action}.

![Propriétés Protocole Internet Version 4 (TCP/IPv4)](images/guides-network-ipaliasing-windows-2008-2.png){.thumbnail}

Dans la partie « Adresse IP », cliquez sur `Ajouter`{.action} :

![Paramètres avancés TCP/IPv4](images/guides-network-ipaliasing-windows-2008-3.png){.thumbnail}

Renseignez alors votre Additional IP et le masque de sous-réseau « **255.255.255.255** ».

![Adresses TCP/IP](images/guides-network-ipaliasing-windows-2008-4.png){.thumbnail}

Cliquez sur `Ajouter`{.action}.

Votre Additional IP est désormais fonctionnelle.

### Plesk

#### Etape 1 : accéder à la section Gestion de Plesk IP

Dans le panneau de configuration Plesk, choisissez `Outils et paramètres`{.action} dans la barre latérale gauche.

![accès à la gestion des adresses IP](images/pleskip1.png){.thumbnail}

Cliquez sur `Adresses IP`{.action} sous **Outils et ressources**.

#### Etape 2 : ajouter les informations IP supplémentaires

Dans cette section, cliquez sur le bouton `Add IP Address`{.action}.

![ajouter des informations IP](images/pleskip2-2.png){.thumbnail}

Entrez votre adresse Additional IP sous la forme `xxx.xxx.xxx.xxx/32` dans le champ « Adresse IP et masque de sous-réseau », puis cliquez sur `OK`{.action}.

![ajouter des informations IP](images/pleskip3-3.png){.thumbnail}

#### Etape 3 : vérifier la configuration IP actuelle

Dans la section « Adresses IP », vérifiez que l'adresse Additional IP a été correctement ajoutée.

![configuration IP actuelle](images/pleskip4-4.png){.thumbnail}

### FreeBSD

#### Étape 1 : déterminer l’interface

Déterminez le nom de votre interface réseau principale. Vous pouvez utiliser la commande `ipconfig` pour cette opération :

```sh
ifconfig
```

Cela vous donnera le résultat suivant :

```sh
ifconfig
>>> nfe0: flags=8843 metric 0 mtu 1500
>>> options=10b
>>> ether 00:24:8c:d7:ba:11
>>> inet 94.23.196.18 netmask 0xffffff00 broadcast 94.23.196.255
>>> inet 87.98.129.74 netmask 0xffffffff broadcast 87.98.129.74
>>> media: Ethernet autoselect (100baseTX )
>>> status: active
>>> lo0: flags=8049 metric 0 mtu 16384
>>> options=3
>>> inet6 fe80::1%lo0 prefixlen 64 scopeid 0x2
>>> inet6 ::1 prefixlen 128
>>> inet 127.0.0.1 netmask 0xff000000 v comsdvt#
```

Dans notre exemple, le nom de l’interface est donc `nfe0`.

#### Étape 2 : créer une sauvegarde

Ensuite, effectuez une copie du fichier source afin de pouvoir revenir en arrière à tout moment :

```sh
cp /etc/rc.conf /etc/rc.conf.bak
```

#### Étape 3 : éditer le fichier de configuration

Modifiez le fichier `/etc/rc.conf` :

```sh
editor /etc/rc.conf
```

Ajoutez ensuite cette ligne à la fin du fichier `ifconfig_INTERFACE_alias0="inet ADDITIONAL_IP netmask 255.255.255.255 broadcast ADDITIONAL_IP"`.

Remplacez « INTERFACE » et « ADDITIONAL_IP » par le nom de votre interface (identifié à la première étape) et votre Additional IP respectivement. Voici un exemple :

```bash
ifconfig_nfe0_alias0="inet 87.98.129.74 netmask 255.255.255.255 broadcast 87.98.129.74"
```

#### Étape 4 : redémarrer l’interface

Il vous reste à redémarrer votre interface :

```sh
/etc/rc.d/netif restart && /etc/rc.d/routing restart
```

### Solaris

#### Étape 1 : déterminer l’interface

Déterminez le nom de votre interface réseau principale. Vous pouvez utiliser la commande `ipconfig` pour cette opération :

```sh
ifconfig -a
```

Cela vous donnera le résultat suivant :

```sh
ifconfig -a
lo0:     flags=2001000849 mtu 8232 index 1 
         inet 127.0.0.0.1 masque de réseau ff00000000 
e1000g0 : flags=1000843 mtu 1500 index 2 
         >>> inet 94.23.41.167 netmask ffffff00 broadcast 94.23.41.255 
         éther 0:1c:c0:f2:be:42
```

Dans notre exemple, le nom de l’interface est donc `e1000g0`.

#### Étape 2 : créer le fichier de configuration

```sh
editor /etc/hostname.e1000g0:1
```
Dans ce fichier, renseignez ceci : « ADDITIONAL_IP/32 up », où « ADDITIONAL_IP » est votre adresse IP de basculement. Par exemple :

```bash
188.165.171.40/32 up
```

#### Étape 3 : redémarrer l’interface

Il vous reste à redémarrer votre interface :

```sh
svcadm restart svc:/network/physical:default
```

#### Résolution des défauts

Si vous ne parvenez pas à établir une connexion entre le réseau public et votre alias IP et que vous soupçonnez un problème réseau, redémarrez le serveur en [mode rescue](/pages/bare_metal_cloud/dedicated_servers/rescue_mode) et configurez l'alias directement sur le serveur.

Pour ce faire, une fois que vous avez redémarré votre serveur en mode rescue, veuillez exécuter la commande suivante :

```bash
ifconfig eth0:0 ADDITIONAL_IP netmask 255.255.255.255 broadcast ADDITIONAL_IP up
```

Où vous remplacerez « ADDITIONAL_IP » par la véritable Additional IP.

Ensuite, il vous suffit d'effectuer un ping depuis votre Additional IP vers l'extérieur. Si cela fonctionne, cela signifie probablement qu'il y a une erreur de configuration devant être corrigée. Si, au contraire, l'adresse IP ne fonctionne toujours pas, veuillez ouvrir un ticket à l'équipe d'assistance via votre [espace client OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr){.external}.

## Aller plus loin

[Mode bridge IP](/pages/bare_metal_cloud/dedicated_servers/network_bridging)

Échangez avec notre communauté d’utilisateurs sur <https://community.ovh.com>.
