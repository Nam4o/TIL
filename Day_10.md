# Day.10

---

## 목차

- 객체 지향 프로그래밍
- 객체
- 클래스
- 메서드

---

## 객체 지향 프로그래밍

### 1. 절차 지향 프로그래밍

: 프로그램을 ‘데이터’와 ‘절차’로 구성하는 방식의 프로그래밍 패러다임

- ‘데이터’와 해당 데이터를 처리하는 ‘함수(절차)’가 분리되어 있으며, **함수 호출의 흐름이 중요**
- 코드의 순차적인 흐름과 함수 호출에 의해 프로그램이 진행



⇒ 실제로 실행되는 내용이 무엇이 무엇인가가 중요

⇒ 데이터를 다시 재사용하거나 하기보다는 처음부터 끝까지 실행되는 결과물이 중요한 방식

- **소프트웨어 위기**
    

    
    - 하드웨어의 발전으로 컴퓨터 계산용량과 문제의 복잡성이 급격히 증가함에 따라 소프트웨어에 발생한 충격

### 2. 객체 지향 프로그래밍

: 데이터와 해당 데이터를 조작하는 ***메서드**를 **하나의 객체로 묶어 관리**하는 방식의 프로그래밍 패러다임

*객체에 속한 함수

(절차 지향 프로그래밍의 단점을 보완하기 위한 프로그래밍)

‘추상화 ‘ : 복잡한 것은 숨기고, 필요한 것을 들어낸다.

---

| 절차 지향 |  객체 지향 |
| --- | --- |
| 데이터와 해당 데이터를 처리하는 함수(절차)가 분리 | 데이터와 해당 데이터를 처리하는 메서드(메세지)를 하나의 객체(클래스)로 묶음 |
| 함수 호출의 흐름이 중요 | 객체 간 상호작용과 메세지 전달이 중요 |

절차 : 함수가 데이터에서 인자를 받음

객체 : 데이터(객체)가 인자를 받음

---

## 객체

: 클래스에서 정의한 것을 토대로 메모리에 할당된 것 **‘속성’** 과 **‘행동’** 으로 구성된 모든 것

- 객체 예시
    - 속성 (변수) : {직업: 가수}, {생년월일: 1993년 5월 16일}, {국적: 대한민국}
    - 행동 (메서드) : 랩(), 댄스(), 소몰이()
    
    ⇒ 가수 (*클래스) → 객체 (아이유, BTS 등)
    
    *객체를 만들기 위한 틀, 설계도
    

- 클래스와 객체
    - 클래스로 만든 객체를 ***인스턴스** 라고도 함
        
        *실제 메모리에 할당된 객체
        
    
    ```python
    ex) 
    아이유는 객체다 (O)
    
    아이유는 인스턴스다 (X)
    
    아이유는 가수의 인스턴스다 (O)
    
    클래스 (가수)와 객체 (아이유)
    
    └타입(list)  (클래스를 만든다 == **타입**을 만든다) (in Python)
    ```
    
    - 변수 name의 타입은 str 클래스다
    
    ⇒ 변수 name은 **str 클래스의 인스턴스**이다
    
    ⇒ 우리가 사용해왔던 **데이터 타입은 사실 모두 클래스**였다
    
    - 결국 문자열 타입의 변수는 str 클래스로 만든 인스턴스다
    
    ```python
    ‘’, ‘hello’, ‘파이썬’
        
    : 문자열 타입(클래스)의 객체(인스턴스)
        
    [1, 2, 3], [1], [], [’hi’]
        
    : 리스트 타입(클래스)의 객체(인스턴스)
    ```
    
- 인스턴스와 메서드
    
    ```jsx
    ‘hello’.upper() 
    문자열.대문자로()
    
    객체.행동()
    
    인스턴스.메서드()
    
    [1, 2, 3].sort()
    리스트.정렬해()
    객체.행동()
    인스턴스.메서드()
    ```
    
    - 하나의 객체(object)는 특정 타입의 **인스턴스**이다
        
        ex) 123, 900, 5는 모두 int의 인스턴스
        
        ‘hello’, ‘bye’는 모두 string의 인스턴스
        
        [232, 89, 1], []은 모두 list의 인스턴스
        

- 객체(object)의 특징
    - 클래스를 통해 만든 객체 = 클래스의 인스턴스
    - 타입 (type) : 어떤 연산자(operator)와 조작(method)이 가능한가?
    - 속성 (attribute) : 어떤 상태(데이터)를 가지는가?
    - 조작법 (method) : 어떤 행위(함수)를 할 수 있는가?
    
    ⇒ 객체 = 속성 + 기능
    

## 클래스

: 파이썬에서 타입을 표현하는 방법

⇒ 객체를 생성하기 위한 설계도

⇒ 데이터와 기능을 함께 묶는 방법을 제공

```python
# 클래스 정의
class Person:  # 파스칼 케이스 (각 단어의 첫 시작이 대문자)
		pass
# 인스턴스 생성
iu = Person()

# 메서드 호출
iu.메서드()

# 속성 (변수) 접근
iu.attribute
```

```python
# 클래스 정의 
class Person:
    # 속성 (변수)
    blood_color = 'red'
    
    # 메서드
    def __init__(self, name):  # 매직 메서드 : 개발자가 직접 호출하지 않는다
        self.name = name       # init : 초기화
    # 위의 메서드는 '생성자 메서드', 인스턴스를 만들 때 자동으로 호출
        
    def singing(self):
        return f'{self.name}가 노래합니다.'
    
# 인스턴스 생성
singer1 = Person('IU')
singer2 = Person('BTS')

# 메서드 호출
print(singer1.singing())
print(singer2.singing())

# 속성 (변수) 사용
print(singer1.blood_color)
print(singer2.blood_color)
```

- 클래스 기본 활용

```python
# 클래스 정의 
class Person:
    # 속성 (변수)
    blood_color = 'red'
    
    # 메서드
    def __init__(self, name):  # 매직 메서드 : 개발자가 직접 호출하지 않는다
        self.name = name       # init : 초기화
    # 위의 메서드는 '생성자 메서드', 인스턴스를 만들 때 자동으로 호출
        
    def singing(self):
        return f'{self.name}가 노래합니다.'
```

- 생성자 함수
    - 객체를 생성할 때 자동으로 호출되는 특별한 메서드
    - ‘__init__’이라는 이름의 메서드로 정의되며, 객체의 초기화를 담당
    - 생성자 함수를 통해 인스턴스를 생성하고 필요한 초기값을 설정
    
    ```python
    def __init__(self, name):
        self.name = name
    ```
    

- 인스턴스 변수
    - 인스턴스 (객체)마다 별도로 유지되는 변수
    - 인스턴스마다 독립적인 값을 가지며, 인스턴스가 생성될 때마다 초기화됨
    
    ```python
    self.name = name
    ```
    

- 클래스 변수
    - 클래스 내부에 선언된 변수
    - 클래스로 생성된 모든 인스턴스들이 공유하는 변수
    
    ```python
    blood_color = 'red
    ```
    

- 인스턴스 메서드
    - 각각의 인스턴스에서 호출할 수 있는 메서드
    - 인스턴스 변수에 접근하고 수정하는 등의 작업을 수행
    
    ```python
    def singing(self):
        return f'{self.nam}가 노래합니다.'
    ```
    

- 인스턴스와 클래스 간의 이름 공간 (namespace)
    - 클래스를 정의하면, 클래스와 해당하는 이름 공간 생성
    - 인스턴스를 만들면, 인스턴스 객체가 생성되고 **독립적인** 이름 공간 생성
    - 인스턴스에서 특정 속성에 접근하면, 인스턴스 → 클래스 순으로 탐색
    
    ```python
    # Person 정의
    class Person:
        name = 'unknown'
        
        # 인스턴스 메서드
        def talk(self):
            print(self.name)
            
    p1 = Person()
    p1.talk()  # unknown
    # p2 인스턴스 변수 설정 전/후
    
    p2 = Person()
    p2.talk()  #unknown
    p2.name = 'Kim'
    p2.talk()  # Kim
    
    print(Person.name)  # unknown  # 클래스로 접근
    print(p1.name)  # unknown  # 인스턴스로 접근
    print(p2.name)  # Kim  #인스턴스로 접근
    ```
    

- **독립적인 이름공간을 가지는 이점**
    - 각 인스턴스는 독립적인 메모리 공간을 가지며, 클래스와 다른 인스턴스 간에는 서로의 데이터나 상태에 직접적인 접근이 불가능
    - 객체 지향 프로그래밍의 중요한 특성 중 하나로, 클래스와 인스턴스를 모듈화하고 각각의 개체가 독립적으로 동작하도록 보장
    - 이를 통해 클래스와 인스턴스는 다른 객체들과의 상호작용에서 서로 충돌이나 영향을 주지 않으면서 독립적으로 동작할 수 있음
    
    ⇒ 코드의 가독성, 유지보수성, 재사용성을 높이는데 도움을 줌
    

### 클래스 변수와 인스턴스 변수

- 클래스 변수 활용
    - 가수가 몇명인지 확인하고 싶다면?
        
        → 인스턴스가 생성 될 때마다 클래스 변수가 늘어나도록 설정할 수 있음
        
        ```python
        class Person:
            count = 0
        
            def __init__(self, name):
                self.name = name
                Person.count += 1
        
        person1 = Person('IU')
        person2 = Person('BTS')
        
        print(Person.count)  # 2 
        ```
        
    - 클래스 변수를 변경할 때는 항상 **클래스.클래스변수** 형식으로 변경
        
        ```python
        class Circle():
            pi = 3.14
        
            def __init__(self, r):
                self.r = r
        
        c1 = Circle(5)
        c2 = Circle(10)
        
        print(Circle.pi)  # 3.14
        print(c1.pi)  # 3.14
        print(c2.pi)  # 3.14
        
        Circle.pi = 5  # 클래스 변수 변경
        print(Circle.pi)  # 5
        print(c1.pi)  # 5
        print(c2.pi)  # 5
        
        c2.pi = 3  # 인스턴스 변수 변경
        print(Circle.pi)  # 5  (클래스 변수)
        print(c1.pi)  # 5 (클래스 변수)
        print(c1.pi)  # 3 (새로운 인스턴스 변수가 생성됨)
        ```
        

## 메서드

### 1. 인스턴스 메서드

: 클래서로부터 생성된 각 인스턴스에서 호출할 수 있는 메서드

⇒ 인스턴스의 상태를 조작하거나 동작을 수행

- 인스턴스 메서드 구조
    - 클래스 내부에 정의되는 메서드의 기본
    - 반드시 첫 번째 매개변수로 **인스턴스 자신(self)**을 전달받음
    
    ```python
    class MyClass:
    
        def instance_method(self, arg1, ...)
            pass
    ```
    

- self 동작 원리
    
    ```python
    # upper 메서드를 사용해 문자열 ‘hello’를 대문자로 변경하기
    'hello'.upper()
    
    # 하지만 실제 파이썬 내부 동작은 다음과 같이 이루어진다.
    str.upper('hello')
    ```
    
    - str 클래스가 upper 메서드를 호출했고, 그 첫 번째 인자로 문자열 인스턴스가 들어간 것이다
    
    **⇒ 인스턴스 메서드의 첫 번째 매개변수가 반드시 인스턴스 자기 자신인 이유 (self)**
    
    - ‘hello’.upper() 은 str.upper(’hello’) 를 객체 지향 방식의 메서드로 호출하는 표현이다. (단축형 호출)
    - ‘hello’ 라는 문자열 객체가 단순히 어딘가의 함수로 들어가는 인자가 아닌 객체 스스로 메서드를 호출하여 코드를 동작하는 객체 지향적 표현이다.

### 2. 생성자 메서드

: 인스턴스 객체가 생성될 때 자동으로 호출되는 매서드

⇒ 인스턴스 변수들의 초기값을 설정

- 생성자 메서드 구조

```python
class Person:

    def __init__(self):
        print('인스턴스가 생성되었습니다.')

person1 = Person()  # 인스턴스가 생성되었습니다.
```

```python
class Person:

    def __init__(self, name):
        print(f'인스턴스가 생성되었습니다. {name}')

person1 = Person('지민')  # 인스턴스가 생성되었습니다. 지민
```

### 3. 클래스 메서드

: 클래스가 호출하는 메서드

⇒ 클래스 변수를 조작하거나 클래스 레벨의 동작을 수행

- 클래스 메서드 구조
    - @classmethod ***데코레이터**를 사용하여 정의
        
        *포장지, 박스와 같은 역할
        
    - 호출 시, 첫 번째 인자로 호출하는 클래스(cls) 가 전달됨
    
    ```python
    class MyClass:
    
        @classmethod
        def class_method(cls, arg1, ...):
            pass
    ```
    

- 클래스 메서드 예시
    
    ```python
    class Person:
        count = 0
    
        def __init__(self, name):
            self.name = name
            Person.count += 1
    
        @classmethod
        def number_of_population(cls):
            print(f'인구수는 {cls.count}입니다.')
    
    person1 = Person('IU')
    person2 = Person('BTS')
    
    Person.number_of_population()  # 인구수는 2입니다.
    ```
    

### 3. 스태틱(정적) 메서드

: 클래스와 인스턴스와 상관없이 독립적으로 동작하는 메서드

⇒ 주로 클래스와 관련이 있지만 인스턴스와 상호작용이 필요하지 않은 경우에 사용

- @staticmethod 데코레이터를 사용하여 정의

- 호출 시 필수적으로 작성해야 할 매개변수가 없음

- 즉, 객체 상태나 클래스 상태를 수정할 수 없으며 단지 기능(행동)만을 위한 메서드로 사용
    
    ```python
    class MyClass:
    
        @staticmethod
        def static_method(arg1, ...):
            pass    
    ```
    

### 메서드 정리

- 인스턴스 메서드
    
    : 인스턴스의 상태를 변경하거나, 해당 인스턴스의 특정 동작을 수행
    
    - self 매개변수를 통해 인스턴스 조작
    - 클래스 변수와 인스턴스 변수 모두 사용 가능

- 클래스 메서드
    
    : 인스턴스의 상태에 의존하지 않는 기능을 정의
    
    - cls 매개변수를 통해 클래스를 조작
    - 클래스 변수를 조작하거나 클래스 레벨의 동작을 수행
    - 클래스 변수만 사용 가능

- 스태틱 메서드
    
    : 클래스 및 인스턴스와 관련이 없는 일반적인 기능을 수행
    
    - 속성이 없이 독립적인 함수를 수행하고 싶을 때 사용
    - 인스턴스 변수와 클래스 변수 모두 사용할 수 없고, 데코레이터를 사용
    - 기존의 다른 메서드와 달리 추가적인 보조인자가 없음(매개변수만 설정)

### **각자의 역할**

- 클래스가 사용해야 할 것
    - **클래스메서드와 스태틱 메서드만 사용하도록 한다**

- 인스턴스가 사용해야 할 것
    - **인스턴스는 인스턴스 메서드만 사용하도록 한다**

```python
class MyClass:

    def instance_method(self):
         return 'instance method', self

    @classmethod
    def class_method(cls):
    return 'class method', cls
    
@staticmethod
    def static_method():
        retrun'static method'
```

## * 참고

### 할 수 있다 ≠ 써도 된다

⇒ 각자의 메서드는 OOP 패러다임에 따라 명확한 목적에 따라 설계된 것이기 때문에 클래스와 인스턴스 각각 올바른 메서드만 사용하도록 해야한다

### 매직 메서드

- 특별한 인스턴스 메서드
- **특정 상황에 자동으로 호출되는 메서드**
- Double underscore(__)가 있는 메서드는 특수한 동작을 위해 만들어진 메서드
- 스페셜 메서드 혹은 매직 메서드라고 불림

```python
class Circle:
    def __init__(self, r):
        self.r = r

    def area(self):
        return 3.14 * self.r * self.r

    def __str__(self):
        return f'[원] radius: {self.r}'

c1 = Circle(10)
c2 = Circle(1)

print(c1)  # [원] radius: 10
print(c2)  # [원] radius: 1
```

### 데코레이터 (Decorator)

- 다른 함수의 코드를 유지한 채로 수정하거나 확장하기 위해 사용되는 함수

```python
"""
데코레이터 정의
"""

def my_decorator(func):
        def wrapper():
            # 함수 실행 전에 수행할 작업
            print('함수 실행 전')
            # 원본 함수 호출
            result = func()
            # 함수 실행 후에 수행할 작업
            print('함수 실행 후')
            return result
        return wrapper

"""
데코레이터 정의
"""

@my_decorator
def my_function():
    print('원본 함수 실행')

my_function()

"""
함수 실행 전
원본 함수 실행
함수 실행 후
"""
```

---

## 절차 지향과 객체 지향은 대조되는 개념이 아니다

⇒ 객체 지향은 기존 절차 지향을 기반으로 두고 보완하기 위해 객체라는 개념을 도입해 상속, 코드 재사용성, 유지보수성 등의 이점을 가지는 패러다임