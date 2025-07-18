# Exmen-Docker
RANDRIANOMENJANAHARY Stanis Ryan 
212/lA/24-25
L1A
COMMANDES DE BASE
Commande	Description
docker --version	Affiche la version installée de Docker
docker info	Affiche les informations système sur Docker
docker help	Affiche l’aide générale ou celle d’une commande spécifique
GESTION DES IMAGES
Commande	Description
docker pull <image>	Télécharge une image depuis Docker Hub
docker build -t <nom_image> .	Construit une image Docker à partir d’un Dockerfile
docker images	Liste toutes les images Docker locales
docker rmi <image>	Supprime une image (non utilisée par un conteneur)
docker tag <image> <nouveau_nom>	Renomme une image
GESTION DES CONTENEURS
Commande	Description
docker run <image>	Exécute un conteneur basé sur une image
docker run -it <image>	Lance un conteneur en mode interactif (terminal)
docker run -d <image>	Lance un conteneur en arrière-plan (détaché)
docker run --name <nom> <image>	Donne un nom au conteneur
docker ps	Liste les conteneurs en cours d’exécution
docker ps -a	Liste tous les conteneurs (même arrêtés)
docker start <nom/id>	Démarre un conteneur arrêté
docker stop <nom/id>	Arrête un conteneur
docker restart <nom/id>	Redémarre un conteneur
docker rm <nom/id>	Supprime un conteneur arrêté
INSPECTION & LOGS
Commande	Description
docker logs <nom/id>	Affiche les logs d’un conteneur
docker inspect <nom/id>	Affiche les détails d’un conteneur ou d’une image
docker exec -it <nom/id> bash	Ouvre un shell Bash dans un conteneur actif
VOLUMES ET PORTS
Commande	Description
docker run -v <host_path>:<container_path> <image>	Monte un volume dans le conteneur
docker run -p 8080:80 <image>	Redirige le port 8080 du host vers le port 80 du conteneur
NETTOYAGE
Commande	Description
docker system prune	Supprime les objets inutilisés (images, conteneurs arrêtés, etc.)
docker image prune	Supprime les images non utilisées
docker container prune	Supprime les conteneurs arrêtés
DOCKER COMPOSE (si utilisé)
Commande	Description
docker-compose up	Démarre les services définis dans docker-compose.yml
docker-compose up -d	Idem mais en arrière-plan
docker-compose down	Arrête et supprime les services, réseaux, etc.
docker-compose build	Construit les services
docker-compose ps	Liste les conteneurs de Compose
