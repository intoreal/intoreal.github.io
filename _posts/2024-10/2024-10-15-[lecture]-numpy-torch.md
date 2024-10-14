---
layout: post
title: "[강의] pytorch, numpy 비교"
date: 2024-10-15 +0900
categories: [python, pytorch]
tags: [numpy, pytorch]
published: true
author: jihwan
toc: true
---
## 1. 상태 확인

```python
A = np.array([[1,2],[3,4]])
print(A.shape) # (2, 2)
print(A.ndim)  # 2
print(A.dtype) # <class 'numpy.ndarray'>
print(A.size)  # 4
```

```python
A = torch.tensor([[1,2], [3,4]])  
print(A.shape)                   # torch.Size([2, 2])
print(A.ndim)                    # 2
print(A.dtype)                   # <class 'torch.Tensor'>
print(A.numel())                 # 4 # 요소의 갯수 
```

## 2. 데이터 생성

### (1) list to torch(numpy)

```python
A = np.array([[1,2], [3,4]])
```

```python
A = torch.tensor([[1,2], [3,4]])
```

### (2) zeros, ones
```python
A = np.zeros(5)           # [0. 0. 0. 0. 0.]
A = np.zeros((3,3))       # [[0. 0. 0.]
                          # [0. 0. 0.]
                          # [0. 0. 0.]]
A = np.zeros_like(B)      # B와 같은 shape로 생성
```

```python
A = torch.zeros(5)           # tensor([0., 0., 0., 0., 0.])
A = torch.zeros((3,3))       # tensor([[0., 0., 0.],
                             # [0., 0., 0.],
                             # [0., 0., 0.]])
A = torch.zeros_like(B)      # B와 같은 shape로 생성
```

### (3) arange, linspace
* numpy의 linspace는 endpoint를 정의할 수 있다. 
* torch의 linspace는 endpoint가 포함된다. 
```python
A = np.arange(0, 10, 2)                   # [0 2 4 6 8]
# (시작, 미만, 갭)
A = np.linspace(0, 10, 4, endpoint=False)  # [0.  2.5 5.  7.5]
# (시작, 끝, 나누는 갯수, 끝 포함 여부)
```

```python
A = torch.arange(0, 10, 2)                # tensor([0, 2, 4, 6, 8])
# (시작, 미만, 갭)
A = torch.linspace(0, 10, 4)              # tensor([ 0.0000,  3.3333,  6.6667, 10.0000])
# (시작, 끝, 나누는 갯수)
```
### (4) random data
* numpy의 rand와 randn에서는 사이즈를 튜플로 주지 않아도 된다. 
```python
# 균등분포(uniform) [0, 1) 범위 균일하게 분포된 난수, 평균 0.5
A = np.random.rand(3,3)

# 정규분포(normal) 평균 0 표준편차 1
A = np.random.randn(3,3)

# 정수 생성(시작값, 미만값, shape)
A = np.random.randint(1, 10, (3,3))
```

```python
# 균등분포(uniform) [0, 1) 범위 균일하게 분포된 난수, 평균 0.5
A = torch.rand(3,3)

# 정규분포(normal) 평균 0 표준편차 1
A = torch.randn(3,3)

# 정수 생성(시작값, 미만값, shape)
A = torch.randint(1, 10, (3,3))
```

## 3. 데이터 구조 변화

### (1) reshape
```python
A = np.random.rand(2,4)
A = A.reshape(4,2)
```

```python
A = torch.rand(2,4)
A = A.reshape(4,2)
```

### (2) transpose
```python
A = np.random.rand(2,3,4)
A = A.transpose(2,0,1)
print(A.shape)             # (4, 2, 3)
```

```python
A = torch.rand(2,3,4)
A = A.permute(2,0,1)
print(A.shape)             # torch.Size([4, 2, 3])
```



### (2) squeeze, unsqueeze
* squeeze : 차원의 크기가 1인 차원을 제거한다. 

```python
A = np.random.randn(1,1,1,3,1,1,4,1)
print(A.shape)                         # (1, 1, 1, 3, 1, 1, 4, 1)
print(A.squeeze().shape)               # (3, 4)
print(A.squeeze(axis=(0,2,4,5)).shape) # (1, 3, 4, 1)
```

```python
A = torch.randn(1,1,1,3,1,1,4,1)
print(A.shape)                         # torch.Size([1, 1, 1, 3, 1, 1, 4, 1])
print(A.squeeze().shape)               # torch.Size([3, 4])
print(A.squeeze(dim=(0,2,4,5)).shape)  # torch.Size([1, 3, 4, 1])
```

* unsqueeze : 해당 위치에 크기 1짜리 차원을 하나 추가한다. 
```python
A = torch.randn(3,4)
print(A.unsqueeze(dim=0).shape)
print(A.unsqueeze(dim=1).shape)
print(A.unsqueeze(dim=2).shape)
print("---------")
print(A.reshape(1,3,4).shape)
print(A.reshape(3,1,4).shape)
print(A.reshape(3,4,1).shape)
```

## 4. 인덱싱

### (1) basic indexing
```python
A = np.array([1,2,3,4,5,6,7,8,9])
print(A[0])
print(A[-1])
print(A[1:4])
print(A[7:])
print(A[:7])
print(A[:])

B = np.array([[1,2,3], [4,5,6]])
print(B[:][1])                 # B[2]와 같다.  tensor([4, 5, 6])
print(B[:,1])                  # 0번째 차원에서 전체 선책, 1번째 차원에서는 1번째 선택 후 해당 차원 삭제, tensor([2, 5])
```

### (2) boolean indexing
```python

# boolean 인덱싱
A = np.array([[1,2,3,4],[5,3,7,3]])
print(A==3)      # True, False가 담긴 같은 shape의 행렬
print(A[A==3])   # True, False가 담긴 boolean 행렬로 인덱싱 가능!!

A[A==3] = 100    # 마스킹 된 대상에 대해 일괄 수정(3과 같은 요소를 100으로 수정)

A = np.array([[1,2],[3,4],[5,6],[7,8]])
B = np.array([True, False, False, True]) 
print(A[B,:])     
print(A[A[:,0]<0,:]) # 0 번째 열이 음수인 행들
```

```python
A = torch.tensor([[1,2,3,4],[5,3,7,3]])
print(A==3)      # True, False가 담긴 같은 shape의 행렬
print(A[A==3])   # True, False가 담긴 boolean 행렬로 인덱싱 가능!!

A[A==3] = 100    # 마스킹 된 대상에 대해 일괄 수정(3과 같은 요소를 100으로 수정)

A = torch.tensor([[1,2],[3,4],[5,6],[7,8]])
B = torch.tensor([True, False, False, True]) 
print(A[B,:])     
print(A[A[:,0]<0,:]) # 0 번째 열이 음수인 행들
```

### (3) np.array(torch.tensor) indexing
```python
A = np.array([1,2,3,4,5])
print(A[np.array(2)])        # 2번째 요소 출력 3
print(A[np.array([2,3,4])])  # 2 3 4번째 요소를 같은 shape로 출력
print(A[np.array([[2,2,2],[3,3,3]])])   # [[3,3,3], [4,4,4]]

A = np.array([[1,2,3],[4,5,6]])
print(A[np.array([[0,1],[1,1]])]) # [[[1 2 3], [4 5 6]], [[4 5 6], [4 5 6]]]

```

```python
A = torch.tensor([1,2,3,4,5])
print(A[torch.tensor(2)])        # 2번째 요소 출력 3
print(A[torch.tensor([2,3,4])])  # 2 3 4번째 요소를 같은 shape로 출력
print(A[torch.tensor([[2,2,2],[3,3,3]])])   # [[3,3,3], [4,4,4]]

A = torch.tensor([[1,2,3],[4,5,6]])
print(A[torch.tensor([[0,1],[1,1]])]) # [[[1 2 3], [4 5 6]], [[4 5 6], [4 5 6]]]

```

## 5. 데이터 연산

### (1) Hardamad 
* 행렬곱이 아닌 각 요소별 연산을 수행한다. 
```python
A = np.array([[1,2], [3,4]])
B = np.array([[1,2], [3,4]])

print(A+B)  # [[2,4], [6,8]]
print(A-B)  # [[0,0], [0,0]]
print(A*B)  # [[1,4], [9,16]]
print(A/B)  # [[1,1], [1,1]]
print(A**2) # [[1,4], [9,16]]
```

```python
A = torch.tensor([[1,2], [3,4]])
B = torch.tensor([[1,2], [3,4]])

print(A+B)  # [[2,4], [6,8]]
print(A-B)  # [[0,0], [0,0]]
print(A*B)  # [[1,4], [9,16]]
print(A/B)  # [[1,1], [1,1]]
print(A**2) # [[1,4], [9,16]]
```
### (2) 행렬곱
```python
# numpy, torch 모두
A@B
```

## 6. 데이터 메소드

### (1) 삼각함수
```python
print(np.sin(np.pi/6))
print(np.cos(np.pi/3))
print(np.tan(np.pi/4))
print(np.tanh(-10))
```
```python
print(torch.sin(torch.tensor(torch.pi/6)))
print(torch.cos(torch.tensor(torch.pi/3)))
print(torch.tan(torch.tensor(torch.pi/4)))
print(torch.tanh(torch.tensor(-10)))
```

### (2) nan, inf
```python
print(np.isnan([1,2,np.nan,3,4]))
print(np.isinf([1,2,3,4,np.inf]))
```
```python
print(torch.isnan(torch.tensor([1,2,torch.nan,3,4])))
print(torch.isinf(torch.tensor([1,2,3,4,torch.inf])))
```
### (3) max, min
* axis가 지정될 경우 해당 차원이 사라지는 shape로 max, min을 구한다. 
* keepdims True일 경우 해당 차원이 1이 되는 shape로 max, min을 구한다. 
```python
A = np.random.randn(3,4)
print(A)
print(np.max(A))        # 최대값 숫자 하나
print(np.max(A,axis=0))
print(np.max(A,axis=1)) # 1D array로 바꿔버림
print(np.max(A,axis=0, keepdims=True))
print(np.max(A,axis=1, keepdims=True)) # 3 행 1열 짜리 2D array
print(np.min(A))
print(np.min(A,axis=0))
print(np.min(A,axis=1))
print(np.argmax(A))
print(np.argmax(A,axis=0)) # 각 열에서 가장 큰 애가 존재하는 인덱스
print(np.argmax(A,axis=1)) # 각 행에서 가장 큰 애가 존재하는 인덱스

```
```python
A = torch.randn(3,4)
print(torch.max(A))       # 최대값 숫자 하나
print(torch.max(A,dim=0))
print(torch.max(A,dim=1)) # 1D array로 바꿔버림
print(torch.max(A,dim=0, keepdims=True)) # 차원 수는 유지, dim 번째 axis size 는 1차원으로 압축됨
print(torch.max(A,dim=1, keepdims=True)) # 차원 수는 유지, dim 번째 axis size 는 1차원으로 압축됨. 3 행 1열 짜리 2D array

print(torch.argmax(A))
print(torch.argmax(A,dim=0)) # 각 열에서 가장 큰 애가 존재하는 인덱스
print(torch.argmax(A,dim=1)) # 각 행에서 가장 큰 애가 존재하는 인덱스

```
### (4) sum, mean
```python
A = np.random.randn(3,4)
print(A)
print(np.sum(A))
print(np.sum(A,axis=1))
print(np.sum(A,axis=1,keepdims=True))

print(np.mean(A))
print(np.mean(A,axis=1))
print(np.mean(A,axis=1,keepdims=True))
print(np.std(A)) # standard deviation 표준 편차
```
```python
A = torch.randn(3,4,5)
print(A)
print(torch.sum(A))
print(torch.sum(A,dim=1))  # dim 에 해당하는 차원은 날라간다.
print(torch.sum(A,dim=1,keepdims=True))

print(torch.mean(A))
print(torch.mean(A,dim=1))
print(torch.mean(A,dim=1,keepdims=True))
```

### (5) sort
```python
A = np.random.randn(6,2)

np.sort(A)   # 각 행별로 소팅한 결과물 반환
A.sort()     # 각 행별로 소팅한 결과물을 a에 저장
```
```python
A = np.random.randn(6,2)

# torch에서는 결과가 같다. 소팅결과는 반환되고 원본은 유지된다. 
torch.sort(A)
A.sort()
```