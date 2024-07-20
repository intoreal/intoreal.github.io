---
# 사용할 layout file 지정
layout: post
# 게시글 제목
title: "sklearn confusion matrix와 seaborn 시각화"
# 게시글 시간 설정. 파일 명 보다 우선한다.
date: 2024-07-07 +0900
# 게시글의 카테고리. 최상단과 서브 카테고리만 있다.
categories: [pytorch, sklearn]
# 게시글 태그 설정. ,로 태그들을 구분해서 작성 가능하다.
tags: [python, sklearn, seaborn]
# 공개여부 설정. true면 공개하고 false면 공개하지 않는다.
published: true
# 사용자 정의 변수. 본문에서 {{ page. food }} 형태로 사용 가능하다.
author: jihwan
# 만약 우측 Table Of Contents를 사용하고 싶지 않다면 false로 전환
toc: true
---

## 패키지 import 
```python
from sklearn.metrics import confusion_matrix
import matplotlib.pyplot as plt
import seaborn as sns
```
## 혼동행렬 생성
```python
cm = confusion(y_test, y_pred) # 실제 label을 먼저 쓰고, 뒤에 추정결과를 넣는다. 
print(type(cm)) # 결과는 numpy.ndarray
```

## seaborn 시각화
```python
sns.heatmap(cm, annot=True, fmt='d', cmap='Blues')
plt.xlabel('Predicted')
plt.ylabel('True')
plt.show()
```