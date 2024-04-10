---
layout: single
title: "springboot_shop_docker_redis"
categories: java
tag: springboot_shop_docker_redis
toc: true
---
 
# springboot docker, redis

## springboot docker setting

- dockerFile
```
FROM openjdk:17
ARG jar_file=target/*.jar
COPY ${jar_file} app.jar
ENTRYPOINT [ "java","-jar","/app.jar" ]
```

- redis-insite db 데이터 저장가능
- docker-compose

```
version: "3"
services:
  mysql:
   image: mysql:8.0.13
   restart: always
   ports:
    - 3307:3306
   environment:
    MYSQL_USER: root
    MYSQL_ROOT_PASSWORD: root
    MYSQL_DATABASE: shopdb
    SPRING-DATACOURCE_URL: jdbc:mysql://mysql:3306/MYSQL_DATABASE
    SPRING-DATABASE_USERNAME: root
    SPRING-DATABASE_PASSWORD: root
   volumes:
    - ./db/mysql/data:/var/lib/mysql              #DB가 저장되는 경로
    - ./db/mysql/config:/etc/mysql/conf.d		  #외부 접속을 위한 파일들이 저장되는 경로
    - ./db/mysql/init:/docker-entrypoint-initdb.d #도커가 처음 실행될 당시에만 실행되는 초기 세팅 파일 
  redis:
    image: redis:latest
    container_name: redis
    hostname: redisShop
    ports:
      - "6379:6379"
```

- spring-boot-starter-data-redis
  - redishash("") 지원


## springboot_shop_setting

- 의존주입
  - lombok
  - 

