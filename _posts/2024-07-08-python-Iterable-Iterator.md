---
# 사용할 layout file 지정
layout: post
# 게시글 제목
title: "파이썬의 Iterator와 Iterable"
# 게시글 시간 설정. 파일 명 보다 우선한다.
date: 2024-07-08 +0900
# 게시글의 카테고리. 최상단과 서브 카테고리만 있다.
categories: [python, language]
# 게시글 태그 설정. ,로 태그들을 구분해서 작성 가능하다.
tags: [python, iterator, iterable]
# 공개여부 설정. true면 공개하고 false면 공개하지 않는다.
published: true
# 사용자 정의 변수. 본문에서 {{ page. food }} 형태로 사용 가능하다.
author: jihwan
# 만약 우측 Table Of Contents를 사용하고 싶지 않다면 false로 전환
toc: true
---
## Iterable
### 정의
Iterator를 반환하는 `__iter__()` 메서드를 구현하거나, `__getitem()__` 메서드를 구현하고 인덱스 0부터 연속적으로 접근 가능한 객체

### 특징
- **반드시 Iterator인 것은 아니다.**
- 요소에 순차적으로 접근할 수 있는 속성을 제공한다. 
- for 반복문에서 사용 가능하다. 

### 구현
```python
class MyIterable:
    def __init__(self, data):
        self.data = data
    
    def __iter__(self):
        # Iterator 객체를 반환
        return iter(self.data)

# 사용 예제
my_iterable = MyIterable([1, 2, 3, 4, 5])

# for 반복문을 통해 순회 가능
for item in my_iterable:
    print(item)

```

## Iterator
### 정의
Iterable 객체에서 요소를 하나씩 가져오는 객체로써, `__iter__()`메서드 를 구현해야 한다.(`__getitem__()`으로 대체 불가능하다.) 다음 요소를 반환하는 `__next__()`메서드를 구현해야 한다. 

### 특징
- **반드시 Iterable이다.** => Iterable의 특징 참조

### 구현
```python
class MyIterator:
    def __init__(self, max_num):
        self.max_num = max_num
        self.current = 1

    def __iter__(self):
        return self  # Iterator는 자신을 반환해야 합니다.

    def __next__(self):
        if self.current <= self.max_num:
            result = self.current
            self.current += 1
            return result
        else:
            raise StopIteration

# Iterator 객체 생성
my_iterator = MyIterator(5)

# 반복문을 통해 값들을 출력
for num in my_iterator:
    print(num)


```
