### Pull Mongo image
```
docker pull mongo
```

### Run Mongo Container
```
docker container run -d \
    -p 27017:27017 \
    -e MONGO_INITDB_ROOT_USERNAME=root \
    -e MONGO_INITDB_ROOT_PASSWORD=password \
    --network app-network \
    --mount source=app-volume,target=/data/db \
    --name mongo \
    mongo
```


### Pull Mongo-Express image
```
docker pull mongo-express
```

### Run Mongo-Express Container
```
docker container run -d \
    -p 8081:8081 \
    -e ME_CONFIG_MONGODB_ADMINUSERNAME=root \
    -e ME_CONFIG_MONGODB_ADMINPASSWORD=password \
    -e ME_CONFIG_MONGODB_SERVER=mongo \
    --network app-network \
    --name mongo-express \
    mongo-express
```


### Create Volume
```
docker volume create app-volume
```


### Build app-server Image
```
docker build -t app-server .
```

### Run app-server Container
```
docker container run -it -d \
    -p 3000:3000 \
    --network app-network \
    --name app-server \
    app-server
```

### Build web-server Image
```
docker build -t web-server .
```

### Run web-server Container
```
docker run -it -d \
    -p 80:80 \
    --network app-network \
    --name web-server \
    web-server
```

### Push Images to Docker hub
```
docker image build -t hen1l/web21bcp227 .
docker image push hen1l/web21bcp227

docker image build -t hen1l/app21bcp227 .
docker image push hen1l/app21bcp227
```

### Run Docker Compose
```
docker compose -f docker-compose.yaml up
```
