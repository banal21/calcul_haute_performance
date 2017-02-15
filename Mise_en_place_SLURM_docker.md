##Mise en place SLURM - DOCKER

###Test d'une solution de déployement.

####L'idée

Nous avons un maitre qui va essayer d'envoyer des jobs aux nodes.

En distingue deux deamons slurm :

* slurmctld -> Contrôleur présent sur le maitre.
* slurmd -> deamon présent sur les esclaves.

Si nous voulons envoyer des jobs dans des conteneurs, il va faloir que nos conteneurs possède le deamon slurmd (pour les esclaves), eventuellement, un maitre stocké dans un conteneur aura besoin de slurmctld.

En à donc deux possibilités : 

* Créer un docker sur base centOS ou debian, installer nous même slurmd (pour les esclaves), slurmctld (pour les maitres).
* Rechercher et pull des images docker existantes avec slurmd, slurmctld de mis en place.

La première solution parraît très compliqué, et la communauté de Docker est relativement active, nous trouvons sans problèmes des images Dockers avec slurmd / slurmctld de mis en place.

Nous allons donc partir sur la deuxième solution.
Les images les plus populaires avec slurmd : 

* [https://hub.docker.com/r/qnib/slurmd/](https://hub.docker.com/r/qnib/slurmd/) 
* [https://hub.docker.com/r/datadrivenhpc/slurmd/](https://hub.docker.com/r/datadrivenhpc/slurmd/)
* [https://hub.docker.com/r/qnib/slurmctld/](https://hub.docker.com/r/qnib/slurmctld/)
* [https://hub.docker.com/r/datadrivenhpc/slurmctld/](https://hub.docker.com/r/datadrivenhpc/slurmctld/)

