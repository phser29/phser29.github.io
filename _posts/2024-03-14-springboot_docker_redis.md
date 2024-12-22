---
layout: single
title: "springboot_shop_docker_redis"
categories: java
tag: springboot_shop_docker_redis
toc: true
---
 
# springboot docker, redis 활용
- 프로젝트 이름: Springboot 쇼핑몰 프로젝트
- 프로젝트 기술: java, springboot, Mysql, mybatis, jquery, ajax
- 참고 문헌: 구글, 유트브

# Redis란

- Key, Value 구조의 비정형 데이터를 저장하고 관리하기 위한 오픈 소스 기반의 비관계형 데이터 베이스 관리 시스템 (DBMS)이다.

- @RedisHash(value)
  - 리프레시 토큰이 생성된 후 Redis에 저장될 Domain Object를 Redis Hash 자료구조로 변환하는 방식
  - @RedisHash 어노테이션의 value에 특정한 값을 넣어줌으로써, 데이터가 저장될 때 key의 prefix에 붙을 문자열이 정해질 수 있다. 또한, timeToLive 옵션을 통해 입력한 숫자만큼 초 단위로 유효기간을 지정할 수 있다.

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
    volumes:
      - ./redis/data:/data
      - ./redis/conf/redis.conf:/usr/local/conf/redis.conf
```

- spring-boot-starter-data-redis
  - redishash("") 지원

## docker redis-cli 사용법

> docker exec -it redis redis-cli

## springboot_shop_setting

### 의존성 주입

- 
