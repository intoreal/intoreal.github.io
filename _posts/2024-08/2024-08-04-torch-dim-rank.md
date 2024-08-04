---
layout: post
title: "pytorch tensor의 차원(dim)과 랭크(rank)"
date: 2024-08-04 +0900
categories: [python, pytorch]
tags: [python, pytorch]
published: true
author: jihwan
toc: true
---

## 차원(dimension)
### 기본 개념
- tensor 데이터를 표현하는 축의 갯수를 말한다. 
- tensor의 size()의 길이를 말한다. 
- tensor의 dim()의 결과값이다. 

```python
data = [[[ 13,  14,  3],
         [ 4,  5,  6]],
        [[ 1,  2,  15],
         [ 16,  11,  12]]]
data = torch.tensor(data)

print(data.dim())
#3

print(data.size())
#torch.Size([2, 2, 3])
```

### 주의사항!
- 3차원 좌표라고 해서 3차원 데이터인것이 아니다!
- 3차원 좌표 1개는 1개 축으로 표현될 수 있으니 1차원이다

```python
data = torch.tensor([3,5,7])
data.dim()
#1
```

## 랭크(rank)
### 개념
- 엄밀히 말하면 행렬 고유벡터의 숫자를 말하는 것이나
- 비공식적으로는 차원의 크기를 말하기도 한다. 

```python
data = torch.tensor([[1,2],[2,4]], dtype=torch.float64)

data.dim()
#2

torch.linalg.matrix_rank(data)
#tensor(1)
```