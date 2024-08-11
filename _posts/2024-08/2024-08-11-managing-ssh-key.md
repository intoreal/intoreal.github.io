---
layout: post
title: "리눅스(ubuntu)에서 SSH 키 사용 방법"
date: 2024-08-11 +0900
categories: [Linux, SSH]
tags: [linux, ubuntu, ssh, key]
published: true
author: jihwan
toc: true
---

## SSH 키 생성방법

```bash
ssh-keygen -t ed25519 -C "주석 혹은 이메일" -f "파일명"
```

## SSH 키 배포 방법
- 생성된 키 중 pub 키를 접속할 서버에 설정한다. 


## SSH 키 접속 설정

### 1. SSH Config 사용(추천)
- ~/.ssh/config 파일을 작성한다. 
```
IdentityFile ~/.ssh/키파일명

Host 호스트이름
    HostName 서버IP
    User 사용자ID
    Port 접속포트
    IdentityFile SSH파일명

Host github.com
    User git
    IdentityFile ~/.ssh/키파일명
```
- 이 후로는 호스트이름만으로 접속이 가능하다. 
```bash
ssh 호스트이름
```


### 2. SSH-agent 사용
```bash
# 키 파일을 ssh-agent에 등록
ssh-add 키파일명

# 계정이 실행될 때 ssh-agent가 실행되도록 설정
# .bashrc나 .zshrc에 설정
eval $(ssh-agent -s > /dev/null)
```
