# EXAMEN-Docke
ANDRIAMANISA Ny Aina Abraham Ismael 
176/LA/24-25

##  Généralités sur Docker

**Docker** est un outil qui a largement contribué à la popularisation de la conteneurisation, une forme de virtualisation légère permettant d'exécuter plusieurs applications de manière isolée sur une même machine physique ou virtuelle.

###  Objectifs
- Simplifier les déploiements
- Changer le mode de livraison des applications
- Faciliter la gestion des dépendances

###  Concepts de base

#### Image
Une image Docker est un modèle figé contenant tout le nécessaire pour exécuter une application :
- Le code source
- Les dépendances (bibliothèques, paquets)
- Le système de fichiers

#### Conteneur
Un conteneur est une instance d’une image Docker, capable d'exécuter des processus de manière isolée via `cgroups` et `namespaces`.

![Conteneur](concept.png)

---

##  Commandes Docker de base

```bash
sudo usermod -aG docker $USER
```
> Ajoute l'utilisateur courant au groupe Docker pour éviter d’utiliser `sudo` à chaque commande.

```bash
docker ps
```
> Liste les conteneurs en cours d'exécution.

```bash
docker ps -a
```
> Affiche tous les conteneurs (actifs ou non).

```bash
docker ps -q
```
> Affiche uniquement les IDs des conteneurs actifs.

```bash
docker run nginx:latest
```
> Télécharge et exécute un conteneur Nginx.

```bash
docker run -d --name c1 nginx:latest
```
> Exécute Nginx en arrière-plan dans un conteneur nommé `c1`.

```bash
docker rm -f c1
```
> Supprime le conteneur `c1`, même s’il est actif.



## 💾 Cheat Sheet : Docker Volumes

Un volume est un mécanisme pour stocker des données persistantes dans Docker.

```bash
docker volume ls
```
> Liste tous les volumes disponibles.

```bash
docker volume create mynginx
```
> Crée un volume nommé `mynginx`.

```bash
docker volume inspect mynginx
```
> Affiche les détails du volume `mynginx`.

```bash
docker run -d --name c1 -v mynginx:/usr/share/nginx/html nginx:latest
```
> Monte un volume dans le conteneur.

```bash
docker exec -ti c1 bash
```
> Ouvre un terminal interactif dans le conteneur `c1`.

### Bind Mount

```bash
docker run -d --name c1 --mount type=bind,source=/data/,destination=/usr/share/nginx/html/ nginx:latest
```
> Monte un dossier local dans le conteneur (Bind Mount).

```bash
docker inspect --format "{{.Mounts}}" c1
```
> Affiche les infos de montage du conteneur.


##  Cheat Sheet : Docker Networks

```bash
docker network ls
```
> Liste les réseaux Docker existants.

```bash
docker network create --driver=bridge --subnet=192.168.0.0/24 reseau1
```
> Crée un réseau personnalisé.

```bash
docker network inspect reseau1
```
> Donne tous les détails du réseau `reseau1`.

```bash
docker run -d --name c1 --network reseau1 nginx:latest
```
> Lance un conteneur connecté à un réseau spécifique.

```bash
docker exec -ti c1 bash
```
> Accès shell au conteneur `c1`.


## Cheat Sheet : Dockerfile & Construction d'image

### Exemple basique de Dockerfile :

```Dockerfile
FROM debian
WORKDIR /app
COPY . /app
RUN apt update && apt install -y nginx
CMD ["nginx", "-g", "daemon off;"]
```

### Commandes associées

```bash
docker build -t myimage .
```
> Construit une image depuis un Dockerfile.

```bash
docker run -d -p 8080:80 myimage
```
> Lance un conteneur de l’image construite.

```bash
docker images
```
> Liste les images disponibles.

```bash
docker rmi -f myimage
```
> Supprime une image forcée.


## Cheat Sheet : Autres commandes utiles

```bash
docker system prune
```
> Nettoie tous les éléments inutilisés (conteneurs arrêtés, volumes non utilisés, etc.).

```bash
docker rm $(docker ps -aq)
```
> Supprime tous les conteneurs.

```bash
docker rmi $(docker images -q)
```
> Supprime toutes les images.


## Cheat Sheet : Docker Layers

- Chaque instruction d’un `Dockerfile` crée une *couche* (layer)
- Les couches permettent :
  - Le **cache** pour accélérer les reconstructions
  - La **réutilisation** entre plusieurs images
  - Une gestion efficace de l’espace disque
