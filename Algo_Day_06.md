# Day.06 ( Queue )

---

## 목차

- 선형큐
- 원형큐
- 우선순위 큐
- 큐의 활용 : 버퍼
- BFS
- BFS 예제

---

## 1. 선형큐

- 큐의 특성
    - **선형자료구조**
    - 스택과 마찬가지로 삽입과 삭제의 위치가 제한적인 자료구조
        
        → 큐의 뒤에서는 삽입만 하고, 큐의 앞에서는 삭제만 이루어지는 구조
        
    - **선입선출 구조** (FIFO : Frist In First Out)
        
        → 큐에 삽입한 순서대로 원소가 저장되어, 가장 먼저 삽입된 원소는 가장 먼저 삭제된다.
        

- 큐의 선입선출 구조

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4282b97a-b52e-4713-aa29-84560575c68c/Untitled.png)

- 큐의 기본 연산
    - 삽입 : enQueue
    - 삭제 : deQueue

- 큐의 주요 연산
    
    : 큐의 사용을 위해 필요한 주요 연산은 다음과 같음
    
    | 연산 | 기능 |
    | --- | --- |
    | enQueue(item) | 큐의 뒤쪽(rear 다음)에 원소를 삽입하는 연산 |
    | deQueue() | 큐의 앞쪽(front) 에서 원소를 삭제하고 반환하는 연산 |
    | createQueue() | 공백 상태의 큐를 생성하는 연산 |
    | isEmpty() | 큐가 공백상태인지를 확인하는 연산 |
    | isFull() | 큐가 포화상태인지를 확인하는 연산 |
    | Qpeek() | 큐의 앞쪽(front) 에서 원소를 삭제 없이 반환하는 연산 |
- 큐의 연산 과정
    1. 공백 큐 생성 creatQueue()
    2. 원소 A 삽입 enQueue(A)
    3. 원소 B 삽입 enQueue(B)
    4. 원소 반환/삭제 deQueue()
    5. 원소 C 삽입 enQueue(C)
    6. 원소 반환/삭제 deQueue()
    7. 원소 반환 삭제 deQueue()
        
        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2043ebe6-0226-4ee4-bb52-08d044ae43ff/Untitled.png)
        
    
    ### 선형큐
    
    - 1차원 배열을 이용한 큐
        - 큐의 크기 = 배열의 크기
        - front : 저장된 첫 번째 원소의 인덱스
        - rear : 저장된 마지막 원소의 인덱스
    
    ```python
    # 선형큐
    # 정적인 크기의 배열
    QSIZE = 100
    queue = [0] * 100
    
    # 머리, 꼬리 해당되는 인덱스 초기화
    front = rear = -1
    
    # 큐 삽입 연산 enQueue
    # rear ( 꼬리 ) 를 1 증가, 해당 위치에 요소를 삽입
    def enQueue(item):
        global  rear
    
        rear = rear + 1
        return queue[rear] = item
    # 큐 삭제 연산 deQueue
    # front ( 머리 ) 를 1 증가, 해당 위치에 요소를 삭제
    def deQueue():
        global front
    
        front = front + 1
        return queue[front]
    
    # 부가 연산을 만들어줘야 한다
    # 큐가 차있는지
    def isFull():
        return rear == QSIZE - 1
    
    # 큐가 비어있는지
    def isEmpty():
        return front == rear
    # 큐에 뽑을 원소의 값은 무엇인지
    def qPeek():
        return queue[front + 1]
    ```
    
    - 상태 표현
        - 초기 상태 : front = rear = -1
        - 공백 상태 : front == rear
        - 포화 상태 : rear == n - 1 (n : 배열의 크기, n - 1 : 배열의 마지막 인덱스)
    
    - 초기 공백 큐 생성
        - 크기 n 인 1차원 배열 생성
        - front 와 rear 를 -1 로 초기화
        
    
    ```python
    # 큐... 선입선출(FIFO)
    queue = []
    
    # 큐 요소를 추가하는 연산
    def enQueue(item):
        queue.append(item)
    
    # 큐 요소를 삭제하는 연산
    def deQueue():
        return queue.pop(0)
    
    enQueue(1)
    enQueue(2)
    enQueue(3)
    
    item = deQueue()
    print(item)
    item = deQueue()
    print(item)
    item = deQueue()
    print(item)
    ```
    
    ```python
    # deque(데크, Double End Queue)
    from collections import deque
    
    dq = deque()
    # 인큐 (삽입) 1,2,3
    dq.append(1)
    dq.append(2)
    dq.append(3)
    
    # 디큐 (삭제) 1,2,3
    item = dq.popleft()
    print(item)
    item = dq.popleft()
    print(item)
    item = dq.popleft()
    print(item)
    print()
    
    # 스택 : 후입선출 (LIFO)
    stack = deque()
    
    # 스택에 요소를 삽입 (push)
    stack.append(1)
    stack.append(2)
    stack.append(3)
    
    # 요소를 삭제 (pop)
    item = stack.pop()
    print(item)
    item = stack.pop()
    print(item)
    item = stack.pop()
    print(item)
    ```
    
    ### 1️⃣ 삽입  : enQueue(item)
    
    - 마지막 원소 뒤에 새로운 원소를 삽입하기 위해
        1. rear 값을 하나 증가시켜 새로운 원소를 삽입할 자리를 마련
        2. 그 인덱스에 해당하는 배열원소 Q[rear]에 item을 저장
        
        ```python
        def enQueue(item):
            global rear
            
            rear += 1
            Q[rear] = item
        
        Qsize = 3
        Q = [0] * Qsize
        rear = -1
        front = -1
        ```
        
    
    ### 2️⃣ 삭제 : deQueue()
    
    - 가장 앞에 있는 원소를 삭제하기 위해
        1. front 값을 하나 증가시켜 큐에 남아있게 될 첫 번째 원소 이동
        2. 새로운 첫 번째 원소를 리턴 함으로써 삭제와 동일한 기능함
        
        ```python
        def deQueue():
            global front
            front += 1
            return Q[front]
        
        Qsize = 3
        Q = [0] * Qsize
        rear = -1
        front = -1
        ```
        
    
    ### 3️⃣ 공백상태 및 포화상태 검사 : isEmpty(), isFull()
    
    - 공백상태 : front == rear
    - 포화상태 : rear == n - 1 (n : 배열의 크기, n - 1 : 배열의 마지막 인덱스)
    
    ```python
    def isEmpty():
        return front == rear
    
    def Full():
        return rear == len(Q) - 1
    ```
    
    ### 4️⃣ 검색 : Qpeek()
    
    - 가장 앞에 있는 원소를 검색하여 반환하는 연산
    - 현재 front 의 한자리 뒤 (front + 1) 에 있는 원소, 즉 큐의 첫 번째에 있는 원소를 반환
    
    ```python
    def Qpeek():
        if isEmpty():
            print('Queue_Empty')
        else:
            return Q[front + 1]
    ```
    
    ### 선형 큐 이용시의 문제점
    
    - 잘못된 포화상태 인식
        - 선형 큐를 이용하여 원소의 삽입과 삭제를 계속할 경우, 배열의 앞부분에 활용할 수 있는 공간이 있음에도 불구하고, rear = n - 1 인 상태 즉, 포화상태로 인식하여 더 이상의 삽입을 수행하지 않게 됨
    - 해결방법1
        - 매 연산이 이루어질 때마다 저장된 원소들을 배열의 앞부분으로 모두 이동시킴
        - 원소 이동에 많은 시간이 소요되어 큐의 효율성이 급격히 떨어짐
    - 해결방법2
        - 1차원 배열을 사용하되, 논리적으로는 배열의 처음과 끝이 연결되어 원형 형태의 큐를 이룬다고 가정하고 사용
        - 원형 큐의 논리적 구조

---

## 2. 원형큐

- 초기 공백 상태
    
    → front = rear = 0
    
- Index 의 순환
    - front 와 rear 의 위치가 배열의 마지막 인덱스인 n - 1 을 가리킨 후, 그 다음에는 논리적 순환을 이루어 처음 인덱스인 0 으로 이동해야 함
    - 이를 위해 나머지 연산자 mod 를 사용함
- front 변수
    - 공백 상태와 포화 상태 구분을 쉽게 하기 위해 front 가 있는 자리는 사용하지 않고 항상 빈자리로 둠
- 삽입 위치 및 삭제 위치

|  | 삽입 위치 | 삭제 위치 |
| --- | --- | --- |
| 선형큐 | rear = rear + 1 | front = front + 1 |
| 원형큐 | rear = (rear + 1) mod n | front = (front + 1) mod n |

### 원형 큐의 구현

```python
# 원형큐
# 정적인 크기의 배열
QSIZE = 100
queue = [0] * 100

# 머리, 꼬리 해당되는 인덱스 초기화
front = rear = 0

# 큐 삽입 연산 enQueue
# rear ( 꼬리 ) 를 1 증가, 해당 위치에 요소를 삽입
def enQueue(item):
    global  rear

    rear = (rear + 1) % QSIZE
    queue[rear] = item

# 큐 삭제 연산 deQueue
# front ( 머리 ) 를 1 증가, 해당 위치에 요소를 삭제
def deQueue():
    global front

    front = (front + 1) % QSIZE
    return queue[front]

# 부가 연산을 만들어줘야 한다
# 큐가 차있는지
def isFull():
    return front == (rear + 1) % QSIZE

# 큐가 비어있는지
def isEmpty():
    return front == rear
# 큐에 뽑을 원소의 값은 무엇인지
def Qpeek():
    return queue[(front + 1) % QSIZE]
```

- 초기 공백 큐 생성
    - 크기 n 인 1차원 배열 생성
    - front 와 rear 를 0으로 초기화

- 공백상태 및 포화상태 검사 : isEmpty(), isFull()
    - 공백상태 : front == rear
    - 포화상태 : 삽입할 rear 의 다음 위치 == 현재 front
        - - (rear + 1) mod n == front
    
    ```python
    def isEmpty():
        return front == rear
    
    def isFull():
        return (rear + 1) % len(cQ) == front
    ```
    
- 삽입, 삭제
    
    ```python
    def enq(data):
        global rear
        if (rear + 1)%cQsize == front:
            print('cQ is Full')
        else:
            rear = (rear + 1)%cQsize
            cQ[rear] = data
    
    def deq():
        global front
        front = (front + 1)%cQsize
    ```
    


## <연결 큐의 구조>

- 단순 연결 리스트 (Linked List) 를 이용한 큐
    - 큐의 원소 : 단순 연결 리스트의 노드
    - 큐의 원소 순서 : 노드의 연결 순서, 링크로 연결되어 있음
    - front : 첫 번째 노드를 가리키는 링크
    - rear : 마지막 노드를 가리키는 링크

- 상태 표현
    - 초기 상태 : front = rear = null
    - 공백 상태 : front = rear = null

### 연결 큐의 연산 과정

1. 공백 큐 생성 createLinkedQueue()
2. 원소 A 삽입 enQueue(A)
3. 원소 B 삽입 enQueue(B)
4. 원소 삭제 deQueue()
5. 원소 C 삽입 enQueue(C)
6. 원소 삭제 deQueue()


## 3. 우선순위 큐

- 우선순위 큐의 특성
    - 우선순위를 가진 항목들을 저장하는 큐
    - FIFO 순서가 아니라 **우선순위가 높은 순서대로 먼저 나가게 된다.**

- 우서순위 큐의 적용 분야
    - 시뮬레이션 시스템
    - 네트워크 트래픽 제어
    - 운영체제의 테스크 스케줄링

### 우선순위 큐의 구현

- 배열을 이용한 우선순위 큐

- 리스트를 이용한 우선순위 큐

- 우선순위 큐의 기본 연산
    - 삽입 : enQueue
    - 삭제 : deQueue

- 열을 이용하여 우선순위 큐 구현
    - 배열을 이용하여 자료 성장
    - 원소를 삽입하는 과정에서 우선순위를 비교하여 적절한 위치에 삽입하는 구조
    - 가장 앞에 최고 우선순위 원소가 위치하게 됨

- 문제점
    - 배열을 사용하므로, 삽입이나 삭제 연산이 일어날 때 원소의 재배치가 발생함
    - 이에 소용되는 시간이나 메모리 낭비가 큼
    

## 4. 큐의 활용 : 버퍼

### 버퍼

- 데이터를 한 곳에서 다른 한 곳으로 전송하는 동안 일시적으로 그 데이터를 보관하는 메모리의 영역
- 버퍼링 : 버퍼를 활용하는 방식 또는 버퍼를 채우는 동작을 의미

### 버퍼의 자료 구조

- 버퍼는 일반적으로 입출력 및 네트워크와 관련된 기능에서 이용된다.
- 순서대로 입력 / 출력 / 전달되어야 하므로 FIFO 방식의 자료구조인 큐가 활용된다.

## 5. BFS

### 그래프를 탐색하는 두 가지 방법

- 깊이 우선 탐색 (DFS)
- 너비 우선 탐색 (BFS)

### 너비 우선 탐색

- 탐색 시작점의 인접한 정점들을 먼저 모두 차례로 방문한 후에, 방문했던 정점을 시작점으로 하여 다시 인접한 정점들을 차례로 방문하는 방식
- 인접한 정점들에 대해 탐색을 한 후, 차례로 다시 너비 우선 탐색을 진행해야 하므로, **선입선출 형태의 자료구조인 큐를 활용함**

### BFS 알고리즘

- 입력 파라미터 : 그래프 G 와 탐색 시작점 v

```python
def BFS(G, v):  # 그래프 G, 탐색 시작점 v
    visited = [0] * (n + 1)  # n : 정점의 개수
    queue = []               # 큐 생성
    queue.append(v)          # 시작점 v 를 큐에 삽입
    while queue:             # 큐가 비어있지 않은 경우
         t = queue.pop(0)      # 큐의 첫번째 원소 반환
         if not visited[t]:    # 방문되지 않은 곳이라면
             visited[t] = true # 방문한 것으로 표시
             print(t)        # 정점 t 에서 할 일
             for i in G[t]:    # t 와 연결된 모든 정점에 대해
                 if not visited[i]   # 방문되지 않은 곳이라면
                     queue.append(i) # 큐에 넣기 
```
