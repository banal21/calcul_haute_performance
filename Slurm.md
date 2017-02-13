##SURM

[SLURM](https://fr.wikipedia.org/wiki/SLURM) (Simple Linux Utility for Resource Management) est une solution open source d'ordonnancement de tâches informatiques qui permet de créer des grappes de serveurs sous Linux ayant une tolérance aux pannes, type ip-failover, ferme de calcul, système d'ordonnancement des tâches.

Cette solution peut être utilisée sur des grappes de tailles variées, de deux à plusieurs milliers de serveurs. Il est utilisé sur la majorité des plus puissants supercalculateurs de la planète.

Slurm ne nécessite aucune modification du noyau pour son fonctionnement et est relativement autonome.

En tant que gestionnaire de ressources de grappes informatiques, Slurm a **trois fonctions principales** :

1. Premièrement, il alloue l'accès aux ressources (les nœuds de calcul) pour les utilisateurs pendant une durée de temps définie afin qu'ils puissent effectuer des tâches.
2. Deuxièmement, il fournit un cadre pour le démarrage, l'exécution et le suivi des tâches (normalement ce sont des tâches qui sont parallèles) sur l'ensemble des nœuds affectés.
3. Troisièmement, il arbitre l'accès aux ressources par la gestion d'une file d'attente des tâches en cours.

Slurm a centralisé le management avec [**slurmctld**](http://manpages.ubuntu.com/manpages/xenial/man8/slurmctld.8.html) pour surveiller les ressources et le travail.
Il peut y avoir un autre slurmctld en backup au cas ou il y aurait un problème.

Chaque noeud du cluster possède un daemon slurmd, qui attend du travail, exécute le travail, retourne
les status, puis attends pour plus de travail. Le daemon Slurmd est tolérant aux pannes.

Il y a une option ([slurmdbd](http://manpages.ubuntu.com/manpages/xenial/man8/slurmdbd.8.html)) qui peut être utilisé pour enregistrer les infos sur les comptes qui utilise le cluster slurm.


####Les outils utilisateur

* SRUN permet d'initier une tâche.
* SCANCEL permet d'arrêter une tâche en cour ou dans la file d'attente.
* SINFO affiche l'état système.
* SQUEUE affiche l'état des tâches.
* SACCT pour obetenir des informations sur les tâches et les étapes de tâche qui sont en cour ou qui sont terminé.
* SMAP et SVIEW sont des commandes qui font un compte rendu graphique du système, de l'état des tâches
et de la topologie du réseau.
* SCONTROL est un outil admin qui permet de surveiller et/ou modifier la configuration du cluster.
* SACCTMGR est l'outil qui permet de manager la base de données. 



![IMAGE](https://slurm.schedmd.com/arch.gif)

A voir : [http://connect.ed-diamond.com/GNU-Linux-Magazine/GLMF-185/Construire-son-cluster-HPC](http://connect.ed-diamond.com/GNU-Linux-Magazine/GLMF-185/Construire-son-cluster-HPC)
