---
title: "[Computer Science] Chapter 05. 큐 ~ Chapter 08. 트리"
description: 
author:
date: 2024-09-27 20:00:00 +0900
categories: [코딩지식, CS]
tags: [큐, 연결리스트I, 연결리스트II, 트리]
pin: false
math: true
mermaid: true
image:
  path: /assets/img/20240926_post/data_structure.jpg
  lqip: data:image/webp;base64,UklGRpoAAABXRUJQVlA4WAoAAAAQAAAADwAABwAAQUxQSDIAAAARL0AmbZurmr57yyIiqE8oiG0bejIYEQTgqiDA9vqnsUSI6H+oAERp2HZ65qP/VIAWAFZQOCBCAAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
  alt: data_structure.jpg
---




## **0. 들어가기전에**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 
본 포스트는 예전에 공부하였던 자료구조를 복습하는 의미에서 진행하는 공부이며 자세한 설명은 없이 중요한 키워드 중심으로 정리됩니다.  
[C언어로 쉽게 풀어쓴 자료구조_천인국,공용해,하상호_생능출판사](https://www.booksr.co.kr/product/9788970509716/)를 바탕으로 합니다.

## **1. 큐**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

### 특징
선입선출(FIFO, First-In-First-Out)

### 주요 연산 : 기본적으로 스택이랑 비슷하지만 연산 이름과 동작이 살짝씩 다릅니다.
- 삽입(Enqueue)
- 삭제(Dequeue)
- 탑(Peek, Front)
- Size
- isFull
- Clear

### 큐의 종류

- 기본 큐 (Basic Queue)
  - 가장 기본적인 큐 구조로, enqueue와 dequeue를 통해 데이터의 삽입과 삭제가 이루어집니다.

- 원형 큐 (Circular Queue)
  - 기본 큐의 단점인 dequeue 연산이 반복되면 앞부분이 비게 되어 공간이 낭비되는 점을 해결하기 위해 큐의 끌과 앞부분이 연결되어 원형 형태
  - 마지막 인덱스가 되면 다시 처음 인덱스로 돌아와 빈 공간을 재사용함.

- 우선순위 큐 (Priority Queue)
  - 들어온 순서에 상관없이 우선순위가 높은 데이터가 먼저 나가는 큐
  - 일반적으로 최소 힙(min-heap)이나 최대 힙(max-heap) 등의 자료구조를 활용하여 구현함.

- 덱(Deque, Double-Ended Queue)
  - 큐의 앞과 뒤 양쪽에서 데이터의 삽입과 삭제가 가능한 큐
  - 덱은 스택과 큐의 기능을 모두 포함한 형태로, 데이터의 삽입과 삭제가 유연하게 이루어짐.

### 큐의 구현

- 배열
  - 고정 크기를 가지며, 큐가 꽉 차면 더 이상 데이터를 삽입할 수 없다.
  - 배열의 앞쪽 데이터를 삭제할 때, 데이터를 한 칸씩 이동시켜야 하는 단점이 있다.

- 연결 리스트
  - 연결 리스트의 각 노드가 데이터와 다음 노드의 포인터를 포함하는 방식으로, 동적으로 크기를 확장할 수 있다.
  - enqueue와 dequeue 연산이 빠르지만, 노드 간의 연결을 유지하기 위한 추가 메모리가 필요함.

### 장단점
- 장점
  - 큐는 데이터의 처리 순서를 보장하여 순차적으로 작업을 수행하는데 유리합니다.
  - 프로세스 관리, 네트워크 패킷 처리 등 순서가 중요한 작업에서 활용할 수 있습니다.

- 단점
  - 기본 큐는 크기가 고정된 배열로 구현할 경우, 큐의 앞부분이 비게 되면 공간 낭비가 발생합니다.
  - 데이터 삽입과 삭제가 반복되면, 매번 메모리를 재할당해야 할 수 있습니다. 이를 해결하기 위해 원형 큐나 연결 리스트 기반의 큐를 사용합니다.

<br>

## **2. 연결리스트 I & 연결리스트 II**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

### 노드(Node)와 포인터
- 각 노드는 데이터와 다음 노드를 가리키는 포인터로 이루어져 있음  
- 노드는 메모리 상에 비연속적으로 위치할 수 있음.  
- 각 노드의 포인터가 다음 노드의 메모리 위치를 가리킴으로써 리스트가 연결된다.  

### 동적 메모리 할당
- 연결 리스트는 크기가 고정된 배열과 달리, 동적으로 크기가 변할 수 있음.  
- 데이터를 추가하거나 삭제할 때, 메모리 공간을 재할당할 필요 없이 쉽게 조작할 수 있다.

### 순차 접근
- 연결 리스트는 임의 접근(Random Access)이 불가능하다. 처음부터 순차적으로 접근해야 합니다.  
- 특정 위치에 접근하려면 Head(첫 노드)부터 해당 위치까지 순회해야 하므로 접근 시간 복잡도는 O(n)

### 주요 연산
- 노드 삽입 (Insert)
  - 삽입 위치에 따라 헤드 삽입, 꼬리 삽입, 중간 삽입으로 나뉜다.
- 노드 삭제 (Delete)
  - 삭제 위치에 따라 헤드 삭제, 꼬리 삭제, 중간 삭제으로 나뉜다.
- 노드 탐색 (Search)
  - 리스트의 처음부터 순차적으로 원하는 데이터를 찾는 연산.
  - 임의 접근이 불가능하므로 특정 데이터를 찾으려면 처음부터 끝까지 순회해야 한다.
- 노드 접근 (Get Node)
  - 특정 인덱스나 위치에 있는 노드를 반환
- 노드 개수 확인 (Size)
  - 연결 리스트의 노드 개수를 반환하는 연산.
- 연결 리스트 출력 (Print)
  - 연결 리스트의 모든 노드를 순서대로 출력

### 연결리스트 종류

- 단일 연결 리스트
  - 각 노드는 다음 노드를 가리키는 **포인터(Next)**를 가짐
  - 마지막 노드의 Next 포인터는 None 또는 null을 가리켜 리스트의 끝임을 표시
  - 단방향만 가능
<div style="text-align: center; font-family: Arial, sans-serif; margin-top: 20px;">
  <!-- Head -->
  <div style="border: 2px solid #007bff; border-radius: 10px; padding: 5px; margin: 0 auto; width: 150px; display: inline-block; box-shadow: 2px 2px 5px rgba(0,0,0,0.1); background-color: #f0f8ff;">
    Head
  </div>
  <!-- 화살표 -->
  <div style="margin: 0; font-size: 24px;">
    ▼
  </div>
  <!-- Data | Next -->
  <div style="border: 2px solid #28a745; border-radius: 10px; padding: 0; margin: 0 auto; width: 150px; box-shadow: 2px 2px 5px rgba(0,0,0,0.1); background-color: #e6ffed;">
    <!-- Data -->
    <div style="padding: 5px;">
      Data
    </div>
    <!-- 경계선 -->
    <div style="margin: 0 auto; width: 100%; height: 1px; background-color: #28a745;">
    </div>
    <!-- Next -->
    <div style="padding: 5px;">
      Next
    </div>
  </div>
  <!-- 화살표 -->
  <div style="margin: 0; font-size: 24px;">
    ▼
  </div>
  <!-- Data | Next -->
  <div style="border: 2px solid #28a745; border-radius: 10px; padding: 0; margin: 0 auto; width: 150px; box-shadow: 2px 2px 5px rgba(0,0,0,0.1); background-color: #e6ffed;">
    <!-- Data -->
    <div style="padding: 5px;">
      Data
    </div>
    <!-- 경계선 -->
    <div style="margin: 0 auto; width: 100%; height: 1px; background-color: #28a745;">
    </div>
    <!-- Next -->
    <div style="padding: 5px;">
      Next
    </div>
  </div>
  <!-- 화살표 -->
  <div style="margin: 0; font-size: 24px;">
    ▼
  </div>
  <!-- Data | Next -->
  <div style="border: 2px solid #28a745; border-radius: 10px; padding: 0; margin: 0 auto; width: 150px; box-shadow: 2px 2px 5px rgba(0,0,0,0.1); background-color: #e6ffed;">
    <!-- Data -->
    <div style="padding: 5px;">
      Data
    </div>
    <!-- 경계선 -->
    <div style="margin: 0 auto; width: 100%; height: 1px; background-color: #28a745;">
    </div>
    <!-- Next -->
    <div style="padding: 5px;">
      Next
    </div>
  </div>
  <!-- 화살표 -->
  <div style="margin: 0; font-size: 24px;">
    ▼
  </div>
  <!-- None -->
  <div style="border: 2px solid #dc3545; border-radius: 10px; padding: 5px; margin: 0 auto; width: 150px; display: inline-block; box-shadow: 2px 2px 5px rgba(0,0,0,0.1); background-color: #ffe6e6;">
    None
  </div>
</div>

- 원형 연결 리스트
  - 단일 또는 이중 연결 리스트가 원형 형태로 연결된 구조
  - 마지막 노드의 Next 포인터가 다시 첫 번째 노드를 가리켜 리스트의 끝과 처음이 연결
  - Prev 포인터가 있는 이중 원형 연결 리스트도 존재

<div style="text-align: center; font-family: Arial, sans-serif; margin-top: 20px; position: relative;">
  <!-- Head -->
  <div style="border: 2px solid #007bff; border-radius: 10px; padding: 5px; margin: 0 auto; width: 150px; display: inline-block; box-shadow: 2px 2px 5px rgba(0,0,0,0.1); background-color: #f0f8ff;">
    Head
  </div>
  <!-- 화살표 -->
  <div style="margin: 0; font-size: 24px;">
    ▼
  </div>
  <!-- Data | Next (1) -->
  <div style="border: 2px solid #28a745; border-radius: 10px; padding: 0; margin: 0 auto; width: 150px; box-shadow: 2px 2px 5px rgba(0,0,0,0.1); background-color: #e6ffed;" id="data-next-1">
    <!-- Data -->
    <div style="padding: 5px;">
      Data
    </div>
    <!-- 경계선 -->
    <div style="margin: 0 auto; width: 100%; height: 1px; background-color: #28a745;"></div>
    <!-- Next -->
    <div style="padding: 5px;">
      Next
    </div>
  </div>
  <!-- 화살표 -->
  <div style="margin: 0; font-size: 24px;">
    ▼
  </div>
  <!-- Data | Next (2) -->
  <div style="border: 2px solid #28a745; border-radius: 10px; padding: 0; margin: 0 auto; width: 150px; box-shadow: 2px 2px 5px rgba(0,0,0,0.1); background-color: #e6ffed;">
    <!-- Data -->
    <div style="padding: 5px;">
      Data
    </div>
    <!-- 경계선 -->
    <div style="margin: 0 auto; width: 100%; height: 1px; background-color: #28a745;"></div>
    <!-- Next -->
    <div style="padding: 5px;">
      Next
    </div>
  </div>
  <!-- 화살표 -->
  <div style="margin: 0; font-size: 24px;">
    ▼
  </div>
  <!-- Data | Next (3) -->
  <div style="border: 2px solid #28a745; border-radius: 10px; padding: 0; margin: 0 auto; width: 150px; box-shadow: 2px 2px 5px rgba(0,0,0,0.1); background-color: #e6ffed; position: relative;" id="data-next-3">
    <!-- Data -->
    <div style="padding: 5px;">
      Data
    </div>
    <!-- 경계선 -->
    <div style="margin: 0 auto; width: 100%; height: 1px; background-color: #28a745;"></div>
    <!-- Next -->
    <div style="padding: 5px;">
      Next
    </div>
    <!-- 선: Data | Next (3) 오른쪽에서 나와서 위로 이동 -->
    <div style="position: absolute; top: 75%; right: -50px; width: 100px; height: 2px; background-color: #383840;"></div> <!-- 가로선 -->
    <div style="position: absolute; top: -235px; right: -50px; width: 2px; height: 296px; background-color: #383840;"></div> <!-- 세로선 -->
    <div style="position: absolute; top: -235px; right: -50px; width: 90px; height: 2px; background-color: #383840;"></div> <!-- 첫 번째 상자 오른쪽으로 연결되는 가로선 -->
    <!-- 화살표 머리 -->
    <div style="position: absolute; top: -244px; right: 40px; border: 10px solid transparent; border-right: 10px solid #383840;"></div> <!-- 화살표 -->

  </div>
</div>

- 이중 연결 리스트
  - 각 노드는 **다음 노드(Next)**와 **이전 노드(Prev)**를 가리키는 두 개의 포인터를 가지고 있다.
  - 양방향 순회가 가능하며, 단일 연결 리스트보다 역방향 이동이 용이함.
  - 이전 노드를 가리키는 포인터가 추가되어 삽입 및 삭제 연산이 더 복잡하지만, 양쪽 방향으로 쉽게 접근할 수 있다.

<div style="text-align: center; font-family: Arial, sans-serif; margin-top: 20px;">
  <!-- None (첫 번째) -->
  <div style="border: 2px solid #dc3545; border-radius: 10px; padding: 5px; margin: 0 auto; width: 150px; display: inline-block; box-shadow: 2px 2px 5px rgba(0,0,0,0.1); background-color: #ffe6e6;">
    None
  </div>
  <!-- 화살표 -->
  <div style="margin: 0; font-size: 24px;">
    ▲
  </div>
  <!-- Prev | Data | Next -->
  <div style="border: 2px solid #28a745; border-radius: 10px; padding: 0; margin: 0 auto; width: 150px; box-shadow: 2px 2px 5px rgba(0,0,0,0.1); background-color: #e6ffed;">
    <!-- Prev -->
    <div style="padding: 5px; position: relative;">
      Prev
      <!-- Data와의 구분선 -->
      <div style="position: absolute; top: 100%; left: 0; width: 100%; height: 1px; background-color: #28a745;"></div>
    </div>
    <!-- Data -->
    <div style="padding: 5px; position: relative;">
      Data
      <!-- Next와의 구분선 -->
      <div style="position: absolute; top: 100%; left: 0; width: 100%; height: 1px; background-color: #28a745;"></div>
    </div>
    <!-- Next -->
    <div style="padding: 5px;">
      Next
    </div>
  </div>
  <!-- 양방향 화살표 -->
  <div style="margin: 0; font-size: 24px;">
    ▲▼
  </div>
  <!-- Prev | Data | Next -->
  <div style="border: 2px solid #28a745; border-radius: 10px; padding: 0; margin: 0 auto; width: 150px; box-shadow: 2px 2px 5px rgba(0,0,0,0.1); background-color: #e6ffed;">
    <!-- Prev -->
    <div style="padding: 5px; position: relative;">
      Prev
      <!-- Data와의 구분선 -->
      <div style="position: absolute; top: 100%; left: 0; width: 100%; height: 1px; background-color: #28a745;"></div>
    </div>
    <!-- Data -->
    <div style="padding: 5px; position: relative;">
      Data
      <!-- Next와의 구분선 -->
      <div style="position: absolute; top: 100%; left: 0; width: 100%; height: 1px; background-color: #28a745;"></div>
    </div>
    <!-- Next -->
    <div style="padding: 5px;">
      Next
    </div>
  </div>
  <!-- 양방향 화살표 -->
  <div style="margin: 0; font-size: 24px;">
    ▲▼
  </div>
  <!-- Prev | Data | Next -->
  <div style="border: 2px solid #28a745; border-radius: 10px; padding: 0; margin: 0 auto; width: 150px; box-shadow: 2px 2px 5px rgba(0,0,0,0.1); background-color: #e6ffed;">
    <!-- Prev -->
    <div style="padding: 5px; position: relative;">
      Prev
      <!-- Data와의 구분선 -->
      <div style="position: absolute; top: 100%; left: 0; width: 100%; height: 1px; background-color: #28a745;"></div>
    </div>
    <!-- Data -->
    <div style="padding: 5px; position: relative;">
      Data
      <!-- Next와의 구분선 -->
      <div style="position: absolute; top: 100%; left: 0; width: 100%; height: 1px; background-color: #28a745;"></div>
    </div>
    <!-- Next -->
    <div style="padding: 5px;">
      Next
    </div>
  </div>
  <!-- 화살표 -->
  <div style="margin: 0; font-size: 24px;">
    ▼
  </div>
  <!-- None (마지막) -->
  <div style="border: 2px solid #dc3545; border-radius: 10px; padding: 5px; margin: 0 auto; width: 150px; display: inline-block; box-shadow: 2px 2px 5px rgba(0,0,0,0.1); background-color: #ffe6e6;">
    None
  </div>
</div>

<br>

## **3. 트리**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />
계층적 자료를 표현하는데 적합한 비선형 자료구조로, 노드와 간선으로 구성된다.

### 주요 연산
- 삽입 (Insert)
  - 이진 탐색 트리의 경우, 특정 규칙(왼쪽은 작은 값, 오른쪽은 큰 값)에 따라 노드를 삽입.

- 삭제 (Delete)
  - 이진 탐색 트리의 경우, 자식 노드의 개수(0, 1, 2)에 따라 삭제 알고리즘이 달라진다.

- 탐색 (Search)

- 순회 (Traversal)
  - 트리의 모든 노드를 방문하는 연산.
  - 순회 방법에는 전위 순회(Preorder Traversal), 중위 순회(Inorder Traversal), 후위 순회(Postorder Traversal), **레벨 순회(Level-order Traversal)**가 있다.
    - 전위 순회 (Preorder)
      - Root -> Left -> Right
      - 아래표를 참고하여 : A → B → D → H → I → E → J → K → C → F → L → M → G → N → O
    - 중위 순회 (Inorder)
      - Left -> Root -> Right
      - 아래표를 참고하여 : H → D → I → B → J → E → K → A → L → F → M → C → N → G → O
    - 후위 순회 (Postorder)
      - Left -> Right -> Root
      - 아래표를 참고하여 : H → I → D → J → K → E → B → L → M → F → N → O → G → C → A
    - 레벨 순회 (Level-order)
      - 각 레벨을 차례로 방문
      - 아래표를 참고하여 : A → B → C → D → E → F → G → H → I → J → K → L → M → N → O


<div style="display: flex; justify-content: center; align-items: center;">
  <svg width="300" height="220">
    <!-- 간선 (Edges) -->
    <!-- Depth 1 -->
    <line x1="150" y1="20" x2="90" y2="60" stroke="#28a745" stroke-width="2" />
    <line x1="150" y1="20" x2="210" y2="60" stroke="#28a745" stroke-width="2" />

    <!-- Depth 2 -->
    <line x1="90" y1="60" x2="60" y2="100" stroke="#28a745" stroke-width="2" />
    <line x1="90" y1="60" x2="120" y2="100" stroke="#28a745" stroke-width="2" />
    <line x1="210" y1="60" x2="180" y2="100" stroke="#28a745" stroke-width="2" />
    <line x1="210" y1="60" x2="240" y2="100" stroke="#28a745" stroke-width="2" />

    <!-- Depth 3 -->
    <line x1="60" y1="100" x2="45" y2="140" stroke="#28a745" stroke-width="2" />
    <line x1="60" y1="100" x2="75" y2="140" stroke="#28a745" stroke-width="2" />
    <line x1="120" y1="100" x2="105" y2="140" stroke="#28a745" stroke-width="2" />
    <line x1="120" y1="100" x2="135" y2="140" stroke="#28a745" stroke-width="2" />
    <line x1="180" y1="100" x2="165" y2="140" stroke="#28a745" stroke-width="2" />
    <line x1="180" y1="100" x2="195" y2="140" stroke="#28a745" stroke-width="2" />
    <line x1="240" y1="100" x2="225" y2="140" stroke="#28a745" stroke-width="2" />
    <line x1="240" y1="100" x2="255" y2="140" stroke="#28a745" stroke-width="2" />

    <!-- 노드 (Nodes) -->
    <!-- Depth 0 -->
    <circle cx="150" cy="20" r="12" fill="white" stroke="#28a745" stroke-width="2" />
    <text x="146" y="25" fill="black" font-size="14">A</text>
    
    <!-- Depth 1 -->
    <circle cx="90" cy="60" r="12" fill="white" stroke="#28a745" stroke-width="2" />
    <text x="85" y="65" fill="black" font-size="14">B</text>

    <circle cx="210" cy="60" r="12" fill="white" stroke="#28a745" stroke-width="2" />
    <text x="205" y="65" fill="black" font-size="14">C</text>
    
    <!-- Depth 2 -->
    <circle cx="60" cy="100" r="12" fill="white" stroke="#28a745" stroke-width="2" />
    <text x="56" y="105" fill="black" font-size="14">D</text>
    
    <circle cx="120" cy="100" r="12" fill="white" stroke="#28a745" stroke-width="2" />
    <text x="116" y="105" fill="black" font-size="14">E</text>
    
    <circle cx="180" cy="100" r="12" fill="white" stroke="#28a745" stroke-width="2" />
    <text x="176" y="105" fill="black" font-size="14">F</text>
    
    <circle cx="240" cy="100" r="12" fill="white" stroke="#28a745" stroke-width="2" />
    <text x="235" y="105" fill="black" font-size="14">G</text>
    
    <!-- Depth 3 -->
    <circle cx="45" cy="140" r="12" fill="white" stroke="#28a745" stroke-width="2" />
    <text x="40" y="145" fill="black" font-size="14">H</text>
    
    <circle cx="75" cy="140" r="12" fill="white" stroke="#28a745" stroke-width="2" />
    <text x="73" y="145" fill="black" font-size="14">I</text>
    
    <circle cx="105" cy="140" r="12" fill="white" stroke="#28a745" stroke-width="2" />
    <text x="101" y="145" fill="black" font-size="14">J</text>
    
    <circle cx="135" cy="140" r="12" fill="white" stroke="#28a745" stroke-width="2" />
    <text x="130" y="145" fill="black" font-size="14">K</text>
    
    <circle cx="165" cy="140" r="12" fill="white" stroke="#28a745" stroke-width="2" />
    <text x="161" y="145" fill="black" font-size="14">L</text>
    
    <circle cx="195" cy="140" r="12" fill="white" stroke="#28a745" stroke-width="2" />
    <text x="190" y="145" fill="black" font-size="14">M</text>
    
    <circle cx="225" cy="140" r="12" fill="white" stroke="#28a745" stroke-width="2" />
    <text x="220" y="145" fill="black" font-size="14">N</text>
    
    <circle cx="255" cy="140" r="12" fill="white" stroke="#28a745" stroke-width="2" />
    <text x="250" y="145" fill="black" font-size="14">O</text>
  </svg>
</div>


### 용어 설명
- 루트 노드(Root Node) 
  - 트리의 최상단에 위치한 노드로, 트리의 시작점입니다.
- 부모 노드(Parent Node)
  - 다른 노드를 가리키는 노드.
- 자식 노드(Child Node)
  - 부모 노드에 의해 가리켜지는 하위 노드.
- 형제 노드(Sibling Node)
  - 동일한 부모 노드를 가지는 노드들.
- 단말 / 리프 노드(Leaf Node)
  - 자식 노드가 없는 노드로, 트리의 끝에 위치한 노드.
- 서브트리(Subtree)
  - 특정 노드를 루트로 하는 트리 구조.
- 레벨(Level)
  - 루트 노드를 기준으로 특정 노드의 깊이.
- 트리의 높이(Height)
  - 루트 노드에서 가장 멀리 있는 리프 노드까지의 거리.
- 차수(Degree)
  - 특정 노드가 가지는 자식 노드의 개수. 트리 전체의 차수는 가장 큰 차수를 의미.

### 트리 종류
- 이진 트리 (Binary Tree)
  - 말그대로 최대 두개의 자식노드만을 가지는 트리
  - 포화이진트리, 완전 이진트리, 기타 이진트리가 있다
  - 포화 이진트리
    - 모든 노드가 0개 또는 2개의 자식 노드를 가지는 이진 트리
  - 완전 이진트리
    - 마지막 레벨을 제외한 모든 레벨에서 노드들이 꽉 차 있고, 마지막 레벨의 노드들은 왼쪽부터 차례로 채워진 트리
  - 기타 이진트리
    - 나머지 이진트리
- 이진 탐색 트리
  - 왼쪽 자식 노드의 값이 부모 노드의 값보다 작고, 오른쪽 자식 노드의 값이 부모 노드의 값보다 큰 트리.
  - 검색, 삽입, 삭제 연산을 효율적으로 수행할 수 있도록 고안된 트리.



<br>

## **글을 마무리하며**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />

이번에는 책의 5챕터 ~ 8챕터까지 다시 공부해보았습니다.
확실히 오래전에 배웠던 내용이라서 그런지 본능적으로 기억하고 있던것 확실하게 다시 익히며 복습할 수 있었던 좋은 경험이였습니다!