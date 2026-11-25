# TP4 : Docker et Docker Compose (application MERN)

## 1. Clonage

```bash
git clone https://github.com/wiem-kb/MyAppReact.git
cd MyAppReact
```

## 2. Dockerfiles

- `server/Dockerfile` : image node:lts-alpine, installation des dépendances, port 9000, `npm start`.
- `client/Dockerfile` : build React (`npm run build`), serveur `serve` sur le port 3000.

```bash
docker build -t mern-server ./server
docker build -t mern-client ./client
```

## 3. Lancement manuel

```bash
docker network create mern-network
docker run -d --name mongodb --network mern-network mongo
docker run -d --name server --network mern-network -p 9000:9000 -e MONGO_URI=mongodb://mongodb:27017/mydb mern-server
docker run -d --name client --network mern-network -p 3000:3000 mern-client
```

## 4. Docker Compose

```bash
docker compose up --build
```

## 5. Test

- Client : http://localhost:3000
- API : http://localhost:9000

(Ajouter ici les captures d'écran de `docker ps` et du navigateur.)
