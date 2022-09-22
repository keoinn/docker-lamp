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
    └─sql # database information
```

### Build Envirment
```sh
# build and run as container
docker-compose up

# detached mode (background)
docker-compose up -d
```

### Stop Container
```sh
docker-compose down
```

### Networking 
```
127.0.0.1
```

### Commit Version Log
```
[2022-09-22] Apache2 + PHP7.4 with FPM
```

### Referance
* [Apache2 + PHP7.4 with FPM](https://blog.csdn.net/m0_55975991/article/details/124995718)
