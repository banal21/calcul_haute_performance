###Introduction à LXD

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