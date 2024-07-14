---
# 사용할 layout file 지정
layout: post
# 게시글 제목
title: "파이토치 학습 워크플로우"
# 게시글 시간 설정. 파일 명 보다 우선한다.
date: 2024-07-14 +0900
# 게시글의 카테고리. 최상단과 서브 카테고리만 있다.
categories: [python, pytorch]
# 게시글 태그 설정. ,로 태그들을 구분해서 작성 가능하다.
tags: [pytorch, FashionMNIST]
# 공개여부 설정. true면 공개하고 false면 공개하지 않는다.
published: true
# 사용자 정의 변수. 본문에서 {{ page. food }} 형태로 사용 가능하다.
author: jihwan
# 만약 우측 Table Of Contents를 사용하고 싶지 않다면 false로 전환
toc: true
---

## 환경 설정 및 데이터 준비

### GPU/CPU 설정
```python
import torch

device = torch.device("cuda:0" if torch.cuda.is_available() else 'cpu')
```

### 데이터셋 로딩 및 전처리
```python
from torchvision import datasets, transforms

train_dataset = datasets.FashionMNIST(root='./work/FashionMNIST', train=True, download=True, transform = transforms.ToTensor())
test_dataset = datasets.FashionMNIST(root='./work/FashionMNIST', train=False, download=True, transform = transforms.ToTensor())

```

### 데이터 로더 정의
```python
from torch.utils.data import DataLoader

train_loader = DataLoader(train_dataset, batch_size=100)
test_loader = DataLoader(test_dataset, batch_size=100)
```

## 모델 구성

### 모델 클래스 정의
```python
import torch.nn as nn
import torch.nn.functional as F

class FashionDNN(nn.Module):
  def __init__(self):
    super().__init__()
    self.fc1 = nn.Linear(28*28, 512)
    self.dropout = nn.Dropout(0.2)
    self.fc2 = nn.Linear(512, 126)
    self.fc3 = nn.Linear(126, 10)

  def forward(self, input_data):
    out = input_data.view(-1, 28*28)
    out = F.relu(self.fc1(out))
    out = self.dropout(out)
    out = F.relu(self.fc2(out))
    out = self.fc3(out)
    return out
```

### 모델 인스턴스 생성
```python
model = FashionDNN()
```


### 모델을 device로 이동
```python
model = model.to(device)
```

## 손실함수 및 최적화 함수 설정

### 손실함수 정의 
```python
creterion = nn.CrossEntropyLoss()
```


### 최적화 함수 정의
```python
optim = torch.optim.Adam(model.parameters(), lr = 0.001)
```


## 학습 및 검증 루프

### 에포크 설정
```python
epoch = 5

for i in range(epoch):
  pass

```


### 미니 배치 단위로 학습
### Forward pass
### Backword pass
```python
  for imgs, labels in train_loader:
    imgs, labels = imgs.to(device), labels.to(device)

    # Forward pass
    pred = model(imgs)
    loss = creterion(pred, labels)

    # Backward pass
    optim.zero_grad()
    loss.backward()
    optim.step()
```

## 모델 저장

### 모델 저장
```python
torch.save(model.state_dict(), 'model.pth')
```
