Exmen-Docker
RANDRIANOMENJANAHARY Stanis Ryan 
212/lA/24-25
L1A

Documentation Docker (en français)

Introduction à Docker

**Docker** est une plateforme de conteneurisation qui facilite l’exécution d’applications dans des environnements isolés. Grâce à Docker, il est possible de regrouper une application, avec toutes ses dépendances, dans une seule unité portable appelée *conteneur*.

Objectifs de Docker
- Simplifier le déploiement des applications
- Standardiser la livraison des projets
- Gérer efficacement les dépendances et les environnements d’exécution

Concepts clés

Image
Une **image Docker** est un modèle immuable contenant tout ce qu’il faut pour exécuter une application :
- Le code de l’application
- Les bibliothèques nécessaires
- Un système de fichiers propre à l’image

Conteneur
Un **conteneur Docker** est une instance active d’une image. Il exécute les processus de manière isolée en utilisant des technologies comme `cgroups` et `namespaces`.

![Conteneur](concept.png)

---

Commandes Docker de base

```bash
sudo usermod -aG docker $USER
```
> Permet d’ajouter l’utilisateur courant au groupe `docker` pour éviter de devoir précéder chaque commande de `sudo`.

```bash
docker ps
```
> Affiche la liste des conteneurs en cours d'exécution.

```bash
docker ps -a
```
> Montre tous les conteneurs, qu’ils soient actifs ou stoppés.

```bash
docker ps -q
```
> Affiche uniquement les identifiants (ID) des conteneurs actifs.

```bash
docker run nginx:latest
```
> Télécharge l’image `nginx:latest` si nécessaire et exécute un conteneur basé sur celle-ci.

```bash
docker run -d --name c1 nginx:latest
```
> Lance un conteneur Nginx en mode détaché (arrière-plan), nommé `c1`.

```bash
docker rm -f c1
```
> Supprime le conteneur `c1` même s’il est en cours d’exécution.
