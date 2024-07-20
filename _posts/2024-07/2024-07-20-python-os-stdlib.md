---
layout: post
title: "파이썬 표준 라이브러리 - os 모듈"
date: 2024-07-20 +0900
categories: [python, language]
tags: [python, os]
published: true
author: jihwan
toc: true
---

## 개요
- 파이썬 `os` 모듈은 표준 라이브러리에 포함된 모듈이다. 
- `os` 모듈을 사용해서 파일 경로의 탐색 및 조합이 가능하다. 

## 사용법
```python
import os

directoryPath = './work'
fileNames = os.listdir(directoryPath)
print(fileNames)
# 모든 폴더와 파일 이름을 list로 반환된다. 

filePaths = [os.path.join(directoryPath, f) for f in fileNames]
print(filePaths)
# 모든 폴더와 파일 이름이 full path list로 반환된다. 
```