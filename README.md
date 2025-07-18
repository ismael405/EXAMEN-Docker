# EXAMEN-Docke
ANDRIAMANISA Ny Aina Abraham Ismael 
176/LA/24-25
 Commandes de base
docker --version
➤ Affiche la version de Docker installée.

docker info
➤ Donne des informations détaillées sur Docker (conteneurs, images, etc.).

docker help
➤ Liste toutes les commandes disponibles avec leurs descriptions.

 Gestion des conteneurs
docker run <image>
➤ Lance un conteneur à partir d’une image.

docker run -it <image>
➤ Lance un conteneur en mode interactif avec terminal.

docker run -d <image>
➤ Lance un conteneur en arrière-plan (mode détaché).

docker ps
➤ Affiche les conteneurs en cours d’exécution.

docker ps -a
➤ Affiche tous les conteneurs (actifs et arrêtés).

docker stop <id>
➤ Arrête un conteneur.

docker start <id>
➤ Démarre un conteneur arrêté.

docker restart <id>
➤ Redémarre un conteneur.

docker rm <id>
➤ Supprime un conteneur.

docker logs <id>
➤ Affiche les logs d’un conteneur.

docker exec -it <id> bash
➤ Ouvre un terminal bash dans un conteneur.

 Gestion des images
docker images
➤ Liste les images locales.

docker pull <image>
➤ Télécharge une image depuis Docker Hub.

docker build -t <nom>:<tag> .
➤ Construit une image à partir d’un Dockerfile.

docker rmi <image>
➤ Supprime une image.

docker tag <image> <nouveau_nom>
➤ Renomme (ou tague) une image.

 Volumes et réseaux
docker volume ls
➤ Liste les volumes existants.

docker volume create <nom>
➤ Crée un nouveau volume.

docker volume rm <nom>
➤ Supprime un volume.

docker network ls
➤ Liste les réseaux Docker.

docker network create <nom>
➤ Crée un nouveau réseau personnalisé.

 Docker Compose
docker-compose up
➤ Lance les services définis dans docker-compose.yml.

docker-compose up -d
➤ Lance les services en arrière-plan.

docker-compose down
➤ Arrête et supprime tous les services et ressources liées.

docker-compose ps
➤ Liste les services actifs.

docker-compose build
➤ Construit les images des services.

 Nettoyage
docker system prune
➤ Supprime les ressources inutilisées (conteneurs, images, volumes, etc.).

docker rm $(docker ps -aq)
➤ Supprime tous les conteneurs.

docker rmi $(docker images -q)
➤ Supprime toutes les images.
