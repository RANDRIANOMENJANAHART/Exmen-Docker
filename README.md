Exmen-Docker
RANDRIANOMENJANAHARY Stanis Ryan 
212/lA/24-25
L1A

## Généralité sur Docker

Docker est un outil qui a popularisé la conteneurisation. C'est une forme de virtualisation permettant d'exécuter plusieurs services sur une même machine physique ou virtuelle.

### Objectifs

* Simplifier les déploiements
* Modifier le format des livrables
* Gérer plus facilement les dépendances

---

## Concepts de base

**Image** : une archive figée contenant tout le nécessaire pour faire tourner une application :

* Le code exécutable
* Ses dépendances

**Conteneur** : instance d'une image, exécutant un ou plusieurs processus avec isolement via cgroups / namespaces.

---

## Commandes Docker de base

```bash
sudo usermod -aG docker $USER
```

Ajoute l'utilisateur courant au groupe Docker pour exécuter les commandes sans sudo.

```bash
docker ps
```

Liste les conteneurs en cours d'exécution.

```bash
docker ps -a
```

Affiche tous les conteneurs, actifs ou non, avec détails.

```bash
docker ps -q
```

Liste uniquement les IDs des conteneurs en cours d'exécution.

```bash
docker ps -qa
```

Liste les IDs de tous les conteneurs (actifs ou non).

```bash
docker run nginx:latest
```

Démarre un conteneur Nginx en téléchargeant l'image si besoin.

```bash
docker run -d nginx:latest
```

Exécute Nginx en mode détaché (arrière-plan).

```bash
docker run -d --name c1 nginx:latest
```

Lance Nginx dans un conteneur nommé "c1" en mode détaché.

```bash
docker rm -f c1
```

Supprime immédiatement le conteneur "c1", même s'il tourne.

```bash
docker run -ti --name c1 debian:latest
```

Crée un conteneur Debian avec accès terminal (bash).

```bash
docker run -ti --rm --name c1 debian:latest
```

Crée un conteneur Debian temporaire (effacé à la fermeture).

---

## Docker Volume

Un volume Docker est un espace de stockage persistant permettant de sauvegarder les données même après suppression du conteneur.

### Avantages :

* Persistance de données
* Sauvegardes facilitées
* Partage entre plusieurs conteneurs
* Gestion des droits
* Volumes locaux ou distants

```bash
docker volume ls
```

Affiche tous les volumes Docker disponibles.

```bash
docker volume create mynginx
```

Crée un volume nommé "mynginx" pour y stocker les données de conteneur.

```bash
docker run -d --name c1 -v mynginx:/usr/share/ngninx/html/ nginx:latest
```

Monte le volume "mynginx" à l'intérieur du conteneur, dossier web de Nginx.

```bash
docker exec -ti c1 bash
```

Ouvre un terminal dans le conteneur "c1".

```bash
docker volume inspect mynginx
```

Affiche les détails du volume "mynginx" (chemin, métadonnées).

---

## Types de Volumes

### Bind Mount

Permet de relier un dossier local à un dossier du conteneur.

```bash
sudo mkdir /data && sudo mkdir /data2 && sudo touch /data/Hello && sudo mount --bind /data /data2 && sudo findmnt
```

Le montage bind crée un lien entre deux répertoires. Ce qui est dans l'un se retrouve dans l'autre.

### Exemple de commande avec Bind Mount

```bash
docker run -d --name c1 --mount type=bind,source=/data/,destination=/usr/share/nginx/html/ nginx:latest
```

Montage direct du dossier local /data dans le conteneur.

```bash
docker inspect --format "{{.Mounts}}" c1
```

Affiche les informations de montage du conteneur "c1".

### Docker Volume (autre forme)

```bash
docker run -d --name c2 --mount type=volume,source=mynginx,destination=/usr/share/nginx/html/ nginx:latest
```

Utilise le volume "mynginx" de façon équivalente à l'exemple précédent.

---

## Docker Networks

Les réseaux Docker permettent la communication entre conteneurs et avec l'extérieur.

### Bridge (par défaut)

Mode réseau par défaut. Chaque conteneur est connecté à un réseau isolé via docker0 (IP : 172.17.0.1/16).

#### Commandes utiles :

```bash
ip a
sudo ifconfig
docker network ls
```

```bash
docker run --name c1 -d debian sleep infinity
```

Démarre un conteneur Debian en attente.

```bash
docker exec -ti c1 bash
```

Accès au shell du conteneur.

```bash
apt install iputils-ping net-tools
```

Installe les outils de test réseau.

```bash
ifconfig
```

Montre les interfaces et IP.

### Réseau personnalisé

```bash
docker network create --driver=bridge --subnet=192.168.0.0/24 reseau1
```

Crée un réseau privé nommé "reseau1".

```bash
docker network inspect reseau1
```

Détails du réseau "reseau1".

```bash
docker run -d --name c1 --network reseau1 nginx:latest
```

Conteneur connecté au réseau personnalisé.

```bash
docker run -d --name c2 --network reseau1 nginx:latest
```

Lance un second conteneur dans le même réseau.

### Ping entre conteneurs :

```bash
docker exec -ti c2 bash
apt install iputils-ping
ping c1
```

Test de connectivité avec résolution DNS automatique.

---

## Dockerfile

Le Dockerfile est un script décrivant la construction d'une image Docker : base, instructions, configuration, point d'entrée, etc.

### Instructions principales

```bash
docker build -t myimage .
```

Construit une image à partir du Dockerfile courant.

```bash
docker images
```

Liste les images Docker présentes localement.

```bash
docker run -d -p 8080:80 myimage
```

Lance un conteneur accessible via localhost:8080

```bash
docker run -d --name c1 myimage
```

Exécute un conteneur à partir de "myimage".

```bash
docker rmi -f myimage
```

Force la suppression de l'image "myimage".

---

## Docker Layers

Chaque instruction dans un Dockerfile crée une couche. Une couche est une modification enregistrée. L'ensemble des couches constitue l'image.

### Avantages :

* Mise en cache pour accélérer les reconstructions
* Partage entre images
* Optimisation disque
* Isolation logique
