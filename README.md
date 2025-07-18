# Exmen-Docker
RANDRIANOMENJANAHARY Stanis Ryan 
212/lA/24-25
L1A
1. Commandes de base

    docker --version : Affiche la version de Docker installée.

    docker info : Donne les infos système sur le moteur Docker.

    docker help : Affiche l’aide générale ou spécifique à une commande.

2. Commandes sur les images

    docker pull <image> : Télécharge une image depuis Docker Hub.

    docker build -t <nom_image> . : Construit une image à partir d’un Dockerfile.

    docker images : Liste les images locales.

    docker rmi <image> : Supprime une image Docker.

    docker tag <image> <nouveau_nom> : Renomme ou tag une image.

3. Commandes sur les conteneurs

    docker run <image> : Lance un conteneur à partir d’une image.

    docker run -it <image> : Lance un conteneur en mode interactif (terminal).

    docker run -d <image> : Lance un conteneur en arrière-plan.

    docker run --name <nom> <image> : Donne un nom personnalisé au conteneur.

    docker ps : Liste les conteneurs en cours d’exécution.

    docker ps -a : Liste tous les conteneurs, même arrêtés.

    docker start <nom/id> : Démarre un conteneur arrêté.

    docker stop <nom/id> : Arrête un conteneur actif.

    docker restart <nom/id> : Redémarre un conteneur.

    docker rm <nom/id> : Supprime un conteneur arrêté.

4. Inspection et journalisation

    docker logs <nom/id> : Affiche les logs d’un conteneur.

    docker inspect <nom/id> : Affiche les détails techniques d’un conteneur/image.

    docker exec -it <nom/id> bash : Ouvre un terminal Bash dans le conteneur.

5. Volumes et ports

    docker run -v <chemin_hôte>:<chemin_conteneur> <image> : Monte un volume local dans le conteneur.

    docker run -p <port_hôte>:<port_conteneur> <image> : Redirige un port du conteneur vers l’hôte.

6. Nettoyage du système

    docker system prune : Supprime tout ce qui n’est pas utilisé (dangereux si mal utilisé).

    docker image prune : Supprime les images inutilisées.

    docker container prune : Supprime les conteneurs arrêtés.

7. Commandes Docker Compose

    docker-compose up : Démarre les services définis dans le docker-compose.yml.

    docker-compose up -d : Démarre les services en arrière-plan.

    docker-compose down : Arrête et supprime tous les services, réseaux, etc.

    docker-compose build : Construit les images des services.

    docker-compose ps : Liste les conteneurs gérés par Compose.
