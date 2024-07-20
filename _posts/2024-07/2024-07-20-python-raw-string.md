---
layout: post
title: "파이썬의 raw string"
date: 2024-07-20 +0900
categories: [python, syntax]
tags: [python]
published: true
author: jihwan
toc: true
---

## 파이썬 raw string

### 이론
- 파이썬 스트링 앞에 r을 붙이면 raw string으로 해석하여 백슬래시를 escape 문자로 인식하지 않는다. 
- 윈도우에서 경로를 작성할 때 사용하면 가독성이 좋아진다. 리눅스는 백슬래시가 아닌 슬래시를 사용하기 때문에 필요성이 줄어든다.

### 코드
```python
# Linux System
normalStr = '/work/data/newImg.jpg'
rawStr = r'/work/data/newImg.jpg'

print(normalStr)     
print(rawStr)
# /work/data/newImg.jpg
# /work/data/newImg.jpg


# Window System
normalStr = 'C:\work\data\newImg.jpg'
rawStr = r'C:\work\data\newImg.jpg'

print(normalStr)
print(rawStr)
# C:\work\data
# ewImg.jpg
# C:\work\data\newImg.jpg
```