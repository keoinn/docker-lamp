# Docker Compose for Dev Env.

### Document Structure
```sh
Folder
│  docker-compose.yml # Docker Compose YAML
├─compose # Service Application 
│  ├─apache # Service Name
│  │      docker.apache.conf # Service Config
│  │      Dockerfile # Service Dockerfile
│  └─php74
│         ...
└─src # Project Code
    ├─project # mount to /var/www/html
    │      index.php # Test php file
    ├─data # MYSQL mount to /var/lib/mysql
    └─sql # database schema
        ...
```

### Build Envirment
```sh
# build and run as container
docker-compose up

# detached mode (background)
docker-compose up -d

# volume sync and detached (recommend)
docker-compose up -d -V
```

### Stop Container
```sh
docker-compose down
```

### Networking 
```sh
# index
127.0.0.1

# phpmyadmin
127.0.0.1:8080

# list ip address of each container
docker inspect -f '{{.Name}} - {{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' $(docker ps -aq)
```

### Commit Version Log
```
[2023-10-02] Apache2 + PHP7.4 + MySQL + PMA rev 3
    * Modify document file path in docker.apache.conf
[2023-01-15] Apache2 + PHP7.4 + MySQL + PMA rev 2
    * Fix configure file of PHP -> modify POST/UPLOAD file size.
[2022-10-31] Apache2 + PHP7.4 + MySQL + phpMyAdmin rev 1.
[2022-09-23] Apache2 + PHP7.4 + MySQL + phpMyAdmin
[2022-09-22] Apache2 + PHP7.4 with FPM
```

### Referance
* [Apache2 + PHP7.4 with FPM](https://blog.csdn.net/m0_55975991/article/details/124995718)
* [Docker LAMP with phpMyAdmin](https://hackmd.io/@titangene/docker-collection/%2FJo1wfBAaSzKx9anZ0WOv1Q?type=book)
