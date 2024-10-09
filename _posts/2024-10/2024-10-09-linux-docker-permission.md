---
layout: post
title: "리눅스 유저에게 도커 사용 권한 부여"
date: 2024-10-09 +0900
categories: [linux, cli]
tags: [docker]
published: true
author: jihwan
toc: true
---
## 1. docker 그룹 존재 유무 확인
```bash
cat /etc/group | grep -i docker

# 그룹이 없다면 생성
sudo groupadd docker
sudo systemctl restart docker
```

## 2. 사용자 계정 유무 확인
```bash
cat /etc/passwd | grep ubuntu
```

## 3. 사용자 계정을 docker 그룹에 추가
```bash
sudo usermod -aG docker ubuntu
```

## 4. 사용자 계정이 docker 그룹에 추가되었는지 확인
```bash
id -a ubuntu

groups ubuntu
```