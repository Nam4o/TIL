# Day.11 ( Classes 상속 )

---

## 목차

- 상속
- 에러와 예외
- EAFP & LBYL

---

## 상속

: 기존 클래스의 속성과 메서드를 물려받아 새로운 하위 클래스를 생성하는 것

### 1. 상속이 필요한 이유

1. 코드 재사용
    - 상속을 통해 기존 클래스의 속성과 메서드를 재사용할 수 있음
    - 새로운 클래스를 작성할 때 기존 클래스의 기능을 그대로 활용할 수 있으며, 중복된 코드를 줄일 수 있음
2. 계층 구조
    - 상속을 통해 클래스들 간의 계층 구조를 형성할 수 있음
    - 부모 클래스와 자식 클래스 간의 관계를 표현하고, 더 구체적인 클래스를 만들 수 있음
3. 유지 보수의 용이성
    - 상속을 통해 기존 클래스의 수정이 필요한 경우, 해당 클래스만 수정하면 되므로 유지 보수가 용이해짐
    - 코드의 일관성을 유지하고, 수정이 필요한 범위를 최소화 할 수 있음

### 2. 클래스 상속

- 상속 없이 구현하는 경우
    - 학생 / 교수 정보를 나타내기 어려움
    
    ```python
    class Person:
        def __init__(self, name, age):
            self.name = name
            self.age = age
    
        def talk(self):
            print(f'반갑습니다. {self.name}입니다.')
    
    s1 = Person('김학생', 23)
    s1.talk()  # 반갑습니다. 김학생입니다.
    
    p1 = Person('박교수', 59)
    p1.tala()  # 반갑습니다. 박교수입니다.
    ```
    
    - 메서드 중복 정의
    
    ```python
    class Professor:
        def __init__(self, name, age, department):
            self.name = name
            self.age = age
            self.department = department
    
        def talk(self)  # 중복
            print(f'반갑습니다. {self.name}입니다.')
    
    class Student:
        def __init__(self, name, age, gpa):
            self.name = name
            self.age = age
            self.gpa = gpa
    
        def talk(self):  # 중복
            print(f'반갑습니다. {self.name}입니다.')
    ```
    
    - 상속을 사용한 계층구조 변경
    
    ```python
    class Person:
        def __init__(self, name, age):
            self.name = name
            self.age = age
    
        def talk(self):  # 메서드 재활용
            print(f'반갑습니다. {self.name}입니다.')
    
    class Professor(Person):
        def __init__(self, name, age, department):
            self.name = name
            self.age = age
            self.department = department
    
    class Student(Person):
        def __init__(self, name, age, gpa):
            self.name = name
            self.age = age
            self.gpa = gpa
    
    p1 = Professor('박교수', 49, '컴퓨터공학과')
    s1 = Student('김학생', 20, 3.5)
    
    # 부모 Person 클래스의 talk 메서드를 활용
    p1.talk()  # 반갑습니다. 박교수입니다.
    
    # 부모 Person 클래스의 talk 메서드를 활용
    s1.talk()  # 반갑습니다. 김학생입니다.
    ```
    

### 3. super()

:  자식 클래스에서 부모 클래스의 메서드 혹은 요소를 호출하기 위해 사용되는 내장 함수

- super() 사용 예시

```python
# super() 사용 전
class Person:
        def __init__(self, name, age, number, email):
            self.name = name
            self.age = age
            self.number = number
            self.email = email

class Student(Person):
    def __init__(self, name, age, number, email, student_id):
        self.name = name
        self.age = age
        self.number = number
        self.email = email
        self.student_id = student_id

# super() 사용 후
class Person:
    def __init__(self, name, age, number, email):
        self.name = name
        self.age = age
        self.number = number
        self.email = email
        
        
class Student(Person):
    def __init__(self, name, age, number, email, student_id):
        # 부모클래스의 init 메서드 호출
        super().__init__(name, age, number, email)
        self.student_id = student_id
```

- super() 사용 이유
1. 부모 클래스의 이름이 바뀔 경우 자식 클래스에 있는 부모클래스의 이름을 함께 수정해야 하는 번거로움이 있음 (유연하지않음)
2. 다중상속을 받을 시, 상속의

### 4. 다중 상속

- 두 개 이상의 클래스를 상속 받는 경우
- 상속받은 모든 클래스의 요소를 활용 가능함
- 중복된 속성이나 메서드가 있는 경우 **상속 순서에 의해 결정**됨

- 다중 상속 예시

```python
class Person:
    def __init__(self, name):
        self.name = name

    def greeting(self):
        return f'안녕, {self.name}'

class Mom(Person):
    gene = 'XX'

    def swim(self):
        return '엄마가 수영'

class Dad(Person):
    gene = 'XY'

    def walk(self):
        return '아빠가 걷기'

class FirstChild(Dad, Mom):
    def swim(self):
        return '첫째가 수영'

    def cry(self):
        return '첫째가 응애'

baby1 = FirstChild('아가')
print(baby1.cry())  # 첫째가 응애
print(baby1.swim())  # 첫째가 수영
print(baby1.walk())  #아빠가 걷기
print(baby1.gene)  # 상속 순서로 인해 Dad 클래스의 gene 함수 출력
```

- 상속 관련 함수와 메서드
    - mro()
        - Method Resolution Order
        - 해당 인스턴스의 클래스가 어떤 부모 클래스를 가지는지 확인하는 메서드
        - 기존의 인스턴스 → 클래스 순으로 이름 공간을 탐색하는 과정에서 상속 관계에 있으면 인스턴스 → 자식 클래스 → 부모 클래스로 확장
    
    ```python
    print(FirstChild.mro())
    # [<class '__main__.FistChild'>, <class '__main__.Dad'>, <class '__main__.Mom'>, <class '__main__.Person'>, <class 'object'>]
    ```
    

---

## 에러와 예외

### 1. 디버깅

: 소프트웨어에서 발생하는 버그를 찾아내고 수정하는 과정

 프로그램의 오작동 원인을 식별하여 수정하는 작업

- 버그
    
    : 소프트웨어에서 발생하는 오류 또는 결함
    
     프로그램의 예상된 동작과 실제 동작 사이의 불일치
    
- 디버깅 방법
1. print 함수 활용
    
    >> 특정 함수 결과, 반복 / 조건 결과 등 나눠서 생각, 코드를 bisection 으로 나눠서 생각
    
2. 개발 환경 (text editor, IDE) 등에서 제공하는 기능 활용
    
    >> breakpoint, 변수 조회 등
    
3. Python Tutor 활용 ( 단순 파이썬 코드인 경우 )
4. 뇌 컴파일, 눈 디버깅 등

### 2. 에러

: 프로그램 실행 중에 발생하는 예외 상황

- 파이썬의 에러 유형
    - **문법 에러** (Syntax Error)
        
        : 프로그램의 구문이 올바르지 않은 경우 발생
        
        (오타, 괄호 및 콜론 누락 등의 문법적 오류)
        
    
    ⇒ 에러가 있으면 코드를 실행하지 않고 바로 종료
    
    - **예외** (Exception)
    
    ⇒ 프로그램 실행 중에 감지되는 에러
    

```python
# 문법 에러 예시
# Invalid syntax (문법 오류)
while  # SyntaxError: Invalid syntax

# assign to literal (잘못된 할당)
5 = 3  # SyntaxError: cannot assign to literal

# EOL (End of Line)
print('hello  # SyntaxError: EOL while scanning string literal

# EOF (End of File)
print(  # SyntaxError: unexpected EOF while parsing
```

### 3. 예외

: 프로그램 실행 중에 감지되는 에러

- 내장 예외
    
    : 예외 상황을 나타내는 예외 클래스들
    
    ⇒ 파이썬에서 이미 정의되어 있으며, 특정 예외 상황에 대한 처리를 위해 사용
    
    - ZeroDivisionError
        
        : 나누기 또는 모듈로 연산의 두 번째 인자가 0일때 발생
        
    
    ```python
    10 / 10  # ZeroDivisionError: division by zero
    ```
    
    - NameError
        
        : 지역 또는 전역 이름을 찾을 수 없을 때 발생
        
    
    ```python
    print(name_error)  # NameError: name 'name_error' is not defined
    ```
    
    - TypeError
        - 타입 불일치
        
        ```python
        '2' + 2  # TypeError: can only concatenate str (not "int") to str
        ```
        
        - 인자 누락
        
        ```python
        sum()  # TypeError: sum() takes at least 1 positional argument (0 given)
        ```
        
        - 인자 초과
        
        ```python
        sum(1, 2, 3)  # TypeError: sum() takes at most 2 arguments (3 given)
        ```
        
        - 인자 타입 불일치
        
        ```python
        import random
        random.sample(1, 2)  # TypeError: Poupulation must be a sequence.
        										 # For dicts or sets, use sorted(d).
        ```
        
    - ValueError
    
    : 연산이나 함수에 문제가 없지만 부적절한 값을 가진 인자를 받았고, 상황이 IndexError 처럼 더 구체적인 예외로 설명되지 않는 경우 발생
    
    ```python
    int('1,5')  # ValueError: invalid literal for int() with base 10: '3.5'
    
    range(3).index(6)  # ValueError: 6 is not in range
    ```
    
    - IndexError
        
        : 시퀀스 인덱스가 범위를 벗어날 때 발생
        
    
    ```python
    empty_list = []
    empty_list[2]  # IndexError: list index out of range
    ```
    
    - KeyError
        
        : 딕셔너리에 해당 키가 존재하지 않는 경우
        
    
    ```python
    person = {'name': 'Alice'}
    person['age']  # KeyError: 'age'
    ```
    
    - ModuleNotFoundError
        
        : 모듈을 찾을 수 없을 때 발생
        
    
    ```python
    import hahaha  # ModuleNotFoundError: No module named 'hahaha'
    ```
    
    - ImportError
        
        : 임포트 하려는 이름을 찾을 수 없을 때 발생
        
    
    ```python
    from random import hahah
    # ImportError: cannot import name 'hahaha' from 'random'
    ```
    
    - KeyboardInterrupt
        
        : 사용자가 Control-C 또는 Delete를 누를 때 발생
        
        - 무한루프 시 강제 종료
    
    ```python
    while True:
        continue
    '''
    Traceback (most recent call las):
      File "...", line 2, in <module>
        continue
    KeyboardInterrup
    ```
    
    - IndentationError
        
        : 잘못된 들여쓰기와 관련된 문법 오류
        
    
    ```python
    for i in range(10):
    print(i)  # IndentationError: expected an indented block
    ```
    

### 4. 예외 처리

- try 와 except
    
    : 파이썬에서는 **try** 문과 **except** 절을 사용하여 예외 처리
    
- try-except 구조
    - try 블록 안에는 예외가 발생할 수 있는 코드를 작성
    - except 블록 안에는 예외가 발생했을 때 처리할 코드를 작성
    - 예외가 발생하면 프로그램 흐름은 try 블록을 빠져나와 해당 예외에 대응하는 except 블록으로 이동
    
    ```python
    try:
        # 예외가 발생할 수 있는 코드
    
    except 예외:
        # 예외 처리 코드
    ```
    
    ```python
    try:
        result = 10 / 0
    except ZeroDivisionError:
        print('0으로 나눌 수 없습니다.')
    # 0으로 나눌 수 없습니다.
    
    try:
        num = int(input('숫자입력 : '))
    except ValueError:
        print('숫자가 아닙니다.')
    
    """
    숫자입력 : a
    숫자가 아닙니다.
    """
    ```
    

- 복수 예외 처리 연습
    
    >>100을 사용자가 입력한 값으로 나누고 출력하는 코드를 작성해보시오.
    
    - 먼저, 발생 가능한 에러가 무엇인지 예상해보기
    
    ```python
    num = int(input('100으로 나눌 값을 입력하시오 : '))
    print(100 / num) 
    ```
    
    - int(’a’) → 문자열을 int로 형변환 : ValueError
    - 100 / 0 → 0으로 숫자를 나눔 : ZeroDivisionError
    
    ```python
    try:
        num = int(input('100을 나눌 값을 입력하시오 : '))
        print(100 / num)
    except ValueError:
        print('숫자를 넣어주세요.')
    except ZeroDivisionError:
        print('0으로 나눌 수 없습니다.')
    except:
        print('에러가 발생하였습니다.')
    ```
    

- 내장 예외의 상속 계층구조 주의
    - 아래와 같이 예외를 작성하면 코드는 2번째 except 절에 이후로 도달하지 못함
    
    ```python
    try:
        num = int(input('100을 나눌 값을 입력하시오 : '))
        print(100 / num)
    except BaseException:
        print('숫자를 넣어주세요.')
    # 이 블록에 도달하지 못함
    except ZeroDivisionError:  
        print('0으로 나눌 수 없습니다.')
    except:
        print('에러가 발생하였습니다.')
    ```
    
    - 내장 예외 클래스는 상속 계층구조를 가지기 때문에 except 절로 분기 시 **반드시 하위 클래스를 먼저 확인 할 수 있도록 작성** 해야함

---

## EAFP & LBYL

: 예외처리와 값 검사에 대한 2가지 접근 방식

## 1. EAFP

: 예외처리를 중심으로 코드를 작성하는 접근 방식 (try-except)

```python
try:
    result = my_dict['key']
    print(result)
except KeyError:
    print('Key가 존재하지 않습니다.')
```

## 2. LBYL

: 값 검사를 중심으로 코드를 작성하는 접근 방식 (if-else)

```python
if 'key' in my_dict:
    result = my_dict['key']
    print(result)
else:
    print('Key가 존재하지 않습니다.')
```

## 3. 접근 방식 비교

| EAFP | LBYL |
| --- | --- |
| “일단 실행하고 예외를 처리” | “실행하기 전에 조건을 검사” |
| 코드를 실행하고 예외가 발생하면 예외처리를 수행 | 코드 실행 전에 조건문 등을 사용하여 예외 상황을 미리 검사하고, 예외 상황을 피하는 방식 |
| 코드에서 예외가 발생할 수 있는 부분을 미리 예측하여 대비하는 것이 아니라 예외가 발생한 후에 예외를 처리 | 코드가 좀 더 예측 가능한 동작을 하지만, 코드가 더 길고 복잡해질 수 있음 |
| 예외 상황을 예측하기 어려운 경우에 유용 | 예외 상황을 미리 방지하고 싶을 때 유용 |

---

## 참고

### as키워드

- as 키워드를 활용하여 에러 메세지를 except 블록에서 사용할 수 있음
```python
my_list = []

try:
    number = my_list[1]
except IndexError as error:
    print(f'{error}가 발생했습니다.')

# list index out of range가 발생했습니다.
```