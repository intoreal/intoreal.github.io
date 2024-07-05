---
# 사용할 layout file 지정
layout: post
# 게시글 제목
title: "pytorch custom dataset 생성법"
# 게시글 시간 설정. 파일 명 보다 우선한다.
date: 2024-07-05 +0900
# 게시글의 카테고리. 최상단과 서브 카테고리만 있다.
categories: [pytorch, torchvision]
# 게시글 태그 설정. ,로 태그들을 구분해서 작성 가능하다.
tags: [python, pytorch, torchvision, dataset, dataloader]
# 공개여부 설정. true면 공개하고 false면 공개하지 않는다.
published: true
# 사용자 정의 변수. 본문에서 {{ page. food }} 형태로 사용 가능하다.
author: jihwan
# 만약 우측 Table Of Contents를 사용하고 싶지 않다면 false로 전환
toc: true
---
## pytorch dataset의 개념
pytorch의 dataset을 생성하려면 아래의 조건을 만족해야 한다. 
> 1. torch.utils.data.Dataset을 상속하는 클래스일 것
> 2. Sequence 타입일 것(__len__과 __getitem__ 구현)
> 3. __getitem__메서드에서 데이터와 라벨을 반환할 것
> 4. (필요시) transform을 생성자 인자로 받아 __getitem__에 반영할 것

### torchvision.transforms.ToTensor()의 조건?
ToTensor는 클래스로써 호출하여 인스턴스를 사용해야 한다. \
ToTensor는 입력값으로 2차원(shape=(h, w)) 혹은 3차원(RGB, shape=(h,w,c)) 배열을 기대한다. 

## 패키지 import
```python
import torch
from torchvision import transforms
import numpy as np
```
## 기본 데이터 생성
```python
labels = np.random.randint(low=0,high=4,size=(100,))
data = np.array([np.ones(shape=(32,32,3)) * i for i in labels])
```
### 더 개선된 코드
```python
# 라벨 생성
labels = np.random.randint(low=0, high=4, size=100)

# 각 라벨에 해당하는 32x32x3 텐서 생성 (브로드캐스팅을 이용한 방법)
data = np.ones((100, 32, 32, 3)) * labels[:, None, None, None]
```
## CustomDataset 클래스 정의
```python
class CustomDataset(torch.utils.data.Dataset):
  def __init__(self, data, labels, transform=None):
    self.data = data
    self.labels = labels
    self.transform = transform
  
  def __len__(self): # Sequence 타입이 되기 위한 조건
    return len(self.data)
  
  def __getitem__(self, idx):  # Sequence 타입으로 만들기
    sample = self.data[idx]
    label = self.labels[idx]

    if self.transform:
      sample = self.transform(sample)
    
    return sample, label
```
## customDataset 생성
```python
customDataset = CustomDataset(data, labels, transform = transforms.ToTensor())
```

## customDataset의 사용
> 이 경우 dataset에서 slice 기능 [0:10]은 사용할 수 없다. 이것은 torchvision의 다른 데이터셋도 그렇다. 
{: .prompt-warning }
```python
customDataset[0]
```

## DataLoader의 사용
```python
dataLoader = torch.utils.data.DataLoader(customDataset, batch_size=10, shuffle= True)
```