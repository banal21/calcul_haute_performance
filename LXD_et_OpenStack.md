##LXD et OpenStack

Gardons à l'esprit que nous voulons réaliser des calculs dans des conteneurs. En somme, créer un cluser de conteneurs, qui pourrons chacun effectuer un calcul de manière indépendante.

La technologie [Docker](https://fr.wikipedia.org/wiki/Docker_%28logiciel%29) permet déjà de le faire grâce à Docker swarm. [Un tutoriel](https://blogs.msdn.microsoft.com/stephgou/2015/05/11/clusters-de-containers-docker/) proposé par "stephgou" décrit très bien cette technologie.

Nous voulons pousser les recherches pour savoir si cela est possible avec la techonologie LXD (rappel: technologie plus lourde que docker).

Après maintes recherches sur internet, on semble convérger vers le même point : OpenStack.

##Expérimentation

M. Chantrein, tuteur de ce projet, nous à donné le liens d'un [tutoriel](https://www.stgraber.org/2016/10/26/lxd-2-0-lxd-and-openstack-1112/) de mise en place de LXD et d'OpenStack que nous allons suivre.

Plusieurs outils seront utilisés lors de ce tutoriel en voici un bref descriptif :

####OpenStack - Nova

Page wiki : [https://fr.wikipedia.org/wiki/OpenStack](https://fr.wikipedia.org/wiki/OpenStack)

Openstack possède plusieurs outils, celui que nous allons utiliser est [Nova](https://fr.wikipedia.org/wiki/OpenStack#Calcul_:_Nova), qui va contrôler l'hyperviseur LXD.

####Juju 

Juju est développé par [Canonical](https://www.canonical.com/) et est désigné comme un outil d'orchestration cloud. 

Le site web [InfoQ](https://www.infoq.com/fr/) à fait [un entretien](https://www.infoq.com/fr/articles/juju-avancees-et-roadmap) avec Samuel Cozannet, "Strategic Program Manager" chez canonical et membre du projet Juju.

Dans cet entretien, Samuel Cozannet définie l'objectif de Juju comme cela : 

InfoQ FR: Quels sont les buts du projet de façon générale ?

* On assiste aujourd'hui à la nouvelle représentation d'une application, comme un ensemble de micro-services qui sont déployés sur un mix cloud privé/cloud public. L'objectif de Juju, c'est de mettre en relation ces services, de les orchestrer, sur n'importe quel cloud, voire même sur des substrats bare metal (NdE: directement sur des serveurs physiques non-préinstallés), sur des containers, des VM, etc. Toute l'application, complexe, faite de micro-parties va être orchestrée par Juju (on peut penser Big Data, PaaS... Toute application faite de plus de 2 services distincts est potentiellement juju-phile).

####Conjure-up

[Conjure-up](http://conjure-up.io/docs/en/users/#getting-started) est une couche couvrant des technologies sous-jacentes différentes - Juju, MAAS et LXD.

Conjure-up est un package du dépot officiel ubuntu, qui comprend, entre autres, les paquets :

* Juju
* lxd
* lxd-client

Plus de détails sur : [http://packages.ubuntu.com/fr/yakkety/admin/conjure-up](http://packages.ubuntu.com/fr/yakkety/admin/conjure-up)

###Pas à pas

Dans ce tutoriel, il va s'agir d'executer un Openstack complet, en utilisant des conteneurs LXD au lieu de machines virtuelles, et en exécutant le tout dans un "nid" de conteneurs. 

####Etape 1

Création du "nid" de conteneur. Pour faire simple, création d'un conteneur lxd nommé Openstack.

Pour que le "nid" puisse installer les outils Conjure-up / Juju, il lui faut un accès internet mis à place grâce à un "bridge"

	& lxd init
	.
	.
	.
	Would you like LXD to be available over the network (yes/no) [default=no] : **yes**
	Do you want to configure the LXD bridge (yes/no)[default=yes] : **yes**

* Choisir un nom d'interface pour notre bridge : br0
* Choisir un sous-réseau, ici : 10.143.224.1
* CHoisir un masque, ici : /24

* Nota : Ce "nid" de conteneur à besoin de privilèges particuliers

	& lxc launch ubuntu:16.04 openstack -c security.privileged=true -c security.nesting=true -c "linux.kernel_modules=iptable_nat, ip6table_nat, ebtables, openvswitch"

Premier hic : 
	Permisson denied, are you in the lxd group?

Comme préciser [ici](https://github.com/banal21/calcul_haute_performance/blob/master/INSTALL_CONFIG_LXD.md#installation-de-lxd), nous devons créer un nouveau groupe : 

	& newgrp lxd

Relance de la commande : 

	& lxc launch ubuntu:16.04 openstack -c security.privileged=true -c security.nesting=true -c "linux.kernel_modules=iptable_nat, ip6table_nat, ebtables, openvswitch"
	Creating openstack
	Retrieving image: 100%
	Starting openstack

Puis :

	& lxc config device add openstack mem unix-char path=/dev/mem

Pour les versions de LXD inférieur à 2.5, il y a un bug qui est réctifié avec : 

	& lxc exec openstack -- ln -s /bin/true /usr/local/bin/modprobe

Nota : pour voir la version de LXD entrer : 

	& lxd --version

#####Etape 2

Création d'un couple de [PPA](https://doc.ubuntu-fr.org/ppa) et installation de conjure-up, qui va nous permettre d'utiliser l'outil de déployement OpenStack avec Nova :
	
	& lxc exec openstack -- apt-add-repository ppa:conjure-up/next -y
	& lxc exec openstack -- apt-add-repository ppa:juju/stable -y
	& lxc exec openstack -- apt update
	& lxc exec openstack -- apt dist-upgrade -y
	& lxc exec openstack -- apt install conjure-up -y

Configuration de lxd à **l'interieur** du "nid" : 

	& lxc exec openstack -- lxd init

* **/!\** Le système de fichier ZFS ne fonctionne pas dans un conteneurs imbriqué lxd. choisir **dir**
* Ne pas configurer d'adresse Ipv6 lors de la configuration du bridge, conjure-up/Juju ne fonctionne pas bien avec. 

Paramètres du bridge :

* Interface : br0
* Adresse Ipv4 : 10.137.44.1
* Masque : /24




