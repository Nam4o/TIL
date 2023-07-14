---

## 목차

1. Remote Repository
2. 로컬 & 원격 저장소
3. Gitignore
4. Github 활용

---

### Remote Repository (원격 저장소)

코드와 버전 관리 이력을 온라인 상의 특정 위치에 저장하여 여러 개발자가 협업하고 코드를 공유할 수 있는 저장 공간

- Local Repository : 개인 저장소
- Github Repository : 원격 저장소

→ 개인과 원격 간의 push & pull(or clone) 을 통해 remote

```bash
$ git remote add origin remote_repo_url
```

- 원격 저장소 등록

---

```bash
$ git push -u orign master
```

→ 원격 저장소에는 commit이 올라가는것, commit이력이 없다면 push 할 수 없다

```bash
$ git init
$ git remote add origin https://github.com/Nam4o/first_repo.git
$ git add .
$ git status
$ git commit -m "첫번째 커밋"
$ git status
$ git log
$ git push -u origin master
```

---

```bash
$ git pull origin master
```

---

```bash
$ git clone remote_repo_url
```

```bash
$ git clone https://github.com/Nam4o/first_repo
$ cd first_repo/
```

---

```bash
git_practice -> github_repository -> git_advanced
										             clone 
```

```bash
git_practice -> github_repository -> git_advanced
						push                 pull
```

---

## Gitignore

- Git 에서 특정 파일이나 디렉토리를 추적하지 않도록 설정하는데 사용되는 텍스트 파일
    - 프로젝트에 따라 공유하지 않아야 하는 것들도 존재하기 때문에 이용
- [**https://gitignore.io](https://gitignore.io)** ← 작업환경에 맞는 gitignore 파일 목록을 알려주는 웹사이트
- .gitignore 파일을 먼저 작성하고 진행하는 것이 원활한 작업진행 가능하다.

```markdown
**이미 git의 관리를 받은 파일이나 디렉토리는 나중에 gitignore에 작성해도 적용되지 않음**
```

- gitignore의 예시
    1. .gitignore 파일 생성 (파일명 앞에 ‘.’ 입력, 확장자는 따로 x)
    2. a와 b 이름을 가진 텍스트 파일 생성
    3. gitignore에 a.txt 작성
    4. git init
    5. git status

---

## 프로그래밍 언어를 배우는 이유

→ **프로그램을 만들기 위한 도구를 사용하는 방법을 배우는 것**

**→ 컴퓨터는 기계어를 사용, 때문에 기계어의 대안으로 사람이 이해할 수 있는 새로운 언어를 개발하게 됨 (프로그래밍 언어)**

### 프로그래밍 언어의 구성

- 소스코드 : 프로그래밍 언어로 작성된 프로그램
- 번역기(interpreter 혹은 complier)
    - 소스 코드를 컴퓨터가 이해할 수 있는 기계어로 번역
    - 파이썬의 경우 인터프리터를 사용

## 파이썬의 특징

- 파이썬 (Python)
    - 다른 프로그래밍 언어에 비해 문법이 간단하며, 엄격하지 않음
    - 별도의 데이터 타입 지정이 필요 없으며, 재할당이 가능함
    - 문장을 구분할 때 중괄호를 사용하지 않고 들여쓰기를 사용함
    - 소스코드를 기계어로 변환하는 컴파일 과정 없이 바로 실행이 가능함
    - 객체 지향 프로그래밍 언어로 모든 것이 객체로 구현되어 있음
        - 객체 : 속성값과 행동을 가지고 있는 데이터 집합
        

# 파이썬의 기능

---

## 시퀀스(sequence)형 컨테이너

→ 데이터가 순서대로 나열된 형식으로, 정렬(sorted)와는 다른 뜻

## 특징

1. 순서가 있다
2. 특정 위치의 데이터를 가리킬 수 있다

## 종류

파이썬에서 기본적인 시퀀스 타입은 다음과 같다

- 리스트 (list)
- 튜플 (tuple)
- 레인지 (range)
- 문자형 (string)
- 바이너리 (binary)

### 리스트 (List)

**생성과 접근**

```python
[value1, value2, value3]
```

```python
[] 또는 list()로 리스트 생성
```

- 리스트에는 순서가 존재하기 때문에 인덱스를 통해 접근이 가능하다
    - 값에 대한 접근은 list[i] 방식
    - positive index : 0, 1, 2, ... , n-1
    - nagative index : -n, -n+1, -n+2, … , -1

### 튜플 (Tuple)

**생성과 접근**

```python
(value1, value2)
```

튜플은 리스트와 유사하지만, **()**로 묶어서 표현한다

- tuple은 수정 불가능하다
- 직접 사용하기 보다는 파이썬 내부에서 다양한 용도로 활용된다

```python
my_tuple = (1, 2)
print(type(my_tuple))
```

**튜플 생성 주의 사항**

- 단일 항목의 경우
    - 하나의 항목으로 구성된 튜플은 생성 시 값 뒤에 쉼표를 붙여야 한다
    
    ```python
    a = 1,
    print(a)
    print(type(a))
    ```
    
- 복수 항목의 경우
    - 마지막 항목에 붙은 쉼표는 생략 가능
    
    ```python
    b = 1, 2, 3
    print(b)
    print(type(b))
    ```
    
    ```python
    c = 4, 5, 6,
    print(c)
    print(type(c))
    ```
    
- 튜플 대입
    - 우변의 값을 좌변의 변수에 한번에 할당하는 과정
    
    ```python
    x, y = 1, 2
    print(x)
    print(y)
    ```
    
    ```python
    # 변수의 값을 swap하는 코드에 튜플을 활용
    x, y = y, x
    print(x)
    print(y)
    ```
    

### 레인지 (range)

→ range는 정수의 시퀀스를 나타내기 위해 사용된다

```python
기본형 : range(n)
				0 부터 n-1 까지 값을 가짐
범위 지정 : range(n, m)
				n 부터 m-1 까지 값을 가짐
범위 및 스텝 지정 : range(n, m, s)
				n 부터 m-1 까지 +s 만큼 증가함
```