##Docker Swarm


Docker Swarm est la technologie native, proposée par Docker pour gérer le clustering de containers Docker. Plus précisément il permet de créer des groupes de serveurs hôtes exécutant les services de Docker, de les exposer comme un seul hôte Docker virtuel, puis de configurer des containers Docker en gérant automatiquement la répartition de la charge et la gestion de l'état du cluster.

Docker Swarm utilise l'API standard de Docker, pour utiliser Swarm il suffit donc d'être connecté a un outil qui communique avec un démon de Docker pour réaliser les mêmes actions sur de multiples hôtes Docker de manière transparente.

Docker Swarm est fourni nativement avec un mécanisme simple d'orchestration complétée par des points d'extensibilité permettant de le remplacer par des solutions pour les déploiements de production à grande échelle.


###Comment fonctionne Swarm


Swarm est un sheduler de ressources, c'est-à-dire un service qui a une vue sur toutes les instances (serveurs) Docker, et qui est le point d'entrée uiversel vers tous ces noeuds. Par exemple, c'est Swarm qui se charge d'instancier un conteneur sur le cluster. Swarm choisit l'emplacement de ses déploiements en fonction de certaines règles, filtres ou stratégies de déploiement. Par exemple, on peut spécifier les besoins d'un container à un certain niveau de CPU et de RAM; Swarm effectuera son choix d'hôte Docker de façon à répondre à ces conditions.

Autres possibilité offerte par Swarm, celle de tagger les hôtes Docker avec des labels: un label SSD permettra à Swarm d'identifier les hôtes plus performants pour déployer un Docker base de données.
Les labels peuvent aussi être utilisés pour identifier des régions.

Avec la version de Docker 1.12, Swarm est maintenant totalement intégré au Docker engine en tant que Swarm Mode. Il est activable à la volée et permet de monter très facilement un cluster Sawrm. C'est une très grosse évolution qui simplifie énormément la mise en place de Swarm: plus de PKI à gérer soi même, plus besoin de cluster KV tels que Consul ou Etcd.


##Configurer Docker Swarm


###Création des VM


Pour commencer il faut déployer des serveurs afin de lancer le cluster. Créer 3 machines virtuelles avec la commande docker-machine. 

* 1 VM manager : la machine docker swarm qui héberge le système de discovery des services docker.
* 2 VM nodes : les machines docker swarm qui participent à l'hébergement des services.
* consul : datastore permettant le stockage d'élément de configuration
	

###Créer un cluster swarm


Commencer par installer sur chaque serveur, Docker Engine, puis configurer un discovery back-end. Pour que le swarm manager connaisse quel noeud est accessible, il utilise quelque chose appelé "le consul", qui lui travaille comme un discovery back-end. En général, "le consul" tourne sur son propre hôte, mais vous pouvez très bien le mettre sur le manager primaire. Le service du consul va permettre de maintenir une list d'adresse IP dans votre cluster swarm.

La façon la plus simple de configurer une installation Docker swarm est d'utiliser l'image officiel. L'image est construite et mise à jour régulierement par Docker eux-mêmesà  travers des process automatiques.
Une fois installez sur le manager, attribuez des adresses IP a vos serveurs.
Après la configuration des adresse IP docker swarm est prêt a être testé.

Notez que si vous utilisez CentOS ou tout autres OS avec une similarité de restriction de pare-feu par défaut, vous devrez ajouter le numéro de port de chaque commande aux règles de votre pare-feu pour autorisé swarm à communiquer.


###Démarrer swarm


Docker fonctionne de façon très similaire à un Docker traditionnel. Toutefois, vous aurez besoin de définir l'hôte pour exécuter les commandes sur les autres conteneurs Swarm. Le gestionnaire Docker swarm, lorsqu'il est configuré comme-ci dessus, permet d'exécuté des commande à partir de tout hôte avec Docker installé qui a accès au gestionnaire d'hôte. Vérifiez la configuration sur le manager primaire en utilisant la commande ci-dessous:


	'docker -H <manager IP>:4000info'
	
	
Le résultat de la commande listera les informations à propos de swarm et de ces nodes. Si votre consul serveur est apte à découvrir vos nodes, ils seront alors listés ave des informations similaires. Vous aurez alors accès à des informations utiles tels que le nombre de conteneurs installés, le nombre de CPU et de coeur, la quantité de RAM, ...
Si les nodes sont listés comme (unknow), votre consul serveur sera incapable de communiqueravec eux, dans ce cas vérifiez les règles de votre pare-feu.
Vous pouvez démarrer un conteneur sur votre swarm avec la commande habituel run-command. Testez votre installation an lançant le conteneur hello-world avec la commande suivante.


	'docker -H <manager IP>:4000 run hello-world'
	
	
Vérifiez quels nodes de votre cluster fait tourner l'application.


	'docker -H <manager IP>:4000 ps -a'
	
####Sources


[supinfo](https://www.supinfo.com/articles/single/3037-comment-configurer-docker-swarm)
[IT wars](http://www.it-wars.com/posts/virtualisation/docker-swarm-par-lexemple/)
[d2-si](http://blog.d2-si.fr/2016/06/29/start-up-docker-swarm/)
