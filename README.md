# Présentation du Projet : Containerisation d'une application web avec Docker

Ce projet vise à containeriser une application web de démonstration permettant aux utilisateurs de définir et de suivre leurs objectifs. Pour ce faire, nous utiliserons Docker pour créer trois conteneurs distincts : un pour le backend développé avec Node.js, un pour le frontend développé avec React, et un pour notre base de données MongoDB.

## Avant de plonger dans les détails du projet, examinons les prérequis pour chaque conteneur pour assurer le bon fonctionnement de l'application.

### Prérequis pour chaque conteneur

**Conteneur MongoDB**
- **Persistance des données** : Il est essentiel que les données de la base de données MongoDB persistent même si le conteneur est arrêté ou supprimé. Pour cela, nous utiliserons un volume nommé pour stocker les données de manière durable.
- **Accès limité** : Pour améliorer la sécurité du système, nous limiterons l'accès à la base de données MongoDB en utilisant des variables d'environnement.

**Conteneur Node.js (Backend)**
- **Persistance des données** : Pour assurer la persistance des données même en cas d'arrêt ou de suppression du conteneur, nous utiliserons un volume pour stocker les logs du backend.
- **Réflexion des changements de code source** : Pour faciliter le développement et l'itération du code, les modifications apportées au code source du backend seront immédiatement reflétées dans le conteneur grâce à un bind mount.

**Conteneur React (Frontend)**
- **Réflexion des changements de code source** : De manière similaire au backend, les modifications apportées au code source du frontend seront directement reflétées dans le conteneur grâce à un bind mount.

Avec une meilleure compréhension des prérequis pour chaque conteneur, nous pouvons désormais explorer les avantages de l'utilisation de Docker Compose.

## Avantages de l'utilisation de Docker Compose

Docker Compose simplifie grandement la gestion des conteneurs en utilisant un seul fichier YAML pour définir et gérer l'ensemble de l'infrastructure du projet. Il facilite également le déploiement de l'application avec toutes ses dépendances en une seule commande, et permet de configurer l'application pour différents environnements en utilisant des fichiers d'environnement.

Avec ces informations en tête, passons maintenant aux différents types de volumes utilisés dans le projet et les raisons qui les sous-tendent.

### Types de volumes utilisés et leurs raisons

Dans ce projet, nous avons utilisé différents types de volumes pour répondre à des besoins spécifiques :
- **Volume nommé pour la base de données MongoDB (data)** : Ce volume est essentiel pour stocker les données de manière persistante, même lorsque le conteneur est arrêté ou supprimé, assurant ainsi la disponibilité des données entre les redémarrages du conteneur.
- **Volume pour les logs du backend (logs)** : En utilisant un volume, nous préservons les logs du backend de manière persistante, facilitant ainsi le débogage et la surveillance de l'application sans craindre de perdre les données en cas de redémarrage du conteneur.
- **Bind mount pour le code source du backend (./backend:/app)** : L'utilisation d'un bind mount permet aux modifications apportées au code source du backend d'être immédiatement reflétées dans le conteneur, sans nécessiter de nouvelles constructions d'image. Cela facilite le développement et l'itération du code.
- **Bind mount pour le code source du frontend (./frontend/src:/app/src)** : De même, un bind mount est utilisé pour le code source du frontend, permettant des modifications rapides du code sans reconstruire l'image du conteneur.

Enfin, nous examinerons pourquoi l'utilisation d'un fichier .dockerignore est une bonne pratique pour ce projet.

### Explication des Ports

- **Port 80** : Ce port est exposé par le conteneur du backend, ce qui permet aux utilisateurs d'accéder à l'application depuis l'extérieur. Les requêtes HTTP arrivant sur ce port sont acheminées vers le backend de l'application.
- **Port 3000** : Ce port est exposé par le conteneur du frontend. Il permet d'accéder à l'interface utilisateur du frontend de l'application depuis l’extérieur.

### Utilité du fichier .dockerignore

Le fichier .dockerignore est d'une importance capitale pour ce projet car il permet de spécifier les fichiers et dossiers qui ne doivent pas être copiés dans le conteneur lors de la construction de l'image. En excluant les fichiers inutiles tels que node_modules, Dockerfile et les fichiers et dossiers liés à Git, nous réduisons la taille de l'image et accélérons le processus de construction.

Pour conclure, nous verrons comment utiliser le fichier docker-compose.yml pour gérer facilement les conteneurs de l'application.

### Utilisation de Docker Compose

Pour démarrer l'ensemble de l'application avec tous les services, il suffit d'utiliser la commande `docker-compose up`. Lorsque tu souhaites arrêter l'application et supprimer les conteneurs, la commande `docker-compose down` est la solution. Ces commandes simplifient grandement le déploiement et la gestion de l'application, en s'assurant que tous les conteneurs nécessaires sont démarrés dans l'ordre correct et en liant les volumes appropriés pour la persistance des données.


<img width="1021" alt="Screenshot 2023-07-28 at 17 48 44" src="https://github.com/nourdevopss/NodeDocker/assets/120333964/2df4e666-c7b8-455d-9ae2-b7ba2c28f868">


<img width="1267" alt="Screenshot 2023-07-28 at 17 58 26" src="https://github.com/nourdevopss/NodeDocker/assets/120333964/a270f541-bd10-401f-af00-f076a6321875">

<img width="1274" alt="Screenshot 2023-07-28 at 17 47 13" src="https://github.com/nourdevopss/NodeDocker/assets/120333964/b0ec4a04-e7ca-46e6-a7b5-8ccca1eb3454">

<img width="1276" alt="Screenshot 2023-07-28 at 17 47 30" src="https://github.com/nourdevopss/NodeDocker/assets/120333964/44de3202-f9f2-412c-ba1c-cf9407535ef0">

<img width="1272" alt="Screenshot 2023-07-28 at 18 02 13" src="https://github.com/nourdevopss/NodeDocker/assets/120333964/b740dbff-1085-4421-a7c3-9bedab82acf5">

