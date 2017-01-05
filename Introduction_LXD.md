##Introduction à LXD

####Qu'est-ce que c'est ?

LXD est un projet fondé par [Canonical ltd](https://www.canonical.com/). Ce n'est pas une nouvelle verision de [*LXC*](https://github.com/banal21/calcul_haute_performance/blob/master/DOCKER_LXC_recap.md), c'est un projet à part entière.

LXD est donc plus complet que *LXC* et propose :

* Une gestion des images. (Les modèles qui permettent de créer des conteneurs).
* La gestion des conteneurs. (Démarrage, snapshot, annulation, etc ...).
* La gestion de multiples serveurs distant. (Gestion de serveurs distants et locaux).
* La migration de conteneur en ligne.

LXD est nommé [Hyperviseur](https://fr.wikipedia.org/wiki/Hyperviseur) par la société Canonical. 

LXD comprend trois composants : 

* Un démon qui fournit une API REST (voir [http://blog.pilotsystems.net/2012/septembre/les-api-rest](http://blog.pilotsystems.net/2012/septembre/les-api-rest)). Cette API REST va permettre de discuter avec les serveurs en HTTP/HTTPS et de travailler en local ou en distant.
* Un outil en ligne de commande LXC. Avec la même base de stack de commandes, mais en en rajoutant d'autres. 
* Un plug-in Openstack qui va permettre à Openstack d'utiliser les commandes LXC pour gérer les conteneurs. 

(source : [https://www.youtube.com/watch?v=kXnMHZym86Q](https://www.youtube.com/watch?v=kXnMHZym86Q)).

##Installation de LXD

Sur la version UBUNTU 16.04 LTS (celle qui nous utilisons) : 

	$ sudo apt-get install lxd

Par défaut, LXD va créer un nouveau groups d'utilisateur. Les membres des groupes *admin* et *sudoers* sont ajouté automatiquement.
Si votre utilisateur ne fait pas partie de ces groupes, vout pouvez l'ajouter automatiquement avec la commande : 

	$ newgrp lxd

Ensuite, place à la configuration : 

	$ sudo lxd init
	Name of the storage backend to use (dir or zfs) [default=dir]: 

Ici, on nous demande quel système de stockage nous voulons utiliser (dir ou zfs). *ZFS* est beaucoup plus rapide que *dir* et Ubuntu 16.04 LTS supporte le ZFS, nous allons donc partir là-dessus.

A titre de comparaison *"Arne svendsen"* à poster un commentaire sur l'article ["LXD, ZFS and bridged networking on Ubuntu 16.04 LTS"](https://bayton.org/2016/05/lxd-zfs-and-bridged-networking-on-ubuntu-16-04-lts/) :

>I also did some tests in VB with same virtualized hardware and can confirm that the difference is huge compared to zfs and dir.
>
>Create second container:
>ZFS: 16,2
>DIR: 50,2
>DIR ON ZFS: 1,09 seconds
>
>Create LXC snapshot:
>ZFS: 0,5 seconds (My fingers are too slow to react. Probably much less).
>DIR: 44 seconds
>DIR ON ZFS: 1,08 seconds 

Nota : Pour pouvoir utiliser ZFS, des paquets suplémentaires sont necessaires :

	$ sudo apt-get install zfsutils-linux

Et pendant qu'on y est, pour la mise en place du "bridge", nous auront besoin d'utilitaires contenus dans le paquet *bridge-utils* :

	$ sudo apt-get install bridge-utils

