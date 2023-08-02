# Day.02 ( 배열 2. Array )

---

## 목차

- 배열 : 2차원 배열
- 부분집합 생성
- 바이너리 서치 (Binary Search)
- 셀렉션 알고리즘 (Selection Algorithm)
- 선택 정렬 (Selection Sort)

---

## 배열 : 2차원 배열

### 2차원 배열의 선언

- 1차원 List 를 묶어놓은 List

- 2차원 이상의 다차원 List 는 차원에 따라 Index 를 선언

- 2차원 List 의 선언 : 세로길이 (행의 개수), 가로길이 (열의 개수) 를 필요로 함

- Python 에서는 데이터 초기화를 통해 변수선언과 초기화가 가능함
    
    arr = [
    
              [0, 1, 2, 3],
    
              [4, 5, 6, 7]
    
             ] 
    
    ( 2행 4열의 2차원 List )
    
- 참고
    
    N = 3
    
    1  2  3
    
    4  5  6
    
    7  8  9
    
    ```python
    N = int(input())
    arr = [list(map(int,input().split())) for _ in range(N)
    ```
    

### 2차원 배열의 접근

- 배열 순회
    
    : n X m 배열의 n * m 개의 모든 원소를 빠짐없이 조사하는 방법
    

- 행 우선 순회

```python
# i 행의 좌표
# j 열의 좌표
for i in range(n):
    for j in range(m):
        f(Array[i][j])  # 필요한 연산 수행
```

- 열 우선 순회

```python
# i 행의 좌표
# j 열의 좌표
for j in range(m):
    for i in range(n):
        f(Array[i][j])  # 필요한 연산 수행
```

- 지그재그 순회

```python
# i 행의 좌표
# j 열의 좌표

for i in range(n):
    for j in range(m):
        f(Array[i][j + (m -1 - 2 * j) * (i % 2)])
				# 필요한 연산 수행
```

- **델타를 이용한 2차 배열 탐색**
    - 2차 배열의 한 좌표에서 4방향의 인접 배열 요소를 탐색하는 방법

```python
arr[0...N - 1][0...N - 1]  # N x N 배열
di[] <- [0, 1, 0, -1]  #
dj[] <- [1, 0, -1, 0]
for i : 0 -> N - 1
    for j : 0 -> N - 1 :
        for k in range(4) :
            ni <- i + di[k]
            nj <- j + dj[k]
            if 0 <= ni < N and 0 <= nj < N  # 유요한 인덱스면
                f(arr[ni][nj])

# 예시
di = [0, 1, 0, -1]
dj = [1, 0, -1, 0]
N = int(input())
arr = [list(map(int, input().split())) for _ in range(N)]

max_v = 0
for i in range(N):
    for j in range(N):
        # arr[i][j] 중심으로
        s = arr[i][j]
        for k in range(4):
            ni, nj = i + di[k], j + dj[k]
            if 0 <= ni < N and 0 <= nj < N:
                s += arr[ni][nj]
        # 여기까지 주변 원소를 포함한 값
        if max_v < s:
            max_v = s
print(max_v)
```

- 전치 행렬

```python
# i : 행의 좌표, len(arr)
# j : 열의 좌표, len(arr[0])
arr = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]  # 3 * 3 행렬

for i in range(3):
    for j in range(3):
        if i < j:  # 조건문이 없다면 전치가 이루어지지 않음
            arr[i][j], arr[j][i] = arr[j][i], arr[i][j]
```

---

## 부분집합 생성

- 유한 개의 정수로 이루어진 집합이 있을 때, 이 집합의 부분집합 중에서 그 집합의 원소를 모두 더한 값이 0이 되는 경우가 있는지를 알아내는 문제
- 예를 들어 [-7, -3, -2, 5, 8] 라는 집합이 있을 때, [-3, -2, 5] 는 이 집합의 부분집합이면서 (-3) + (-2) + 5 = 0 이므로 이 경우의 답은 참이 된다.
- 완전검색 기법으로 부분집합 합 문제를 풀기 위해서는, 우선 집합의 모든 부분집합을 생성한 후에 각 부분집합의 합을 계산해야 한다.
- 주어진 집합의 부분집합을 생성하는 방법에 대해서 생각해보자.

### 부분집합의 수

- 집합의 원소가 n 개일 때, 공집합을 포함한 부분집합의 수는 2^n 개이다.

- 이는 각 원소를 부분집합에 포함시키거나 포함시키지 않는 2가지 경우를 모든 원소에 적용한 경우의 수와 같다.

- 예)
    
    {1, 2, 3, 4}  ⇒  2 x 2 x 2 x 2 = 16가지
    

- 각 원소가 부분집합에 포함되었는지를 loop 이용하여 확인하고 부분집합을 생성하는 방법

```python
bit = [0, 0, 0, 0]
for i in range(2):
    bit[0] = i                    # 0번 원소
    for j in range(2):
        bit[1] = j                # 1번 원소
        for k in range(2)
            bit[2] = k            # 2번 원소
            for l in range(2):
                bit[3] = l        # 3번 원소
                print(bit)     # 생성된 부분집합 출력
```

### 비트 연산자

```python
&    ->  비트 단위로 AND 연산을 한다
|    ->  비트 단위로 OR 연산을 한다
<<   ->  피연산자의 비트 열을 왼쪽으로 이동시킨다
>>   ->  피연산자의 비트 열을 오른쪽으로 이동시킨다
```

- << 연산자
    - 1 << n : 2^n 즉, 원소가 n개일 경우의 모든 부분집합의 수를 의미한다.
- & 연산자
    - i & (1 << j) : i 의 j 번째 비트가 1인지 아닌지를 검사한다.
    
- 보다 간결하게 부분집합을 생성하는 방법

```python
arr = [3, 6, 7, 1, 5, 4]

n = len(arr)  # n : 원소의 개수

for i in range(1 << n):    # 1<<n : 부분집합을 만들 수 있는 개수
    for j in range(n):     # 원소의 수만큼 비트를 비교함
        if i & (1 << j):   # i 의 j 번 비트가 1 인경우
            print(arr[j], end=', ')    # j 번 원소 출력
    print()
print()
```