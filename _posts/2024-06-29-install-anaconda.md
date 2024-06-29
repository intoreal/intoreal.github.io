---
# 사용할 layout file 지정
layout: post
# 게시글 제목
title: "리눅스에 Anaconda 설치"
# 게시글 시간 설정. 파일 명 보다 우선한다.
date: 2024-06-29
# 게시글의 카테고리. 최상단과 서브 카테고리만 있다.
categories: [python, anaconda]
# 게시글 태그 설정. ,로 태그들을 구분해서 작성 가능하다.
tags: [python, anaconda]
# 공개여부 설정. true면 공개하고 false면 공개하지 않는다.
published: true
# 사용자 정의 변수. 본문에서 {{ page. food }} 형태로 사용 가능하다.
food: Pizza
# 작성자. authors.yml 파일의 아이디를 사용한다.
author: jihwan
# 만약 우측 Table Of Contents를 사용하고 싶지 않다면 false로 전환
toc: true
---

## Anaconda3 설치

### 다운로드
https://www.anaconda.com/download/success

### .zshrc 설정 추가
```shell  
# 아나콘다 설치 폴더의 bin 폴더를 PATH에 추가
export PATH="/home/jihwan/.anaconda3/bin:$PATH"
```

## Anaconda3 명령
```shell
# conda 버전 확인
conda --version

# conda 업데이트
conda update conda

# 가상환경 리스트 확인
conda info -e

# 가상환경 신규 생성
conda create -n 가상환경이름 python=원하는버전

# 가상환경 삭제
conda remove -n 가상환경이름 --all

# 가상환경 activate
conda activate 가상환경이름

# 가상환경 deactivate
conda deactivate

# 현재 가상환경의 패키지 조회
conda list

# 현재 가상환경에 패키지 설치
conda install 패키지

# 현재 가상환경에 패키지 삭제
conda remove 패키지
```