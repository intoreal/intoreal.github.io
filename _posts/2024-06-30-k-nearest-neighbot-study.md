---
# 사용할 layout file 지정
layout: post
# 게시글 제목
title: "K-최근접 이웃 분석 방법 정리"
# 게시글 시간 설정. 파일 명 보다 우선한다.
date: 2024-06-30 +0900
# 게시글의 카테고리. 최상단과 서브 카테고리만 있다.
categories: [python, sklearn]
# 게시글 태그 설정. ,로 태그들을 구분해서 작성 가능하다.
tags: [python, sklearn, knn, k-neighbor]
# 공개여부 설정. true면 공개하고 false면 공개하지 않는다.
published: true
# 사용자 정의 변수. 본문에서 {{ page. food }} 형태로 사용 가능하다.
author: jihwan
# 만약 우측 Table Of Contents를 사용하고 싶지 않다면 false로 전환
toc: true
---

## 패키지 import
```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from sklearn import metrics
from sklearn.model_selection import train_test_split # train/test 데이터 분리
from sklearn.preprocessing import StandardScaler     # 열 데이터 정규화
from sklearn.neighbors import KNeighborsClassifier   # KNN 모델 사용
from sklearn.metrics import accuracy_score           # 정확도 계산
```
## 데이터 load
```python
dataset = pd.read_csv('./work/data/chap03/data/iris.data', names=names)

x = dataset.iloc[:, :-1].values
y = dataset.iloc[:, 4].values
```

## train, test 데이터 분리
```python
X_train, X_test, y_train, y_test = train_test_split(x, y, test_size=0.2)
```

## knn 알고리즘 학습
```python
knn = KNeighborsClassifier(n_neighbors=5)
knn.fit(X_train, y_train)
```

## knn 학습 모델 활용
```python
y_pred = knn.predict(X_test)
print(accuracy_score(y_test, y_pred))
```