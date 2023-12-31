# Day. 10 ( 완전검색 & 그리디 )

---

## 목차

- 반복 (Iteration) 과 재귀 (Recursion)
- 완전검색기법
- 순열
- 부분 집합
- 조합
- 탐욕 알고리즘
- 활동 선택 문제
- Baby-jin

---

## 1. 반복과 재귀

- 반복과 재귀는 유사한 작업을 수행할 수 있다.

- 반복은 수행하는 작업이 완료될 때까지 계속 반복
    - 루프 (for, while 구조)
    
- 재귀는 주어진 문제의 해를 구하기 위해 동일하면서 더 작은 문제의 해를 이용하는 방법
    - 하나의 큰 문제를 해결할 수 있는 (해결하기 쉬운) 더 작은 문제로 쪼개고 결과들을 결합한다.
    - 재귀 함수로 구현

### 반복 구조

- 초기화
    - 반복되는 명령문을 실행하기 전에 (한번만) 조건 검사에 사용할 변수의 초기값 설정
    - 조건검사 (check control expression)
    - 반복할 명령문 실행 (action)
    - 업데이트 (loop update)
        - 무한 루프 (infinite update) 가 되지 않게 조건이 거짓 (false) 이 되게 한다.

- 반복을 이용한 선택정렬

```python
def SelectionSort(A):
    
    n = len(A)
    
    for i in range(0, n - 1):
        minI = i
        for j in range(i + 1, n):
            if A[j] < A[minI]:
                minI = j
        A[minI], A[i] = A[i], A[minI]
```

### 재귀적 알고리즘

- 재귀적 정의는 두 부분으로 나뉜다.

- 하나 또는 그 이상의 기본 경우 (basis case  or rule)
    - 집합에 포함되어 있는 원소로 induction 을 생성하기 위한 시드 (seed) 역할
    
- 하나 또는 그 이상의 유도된 경우 (inductive case or rule)
    - 새로운 집합의 원소를 생성하기 위해 결합되어지는 방법

### 재귀 함수 (recursive function)

- 함수 내부에서 직접 혹은 간접적으로 자기 자신을 호출하는 함수

- 일반적으로 재귀적 정의를 이용해서 재귀 함수를 구현한다.

- 따라서,  기본 부분 (basis part) 와 유도 부분 (inductive part) 로 구성된다.

- 재귀적 프로그램을 작성하는 것은 반복 구조에 비해 간결하고 이해하기 쉽다.
    - 그러나, 재귀에 대해 익숙하지 않은 개발자들은 재귀적 프로그램이 어렵다고 느낀다.

- 함수 호출은 프로그램 메모리 구조에서 스택을 사용한다. 따라서 재귀 호출은 반복적인 스택의 사용을 의미하며 메모리 및 속도에서 성능 저하가 발생한다.

### 팩토리얼 재귀 함수

- 재귀적 정의

```python
Basis rule:
						N <= 1 경우, n = 1
Inductive rule:
						N > 1, n! = n * (n - 1)!
```

- n! 에 대한 재귀함수

```python
def fact(n):
    if n<= 1:
        return 1  # basis part
    else:
        return n * fact(n - 1)  # Inductive part
```

### 반복 or 재귀?

- 해결할 문제를 고려해서 반복이나 재귀의 방법을 선택

- 재귀는 문제 해결을 위한 알고리즘 설계가 간단하고 자연스럽다.
    - 추상 자료형 (List, tree 등) 의 알고리즘은 재귀적 구현이 간단하고 자연스러운 경우가 많다.

- 일반적으로, 재귀적 알고리즘은 반복 (Iterative) 알고리즘보다 더 많은 메모리와 연산을 필요로 한다.

- **입력 값 n 이 커질수록 재귀 알고리즘은 반복에 비해 비효율적일 수 있다.**

|  | 재귀 | 반복 |
| --- | --- | --- |
| 종료 | 재귀 함수 호출이 종료되는 베이스 케이스(base) | 반복문의 종료 조건 |
| 수행 시간 | (상대적) 느림 | 빠름 |
| 메모리 공간 | (상대적) 많이 사용 | 적게 사용 |
| 소스 코드 길이 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 짧고 간결 | 길다 |
| 소스 코드 형태 | 선택 구조 (If…else) | 반복 구조 (for , while) |
| 무한 반복시 | 스택 오버플로우 | CPU를 반복해서 점유 |

---

## 2. 완전 검색 기법

- Baby-gin game

- 브루트포스
    - 문제를 해결하기 위한 간단하고 쉬운 접근법
    - 대부분의 문제에 적용이 가능
    - 상대적으로 빠른 시간에 문제 해결을 할 수 있다.
    - 문제에 포함된 자료 (요소, 인스턴스) 의 크기가 작다면 유용하다.
    - 학술적 또는 교육적 목적을 위해 알고리즘의 효율성을 판단하기 위한 척도로 사용된다.

### 완전 검색으로 시작하라

- 모든 경우의 수를 생성하고 테스트하기 때문에 수행 속도는 느리지만, 해답을 찾아내지 못할 확률이 작다.
    - 완전검색은 입력의 크기를 작게 해서 간편하고 빠르게 답을 구하는 프로그램을 작성한다.

- 이를 기반으로 그리디 기법이나 동적 계획법을 이용해서 효율적인 알고리즘을 찾을 수 있다.

- 검정 등에서 주어진 문제를 풀 때, **우선 완전 검색으로 접근하여 해답을 도출한 후, 성능 개선을 위해 다른 알고리즘을 사용하고 해답을 확인하는 것이 바람직**하다.

## 3. 순열

- 서로 다른 것들 중 몇 개를 뽑아서 한 줄로 나열하는 것

- 서로 다른 n 개 중 r 개를 택하는 순열은 아래와 같이 표현한다.
    
    ⇒ nPr
    

- 그리고 nPr 은 다음과 같은 식이 성립한다.
    
    nPr = n * (n - 1 ) * (n -2 )* … * (n - r + 1)
    
- nPn = n! 이라고 표기하며 Factorial 이라 부른다.
    
    n! = n * (n - 1) * (n - 2) * … * 2 * 1
    

- 다수의 알고리즘 문제들은 순서화 된 요소들의 집합에서 최선의 방법을 찾는 것과 관련있다. ( 예, TSP )

- N 개의 요소들에 대해서 n! 개의 순열들이 존재한다.
    - 12! = 479,001,600
    - n > 12인 경우, 시간복잡도 폭발적으로 ↑

### 단순하게 순열을 생성하는 방법

- 예) {1, 2, 3} 을 포함하는 모든 순열을 생성하는 함수
    - 동일한 숫자가 포함되지 않았을 때, 각 자리수 별로 loop을 이용해 아래와 같이 구현할수 있다.

```python
def recur(depth):
    '''
    :param depth: 재귀 호출을 몇 번 진행했는지 (카운트값)
    :return: 없음
    '''
    # 기저조건
    if depth == len(s):
        for i in nums:
            print(i, end=' ')
        print()
        return
    #유도조건 (재귀호출)
    # i : 1 -> 3
    for i in range(1, 4):

        nums.append(i)  # 결정
        recur(depth + 1)
        nums.pop()  # 복구

s = [1, 2, 3]
nums = []  # 상태 저장 리스트 [i[1], i[2], i[3]]

recur(0)
```

## 4. 부분 집합

- 집합에 포함된 원소들을 선택하는 것

- 다수의 중요 알고리즘들이 원소들의 그룹에서 최적의 부분 집합을 찾는 것 ex) 배낭 짐싸기 (knapsack)

- N 개의 원소를 포함한 집합
    - 자기 자신과 공집합을 포함한 모든 부분집합 (power set) 의 개수는 2^n 개
    - 원소의 수가 증가하면 부분집합의 개수는 지수적으로 증가

---

## 5. 조합

- 서로 다른 n 개의 원소 중 r 개를 순서 없이 골라낸 것을 조합 (combination) 이라고 부른다.

- 조합의 수식

- 재귀 호출을 이용한 조합 생성 알고리즘

```python
an = []  # n 개의 원소를 가지고 있는 배열
tr = []  # r 개의 크기의 배열, 조합이 임시 저장될 배열

def comb(n, r):
    if r == 0:
        print(arr)
    elif n < r:
        return
    else:
        tr[r - 1] = an[n - 1]
        comb(n - 1, r - 1)  # 5C3 -> 4C2
        comb(n - 1, r)  # 5C3 -> 4C3

# 작동
an = [0, 1, 2, 3, 4]  # n 개의 원소를 가지고 있는 배열
r = len(an)
n = 3  # 수들을 담을 배열의 임의 길이
tr = [0] * r  # r 개의 크기의 배열, 조합이 임시 저장될 배열

def comb(n, r):
    if r == 0:
        print(tr)
    elif n < r:
        return
    else:
        tr[r - 1] = an[n - 1]
        comb(n - 1, r - 1)  # 5C3 -> 4C2
        comb(n - 1, r)  # 5C3 -> 4C3

comb(5, 3)
```

---

## 탐욕 알고리즘
- 탐욕 알고리즘은 최적해를 구하는 데 사용되는 근시안적인 방법

- 일반적으로, 머리 속에 떠오르는 생각을 검증 없이 바로 구현하면 Greedy 접근이 된다.

- 여러 경우 중 하나를 선택 할 때마다 그 순간에 최적이라고 생각되는 것을 선택해 나가는 방식으로 진행하여 최종적인 해답에 도달한다.

- 각 선택 시점에서 이루어지는 결정은 지역적으로는 최적이지만, 그 선택들을 계속 수집하여 최종적인 해답을 만들었다고 하여, **그것이 최적이라는 보장은 없다.**

- 일단, 한번 선택된 것은 번복하지 않는다. 이런 특성 때문에 대부분의 탐욕 알고리즘들은 단순하며, 또한 제한적인 문제들에 적용된다.

- 최적화 문제 (optimization) 란 가능한 해들 중에서 가장 좋은 (최대 또는 최소) 해를 찾는 문제이다.
