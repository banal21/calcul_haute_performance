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

	On assiste aujourd'hui à la nouvelle représentation d'une application, comme un ensemble de micro-services qui sont déployés sur un mix cloud privé/cloud public. L'objectif de Juju, c'est de mettre en relation ces services, de les orchestrer, sur n'importe quel cloud, voire même sur des substrats bare metal (NdE: directement sur des serveurs physiques non-préinstallés), sur des containers, des VM, etc. Toute l'application, complexe, faite de micro-parties va être orchestrée par Juju (on peut penser Big Data, PaaS... Toute application faite de plus de 2 services distincts est potentiellement juju-phile).

####Conjure-up

[Conjure-up](http://conjure-up.io/docs/en/users/#getting-started) est une couche couvrant des technologies sous-jacentes différentes - Juju, MAAS et LXD.
