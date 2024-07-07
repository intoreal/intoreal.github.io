---
# 사용할 layout file 지정
layout: post
# 게시글 제목
title: "결정 트리 분석 방법 정리"
# 게시글 시간 설정. 파일 명 보다 우선한다.
date: 2024-07-01 +0900
# 게시글의 카테고리. 최상단과 서브 카테고리만 있다.
categories: [python, sklearn]
# 게시글 태그 설정. ,로 태그들을 구분해서 작성 가능하다.
tags: [python, sklearn, decision tree]
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
from sklearn import metrics
from sklearn.model_selection import train_test_split # train/test 데이터 분리
from sklearn.tree import DecisionTreeClassifier
from sklearn.metrics import accuracy_score, confusion_matrix           # 정확도 계산
```
## 데이터 load
```python
dataset = pd.read_csv('./work/data/chap03/data/titanic/train.csv', index_col='PassengerId')

dataset = dataset[['Pclass', 'Sex', 'Age', 'SibSp', 'Parch', 'Fare', 'Survived']]
dataset['Sex'] = dataset['Sex'].map({'male':0, 'female':1})
dataset = dataset.dropna()
x = df.drop('Survived', axis=1)
y = df['Survived']
```

## train, test 데이터 분리
```python
X_train, X_test, y_train, y_test = train_test_split(x, y, random_state=1)
```

## 결정 트리 알고리즘 학습
```python
model = DecisionTreeClassifier()

model.fit(x_train, y_train)
```

## 학습 모델 활용
```python
y_pred= model.predict(x_test)
print(accuracy_score(y_test, y_pred))
pd.DataFrame(
  comfusion_matrix(y_test, y_pred),
  columns=['Predicted Not Survival', 'Predicted Survival' ]
  index = ['True Not Survival', 'True Survival']
)
```