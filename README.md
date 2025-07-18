# Exmen-Docker
RANDRIANOMENJANAHARY Stanis Ryan 
212/lA/24-25
L1A

# 📦 Cheat Sheet Docker (avec explication en français)

## 🐳 Docker : Généralités
Docker est un outil qui a révolutionné le monde de l’infrastructure en permettant la conteneurisation des applications. Il facilite le déploiement, l’automatisation et la livraison des logiciels.

---

## 🎯 Objectifs de Docker
- Simplifie les processus de déploiement
- Change la manière de livrer les applications
- Gère efficacement les dépendances

---

## 🧱 Concepts Clés

### 📄 Image
Une **image** Docker est une entité inactive contenant :
- Le code de l'application
- Ses dépendances
- Les configurations nécessaires

### 📦 Conteneur
Un **conteneur** est une instance d’une image, active, isolée, pouvant exécuter un ou plusieurs processus.

---

## 🔧 Commandes de Base

| Commande | Description |
|---------|-------------|
| `sudo usermod -aG docker $USER` | Ajouter l'utilisateur courant au groupe docker |
| `docker ps` | Liste les conteneurs actifs |
| `docker ps -a` | Liste tous les conteneurs (actifs et inactifs) |
| `docker ps -q` | Affiche les IDs des conteneurs actifs |
| `docker ps -qa` | Affiche les IDs de tous les conteneurs |
| `docker run nginx:latest` | Lance l’image nginx |
| `docker run -d nginx:latest` | Lance nginx en arrière-plan (détaché) |
| `docker run -d --name c1 nginx:latest` | Lance nginx avec le nom `c1` |
| `docker rm -f c1` | Supprime le conteneur nommé `c1` |
| `docker run -ti --name c1 debian:latest` | Lance debian avec terminal interactif |
| `docker run -ti --rm --name c1 debian:latest` | Comme ci-dessus, mais le conteneur se supprime à la fermeture |

---

## 📁 Docker Volume

Les **volumes Docker** permettent de stocker les données en dehors du cycle de vie d’un conteneur.

### 🔸 Avantages
- Persistance des données
- Partage entre conteneurs
- Sauvegarde facilitée
- Gestion des permissions

### 📌 Commandes
| Commande | Description |
|---------|-------------|
| `docker volume ls` | Liste tous les volumes |
| `docker volume create monvolume` | Crée un volume nommé `monvolume` |
| `docker volume inspect monvolume` | Détaille un volume |

```bash
docker run -d --name c1 -v monvolume:/usr/share/nginx/html/ nginx:latest
docker exec -ti c1 bash
```

---

## 🔗 Bind Mount

Permet de lier un dossier de l’hôte vers un conteneur.

```bash
sudo mkdir /data /data2
sudo touch /data/Hello
sudo mount --bind /data/ /data2
sudo findmnt
```

| Type | Effet |
|------|-------|
| **Bind mount** | Écrase les fichiers présents dans l’image par ceux de l’hôte |
| **Docker volume** | Si vide, récupère les fichiers de l’image |

#### Exemple :
```bash
docker run -d --name c1 \
  --mount type=bind,source=/data/,destination=/usr/share/nginx/html/ \
  nginx:latest
```

---

## 🌐 Réseau Docker

Les conteneurs peuvent communiquer entre eux via des réseaux Docker.

### Réseau par défaut (bridge)

```bash
docker run --name c1 -d debian sleep infinity
docker exec -ti c1 bash
apt install iputils-ping net-tools
ifconfig
```

### Commandes réseau

| Commande | Description |
|---------|-------------|
| `docker network ls` | Liste les réseaux |
| `docker network create --driver=bridge --subnet=192.168.0.0/24 reseau1` | Crée un réseau personnalisé |
| `docker network inspect reseau1` | Détaille les infos du réseau |

#### Connexion de conteneurs à un réseau :
```bash
docker run -d --name c1 --network reseau1 nginx:latest
docker run -d --name c2 --network reseau1 nginx:latest
docker exec -ti c2 bash
ping c1
```

---

## 🧰 Dockerfile

Un `Dockerfile` est un fichier de configuration permettant de construire une image personnalisée.

### Principales instructions :
- `FROM` : base de l’image
- `RUN` : exécution de commandes
- `COPY` ou `ADD` : ajout de fichiers
- `ENV` : variables d’environnement
- `EXPOSE` : ports
- `CMD` ou `ENTRYPOINT` : point d’entrée

### Commandes associées :
```bash
docker build -t monimage .
docker images
docker run -d -p 8080:80 monimage
docker rmi -f monimage
```

---

## 🧱 Docker Layers (couches)

Chaque instruction du Dockerfile crée une couche. Ces couches sont :
- **Indépendantes**
- **Mises en cache**
- **Réutilisables**
