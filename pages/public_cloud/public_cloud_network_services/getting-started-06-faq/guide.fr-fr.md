---
title: Public Cloud Network Services - FAQ
excerpt: Foire aux questions sur les services réseau Public Cloud
updated: 2023-12-12
---

## Objectif

Retrouvez ici les questions les plus fréquemment posées concernant les services réseau Public Cloud.

## Load Balancer

### Le tarif de la solution Load Balancer  varie en fonction de la capacité en bande passante. Comment cela peut-il être paramétré / modifié ?

Le Load Balancer est proposé en différentes tailles (S/M/L) pour répondre au mieux aux besoins de nos clients. Ces différentes tailles sont définies par des flavors. À ce jour, pour modifier la taille de votre Load Balancer, il vous faudra en créer un nouveau, le configurer de la même manière (avec les mêmes backends que l'ancien) et reconnecter l'adresse Floating IP au nouveau Load Balancer. Vous pourrez alors supprimer l'ancien Load Balancer.

### Puis-je utiliser mon Load Balancer avec des serveurs Bare Metal comme backends ? Puis-je utiliser mon Load Balancer avec des backends dans différentes régions Public Cloud ?

Actuellement, ces modes ne sont pas pris en charge. Pour du load balancing public-privé, les produits Gateway devaient être reliés entre eux. À ce jour, Gateway ne prend en charge que le scope mono-région dans les réseaux privés. Cela signifie également que le scope est limité au Public Cloud, seul périmètre suggéré pour des architectures de type production.<br>
À ce jour, les autres configurations (y compris l'utilisation interunivers avec des serveurs bare metal ou interrégion) ne sont pas prises en charge.

### Puis-je connecter mon Load Balancer à mon Managed Kubernetes Service (MKS) ?

Une version bêta est en cours pour fournir une intégration avec Managed Kubernetes Service. Merci de contacter notre [communauté Discord](https://discord.gg/ovhcloud) sur le canal **#beta-lb-for-k8s**


### Je souhaite monitorer le Load Balancer Octavia. Est-il possible d’activer [metrics](https://docs.openstack.org/octavia/latest/user/guides/monitoring.html) automatiquement sur le Load Balancer ?

Oui cette fonctionnalité est disponible depuis le déploiement de la version Zed en juin 2023.

### Comment est mise en oeuvre la redondance pour chaque type d'offre ? Les Amphoras sont-ils configurés en mode ACT/STBY ?

Oui, nous proposons le mode Active/Standby pour toutes les offres S/M/L.

### Le Load Balancer peut-il être utilisée avec des adresses Additional IP (Failover IP) ?

Non, un nouveau type d’adresse IP a été créé pour ce rôle, Floating IP. Cette nouvelle solution est plus flexible, basée sur un modèle de « paiement à l'usage » (pay-as-you-go). Avec Floating IP, vous pouvez utiliser une seule Floating IP par service Load Balancer.

### Puis-je utiliser plusieurs protocoles (UDP, TCP, HTTP) sur un même Load Balancer ?

Oui, plusieurs *listeners* (frontends) et *pools* (backends) peuvent être configurés. Il n'y a qu'une limitation d'une seule Floating IP par Load Balancer.

### Que se passe-t-il si l'Octavia Load Balancer reçoit plus de requêtes que prévu ? Le prix va-t-il augmenter ? En serai-je informé ?

Tout d'abord, les valeurs indiquées ne sont qu'une estimation des capacités du Load Balancer. Le prix n'augmentera pas. La tarification est liée aux types (small, medium, large) et nous ne pouvons pas changer la flavor pour le moment. Le choix d'orchestration de ses services est à la charge du client.

Il vous revient en tant que client de surveiller le Load Balancer à l'aide de la fonction de metrics et de modifier la flavor en conséquence.

### Je ne vois pas l'interface du Load Balancer dans l'espace client OVHcloud. Où créer des services et modifier des paramètres ?

Load Balancer est disponible via l'interface CLI OpenStack, l'interface utilisateur Horizon et l'APIv6 OVHcloud. L’interface utilisateur de votre espace client sera disponible prochainement.

## Gateway

### Qu’est-ce que la Gateway ? Quelle est sa place dans l’écosystème OpenStack ?

La Gateway est le nom de produit du composant Distributed Virtual Router (DvR) dans OpenStack. Elle est proposée en High Availability et avec un Service Level Agreement.

### Les tarifs de la solution Gateway varient selon la capacité en bande passante. Comment cela peut-il être paramétré / modifié ?

La solution Gateway est proposée en différentes tailles (S/M/L) pour répondre au mieux aux besoins de nos clients. Ces différentes tailles sont définies au travers de règles de QoS. À ce jour, pour modifier la taille de la passerelle, un changement de politique QoS entre S/M/L peut être effectué.

### Est-ce que Gateway peut être utilisé avec des instances Load Balancer dans d'autres régions ?

Ce mode n'est actuellement pas pris en charge. À ce jour, la Gateway prend uniquement en charge les réseaux privés en mono-région pour Public Cloud et il s'agit du seul mode de réseau privé recommandé pour les configurations en environnement de production pour ce produit. Cela inclut également le cas d'usage du Load Balancer public-privé qui nécessite Gateway. Les autres configurations (y compris l'utilisation avec des serveurs bare metal ou multi-région) ne sont pas prises en charge.

### Le routeur virtuel L3 (Gateway) peut-il m'aider si je souhaite avoir une Gateway d'accès à Internet pour toutes les VMs de mon vRack ?

Oui, c'est le cas pour une Gateway (routeur L3 avec option SNAT). Actuellement, seules les instances en **mode privé** de réseau et connectées à un réseau privé à région unique sont prises en charge. Pour plus d'informations, consultez notre [guide concept sur le réseau Public Cloud](/pages/public_cloud/public_cloud_network_services/concepts-01-public-cloud-networking-concepts).

### Puis-je utiliser un routeur L3 pour router le trafic entre différents sous-réseaux dans une région Public Cloud ?

Oui, vous pouvez utiliser un routeur L3 sans option SNAT via l’interface graphique OpenStack / CLI / Terraform. Dans ce cas, les limites de bande passante sont déterminées par la qualité de service sur la bande passante privée de l'instance. Par conséquent, le choix d'une flavor `S` n'aurait pas d'impact sur les performances.

### Le service Gateway sera-t-il fourni avec une IP et un port publics ?

Tout dépend de l’usage :

- Pour les cas d'utilisation sortante (outbound), nous proposons une IP publique incluse dans le prix de la Gateway. Cette IP est associée à la Gateway instanciée et ne peut pas être déplacée vers une autre. En d'autres termes, l'IP utilisée pour le trafic sortant n'est pas une Floating IP. Si cela crée des difficultés pour votre cas d'usage, veuillez voter en faveur de cet item de notre [roadmap](https://github.com/ovh/public-cloud-roadmap/issues/448).
- Pour les cas d'utilisation entrante (inbound) (pour exposer un service s'exécutant sur une instance privée vers Internet), vous devez disposer d'une Floating IP à connecter via Gateway à votre instance ou service réseau.

### Comment générer une instance privée à utiliser avec l'option Gateway et SNAT ?

Vous pouvez créer un réseau privé dans une région sélectionnée et y attacher la Gateway. Puis, lors de la création d’une instance, sélectionnez « Attacher au réseau privé » et validez à l’aide du bouton « Oui, je veux que mon instance soit totalement privée ».

### J'ai créé une instance en mode privé (elle n'a que des ports privés). Comment s’y connecter ?

Deux options peuvent être utilisées : 

- Utiliser un « jump host » (SSH proxy) : Vous devez utiliser une autre instance disposant d'une Floating IP (permettant un accès externe) et d'un port privé dans le même réseau privé que votre nouvelle instance. Connectez-vous dessus et connectez-vous en SSH à l'IP privée de votre nouvelle instance.
- Associer une adresse Floating IP (au moins pendant le temps de la maintenance) à votre instance nouvellement créée et vous y connecter en utilisant cette adresse Floating IP, puis détacher l'adresse Floating IP.

## Les adresses Floating IP

### Lorsque j'essaie d'associer une Floating IP au port du réseau Ext-Net, j'obtiens l'erreur suivante : "External network ... is not reachable from subnet .... Therefore, cannot associate Port ... with a Floating IP."

Une Floating IP est une adresse IP publique flexible qui peut être associée à un port privé uniquement (port sur réseau privé dans le vRack). Une Gateway est également nécessaire pour que cela fonctionne.

### J'ai des VMs qui communiquent sur un réseau privé et je veux associer une Floating IP à une de ces VMs. Quel est le pool à choisir pour l'adresse Floating IP ?

Le pool d'une Floating IP doit être « Ext-Net » et vous pouvez l'associer à un port du réseau privé.

## Aller plus loin

Si vous avez besoin d'une formation ou d'une assistance technique pour la mise en oeuvre de nos solutions, contactez votre commercial ou cliquez sur [ce lien](https://www.ovhcloud.com/fr/professional-services/) pour obtenir un devis et demander une analyse personnalisée de votre projet à nos experts de l’équipe Professional Services.

Échangez avec notre communauté d'utilisateurs sur <https://community.ovh.com/>.