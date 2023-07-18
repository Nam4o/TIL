#Day.5
---

# 목차

- Data Types
- Numeric Types
- Sequence Type
- Non-sequence Type
- Other Types
- Collection
- Type Conversion
- 연산자

---

## Data Types

: 값의 종류와 그 값에 적용 가능한 연산과 동작을 결정하는 속성

### 데이터 타입이 필요한 이유

- 값들을 구분하고, 어떻게 다뤄야 하는지를 알 수 있음
- 요리 재료마다 특정한 도구가 필요하듯이 각 데이터 타입 값들도 각자에게 적합한 도구를 가짐
- 타입을 명시적으로 지정하면 코드를 읽는 사람이 변수의 의도를 더 쉽게 이해할 수 있고, 잘못된 데이터 타입으로 인한 오류를 미리 예방

---

## Numeric Types

### 1. int : 정수 자료형, 정수를 표현하는 자료형

- **진수 표현**
    - 2진수(binary) : 0b
    - 8진수(octal) : 0o
    - 16진수(hexadecimal) : 0x
    
    ```python
    print(0b10) # 2
    print(0o30) # 24
    print(0x10) # 16
    ```
    

### 2. float : 실수 자료형, 실수를 표현하는 자료형

→프로그래밍 언어에서 float는 실수에 대한 **근삿값**

- **유한 정밀도**
    - 컴퓨터 메모리 용량이 한정되어 있고 한 숫자에 대해 저장하는 용량이 제한 됨
    - 0.6666666666666666과 1.6666666666666667은 제한된 양의 메모리에 저장할 수 있는 2/3과 5/3에 가장 가까운 값
- **실수 연산 시 주의사항**
    - 컴퓨터는 2진수를 사용, 사람은 10진법을 사용
    - 이때 10진수 0.1은 2진수로 표현하면 0.0001100110011001100110… 같이 무한대로 반복
    - 무한대 숫자를 그대로 저장할 수 없어서 사람이 사용하는 10진법의 근삿값만 표시
    - 0.1의 경우 3602879701896397 / 2 ** 55 이며, 0.1에 가깝지만 정확히 동일하지는 않음
    - 이런 과정에서 예상치 못한 결과가 나타남
    - 이런 증상을 **Floating point rounding error** 라고 함
- **실수 연산 시 해결책**
    - 두 수의 차이가 매우 작은 수보다 작은지를 확인하거나 math 모듈 활용
    
    ```python
    a = 3.2 - 3.1 # 0.10000000000000009
    b = 1.2 - 1.1 # 0.09999999999999987
    
    # 1. 임의의 작은 수 활용
    print(abs(a - b) <= 1e-10) # True
    
    # 2. math 모듈 활용
    import math
    print(math.isclose(a, b)) # True
    ```
    
- **지수 표현 방식**
    - e 또는 E 를 사용한 지수 표현
    
    ```python
    # 314 * 0.01
    number = 314e-2
    
    # float
    print(type(number))
    
    # 3.14
    print(number)
    
    # 지수 (제곱하는 횟수) 표현 10^
    print(314e-2) # 3.14
    print(314e2) # 31400.0
    ```
    

---

## Sequence Types

: 여러 개의 값들을 **순서대로 나열**하여 저장하는 자료형

 ( str, list, tuple, range )

- **Sequence Types 특징**
    1. 순서 (Sequence) :
        - 값들이 순서대로 저장 (정렬X)
    2. 인덱싱 (Indexing) :
        - 각 값에 고유한 인덱스 (번호)를 가지고 있으며, 인덱스를 사용하여 특정 위치의 값을 선택하거나 수정할 수 있음
    3. 슬라이싱 (Slicing) :
        - 인덱스 범위를 조절해 부분적인 값을 추출할 수 있음
    4. 길이 (Length) :
        - len() 함수를 사용하여 저장된 값의 개수(길이)를 구할 수 있음
    5. 반복 (Iteration) :
        - 반복문을 사용하여 저장된 값들을 반복적으로 처리할 수 있음

### 1. str : 문자열, 문자들의 순서가 있는 변경 불가능한 시퀀스 자료형

- **문자열 표현**
    - 문자열은 단일 문자나 여러 문자의 조합으로 이루어짐
    - 작은 따옴표(’) 또는 큰 따옴표(”) 감싸서 표현
    
    ```python
    # Hello World!
    print('Hello World!)
    
    # str
    print(type('Hello World!))
    ```
    
- **중첩 따옴표**
    - 따옴표 안에 따옴표를 표현할 경우
        - 작은 따옴표가 들어 있는 경우는 큰 따옴표로 문자열 생성
        - 큰 따옴표가 들어 있는 경우는 작은 따옴표로 문자열 생성
- **Escape sequence**
    - 역슬래시 (backslash) 뒤에 특정 문자가 와서 특수한 기능을 하는 문자 조합
    - 파이썬의 일반적인 문법 규칙을 잠시 탈출한다는 의미
    
    ```python
    \n : 줄바꿈 , \t : 탭 , \\ : 백슬래시
    \' : 작은 따옴표 , \" : 큰 따옴표
    ```
    
- **String Interpolation** : 문자열 내에 변수나 표현식을 삽입하는 방법
    - **f-string** : 문자열에 f 또는 F 접두어를 붙이고 표현식을 {expression} 로 작성하여 문자열에 파이썬 표현식의 값을 삽입할 수 있음
    
    ```python
    bugs = 'roaches'
    counts = 13
    area = 'living room'
    
    # Debugging roaches 13 living room
    print(f'Debugging {bugs} {counts} {area}')
    # print('Debugging {} {} {}'.format(bugs, counts, area))
    # print('Debugging %s %d %s' % (bugs, counts, area))
    
    # f-string 응용 (f-string advanced)
    greeting = 'hi'
    print(f'{greeting:^10}') # 10칸 중 가운데에 greeting 출력
    print(f'{greeting:>10}') # 10칸 중 오른쪽에 greeting 출력
    print(f'{3.141592:.4f}') # 3.141592 에서 소숫점 뒤의 4칸만 출력
    ```
    
- **문자열의 시퀀스 특징**
    
    ```python
    my_str = 'hello'
    
    # 인덱싱
    print(my_str[1]) # e
    
    # 슬라이싱
    print(my_str[2:4]) # ll
    
    # 길이
    print(len(my_str)) # 5
    ```
    
1.  **인덱스 (Index)** : 시퀀스 내의 값들에 대한 고유한 번호로, 각 값의 위치를 식별하는 데 사용되는 숫자
2. **슬라이싱 (slicing)** : 시퀀스의 일부분을 선택하여 추출하는 작업
    
    → 시작 인덱스와 끝 인덱스를 지정하여 해당 범위의 값을 포함하는 새로운 시퀀스를 생성
    
    ```python
     0  1  2  3  4    # 공백을 기준으로 숫자를 셈
    ' h  e  l  l  o '
    
    my_str[:3]  # 0 부터 시작하는 부분은 생략 가능
    my_str[3:]  # 마지막까지 가는 부분은 생략 가능
    my_str[0:5:2]  # 0 부터 5 까지 2칸씩 step 으로 출력
    
    # step 이 음수일 경우
    my_str[::-1]  # 'hello' -> 'olleh' (문자열 뒤집기)
    ```
    
- **문자열은 불변 (변경 불가)**
    
    ```python
    my_str = 'hello'
    
    # TypeError : 'str' object does not support item assignment
    my_str[1] = 'z'
    ```
    
1. **길이 (length)**

### 2. list : 여러 개의 값을 순서대로 저장하는 변경 가능한 시퀀스 자료형

- **리스트 표현**
    - 0개 이상의 객체를 포함하며 데이터 목록을 저장
    - 대괄호([])로 표기
    - 데이터는 어떤 자료형도 저장할 수 있음
    
    ```python
    my_list_1 = []
    my_list_2 = [1, 'a', 3, 'b', 5]
    my_list_3 = [1, 2, 3, 'Python', ['hello', 'world', '!!!']
    ```
    
- **리스트의 시퀀스 특징**
    1. **인덱싱**
    2. **슬라이싱**
    3. **길이**
- **중첩된 리스트 접근**
    - 출력 값 예상해보기
    
    ```python
    my_list = [1, 2, 3, 'Python', ['hello', 'world', '!!!']
    
    print(len(my_list))  # 5
    print(my_list[4][-1])  # !!!
    print(my_list[-1][1][0]  # w
    ```
    
- **리스트는 가변 (변경 가능)**
    
    ```python
    my_list = [1, 2, 3]
    my_list[0] = 100
    
    print(my_list)  # [100, 2, 3]
    ```
    

### 3. tuple : 여러 개의 값을 순서대로 저장하는 변경 불가능한 시퀀스 자료형

- **튜플 표현**
    - 0개 이상의 객체를 포함하며 데이터 목록을 저장
    - 소괄호(())로 표기
    - 데이터는 어떤 자료형도 저장할 수 있음
    
    ```python
    my_tuple_1 = ()
    my_tuple_2 = (1,)  # tuple의 요소가 1개라도 ',' 사용
    my_tuple_3 = (1, 'a', 3, 'b', 5)
    ```
    
- **튜플의 시퀀스 특징**
    1. **인덱싱**
    2. **슬라이싱**
    3. **길이**
- **튜플은 불변 (변경 불가)**
    
    ```python
    my_tuple = (1, 'a', 3, 'b', 5)
    
    # TypeError: 'tuple' object does not support item assignment
    my_tuple[1] = ('z')
    ```
    
- **튜플은 어디에 쓰일까?**
    - 튜플은 불변 특성을 사용한 안전하게 여러 개의 값을 전달, 그룹화, 다중 할당 등
    
    → 개발자가 직접 사용하기 보다 ‘파이썬 내부 동작’ 에서 주로 사용됨
    
    ```python
    x, y = (10, 20)
    
    print(x)  # 10
    print(y)  # 20
    
    # 파이썬은 쉼표를 튜플 생성자로 사용하니 괄호는 생략 가능
    x, y = 10, 20
    ```
    

### 3. range : 연속된 정수 시퀀스를 생성하는 변경 불가능한 자료형

- **range 표현**
    - range(n) ****: 0 부터 n-1 까지의 숫자의 시퀀스
    - range(n, m) : n 부터 m-1 까지의 숫자 시퀀스
    
    ```python
    my_range_1 = range(5)
    my_range_2 = range(1, 10)
    
    print(my_range_1)  # range(0,5)
    print(my_range_2)  # range(1, 10)
    ```
    
    - 주로 반복문과 함께 사용 예정
    
    ```python
    # 리스트로 형 변환 시 데이터 확인 가능
    print(list(my_range_1))  # [0, 1, 2, 3, 4]
    print(list(my_range_2))  # [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
    ```
    

---

## Non-sequence Types

### 1. dict : key - value 쌍으로 이루어진 순서와 중복이 없는 변경 가능한 자료형

- **딕셔너리 표현**
    - key는 변경 불가능한 자료형만 사용 가능 (str, int, float, tuple, range …)
    - value는 모든 자료형 사용 가능
    - 중괄호 ({}) 로 표기
    
    ```python
    my_dict_1 = {}
    my_dict_2 = {'key': 'value'}
    
    # 딕셔너리의 요소는 ',' 를 기준으로 구분
    my_dict_3 = {'apple': 12, 'list': [1, 2, 3]}  # 2개의 요소
    ```
    
    - key를 통해 value에 접근
    
    ```python
    my_dict = {'apple': 12, 'list': [1, 2, 3]}
    
    print(my_dict['apple'])  # 12
    print(my_dict['list'])  # [1, 2, 3]
    
    # 값 변경
    my_dict['apple'] = 100
    print(my_dict) #  {'apple': 100, 'list': [1, 2, 3]}
    ```
    

### 2. set : 순서와 중복이 없는 변경 가능한 자료형

- **세트 표현**
    - 수학에서의 집합과 동일한 연산 처리 가능
    - 중괄호 ({})로 표기 ( 딕셔너리와 동일)
    
    ```python
    my_set_1 = set()  # 빈 세트는 중괄호 대신 소괄호(())
    my_set_2 = {1, 2, 3}
    my_set_3 = {1, 1, 1}
    
    print(my_set_1)  # set()
    print(my_set_2)  # {1, 2, 3}
    print(my_set_3)  # {1}  #  중복이 없는 것이 특징
    ```
    
    - 순서가 없기 때문에 인덱스가 없음
- **세트의 집합 연산**
    
    ```python
    my_set_1 = {1, 2, 3}
    my_set_2 = {3, 6, 9}
    
    # 합집합
    print(my_set_1 | my_set_2)  # {1, 2, 3, 6 ,9}
    
    # 차집합
    print(my_set_1 - my_set_2)  # {1, 2}
    
    # 교집합
    print(my_set_1 & my_set_2)  # {3}
    ```
    

---

## Other Types

### 1. None : 파이썬에서 ‘값이 없음’ 을 표현하는 자료형

- None 표현
    
    ```python
    variable = None
    print(variable)  # None
    ```
    

### 2. Boolean : 참(True) 과 거짓(False) 을 표현하는 자료형

- 불리언 표현
    - 비교 / 논리 연산의 평가 결과로 사용됨
    - 주로 조건 / 반복문과 함께 사용
    
    ```python
    bool_1 = True
    bool_2 = False
    
    print(bool_1)  # True
    print(bool_2)  # False
    print(3 > 1)  # True
    print('3' != 3)  #True
    ```
    

---

## Collection

→ 여러 개의 항목 또는 요소를 담는 자료 구조

(str, list, tuple, set, dict)

- 컬렉션 정리
    
    
    | 컬렉션 | 변경 가능 여부 | 정렬 여부 |
    | --- | --- | --- |
    | str | X | O |
    | list | O | O |
    | tuple | X | O |
    | set | O | X |
    | dict | O | X |

---

## Type conversion

```python
데이터(값)
자료형 A -----> 자료형 B
        '형변환'
```

1. **암시적 형변환** : 파이썬이 자동으로 형변환을 하는 것
    - 암시적 형변환의 예시
        - Boolean 과 Numeric Type 에서만 가능
        
        ```python
        print(3 + 5.0)  # 8.0
        print(True + 3)  # 4
        print(True + False)  # 1
        ```
        
2. **명시적 형변환** : 
    - 명시적 형변환 예시
        - str → integer : 형식에 맞는 숫자만 가능
        - integer → str : 모두 가능
        
        ```python
        print(int('1'))  # 1
        print(str(1) + '등')  # 1등
        print(float('3.5'))  # 3.5
        print(int(3.5))  # 3
        
        #ValueError: invalid
        print(int('3.5'))
        ```
        

---

## 연산자

- **복합 연산자**
    - 연산과 할당이 함께 이뤄짐
    - +=, -=, *=, /=, //=. **=
    
- **비교 연산자**
    - <, ≤, >, ≥, ==, ≠, is, is not
- **논리 연산자**
    - and, or, not
- **단축평가** : 논리 연산에서 두 번째 피연산자를 평가하지 않고 결과를 결정하는 동작
    - 뒷 부분은 아예 생략이 되어 실행조차 되지 않음
    - 단축평가 예시 문제
    
    ```python
    vowels = 'aeiou'
    
    print(('a' and 'b') in vowels)  # ('a' and 'b') 에서 둘 다 True 이기 때문에 'b' 출력
    print(('b' and 'a') in vowels)  # ('b' and 'a') 에서 둘 다 True 이기 때문에 'a' 출력
    
    print(3 and 5)  # 5
    print(3 and 0)  # 0
    print(0 and 3)  # 0
    print(0 and 0)  # 0
    
    print(3 and 0 and 2)  # 0
    
    print(5 or 3)  # 5
    print(3 or 0)  # 3
    print(0 or 3)  # 3
    print(0 or 0)  # 0
    
    ```
    
    - 단축평가 이유 : 코드 실행을 최적화하고, 불필요한 연산을 피할 수 있도록 함
- **멤버십 연산자** : 특정 값이 시퀀스나 다른 컬렉션에 속하는지 여부를 확인
    - in
    - not in
- **시퀀스형 연산자**
    - + 와  * 는 시퀀스 간 연산에서 산술 연산자일때와 다른 역할을 가짐
    - + : 결합 연산자
    - * : 반복 연산자