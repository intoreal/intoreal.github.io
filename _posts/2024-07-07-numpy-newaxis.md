---
# 사용할 layout file 지정
layout: post
# 게시글 제목
title: "numpy에서 새로운 축 생성"
# 게시글 시간 설정. 파일 명 보다 우선한다.
date: 2024-07-07 +0900
# 게시글의 카테고리. 최상단과 서브 카테고리만 있다.
categories: [python, numpy]
# 게시글 태그 설정. ,로 태그들을 구분해서 작성 가능하다.
tags: [python, numpy]
# 공개여부 설정. true면 공개하고 false면 공개하지 않는다.
published: true
# 사용자 정의 변수. 본문에서 {{ page. food }} 형태로 사용 가능하다.
author: jihwan
# 만약 우측 Table Of Contents를 사용하고 싶지 않다면 false로 전환
toc: true
---
## 기본 데이터
```python
data = np.random.randint(0,4,size=(2,3))
```
## new axis 방법 
```python
data = data[:, None, :]
```
## reshape 방법
```python
data = data.reshape(2, 1, 3)
```
