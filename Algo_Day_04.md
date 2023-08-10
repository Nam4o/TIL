# Day.04 ( 스택 1 )

---

## 목차

- 스택
- 재귀호출
- Memoization
- DP
- DFS

---

자기 자신을 호출하는 함수가

**재귀호출**

재귀호출을 사용해서 완전 탐색을 수행할 수 있는 깊이 우선 탐색

**DFS**

재귀호출에 수행 결과를 저장해서 다시 호출할 때의 성능을 최적화하는

**메모이즈**

메모라이즈를 통해서 계산하고 재귀적인 탐색 성능을 최적화 그리고 명료화해주는

**DP**

위의 네 가지 방법 모두 스택 (stack) 자료구조를 기반으로 한다.

---

## 1. 스택

### 스택의 특성

- 물건을 쌓아 올리듯 자료를 쌓아 올린 형태의 **자료구조** (데이터 효율 관리 구조) 이다.
- 스택에 저장된 자료는 선형 구조를 갖는다.
    - 선형구조 : 자료 간의 관계가 1대1 의 관계를 갖는다.
    - 비선형구조 : 자료 간의 관계가 1대N 의 관계를 갖는다. (예: 트리)
- 스택에 자료를 삽입하거나 스택에서 자료를 꺼낼 수 있다.
- 마지막에 삽입한 자료를 가장 먼저 꺼낸다. 후입선출( LIFO, Last-In-FIrst-Out )
    - 예를 들어 스택에 1, 2, 3 순으로 자료를 삽입한 후 꺼내면 역순으로 즉 3, 2, 1 순으로 꺼낼 수 있다.

⇒ 상자를 쌓는 것처럼, 먼저 넣은 것이 나중에 나오고 나중에 넣은 것이 먼저 나오는 구조

### 스택의 구현

- 스택을 프로그램에서 구현하기 위해서 필요한 자료구조와 연산
    - 자료구조 : 자료를 선형으로 저장할 저장소
        - 배열을 사용할 수 있다.
        - 저장소 자체를 스택이라 부르기도 한다.
        - 스택에서 마지막 삽입된 원소의 위치를 top 이라 부른다.
    - 연산
        - **삽입** : 저장소에 자료를 저장한다. 보통 **push** 라고 부른다.
        - **삭제** : 저장소에서 자료를 꺼낸다. 꺼낸 자료는 삽입한 자료의 역순으로 꺼낸다. 보통 **pop** 이라고 부른다.
        - 스택이 공백인지 아닌지를 확인하는 연산. isEmpty
        - 스택의 top 에 있는 item (원소) 을 반환하는 연산. peek
        
- 스택의 삽입 / 삭제 과정
    - 빈 스택에 원소 A, B, C 를 차례로 삽입 후 한번 삭제하는 연산과정
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/21573294-a7f9-4c0f-8420-e19679cc9eee/Untitled.png)
    

- 스택의 push 알고리즘
    - append 메소드를 통해 리스트의 마지막에 데이터를 삽입
    
    ```python
    def push(item):
        s.append(item)
    ```
    
    ```python
    def push(item, size):
        global top
    		top += 1
    		if top == size:
    		    print('overflow!')
    		else:
    				stack[top] = item
    
    size = 10
    stack = [0] * size
    top = -1
    
    push(10, size)
    top += 1        # push(20)
    stack[top] = 20
    ```
    
- 스택의 pop 알고리즘
    
    ```python
    def pop():
        if len(s) == 0:
            # underflow
    				return
        else:
    				return s.pop()
    ```
    
    ```python
    def pop():
        global top
    		if top == -1:
    		    print('underflow!')
    				return 0
    		else:
    				top -= 1              # top 의 위치를 미리 한 칸 당기고
    				retrun stack[top + 1] # 당기기 전의 top (현재 top + 1) 의 요소를 return
    
    print(pop())
    
    if top > -1:  # pop()
        top -= 1
        print(stack[top + 1])
    ```
    

- 참고

```python
# 빈 리스트
stack = []

# push : 요소를 '마지막'에 삽입
def push(item):
    stack.append(item)

# pop : '마지막'의 요소를 꺼내는 연산
# pop 을 시행했을 때 요소가 없다면 -> 에러 발생
def pop():
    if len(stack) == 0:
    # if not stack:
        return
    return stack.pop()

# 삽입(push) 3개
push(10)
push(20)
push(30)

# 삭제(pop) 3개
item = pop()
print(item)  # 30
item = pop()
print(item)  # 20
item = pop()
print(item)  # 10

# peek : 가장 마지막에 넣었던 요소의 값을 반환 함수
def peek(stack):
    if stack == []:
        return
    return stack[-1]

# isEmpty : 현재 스택이 비어있는지 여부를 반환해주는 함수
def isEmpty(stack):
    if len(stack) == 0:
        return True
    else:
        return False

# 삽입(push) 3개
push(10)
push(20)
push(30)
print(peek(stack))

print(isEmpty(stack))
```

### 스택 구현 고려 사항

- 1차원 배열을 사용하여 구현할 경우 구현이 용이하다는 장점이 있지만 스택의 크기를 변경하기가 어렵다는 단점이 있다.

- 이를 해결하기 위한 방법으로 저장소를 동적으로 할당하여 스택을 구현하는 방법이 있다. 동적 연결리스트를 이용하여 구현하는 방법을 의미한다. 구현이 복잡하다는 단점이 있지만 **메모리를 효율적으로 사용한다**는 장점을 가진다. 스택의 동적 구현은 생략한다.

### 스택의 응용 ( 괄호검사 )

- 괄호의 종류 : 대괄호 (’[’, ‘]’), 중괄호 (’{’, ‘}’), 소괄호 (’(’, ‘)’)
- 조건
    1. 왼쪽 괄호의 개수와 오른쪽 괄호의 개수가 같아야 한다.
    2. 같은 괄호에서 왼쪽 괄호는 오른쪽 괄호보다 먼저 나와야 한다.
    3. 괄호 사이에는 포함 관계만 존재한다.
- 잘못된 괄호 사용의 예
    
    → (a(b)  ,  a(b)c)  ,  a{b(c[d]e}f)
    

```python
brakets = input()

stack = []

for i in brakets:
    if i == '(':
        stack.append(i)
    elif i == ')':
        if stack == []:
            stack.append(i)
            break
        stack.pop()

if stack == []:
    print(True)
else:
    print(False)
```

### 스택의 응용 ( function call )

- Function call
    - 프로그램에서의 함수 호출과 복귀에 따른 수행 순서를 관리
        - 가장 마지막에 호출된 함수가 가장 먼저 실행을 완료하고 복귀하는 후입선출 구조이므로, 후입선출 구조의 스택을 이용하여 수행순서 관리
        - 함수 호출이 발생하면 호출한 함수 수행에 필요한 지역변수, 매개변수 및 수행 후 복귀 할 주소 등의 정보를 스택 프레임에 저장하여 시스템 스택에 삽입
        - 함수의 실행이 끝나면 시스템 스택의 top 원소 (스택 프레임) 를 삭제 (pop) 하면서 프레임에 저장되어 있던 복귀주소를 확인하고 복귀
        - 함수 호출과 복귀에 따라 이 과정을 반복하여 전체 프로그램 수행이 종료되면 시스템 스택은 공백 스택이 된다.
        
- 함수 호출과 복귀에 따른 전체 프로그램의 수행 순서

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/792c8826-ce01-4f81-a451-bccb3506e7a4/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ec331446-0618-4dce-a5ff-ae6d334439ef/Untitled.png)

---

## 2. 재귀호출

- 자기 자신을 호출하여 순환 수행되는 것
- 함수에서 실행해야 하는 작업의 특성에 따라 일반적인 호출방식보다 재귀호출방식을 사용하여 함수를 만들면 프로그램의 크기를 줄이고 간단하게 작성
    - 재귀호출의 예) factorial
    
    → n에 대한 factorial : 1 부터 n 까지의 모든 자연수를 곱하여 구하는 연산
    
    ```python
    n! = n x (n - 1)!
    	(n - 1)! = (n - 1) x (n - 2)!
    	(n - 2)! = (n - 2) x (n - 3)!
    ...
    	2! = 2 x 1!
    	1! = 1
    ```
    
    → 마지막에 구한 하위 값을 이용하여 상위 값을 구하는 작업을 반복
    
- factorial 함수에서 n = 4 인 경우의 실행

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b4bce056-6a38-4066-9984-add796fd6b9c/Untitled.png)

- 0 과 1 로 시작하고 이전의 두 수 합을 다음 항으로 하는 수열을 피보나치라 한다.
    
    → 0, 1, 1, 2, 3, 5, 8, 13, …
    
- 피보나치 수열의 i 번째 값을 계산하는 함수 F 를 정의하면 다음과 같다.
    
    → F0 = 0, F1 = 1
    
    → Fi = F(i-1) + F(i-2) for i ≥ 2
    
- 위의 정으로부터 피보나치 수열의 i 번째 항을 반환하는 함수를 재귀함수로 구현할 수 있다.

```python
def fibo(n):
		if n < 2:
				return n
		else:
				return fibo(n - 1) + fibo(n - 2)
```

⇒ **엄청난 중복 호출이 존재함 ( 문제점 )**

---

## 3. Memoization

- 메모이제이션 (memoization)은 컴퓨터 프로그램을 실행할 때 이전에 계산한 값을 메모리에 저장해서 매번 다시 계산하지 않도록 하여 전체적인 실행속도를 빠르게 하는 기술이다. 동적 계획법의 핵심이 되는 기술
- 참고
    
    ‘memoization’은 글자 그대로 해석하면 ‘메모리에 넣기’라는 의미이며 ‘기억되어야 할 것’이라는 뜻의 라틴어에서 파생되었다. 흔히 ‘기억하기’, ‘암기하기’라는 뜻의 memorization과 혼동하지만, 정확한 단어는 memoization이다.
    
- 앞의 예에서 피보나치 수를 구하는 알고리즘에서 fibo(n)의 값을 계산하자마자 저장하면(memoize), 실행시간을 Θ(n)으로 줄일 수 있다.
- Memoization 방법을 적용한 알고리즘은 다음과 같다.

```python
# memo를 위한 배열을 할당하고, 모두 0 으로 초기화 한다.
# memo[0]을 0 으로 memo[1]은 1로 초기화한다.

def fibo1(n):
		global memo
		if n >= 2 and memo[n] == 0:
				memo[n] = (fibo(n - 1) + fibo1(n - 2))
		return memo[n]

memo = [0] * (n + 1)
memo[0] = 0
memo[1] = 1
```

```python
memo = [0] * 1001

def fibo1(n):
		global memo
		# 기저 조건
		if n > 2:
				return n
		if memo[n] != 0:
				return memo[n]

		memo[n] = fibo1(n - 1) + fibo1(n - 2)
		return memo[n]
```

---

## 4. DP

: 그리디 알고리즘과 같이 **최적화 문제**를 해결하는 알고리즘.

- 동적 계획 알고리즘은 먼저 입력 크기가 작은 부분 문제들을 모두 해결한 후에 그 해들을 이용하여 보다 큰 크기의 부분 문제들을 해결하여, 최종적으로 원래 주어진 입력의 문제를 해결하는 알고리즘이다.
- 피보나치 수 DP 적용
    - 피보나치 수는 부분 문제의 답으로부터 본 문제의 답을 얻을 수 있으므로 최적 부분 구조로 이루어져 있다.
    
    ```python
    def fibo(2):
    		f = [0] * (n + i)
    		f[0] = 0
    		f[1] = 1
    		for i in range(2, n + 1):
    				f[i] = f[i - 1] + f[i - 2]
    
    		return f[n]
    ```
    
- DP의 구현 방식
    - recursive 방식 : fib1()
    - iterative 방식 : fib2()
    - memoization을 재귀적 구조에 사용하는 것보다 반복적 구조로 DP를 구현한 것이 성능 면에서 보다 효율적이다.
    - 재귀적 구조는 내부 시스템 호출 스택을 사용하는 오버헤드가 발생하기 때문
    
    ---
    

## 순열과 조합

- 순열

```python
arr = [1, 2, 3, 4, 6, 7, 8]

# 재귀호출
# 순열, 4개의 값을 뽑아내는 경우를 모두 출력
result = []

checked = [False for _ in range(len(arr))]

cnt = 0

def generate_Permutations(arr, depth):
    global cnt
    # 기저 조건
    if depth == 4:
        cnt += 1
        # result 의 값을 출력
        print(result)
        return

    # arr 를 순회하면서 하나의 값을 뽑아낸다.
    for idx in range(len(arr)):
        # 해당 번호를 뽑게 되면, 다음에 뽑지 못하도록 체크를 해줘야함
        if checked[idx]:
            continue
        # 사용 표시
        checked[idx] = True
        result.append(arr[idx])
        generate_Permutations(arr, depth + 1)  # 재귀호출
        # 복구
        checked[idx] = False
        result.pop()

generate_Permutations(arr,0 )
print(cnt)
# 조합, 4개의 값을 뽑아내는 경우를 모두 출력
```

- 조합

```python
arr = [1, 2, 3, 4, 6, 7, 8]

# 재귀호출
# 조합, 4개의 값을 뽑아내는 경우를 모두 출력
result = []

checked = [False for _ in range(len(arr))]

cnt = 0

def generate_Combination(arr, depth, current):
    global cnt
    # 기저 조건
    if depth == 4:
        cnt += 1
        # result 의 값을 출력
        print(result)
        return

    # arr 를 순회하면서 하나의 값을 뽑아낸다.
    for idx in range(current, len(arr)):
        # 해당 번호를 뽑게 되면, 다음에 뽑지 못하도록 체크를 해줘야함
        if checked[idx]:
            continue
        # 사용 표시
        checked[idx] = True
        result.append(arr[idx])
        generate_Combination(arr, depth + 1, idx + 1)
        # 복구
        checked[idx] = False
        result.pop()

generate_Combination(arr, 0, 0)
print(cnt)
```

---

## 5. DFS (깊이우선탐색)

- 비선형구조인 그래프 구조는 그래프로 표현된 모든 자료를 빠짐없이 검색하는 것이 중요함

- 두 가지 방법
    - 깊이 우선 탐색 (Depth First Search, DFS)
    - 너비 우선 탐색 (Breadth First Search, BFS)

- 시작 정점의 한 방향으로 갈 수 있는 경로가 있는 곳까지 깊이 탐색해 가다가 더 이상 갈 곳이 없게 되면, 가장 마지막에 만났던 갈림길 간선이 있는 정점으로 되돌아와서 다른 방향의 정점으로 탐색을 계속 반복하여 결국 **모든 정점을 방문 (완전탐색)** 하는 순회방법

- 가장 마지막에 만났던 갈림길의 정점으로 되돌아가서 다시 깊이 우선 탐색을 반복해야 하므로 후입선출 구조의 스택 사용

```python
1. 시작 정점 v 를 결정하여 방문한다.

2. 정점 v 에 인접한 정점 중에서
	2-1. 방문하지 않은 정점 w 가 있으면, 정점 v 를 스택에 push 하고
			정점 w 를 방문한다.
  2-2. 방문하지 않은 정점이 없으면, 탐색의 방향을 바꾸기 위해서
			스택을 pop 하여 받은 가장 마지막 방문 정점을 v 로 하여 다시
			2. 를 반복한다.

3. 스택이 공백이 될 때까지 2. 를 반복한다.
```

```python
visited[], stack[] 초기화

DFS(v)
		시작점 v 방문;
		visited[v] <- true;
		while {
			if ( v의 인접 정점 중 방문 안 한 정점 w 가 있으면)
					 push(v);
					 visited[w] <- true;
			else
					 if (스택이 비어 있지 않으면)
							 v <- pop(stack);
						else
								break
		}
end DFS()
```

- 연결 관계
    - 인접 행렬
        - 연결 된 지점 1 , 연결 되지 않은 지점 0
    - 인접 리스트
        - 1 : [1번 정점과 연결 된 지점]
        - 2 : [2번 정점과 연결 된 지점]
        - . . .
        - N : [N번 정점과 연결 된 지점]
        

- **재귀 호출을 이용한 방법**

```python
N = 7

# 방문 체크
visited = [False for _ in range(N)]
graphs = [
    [1, 2],
    [0, 3, 4],
    [0, 4],
    [1, 5],
    [1, 2, 5],
    [3, 4, 6],
    [5]
]

# 0 번 노드에서 갈 수 있는 지점은?
graphs[0]  # [1, 2] 1 번과 2 번 노드로 갈 수 있다

def dfs(v):
    global visited
    visited[v] = True
    print(v, end='-')
    # v 노드에서 갈 수 있는 노드를 확인 (인접한 노드)
    for u in graphs[v]:
        # 방문을 했다면
        if visited[u] == True:
            continue
        # 방문을 하지 않았다면 방문을 진행
        dfs(u)

dfs(0)  # 0-1-3-5-4-2-6-
```

- **스택을 이용한 방법**

```python
def dfs(n, V, adj_m):
    stack = []              # stack 생성
    visited = [0] * (V+1)   # visited 생성
    visited[n] = 1          # 시작점 방문 표시
    print(n)                # do[n]
    while True:
        for w in range(1, V+1):  # 현재 정점 n에 인접하고 미방문 w 찾기
            if adj_m[n][w] == 1 and visited[w]==0:
                stack.append(n) # push(n), v = w
                n = w
                print(n)        # do(w)
                visited[n] = 1  # w 방문 표시
                break   # for w , n에 인접인 w c찾은경우
        else:
            if stack:# 스택에 지나온 정점이 남아있으면
                n = stack.pop() # pop()해서 다시 다른 w를 찾을 n 준비
            else:       # 스택이 비어있으면
                break       # while True 탐색 끝
    return

V, E = map(int, input().split()) # 1번부터 V번 정점, E개의 간선
arr = list(map(int, input().split()))
adj_m = [[0]*(V+1) for _ in range(V+1)]
for i in range(E):
    v1, v2 = arr[i*2], arr[i*2+1]
    adj_m[v1][v2] = 1
    adj_m[v2][v1] = 1

dfs(1, V, adj_m)
```

---

## 선생님 말씀

일단 DFS, BFS 알고리즘들은 **완전탐색**을 하기위한 탐색 방법 중에 하나라고 소개를 드렸어요.

자. 완탐을 하는 이유가 결과적으로 문제를 확실하게 최적의 해답을 내기 위해 모든 가능한 경우를 다 확인해보는 방법이라고 말씀드렸어요.

그래서 모든 해답을 탐색하는 방법, 완전탐색을 진행할 때에 이 탐색의 방법을 순회할 때에 가장 효율적으로 순회하는 방법. 탐색하는 방법이 무엇이냐! 하는 부분이 가장 큰 문제가 되겠죠.

그래서 그 중에서 DFS, BFS 라는 알고리즘을 통해서 효율적으로 완전 탐색을 진행하게 되는건데요. 
어떻게 해서 효율적으로 진행하는거냐면. 두가지의 알고리즘이 동작하는 방식에 대해서 어떤 문제를 풀게 될 것이냐에 따라 나뉘게 됩니다.

DFS 알고리즘의 경우에 미로 찾기 같은 문제가 주어진다. 라는 경우에 하나의 경로를 최대한 깊이 탐색을 하면서 끝까지 탐색을 하게 되므로, 적어도 갈 수 있는 경로 하나가 있는지 없는지를 확인할 때에 탐색을 효율적으로 할 수 있습니다.

그리고 한 경우를 최대한 깊이 탐색하기 때문에 특정 깊이 이하의 해답을 반드시 하나 찾아야한다! 라는 상황에 상당히 유용히 사용할 수가 있어요.

그에 반해서 BFS 알고리즘은 우리가 탐색할 수 있는 정점을 하나의 깊이씩, 이걸 레벨이라고 표현하는데, 한 레벨씩 순회하기 때문에 이런 레벨과 관련된 완전 탐색을 할 때에 유용하게 사용할 수 있습니다.

대표적으로 최단 경로를 찾는 문제가 주어질 때인데요. 몇 초 만에 이 미로를 최대한 빨리 탈출할 수 있느냐! 라는 문제가 주어지면 BFS 알고리즘을 쓸 수 있습니다.


모든 경로를 다 탐색하되, 이렇게 탐색 순서만 바뀐다고 보시면 되겠습니다.

정리하자면 두개 다 모든 경로를 탐색하기 위한 완전탐색기법이다.
DFS는 깊이를 우선적으로 탐색을 진행하기 때문에 하나의 해답을 빠르게 찾을 때 유용하다.
BFS는 너비 우선 탐색이기 때문에 최단 경로 결과를 찾을 때 유용하다