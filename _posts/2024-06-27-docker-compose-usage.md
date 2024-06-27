---
# 사용할 layout file 지정
layout: post
# 게시글 제목
title: "Docker-compose 사용법"
# 게시글 시간 설정. 파일 명 보다 우선한다.
date: 2024-06-27
# 게시글의 카테고리. 최상단과 서브 카테고리만 있다.
categories: [docker, docker-compose]
# 게시글 태그 설정. ,로 태그들을 구분해서 작성 가능하다.
tags: [docker, docker-compose]
# 공개여부 설정. true면 공개하고 false면 공개하지 않는다.
published: true
# 사용자 정의 변수. 본문에서 {{ page. food }} 형태로 사용 가능하다.
food: Pizza
# 작성자. authors.yml 파일의 아이디를 사용한다.
author: jihwan
# 만약 우측 Table Of Contents를 사용하고 싶지 않다면 false로 전환
toc: true
# 댓글 사용 여부, _config.yml의 comments.active를 사용한다.
comments: false
---

## yaml 파일 작성 법
```yaml
version: 3.9                       # docker-compose의 버전. 생략 가능

services:                          # 실행하고 싶은 컨테이너를 service로 명시한다. 
  redis:
    image: redis:alpine
    voluems: ~/docker/volume/data:/data
    network:
    - mynetwork
    
  web:                             # web이라는 컨테이너를 실행한다. 
    depends_on:
    - redis
    image: real/nextjs-web:latest  # 실행할 image를 지정한다. 
    volumes:
    - ~/docker/volume/data:/data   # 호스트 저장공간을 마운트한다. 
    network:
    - mynetwork                    # mynetwork라는 도커 네트워크를 사용한다. 
    ports:
    - "80:3000"                    # 포트 포워딩을 설정한다. 따옴표 주의!
    restart: always  


```
## 실행 방법(--detach 모드)
```shell
docker-compose up -d
docker-compose -f ~/project/lab/docker-compose.yml up -d

```

## 실행 상황 확인
```shell
# yaml 파일이 있는 위치에서 실행
docker-compose ps

```

## 정지
```shell
# yaml 파일이 있는 위치에서 실행
docker-compose stop

```


## 특이사항
* docker-compose가 실행하는 컨테이너의 이름은 폴더명에 영향을 받는다. 
* 같은 폴더에서 같은 service 이름의 컨테이너가 실행되면 기존 컨테이너는 종료된다. 


