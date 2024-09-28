---
title: "[Python] 입력값의 차이 - input(), sys.stdin.readline() 시간초과 그 차이를 찾아서"
description: 
author:
date: 2024-09-09 20:27:00 +0900
categories: [코딩지식, python]
tags: [python]
pin: false
math: true
mermaid: true
# image:
#   path: /assets/img/20240912_post/KT_모집요강.jpg
#   lqip: data:image/webp;base64,UklGRpoAAABXRUJQVlA4WAoAAAAQAAAADwAABwAAQUxQSDIAAAARL0AmbZurmr57yyIiqE8oiG0bejIYEQTgqiDA9vqnsUSI6H+oAERp2HZ65qP/VIAWAFZQOCBCAAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
#   alt: .
---

## **0. 들어가기에 앞서**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />
파이썬으로 코테 문제를 풀다보면 의문점이 생깁니다.  
입력받는 방법에 따라서 시간초과가 걸릴때도 있고 걸리지 않을때도 있다는것입니다.  
이러한 시간초과는 보통 코더가 간단하게 입력할 수 있는 input()를 입력했을때 발생한다는것을 경험으로 알 수 있습니다.  
이번 게시글에서는 시간초과가 발생하는 이유와 입력값을 받는 다양한 방법에 대해서 알아보고자 합니다.  

<br/>

## **1. 파이썬 입력**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />

### **1.1) input()함수**
- **장점**
  - 함수를 호출하는것만으로 값을 즉시 받아오는 간편함을 가졌습니다.
  - 자동으로 개행문자를 제거해줍니다
- **단점**
  - 한줄씩 입력받을때마다 추가 작업 후 버퍼에서 읽어 속도가 느립니다. 이는 대용량의 데이터를 읽을때 매우 비효율적입니다.
  - 사용자의 엔터단위로 입력받아 여러줄을 입력받으려면 `for` 혹은 `while`등을 이용해 입력받습니다.

### **1.2) sys.stdin.readline()함수**
- **장점**
  - 버퍼에서 읽어오는것은 같으나 개행문자를 제거하는등의 추가작업이 없어 상대적으로 속도가 빠릅니다.
  - 버퍼에서 한번에 입력값을 읽어와 성능면에서 유리합니다.
- **단점**
  - 입력한 문자열 끝에 개행문자를 포함하여 반환합니다.
  - 모듈 `import sys` 가 필요합니다.

### **1.3) 속도차이가 존재하는 이유**
이쯤에서 의문이 생길 수 있습니다.  
**그래서 속도차이가 생기는 이유가 뭔데?**라는 의문입니다.

이 의문을 해결하기전에 아래 코드를 입력해봅시다.
```python
import sys
import time

# input() 성능 테스트
start_time = time.time()
with open('C:/Users/tjdud/Downloads/read.txt', 'r') as f:
    for _ in range(1000000):
        input_data = f.readline().rstrip()  # input()과 유사한 처리
end_time = time.time()
print(f"파일을 이용한 input() 함수 실행 시간: {end_time - start_time:.6f}초")

# sys.stdin.readline().rstrip() 성능 테스트
start_time = time.time()
with open('C:/Users/tjdud/Downloads/read.txt', 'r') as f:
    for _ in range(1000000):
        f.readline().rstrip()
end_time = time.time()
print(f"파일을 이용한 sys.stdin.readline().rstrip() 함수 실행 시간: {end_time - start_time:.6f}초")
```
결과를 보면 다음과 같습니다.
```
파일을 이용한 input() 함수 실행 시간: 0.158999초
파일을 이용한 sys.stdin.readline().rstrip() 함수 실행 시간: 0.147001초
```
실제 input()와 sys.stdin.readline()의 비교가 아닌 최대한 비슷한 방법으로 실행한것으로 결과값이 다를 수 있으나 sys.stdin.readline()가 보다 빠른것을 볼 수 있습니다.  

이렇게 성능 차이가 나는 이유는 input()함수는 근본적으로 개행문자를 제거하는등의 추가적인 작업이 일어나면서 여러번의 작업이 일어나 속도면에서 sys.stdin.readline()보다 느려지게됩니다.  

### **1.3) 추가적인 의문 rstrip()**

그러면 이쯤에서 추가적인 의문이 생길 수 있습니다.  
**`input()`랑 `sys.stdin.readline().rstrip()`는 둘다 개행문자를 제거하는거니까 속도가 비슷한거 아니야?**라는 의문입니다.  
하지만 이는 틀렸습니다.  

input()가 여전히 sys.stdin.readline().rstrip()보다 동작 속도가 느린 이유는 아래와 같습니다.  

#### **- 함수호출 오버헤드**
- 물론 sys.stdin.readlin().rstrip()또한 오버헤드가 존재합니다.  
하지만 이는 추가적인 편의기능이 포함되어있는 input()보다 간소합니다.  

#### **- 입력 검증 및 처리**
- input()의 개행문자 처리와 rstrip()와 개행문자 제거라는 결과는 비슷해보이나 내부적으로 보면 다릅니다.
input()은 표준입력 데이터를 읽고, 자동으로 개행문자를 제거하는 과정에서 이를 위한 추가적인 시스템 호출이 일어나게됩니다.  

#### **- 로컬화 및 유니코드 처리**
- sys.stdin.readline()은 로케일 혹은 인코딩에대한 추가적인 처리 없이 값을 그대로 반환하는 저수준 함수인 반면에, input()은 고수준 함수로, 다양한 문자 인코딩이나 로컬화된 환경에서의 입력을 처리합니다.  
이로 인해 입력 데이터를 처리하는 과정에서 추가적인 연산이 포함될 가능성이 높습니다.  

#### **- 에러 처리**
- sys.stdin.readline().rstrip()도 EOD같은 예외상황을 처리하지만 input()가 보다 더 포괄적인 에러 처리를 내장하고 있습니다. 이는 목적의 차이로 input()는 보다 다양한 상황에대한 복합적인 예외를 포함하는 반면에 sys.stdin.readline()은 단순히 입력을 읽고 이를 반환하는 것에 초점이 맞춰져 있어서 그렇습니다.

<br/>

## **2. 내용 요약**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />

| 특성            | input()                            | sys.stdin.readline()                         |
|-----------------|------------------------------------|---------------------------------------------|
| 속도            | 느림                               | 빠름                                        |
| 개행 처리        | 자동으로 개행 문자 제거             | 개행 문자를 수동으로 제거해야 함              |
| 사용 용이성      | 간편                               | 약간 복잡                                   |
| 여러 줄 입력     | 기본적으로는 불가능, 반복문 필요    | `sys.stdin.read()`로 가능                    |
| 대용량 입력 처리 | 비효율적                           | 효율적                                       |

보는것과 같이 input()을 사용하면 sys.stdin.readline()에 배해 보편적으로 사용할 수 있으나 효율성이 떨어져 시간초과가 나오게 되는것입니다.

<br/>

## **글을 마무리하며**

<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />

이번 포스팅에서는 여러분이 코딩테스트할때 혹은 평소에 간과할 수 있었던 입력값에따른 작동방식의 차이점을 알아보았습니다.
혹시 잘못된 부분이 있으면 지적은 언제나 환영이며 이를 적극 반영하여 보다 질높은 정보를 제공하도록 하겠습니다!
다음에는 좀 더 흥미로운 코딩지식과 다양한 정보를 가지고 찾아올 수 있도록 하겠습니다!

이만 가보겠습니다!
