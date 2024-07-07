---
# 사용할 layout file 지정
layout: post
# 게시글 제목
title: "파이썬의 Sequence 타입 정리"
# 게시글 시간 설정. 파일 명 보다 우선한다.
date: 2024-07-08 +0900
# 게시글의 카테고리. 최상단과 서브 카테고리만 있다.
categories: [python, language]
# 게시글 태그 설정. ,로 태그들을 구분해서 작성 가능하다.
tags: [python, language]
# 공개여부 설정. true면 공개하고 false면 공개하지 않는다.
published: true
# 사용자 정의 변수. 본문에서 {{ page. food }} 형태로 사용 가능하다.
author: jihwan
# 만약 우측 Table Of Contents를 사용하고 싶지 않다면 false로 전환
toc: true
---
## Sequence 타입의 특징
- 데이터에 순서가 있다. 
- 인덱싱과 슬라이싱이 가능하다. 
- len() 함수로 길이를 잴 수 있고, in 연산자로 멤버십 테스트가 가능하다. 
- iterable 하다. => for 문에서 사용가능하다. 

## Sequence 타입 정의의 조건
- collection.abc.Sequence 클래스를 상속받는다. 
- `__len__(self)` 함수를 구현한다. 
- `__getitem__(self, idx)`함수를 구현한다. 

### 예시
```python
from collections.abc import Sequence

class MySequence(Sequence):
    def __init__(self, elements):
        self.elements = list(elements)  # 내부적으로 리스트로 저장합니다

    def __len__(self):
        return len(self.elements)

    def __getitem__(self, index):
        return self.elements[index]

    # 추가적으로 필요한 메서드들을 구현할 수 있습니다
    def append(self, element):
        self.elements.append(element)

    def __repr__(self):
        return f'MySequence({self.elements})'

# 테스트용 예제
if __name__ == '__main__':
    seq = MySequence([1, 2, 3, 4, 5])
    print(seq)         # MySequence([1, 2, 3, 4, 5])
    print(len(seq))    # 5
    print(seq[2])      # 3
    print(seq[-1])     # 5

    seq.append(6)
    print(seq)         # MySequence([1, 2, 3, 4, 5, 6])

```

