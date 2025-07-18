Exmen-Docker
RANDRIANOMENJANAHARY Stanis Ryan 
212/lA/24-25
L1A
Documentation Docker (en français)

Introduction à Docker

**Docker** est un outil incontournable de la conteneurisation, une technique de virtualisation légère qui permet d’exécuter plusieurs applications de façon isolée sur une même machine physique ou virtuelle.

Objectifs de Docker
- Simplifier et automatiser les déploiements
- Moderniser la livraison des applications
- Gérer efficacement les dépendances et environnements
Concepts clés

Image
Une *image Docker* est un modèle figé contenant tout le nécessaire pour faire fonctionner une application :
- Le code source
- Les bibliothèques et dépendances
- Le système de fichiers

Conteneur
Un *conteneur Docker* est une instance d’image en cours d’exécution, isolée via les mécanismes `cgroups` et `namespaces`.

![Conteneur](concept.png)

---
Commandes Docker de base

```bash
sudo usermod -aG docker $USER

    Ajoute l'utilisateur actuel au groupe docker, afin de ne plus avoir à utiliser sudo pour les commandes Docker.

docker ps

    Affiche la liste des conteneurs actuellement en cours d’exécution.

docker ps -a

    Affiche tous les conteneurs, qu’ils soient actifs ou arrêtés.

docker ps -q

    Affiche uniquement les identifiants (ID) des conteneurs actifs.

docker run nginx:latest

    Télécharge (si nécessaire) puis lance un conteneur basé sur l’image nginx:latest.

docker run -d --name c1 nginx:latest

    Démarre le conteneur Nginx nommé c1 en arrière-plan (mode détaché).

docker rm -f c1

    Supprime le conteneur c1, même s’il est encore en cours d’exécution.

