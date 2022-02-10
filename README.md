## Partie II : sur une infrastructure "Cloud"

Mots-cléfs : `docker`, `déploiement continu`, `kubernetes`

### Préparation des images

Le travail se fera dans un dépots Git distinct du premier.

Nous allons chercher à créer une image pour le service _Dolibarr_.

Pour chaque service, écrire les scripts et configuration (`Dockerfile`, `docker-compose.yml`, etc.) permettant de :

* créer une image docker
* vérifier son bon fonctionnement
* pousser cette image en ligne sur DockerHub.

Notez que cette image: 

* doit être basées sur Debian Buster 64 bits
* doit intégrer Apache2 et PHP 7 et les modules nécessaires à Dolibarr
* dépend d'un container MariaDB indépendant pour fonctionner

### Préparation de l'infrastructure

Créer un cluster Kubernetes avec 3 noeuds 

* soit sur un opérateur Cloud de votre choix (Digital Ocean, Linode, OVH, Azure, AWS, GCP, etc)
* soit installé _on-premises_ (pour les plus motivés) 
  * sur des serveurs VPS
  * ou sur des VM Vagrant

__Attention:__ la version _on-premises_ sera plus compliquée à gérer pour le load-balancing.

### Déploiement

Ecrire la configuration Kubernetes permettant de déployer le services suivants :

* _MariaDB_ 
  * sur une seule réplique ;
  * avec les bons volumes pour sauver les données et la configuration de l'application ;
* _Dolibarr_ 
  * sur 2 répliques
  * paramétré pour se connecter sur MariaDB ;
  * avec les bons volumes pour sauver les données et la configuration de l'application ;
* un _load balancer_ permettra de balancer les requêtes entrantes d'une réplique à l'autre (round-robin).


### Déploiement continu

Utiliser un outil de déploiement continu (Jenkins, Travis, CircleCI, Gitlab-CI, etc) connecté à votre dépot Git de telle sorte que 
  * chaque `git push` déclanche le _rebuild_ des images concernées ;
  * si le build de l'image réussi, alors la nouvelle version de l'image est déployée sur votre cluster.

## Méthodologie

### Organisation

Le projet sera réalisé en équipes de deux ou trois personnes.

Vous vous organiserez pour distribuer les taches afin que tout le monde participe aux deux parties du projet.

L'utilisation d'un outil de gestion de projet (gitlab, trello, etc.) sera fortement apprécié.

Note: à trois, donnez-vous à fond pour faire quelques élements bonus également.


### Suivi et questions

Vous pouvez envoyer un email avec vos questions à  teaching@glenux.net. Ce mail devra indiquer `[DEVOPS FITEC] QUESTION` dans le titre.

Une réponse sera fournie lors de la prochaine journée de suivi/accompagnement de projet.

### Rendu du projet

Le rendu sera fait par l'envoi d'un email, à destination de teaching@glenux.net. Ce mail devra indiquer `[DEVOPS FITEC] RENDU FINAL` dans le titre.

Cet email listera les membres de votre groupe (nom, prénom & email) 

Il devra également fournir les liens vers vos deux dépots GIT publics (distincts pour chaque partie).

Chaque dépot GIT contiendra un fichier `README.md` qui documentera votre démarche et expliquera étape par étape comment utiliser vos scripts pour obtenir l'infrastructure demandée dans ce projet.

### Soutenance

Durant la soutenance vous présenterez au jury le projet, ses enjeux et l'apport votre travail.

Vous expliquerez plus particulierement votre démarche de travail, l'organisation du projet et les différents points techniques (avec schéma, documentation, etc.)

Vous ferez la démonstration du bon fonctionnement de chacune des infrastructures que vous avez conçu. Le détail des démonstration attendues est précisé ci-dessous.

Vous pouvez utiliser un support de présentation (ex: diaporama).
  
#### Démonstration pour la Partie II

* Détruire l'un des pods de Dolibarr
* Montrer que le service continue à fonctionner
* Montrer que la seconde réplique du Pod est revenue


:thumbsup: 
