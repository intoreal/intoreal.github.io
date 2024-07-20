---
layout: post
title: "전이학습, 특성추출 방법 워크플로우"
date: 2024-07-19 +0900
categories: [python, pytorch]
tags: [pytorch, transferLearning]
published: true
author: jihwan
toc: true
---

## 환경 설정 및 데이터 준비
### 관련 패키지 로딩
```python
import torch
import torch.nn as nn
from torch.utils.data import DataLoader
from torchvision import datasets, transforms, models

```
### GPU/CPU 설정
```python
device = torch.device("cuda:0" if torch.cuda.is_available() else "cpu")
```

### 데이터셋 로딩 및 전처리
```python
# resnet18은 입력 데이터의 사이즈가 244
transform = transforms.Compose([
    transforms.Resize(244), 
    transforms.CenterCrop(244),
    transforms.ToTensor()
])
train_dataset = datasets.ImageFolder(root = './work/data/chap05/data/catanddog/train', transform = transform)
test_dataset = datasets.ImageFolder(root = './work/data/chap05/data/catanddog/test', transform = transform)
```
### 데이터 로더 정의
```python
train_loader = DataLoader(train_dataset, batch_size = 32, num_workers = 8, shuffle=True)
test_loader = DataLoader(test_dataset, batch_size = 32, num_workers = 8, shuffle = True)
```

## 모델 구성
### 모델 클래스 정의
```python
# 생략
```
### 모델 인스턴스 생성
```python
model = models.resnet18(pretrained=True)

model.fc = nn.Linear(512,2)
```
### 전이학습 설정
```python
for param in model.parameters():
  param.requires_grad = False

for param in model.fc.parameters():
  param.requires_grad = True
```
### 모델을 device로 이동
```python
model = model.to(device)
```

## 손실함수 및 최적화 함수 설정
```python
criterion = nn.CrossEntropyLoss()
optim = torch.optim.Adam(model.parameters(), lr = 0.001)
```

## 학습 및 검증 루프
```python
epoch = 20

for i in range(epoch):
  for imgs, labels in train_loader:
    imgs, labels = imgs.to(device), labels.to(device)

    outs = model(imgs)
    loss = criterion(outs, labels)

    optim.zero_grad()
    loss.backward()
    optim.step()

  score = 0
  for imgs, labels in test_loader:
    imgs, labels = imgs.to(device), labels.to(device)

    outs = model(imgs)
    pred = torch.max(outs, dim=1)[1]

    score += (pred == labels).sum()
  
  print("Accuracy: ", score/len(test_dataset)) 
```


