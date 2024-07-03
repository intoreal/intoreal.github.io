---
# 사용할 layout file 지정
layout: post
# 게시글 제목
title: "로지스틱 회귀 분석 방법 정리"
# 게시글 시간 설정. 파일 명 보다 우선한다.
date: 2024-07-02 +0900
# 게시글의 카테고리. 최상단과 서브 카테고리만 있다.
categories: [python, sklearn]
# 게시글 태그 설정. ,로 태그들을 구분해서 작성 가능하다.
tags: [python, sklearn, logisticRegression]
# 공개여부 설정. true면 공개하고 false면 공개하지 않는다.
published: true
# 사용자 정의 변수. 본문에서 {{ page. food }} 형태로 사용 가능하다.
author: jihwan
# 만약 우측 Table Of Contents를 사용하고 싶지 않다면 false로 전환
toc: true
---

## 패키지 import
```python
import pandas as pd
import matplotlib.pyplot as plt
from sklearn import metrics
from sklearn.model_selection import train_test_split # train/test 데이터 분리
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score, confusion_matrix           # 정확도 계산
from sklern.datasets import load_digits
```
## 데이터 load
```python
digits = load_digits()
```

## 데이터 확인 
```python
plt.figure(figsize=(10,4))
for index, (image, label) in enumerate(zip(digits.data[0:5], digits.target[0:5]))
  plt.subplot(1,5, index+1)
  plt.imshow(np.reshape(image, (8,8)), cmap=plt.cm.gray)
  plt.title('Training: %i' % label, fontsize=20)
```

## train, test 데이터 분리
```python
x_train, x_test, y_train, y_test = train_test_split(x, y, test_size=0.25, random_state=42)
```

## 로지스틱 회귀 알고리즘 학습
```python
logisticReg = LogisticRegression()
logisticReg.fit(x_train, y_train)
```

## svc 학습 모델 활용
```python
y_pred= logisticReg.predict(x_test)
logisticReg.score(x_test, y_test)
```

## 결과 시각화
```python
import seaborn as sns

cm = confusion_matrix(y_test, y_pred)
plt.figure(figsize=(9,9))

sns.heatmap(cm, annot=True, fmt=".3f", linewidths = .5, squre=True, cmap='Bluts_r)

plt.ylabel('Acutual label')
plt.xlabel('Predicted label')
print(accuracy_score(y_pred, y_test))
plt.title('Accuracy Score', size=15)
plt.show()



```