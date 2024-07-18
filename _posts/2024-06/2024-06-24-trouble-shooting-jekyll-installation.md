---
# 사용할 layout file 지정
layout: post
# 게시글 제목
title: "Ubuntu 22.04.3에서 Jekyll 설치가 안되는 문제 해결"
# 게시글 시간 설정. 파일 명 보다 우선한다.
date: 2024-06-24
# 게시글의 카테고리. 최상단과 서브 카테고리만 있다.
categories: [git, gitpage]
# 게시글 태그 설정. ,로 태그들을 구분해서 작성 가능하다.
tags: [git, github, blog, jekyll, ubuntu, ruby]
# 공개여부 설정. true면 공개하고 false면 공개하지 않는다.
published: true
# 사용자 정의 변수. 본문에서 {{ page. food }} 형태로 사용 가능하다.
food: Pizza
# 작성자. authors.yml 파일의 아이디를 사용한다.
author: jihwan
# 요약문
description: bretfisher/jekyll-serve docker를 대안으로 사용함
# 만약 우측 Table Of Contents를 사용하고 싶지 않다면 false로 전환
toc: true
# 댓글 사용 여부, _config.yml의 comments.active를 사용한다.
comments: true
---

## 문제 상황

**Ubuntu 22.04.3**에서 zsh을 사용하고 있었는데 패키지 의존성 문제가 발생하면서 Jekyll이 설치되지 않았다.

## Jekyll docker로 해결

[BretFisher/jekyll-serve](https://github.com/BretFisher/jekyll-serve)를 사용해서 문제를 해결했다. 다음부터 패키지 버전문제가 있을 때는 docker를 적극 사용해야겠다.
