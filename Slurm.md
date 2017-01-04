SURM :

SLURM (Simple Linux Utility for Resource Management) est une solution open source d'ordonnancement de tâches informatiques qui permet de créer des grappes de serveurs sous Linux ayant une tolérance aux pannes, type ip-failover, ferme de calcul, système d'ordonnancement des tâches.

Cette solution peut être utilisée sur des grappes de tailles variées, de deux à plusieurs milliers de serveurs. Il est utilisé sur la majorité des plus puissants supercalculateurs de la planète.

Slurm ne nécessite aucune modification du noyau pour son fonctionnement et est relativement autonome.

En tant que gestionnaire de ressources de grappes informatiques, Slurm a trois fonctions principales :

    premièrement, il alloue l'accès aux ressources (les nœuds de calcul) pour les utilisateurs pendant une durée de temps définie afin qu'ils puissent effectuer des taches ;
    deuxièmement, il fournit un cadre pour le démarrage, l'exécution et le suivi des taches (normalement ce sont des taches qui sont parallèles) sur l'ensemble des nœuds affectés ;
    troisièmement, il arbitre l'accès aux ressources par la gestion d'une file d'attente des taches en cours.

Slurm a centralisé le management avec slurmctld pour surveillé les ressources et le travail.
Il peut y avoir un autre slurmctld en backup au cas ou il y aurait un problème.

Chaque noeud du cluster possède un daemon slurmd, qui attend du travail, execute le travail, retourne
les status, puis attends pour plus de travail. Le daemon Slurmd est tolèrent au pannes.

Il y a une option "slurmdbd" qui peut être utilisé pour enregistrer les infos sur les compte qui utilise le cluster slurm. ???????????????


Les outils utilisateur :

SRUN permet d'initier une tâche.
SCANCEL permet d'arrêter une tache en cour ou dans la file d'attente.
SINFO affiche l'état système.
SQUEUE affiche l'état des tâches.
SACCT pour obetenir des informations sur les tâches et les étapes de tâche qui sont en cour ou qui sont terminé.
SMAP et SVIEW sont des commandes qui font un compte rendu graphique du système, de l'état des tâches
et de la topologie du réseau.
SCONTROL est un outils adimin qui permet de surveiller et/ou modifier la configuration le cluster.
SACCTMGR est l'outils qui permet de manager la base de donnée. 

##### IMAGE ######
https://slurm.schedmd.com/arch.gif
##################
