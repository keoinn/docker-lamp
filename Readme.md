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
docker-compose up # Windows
docker compose up # Linux

# detached mode (background)
docker-compose up -d # Windows
docker compose up -d # Linux

# volume sync and detached (recommend)
docker-compose up -d -V # Windows
docker compose up -d -V # Linux
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

# list port usage
docker ps
```

### Execute Command in Cotainer
```sh
docker exec [container name] [command]
# example
docker exec lamp_php74 composer create-project codeigniter4/appstarter project-root
```

## DNS Settins
#### Windows

add following code to `C:\Windows\System32\drivers\etc\hosts`
```sh
127.0.0.1 local.test
```

#### Mac

```sh
sudo echo "127.0.0.1 local.test" >> /private/etc/hosts
```

#### Linux

```sh
sudo echo "127.0.0.1 local.test" >> /etc/hosts
```

### .env file
```
mv env .env
```

- modify the `HTTPD_ADMIN` value which is yourself in .env file.


### ChangeLog
```
[2024-12-25] Apache2 + PHP7.0/7.4 FPM + PMA
    * Change base images from debain to alpine linux.
[2023-10-12] Apache2 + PHP7.4 + MySQL + PMA rev 4
    * Upgrade PHP 7.4.0 to PHP 7.4.33
    * Modify Apache2 Settings with individual domain configure files
[2023-10-02] Apache2 + PHP7.4 + MySQL + PMA rev 3
    * Modify document file path in docker.apache.conf
[2023-01-15] Apache2 + PHP7.4 + MySQL + PMA rev 2
    * Fix configure file of PHP -> modify POST/UPLOAD file size.
[2022-10-31] Apache2 + PHP7.4 + MySQL + phpMyAdmin rev 1.
[2022-09-23] Apache2 + PHP7.4 + MySQL + phpMyAdmin
[2022-09-22] Apache2 + PHP7.4 with FPM
```

### Referance
* [Performance for PHP-FPM](https://www.ernestchiang.com/zh/posts/2024/nginx-php-fpm-benchmark-2024-q1/)
* [Apache2 + PHP7.4 with FPM](https://blog.csdn.net/m0_55975991/article/details/124995718)
* [Docker LAMP with phpMyAdmin](https://hackmd.io/@titangene/docker-collection/%2FJo1wfBAaSzKx9anZ0WOv1Q?type=book)
