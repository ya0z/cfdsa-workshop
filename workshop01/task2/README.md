# Workshop01/Task2
## Step 1:
```
docker network create mynet
```
verify network is created
```
docker network list
```
## Step 2:
Create volume for database
```
docker volume create myvol
```
## Step 3:
Create the db
```
docker run -d --name mydb \
    --network mynet \
    -v myvol:/var/lib/mysql \
    stackupiss/northwind-db:v1
```

## Step 4:
Create the app
```
docker run -d --name myapp \
    -p 8080:3000 \
    --network mynet \
    -e DB_HOST=db \
    -e DB_USER=root -e DB_PASSWORD=changeit \
    stackupiss/northwind-app:v1
```