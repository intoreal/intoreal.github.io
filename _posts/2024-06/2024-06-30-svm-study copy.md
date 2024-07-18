---
# 사용할 layout file 지정
layout: post
# 게시글 제목
title: "서포트 벡터 머신 분석 방법 정리"
# 게시글 시간 설정. 파일 명 보다 우선한다.
date: 2024-06-30 +0900
# 게시글의 카테고리. 최상단과 서브 카테고리만 있다.
categories: [python, sklearn]
# 게시글 태그 설정. ,로 태그들을 구분해서 작성 가능하다.
tags: [python, sklearn, svc]
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
from sklearn import metrics
from sklearn.model_selection import train_test_split # train/test 데이터 분리
from sklearn.svm import SVC
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
X_train, X_test, y_train, y_test = train_test_split(x, y, test_size=0.2, random_state=42)
```

## svc 알고리즘 학습
```python
svm = SVC(kernel='linear', C=1.0, gamma=0.5) 
# kernel의 종류는 linear, poly, rbf, sigmoid, precomputed가 있음
# C값이 클수록 이상치를 허용하지 않는다.(하드마진)
# gamma 값이 높으면 결정경계가 유연해져 오버피팅 발생 가능

svm.fit(x_train, y_train)
```

## svc 학습 모델 활용
```python
y_pred= svm.predict(x_test)
print(accuracy_score(y_test, y_pred))
```