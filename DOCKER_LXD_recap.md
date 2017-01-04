### Docker et lxc, des outils de création de *containers* 

Pour la réalisation de se projet, nous allons nous intéresser à quelques outils de création de *containers* tel que :

* Docker
* lxc

Ces technologie de conteneurisation est relativement récente et permet :

* aux développeurs de faire tourner n'importe quel langage, n'importe quelle base de donées, dans n'importe quel système LINUX. Le développeur gère lui-même les applications qu'il utilise, les librairies, le code... Et ne se préoccupe pas du déploiement.

* aux "opérationnels" ou administrateur système, d'utiliser ces outils sur n'importe quel système LINUX, tournant sur n'importe quel cloud, ou type de machine (physique ou virtuel). Ils s'occupent du déploiement, du monitoring, de la configuration réseau.

Extrait de [www.infoq.com](https://www.infoq.com/fr/articles/docker-sous-le-capot)


#####Ces utilitaires utilisent des fonctionnalités du noyau LINUX tel que les *namespaces*, le contrôle d'accès obligatoire (MAC) et les groupes de contrôles (CGROUPS).

* Les namespaces vont permettre de rendre indépendante des fonctionnalités. Par exemple, plusieurs interfaces réseaux avec chacunes leur propre table de routage évoluront indépendamment les unes des autres. Ou des processus seront isolés et ne pourrons pas communiquer les uns avec les autres. Ou encore, des utilisateurs partageront des espaces de droit isolés, permettant ainsi d'être root dans un conteneurs sans pouvoir être root sur l'hôte.

* [Le MAC (Mandatory acces control)](http://blog.securite.free.fr/index.php/mac-dac-rbac-on-parle-de-controle-dacces) utilisé lorsque les décisions de protection ne doivent pas être prises par le propriétaire des objets concernés.

* CGROUPS (groupe de contrôle). Cette fonctionnalité du noyau est utilisé pour limiter (et mesurer) l'usage du [CPU](https://fr.wikipedia.org/wiki/Processeur), l'utilisation réseau, la consommation de RAM pour chaque conteneurs.

C'est grâce à ces fonctionnalités du noyau LINUX que l'équipe de développeurs composée de Daniel Lezcano, Serge Hallyn, Stéphane Graber a pu déployer [lxc](https://linuxcontainers.org/fr/).
