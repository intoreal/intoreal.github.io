---
layout: post
title: "torch.max와 torch.argmax의 이해"
date: 2024-08-04 +0900
categories: [python, pytorch]
tags: [python, pytorch]
published: true
author: jihwan
toc: true
---

## torch.max
### 기본 사용법
- 텐서의 가장 큰 값을 구한다. 

```python
data = [[[ 13,  14,  3],
         [ 4,  5,  6]],
        [[ 1,  2,  15],
         [ 16,  11,  12]]]
data = torch.tensor(data)

print(torch.max(data))
# tensor(16)
```

### dim 지정 사용법
- 큰 값을 찾는 차원을 설정하여 큰 값과 그 index를 구한다. 

```python
data = [[[ 13,  14,  3],
         [ 4,  5,  6]],
        [[ 1,  2,  15],
         [ 16,  11,  12]]]
data = torch.tensor(data)

print(torch.max(data, dim=0))
#torch.return_types.max(
# values=tensor([[13, 14, 15],
#         [16, 11, 12]]),
# indices=tensor([[0, 0, 1],
#         [1, 1, 1]]))

print(torch.max(data, dim=1))
# torch.return_types.max(
# values=tensor([[13, 14,  6],
#         [16, 11, 15]]),
# indices=tensor([[0, 0, 1],
#         [1, 1, 0]]))

print(torch.max(data, dim=2))
# torch.return_types.max(
# values=tensor([[14,  6],
#         [15, 16]]),
# indices=tensor([[1, 2],
#         [2, 0]]))
```

### 어떤 차원에서 가장 큰 값을 찾는다?
- 해당 차원이 아닌 상위 차원은 슬라이싱(:)으로 선택하고 해당 차원을 인덱스 0부터 n 까지 늘려가며 찾는다. 
- 해당 차원의 인덱스를 indices에 넣어준다. 

```python
torch.max(data, dim=1)
# torch.return_types.max(
# values=tensor([[13, 14,  6],
#         [16, 11, 15]]),
# indices=tensor([[0, 0, 1],
#         [1, 1, 0]]))

data[:, 0]
# tensor([[13, 14,  3],
#         [ 1,  2, 15]])

data[:, 1]
# tensor([[ 4,  5,  6],
#         [16, 11, 12]])
```

## torch.argmax
### 기본사용법
- tensor를 flatten했을 경우의 최대값의 인덱스를 반환한다. 

### dim 지정 사용법
- torch.max(data, dim= 0)결과값의 indices 부분만 반환한다.
