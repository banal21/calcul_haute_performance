#Calcul haute performance

Pour réaliser leurs calculs, certains chercheurs utilisent des grappes de serveurs de calcul (cluster de calcul).

Les utilisateurs s'authentifient sur le serveur maître et soumettent leurs travaux (jobs) à un planificateur (sheduler), qui placent ces processus sur les machines "esclaves".

Ce systèmes présente 2 défauts majeurs :

1. Les processus sont perdus en cas de panne de courant.
2. Les processus ne sont pas isolés entre eux. Un processus défectueux est donc en mesure de créer des effets de bords sur un autre processus.

Les nouvelles technologies de contenerisations (docker, lxd) sont en mesure d'apporter une réponse à ces deux défauts : 

* Un conteneur permet d'isoler un ou plusieurs processus
* On peut effectuer un instantané mémoire incluse (snapshot stateful) d'un conteneur, ce qui permet, en cas de coupure de courant, de relancer le processus à partir de son dernier instantané.

_L'objectif_ du projet est de réaliser un état de l'art sur l'utilisation de technologie de conteneurisation dans le contexte des calculs hautes performance.