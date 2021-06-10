---
layout: post
current: post
cover: 'assets/images/summit.jpg'
navigation: True
title: 자주 사용하는 docker 기능 정리
date: 2021-06-10 10:18:00
tags: fiction
class: post-template
subclass: 'post'
author: lewis
---

# 자주 사용하는 docker 기능 정리

## docker container 확인

```sh
docker ps -a
```

## docker image 확인

```sh
docker images
```

## docker image 확보(docker hub)

```sh
docker pull 배포자id/배포image
```

## docker image 실행(컨테이너 시작)

```sh
docker run -it -p 연결할pc포트:연결할container포트 ubuntu
```

컨테이너를 생성하고 동시에 실행시킨다.

## docker container 시작/정지

+ container 시작

```sh
docker start 컨테이너id -i
```

사용자 입력 콘솔을 위하여 -i 옵션 추가

+ container 정지

```sh
docker stop 컨테이너id
```

## PC와 docker container간 데이터 복사

+ PC에서 container로 

```sh
docker cp PC파일경로 containerid:container경로
```

+ container에서 PC로

```sh
docker cp containerid:container파일경로 PC경로
```

## docker image 제작

+ docker image 최초 제작

```sh
docker commit containerid 이미지명
```

+ docker image 이름 변경

```sh
docker image tag containerid 배포자id/이미지명:tag
```

## docker image 배포(docker hub)

