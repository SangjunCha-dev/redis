# 간단한 redis 서버 구축하기

Docker로 구축하는 `redis` 서버입니다.  
사용 예시는 `Standalone Mode`로 설정되어 있습니다.  


---

## 1. redis.conf 설정

```
bind 127.0.0.1
port 6379

maxmemory 1gb
maxmemory-policy allkeys-lru
```
- bind: redis 서버 Host
- port: redis 서버 Port
- maxmemory: 최대 메모리 용량
- maxmemory-policy: 메모리 사용량이 최대 메모리를 초과시 데이터 삭제 정책
    - allkeys-lru: 가장 오랫동안 참조되지 않은 데이터 삭제 (LRU Cache)


---

## 2. docker-compose 실행 명령어

- redis 이미지 실행
    ```
    $ docker-compose up -d --build
    ```
- redis 이미지 종료
    ```
    $ docker-compose down
    ```


---

## 3. redis 접속

redis 이미지에 따라 지원하는 shell 이 다르다.

- redis
    ```
    $ docker exec -it redis_cache /bin/bash
    /data# redis-cli
    ```
- redis:alpine
    ```
    $ docker exec -it redis_cache /bin/sh
    /data# redis-cli
    ```


---

## 4. redos 기본 명령어

- redis version 확인
    ```
    127.0.0.1:6379> info
    # Server
    redis_version:6.2.6
    ```

- strings
    - Key-Value 구조로 데이터 저장 및 관리
    - 데이터 저장: set Key Value
    - 데이터 조회: get Key
    - 데이터 삭제: del Key
    - 예시
        ```
        127.0.0.1:6379> set car 100
        OK
        127.0.0.1:6379> get car
        "100"
        127.0.0.1:6379> del car
        (integer) 1
        127.0.0.1:6379> get car
        (nil)
        ```
