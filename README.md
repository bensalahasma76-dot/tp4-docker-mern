# TP4 : Docker et Docker Compose (Application MERN)

## Objectifs du TP
- Apprendre à utiliser Docker pour containeriser des applications.
- Découvrir Docker Compose pour orchestrer plusieurs conteneurs.
- Comprendre comment déployer une application MERN (MongoDB, Express, React, Node.js) en utilisant Docker.

---

## Commandes exécutées par étape

### Étape 1 : Cloner et préparer le projet
```bash
git clone [https://github.com/wiem-kb/MyAppReact.git](https://github.com/wiem-kb/MyAppReact.git)
cd MyAppReact
ls

Étape 2 : Créer les Dockerfiles et construire les images (Build):
docker build -t mern-server ./server
docker build -t mern-client ./client
docker images

Étape 3 : Créer le réseau Docker (Network):
docker network create mern-network
docker network ls

Étape 4 : Lancer MongoDB (Run)
docker run -d --name mongodb --network mern-network mongo
docker ps

Étape 5 : Lancer le serveur et le client (Run)
docker run -d --name server --network mern-network -p 9000:9000 -e MONGO_URI=mongodb://mongodb:27017/mern mern-server
docker run -d --name client --network mern-network -p 3000:3000 mern-client
docker ps
docker logs server
docker logs client
docker rm -f client server mongodb


Étape 6 : Orchestrer avec Docker Compose (Compose):
docker compose up --build

Commandes de vérification et d'arrêt :

docker compose ps
docker compose logs server
docker compose down