# Day.05 ( 스택 2 )

---

## 목차

- 계산기 1
- 계산기 2
- 백트래킹
- [참고] 부분집합, 순열
- 분할정복

---

## 1. 계산기1

- 문자열로 된 계산식이 주어질 때, 스택을 이용하여 이 계산식의 값을 계산할 수 있다.
- 문자열 수식 계산의 일반적 방법
    - step1. 중위 표기법의 수식을 후위 표기법으로 변경한다. (스택 이용)
    - step2. 후위 표기법의 수식을 스택을 이용하여 계산한다.
    
    ```python
    중위 표기법(infix notation)
    - 연산자를 피연산자의 가운데 표기하는 방법
      예) A + B
    
    후위 표기법(postfix notation)
    - 연산자를 피연산자 뒤에 표기하는 방법
      예) AB+
    ```
    

### **STEP 1**. 중위 표기식의 후위 표기식 변환 방법 1

- 수식의 각 연산자에 대해서 우선순위에 따라 괄호를 사용하여 다시 표현한다.
- 각 연산자를 그에 대응하는 오른쪽 괄호의 뒤로 이동시킨다.
- 괄호를 제거한다.

```python
예) A * B - C / D
	1단계 : ((A * B) - (C / D))
	2단계 : ((A B) * (C D)/)-
	3단계 : AB * CD / -
```

### **STEP 1.** 중위 표기법에서 후위 표기법으로의 변환 알고리즘(스택 이용)2

1. 입력 받은 중위 표기식에서 토큰을 읽는다.
2. 토큰이 피연산자이면 토큰을 출력한다.
3. 토큰이 연산자(괄호포함)일 때, 이 토큰이 스택의 top 에 저장되어있는 연산자보다 우선순위가 높으면 스택에 push 하고, 그렇지 않다면 스택 top 의 연산자의 우선순위가 토큰의 우선순위보다 작을 때까지 스택에서 pop 한 후 토큰의 연산자를 push 한다. 만약 top 에 연산자가 없으면 push 한다.
4.  토큰이 오른쪽 괄호 ‘)’ 이면 스택 top 에 왼쪽 괄호 ‘(’ 가 올 때까지 스택에 pop 연산을 수행하고 pop 한 연산자를 출력한다. 왼쪽 괄호를 만나면 pop 만 하고 출력하지는 않는다.
5. 중위 표기식에 더 읽을 것이 없다면 중지하고, 더 읽을 것이 있다면 1 부터 다시 반복한다.
6. 스택에 남아 있는 연산자를 모두 pop 하여 출력한다.
    - 스택 밖의 왼쪽 괄호는 우선 순위가 가장 높으며, 스택 안의 왼쪽 괄호는 우선 순위가 가장 낮다.

- 우선 중위 표기법에서 후위 표기법으로의 변환 한다.

- 중위 표기법으로 표현된 수식 예
    - (6 + 5 * (2 - 8) / 2)
    - 중위 표현식 문자 순회 ( 높은 우선순위 → 낮은 우선순위 까지 if 와 elif 를 활용)

```python
'''
(6+5*(2-8)/2)
'''

stack = [0] * 100
top = -1
icp = {'(':3, '*':2, '/':2, '+':1, '-':1}
isp = {'(':0, '*':2, '/':2, '+':1, '-':1}

fx = '(6+5*(2-8)/2)'
susik = ''
for x in fx:
    if x not in '(+-*/)':    # 피연산자
        susik += x
    elif x == ')':    # '(' 까지 pop()
        while stack[top] != '(':    # peek
            susik += stack[top]
            top -= 1
        top -= 1    # '(' 버림
    else:    # '(+-*/'
        if top == -1 or isp[stack[top]] < icp[x]:    # 토큰의 우선순위가 더 높으면
            top += 1    # push
            stack[top] = x
        elif isp[stack[top]] >= icp[x]:
            while top > -1 and isp[stack[top]] >= icp[x]:
                susik += stack[top]
                top -= 1
            top += 1
            stack[top] = x

print(susik)
```

- for 문을 활용한 중위식 표현식을 후위식 표현식으로 표현

```python
'''
'2+3*4/5'
'''

txt = input()  # 중위식 표현식

stack = []

for ch in txt:
    # 1. 피연산자 (숫자)
    if ch.isdigit():
        # 숫자는 그대로 출력한다
        print(ch, end=' ')

    # 2. 여는 괄호 (    3/0
    # 가장 우선 순위가 높기 때문에 스택에 바로 push
    if ch == '(':
        stack.append(ch)
    # 3. * / 연산    2
    elif ch in ['*', '/']:
        if len(stack) > 0 and stack[-1] in ['*', '/']:
            # 같은 우선 순위를 가진 연산자이기에
            # stack 에서 빼주고 출력
            oper = stack.pop()
            print(oper, end=' ')
        stack.append(ch)
    # 4. + - 연산    1
    elif ch in ['+', '-']:
        while len(stack) > 0 and stack[-1] in ['+', '-', '*', '/']:
            # 같은 우선 순위를 가진 연산자이기에
            # stack 에서 빼주고 출력
            oper = stack.pop()
            print(oper, end=' ')
        stack.append(ch)
    # 5. 닫는 괄호 )    -1
    # 여는 괄호가 나올 때까지 스택을 pop 하면서 진행한다.
    elif ch == ')':
        while len(stack) > 0 and stack[-1] != '(':
        # 같은 우선 순위를 가진 연산자이기에
        # stack 에서 빼주고 출력
            oper = stack.pop()
            print(oper, end=' ')
        stack.pop()

# 스택에 남아 있는 연산자
# 남아 있는 연산자를 pop 하며 출력
while len(stack) > 0:
    oper = stack.pop()
    print(oper, end=' ')

print()  # 후위식 표현식
```

## 2. 계산기 2

### STEP 2. 후위 표기법의 수식을 스택을 이용하여 계산

1. 피연산자를 만나면 스택에 push 한다.
2. 연산자를 만나면 필요한 만큼의 피연산자를 스택에서 pop 하여 연산하고, 연산 결과를 다시 스택에 push 한다.
3. 수식이 끝나면, 마지막으로 스택을 pop 하여 출력한다.

```python
'''
STEP1 을 통해 구한 수식
'6528-*2/+'
'''

stack = [0] * 100
top = -1
susik = '6528-*2/+'

for x in susik:
    if x not in '+-/*':  # 피연산자면
        top += 1         # push(x)
        stack[top] = int(x)
    else:
        op2 = stack[top]  # pop()
        top -= 1
        op1 = stack[top]  # pop()
        top -= 1
        if x == '+':    # op1 + op2
            top += 1
            stack[top] = op1 + op2
        elif x == '-':
            top += 1
            stack[top] = op1 - op2
        elif x == '/':
            top += 1
            stack[top] = op1 / op2
        elif x == '*':
            top += 1
            stack[top] = op1 * op2

print(stack[top])
```

## 3. 백트래킹
- 백트래킹 (Backtracking) 기법은 해를 찾는 도중에 ‘막히면’ (즉, 해가 아니면) 되돌아가서 다시 해를 찾아 가는 기법이다.
- 백트래킹 기법은 최적화 (optimization) 문제와 결정 (decision) 문제를 해결할 수 있다.
- 결정 문제 : 문제의 조건을 만족하는 해가 존재하는지의 여부를 ‘yes’ 또는 ‘no’ 가 답하는 문제
    - 미로 찾기
    - n-Queen 문제
    - Map coloring
    - 부분 집합의 합 (Subset Sum) 문제 등

### 미로 찾기

- 입구와 출구가 주어진 미로에서 입구부터 출구까지의 경로를 찾는 문제
- 이동할 수 있는 방향은 4방향으로 제한한다.
    - 스택을 이용하여 지나온 경로를 역으로 되돌아간다.
    - 스택을 이용하여 다시 경로를 찾는다.


- 모든 후보를 검사하지 않는다.

- **백트래킹 기법**
    - 어떤 노드의 유망성을 점검한 후에 유망 (promising) 하지 않다고 결정되면 그 노드의 부모로 되돌아가 (backtracking) 다음 자식 노드로 감
    - 어떤 노드를 방문하였을 때 그 노드를 포함한 경로가 해답이 될 수 없으면 그 노드는 유망하지 않다고 하며, 반대로 해답의 가능성이 있으면 유망하다고 한다.
    - 가지치기 (pruning) : 유망하지 않는 노드가 포함되는 경로는 더 이상 고려하지 않는다.

- 백트래킹을 이용한 알고리즘은 다음과 같은 절차로 진행된다.
    1. 상태 공간 트리의 깊이 우선 검색을 실시한다.
    2. 각 노드가 유망한지를 점검한다.
    3. 만일 그 노드가 유망하지 않으면, 그 노드의 부모 노드로 돌아가서 검색을 계속한다.
    
    ***가능성이 0% 가 아니라면 계속 진행**
    

### 부분집합 구하기

- 어떤 집합의 공집합과 자기자신을 포함한 모든 부분집합을 powerset 이라고 하며 구하고자 하는 어떤 집합의 원소 개수가 n 일 경우 부분집합의 개수는 2^n 개 이다.

- 백트래킹 기법으로 powerset 을 구해보자.
    - 앞에서 설명한 일반적인 백트래킹 접근 방법을 이용한다.
    - n 개의 원소가 들어있는 집합의 2^n 개의 부분집합을 만들 때는, true 또는 false 값을 가지는 항목들로 구성된 n 개의 배열을 만드는 방법을 이용
    - 여기서 배열의 i 번째 항목은 i 번째의 원소가 부분집합의 값인지 아닌지를 나타내는 값이다.
    
- powerset 을 구하는 백트래킹 알고리즘

```python
def backtrack(a, k, input):
    global MAXCANDIDATES
    c = [0] * MAXCANDIDATES

    if k == input:
       process_solution(a, k)  # 답이면 원하는 작업을 한다
    else:
        k += 1
        ncandidates = construct_candidates(a, k, input, c)
        for i in range(ncandidates):
            a[k] = c[i]
            backtrack(a, k, input)

def construct_candidates(a, k, input, c):
    c[0] = True
    c[1] = False
    return 2

MAXCANDIDATES = 2
NMAX = 4
a = [0] * NMAX
backtrack(a, 0, 3)
```

- 백트래킹을 이용하여 순열 구하기

```python
def backtrack(a, k, input):
    global MAXCANDIDATES
    c = [0] * MAXCANDIDATES

    if k == input:
        for i in range(1, k + 1):
            print(a[i], end=" ")
        print()
    else:
        k += 1
        ncandidates = construct_candidates(a, k, input, c)
        for i in range(ncandidates):
            a[k] = c[i]
            backtrack(a, k, input)

def construct_candidates(a, k, input, c):
    in_perm = [False] * NMAX

    for i in range(1, k):
        in_perm[a[i]] = True
    
    ncandidates = 0
    for i in range(1, input + 1):
        if in_perm[i] == False:
            c[ncandidates] = i
            ncandidates += 1
    return ncandidates
```

- 연습문제
    - {1, 2, 3, 4, 5, 6, 7, 8, 9, 10} 의 powerset 중 원소의 합이 10인 부분집합을 구하시오.

```python
for i1 in range(1, 4):
    for i2 in range(1, 4):
        if i2 != i1:
            for i3 in range(1, 4):
                if i3 != i1 and i3 != i2:
                    print(i1, i2, i3
```

```python
# 재귀함수로 부분집합 만들기

# bits : 해당 인덱스의 요소를 사용할지의 유무 (1 : o, 0: x)
# depth : 내가 얼마나 함수를 재귀호출했는지에 대한 카운트 값
def recur(bits, depth):
    # 기저조건
    if depth == N:
        # print(bits)
        for i in range(N):
            if bits[i] == 1:
                print(arr[i], end=' ')
        print()
        return

    for i in range(2):  # 0, 1
        bits[depth] = i
        # 자기 자신을 호출
        recur(bits, depth + 1)

N = 4
arr = [1, 2, 3, 4]
recur([0] * N, 0)
    
```

```python
# 백트래킹 (가지치기)로 부분집합 합 구하기

# bits : 해당 인덱스의 요소를 사용할지의 유무 (1 : o, 0: x)
# depth : 내가 얼마나 함수를 재귀호출했는지에 대한 카운트 값
# current : 현재까지 부분 집합 요소들의 중간합
cnt = 0

def recur(bits, depth, current):
    if current > 10:  # 가지치기
        return

    # 기저조건
    if depth == N:
        if current == 10:
            # 총 합이 10 이라면
            # 부분집합을 출력하는 코드
            for i in range(N):
                if bits[i] == 1:
                    print(arr[i], end=' ')
            print()
        return

    for i in range(2):  # 0, 1
        bits[depth] = i
        # 자기 자신을 호출
        if bits[depth] == 1:
            recur(bits, depth + 1, current + arr[i])
        else:  # 0
            recur(bits, depth + 1, current)

arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
N = len(arr)
recur([0] * N, 0, 0)
```

### 일반 백트래킹 알고리즘

```python
def checknode(v):  # node
    if promising(v):
        if there is a solution at v:
            write the solution
        else:
            for u in each child of v:
                checknode(u)
```

---

**<백트래킹과 DFS의 차이>**
```
- 어떤 노드에서 출발하는 경로가 해결책으로 이어질 것 같지 않으면
더 이상 그 경로를 따라가지 않음으로써 시도의 횟수를 줄임
(Pruning 가지치기)

- DFS 가 모든 경로를 추적하는데 비해 백트래킹은 불필요한 경로를
조기에 차단

- DFS 를 가하기에는 경우의 수가 너무나 많음. 즉, N! 가지의 경우의
수를 가진 문제에 대해 DFS 를 가하면 당연히 처리 불가능한 문제

- 백트래킹 알고리즘을 적용하면 일반적으로 경우의 수가 줄어들지만
이 역시 최악의 경우에는 여전히 지수함수 시간을 요하므로 처리 불가능
```