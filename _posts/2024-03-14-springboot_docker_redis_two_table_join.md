---
layout: single
title: "2024-03-14-springboot_docker_redis_two_table_join"
categories: java
tag: springboot_shop_docker_redis
toc: true
---
 

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
  
  - String
    - get key - key에 해당하는 value를 가져온다.
    - set key value - key에 value를 저장한다.
    - del key - key를 삭제한다.

    ```
    root@0315e1ddb32e:/data# redis-cli
    127.0.0.1:6379> get home(nil)
    127.0.0.1:6379> set home helloWorldOK
    127.0.0.1:6379> get home"helloWorld"
    127.0.0.1:6379> del home(integer) 1
    127.0.0.1:6379> get home(nil)
    ```

  - List
    - lpush key value - List의 index 0에 데이터를 넣는다.
    - rpush key value - List의 index last에 데이터를 넣는다.
    - lrange key start end - List의 start~end의 element를 반환한다.
    - lpop key - List의 데이터를 꺼낸다.

    ```
    127.0.0.1:6379> lpush home one(integer) 
    1127.0.0.1:6379> lpush home two(integer) 2
    127.0.0.1:6379> lpush home three(integer) 3
    127.0.0.1:6379> llen home(integer) 3
    127.0.0.1:6379> lrange home 0 31) "three"2) "two"3) "one"
    127.0.0.1:6379> lpop home"three"
    127.0.0.1:6379> lpop home"two"
    127.0.0.1:6379> lpop home"one"
    127.0.0.1:6379> lpop home(nil)
    ```

  - Set
    - sadd key member - set에 value를 하나 추가한다.
    - smembers key - set에 속해있는 모든 member를 조회한다.
    - scard key - set에 속해있는 member을 개수를 구한다.
    - spop - set에서 무작위로 member를 가져온다.

    ```
    127.0.0.1:6379> sadd home one(integer) 1
    127.0.0.1:6379> sadd home two(integer) 1
    127.0.0.1:6379> sadd home two(integer) 0
    127.0.0.1:6379> smembers home1) "one"2) "two"
    ```

  - Hash
    - hset key field value, key에 field와 value를 쌍으로 저장한다.
    - hget key field : key에서 field로 value를 가져온다.
    - hdel key field : key에서 field를 삭제한다.
    - hlen key : field의 개수를 반환한다.
    - hgetAll key : field와 value를 모두 반환한다.
    - hkeys key : 모든 field를 반환한다.
    - hvals key : 모든 value를 반환한다.

    ```
    127.0.0.1:6379> hset summary 10001 20(integer) 1
    127.0.0.1:6379> hset summary 10002 10(integer) 1
    127.0.0.1:6379> hset summary 10003 0(integer) 1
    127.0.0.1:6379> hget summary 10002"10"
    127.0.0.1:6379> hlen summary(integer) 3
    127.0.0.1:6379> hgetAll summary1) "10001"2) "20"3) "10002"4) "10"5) "10003"6) "0"
    127.0.0.1:6379> hkeys summary1) "10001"2) "10002"3) "10003"
    127.0.0.1:6379> hvals summary1) "20"2) "10"3) "0"
    127.0.0.1:6379> hdel summary 10001(integer) 1
    127.0.0.1:6379> hkeys summary1) "10002"2) "10003"
    ```

  - expire
    - expire key member second : key에 ttl을 설정한다.
    - ttl key : 남은 ttl을 초단위로 확인한다.

    ```
    127.0.0.1:6379> expire summary 10(integer) 1
    127.0.0.1:6379> ttl summary(integer) 7
    127.0.0.1:6379> hgetAll summary(empty array)
    ```

## springboot_shop_setting

### 의존성 주입

- 
