# 관통 프로젝트

## 실습 목표

: 파이썬으로, **인터넷에 있는 날씨 정보**를 가져와, 내가 원하는 정보만 출력

## 날씨 정보

- 실습 프로젝트를 진행하기 위해선 날씨 데이터가 있어야 한다.
- 그러나 직접 데이터를 모으기엔 너무 어렵다.
- 간단하게, 인터넷에 있는 데이터를 가져오면 된다
    - 데이터를 가져오는 방법을 이해하기 위해서 반드시 알아야 할 전문용어들이 있다.

### 전문용어 이해하기

- 서버와 클라이언트
- 서버 : 부탁을 받으면 처리해주거나, 부탁대로 원하는 값을 돌려주는 역할
- 클라이언트 : 부탁을 하는 역할

```python
서버 <-----> 클라이언트
```

- 우리가 네이버 홈페이지에 접속하는 것은 다음과 같이 표현 가능
    - 네이버 주소를 입력하면 익히 알고 있는 네이버 메인 화면을 달라고 요청한다.
    - 서버는 클라이언트가 요청한 네이버 메인 화면을 돌려준다.

```python
서버 (네이버 서버) <-----> 클라이언트
```

- 이번 프로젝트에서는 날씨 정보가 필요하다.
    - 날씨 정보를 가지고 있는 서버가 있다.
    - 해당 서버에 날씨 정보를 달라고 요청하면 된다.

```python
서버 (날씨 정보를 가지고 있는 서버) <-----> 클라이언트
							날씨 정보 제공 --->           <--- 날씨 정보 요구
```

- 정리하면 다음과 같다.
    - 클라이언트가 정보를 달라고 요청
    - 서버는 클라이언트의 요청에 따라 원하는 정보를 돌려줌
- **클라이언트는 어떻게 요청을 보낼 수 있을까**
    1. 웹 브라우저 (ex. 크롬) 를 켜서 주소창에 주소(URL)를 입력
        
        ```python
        # 테스트용 더미 데이터
        https://fakestoreapi.com/carts
        ```
        
    2. 서버에 정보를 요청하는 파이썬 코드를 작성
        - vscode를 켜고, 터미널 창을 연다
        - 아래 명령어를 실행하여 필요한 도구를 설치
        
        ```bash
        $ pip install requests
        ```
        
        ### 파이썬 코드 이해하기
        
        - url : 요청을 보내는 서버의 주소
        - requests.get(url)
            
            : 해당 서버(url)에 데이터를 달라고 요청을 보내는 함수
            
        - .json()
            
            : 내부의 데이터를 JSON (파이썬의 딕셔너리와 비슷함) 형태로 변환해주는 함수
            
- **서버는 어떻게 요청을 해석할까**
    - 서버에 요청을 보내는 클라이언트는 매우 다양하다
        - 클라이언트들은 각자 다른 방식으로 요청을 보낸다
    - 서버가 어떻게 모두 해석할 수 있을까
    - 

### API

- 클라이언트가 원하는 기능을 수행하기 위해서 서버 측에 만들어 놓은 프로그램
    - 기능 예시 : 데이터 저장, 조회, 수정, 삭제 등등
- 서버 측에 특정 주소로 요청이 오면 정해진 기능을 수행하는 API를 미리 만들어 둔다.
    - 클라이언트는 서버가 미리 만들어 놓은 주소로 요청을 보낸다.
    
    ```bash
    내 코드      <--------->      API      <--------->      DATA
      요청--->      <---데이터 전달  데이터 검색--->  <--- 데이터 조회
    ```
    

### 날씨 정보를 제공해주는 API

- 날씨 정보를 수집하기 위해서는 두 가지를 찾아야 한다
    - 날씨 정보를 가지고 있는 서버
    - 해당 서버가 제공하는 API

### 오픈 API

- 외부에서 사용할 수 있도록 무료로 개방 (OPEN) 된 API
- 사용법은 공식 문서 (Docs) 에 명시되어 있다.
- 프로젝트에서 사용되는 API
    - OpenWeatherMap API
        
        : 기상 데이터 및 날씨 정보를 제공하는 오픈 API
        
    - 금융상품통합비교공시 API
        
        : 금융감독원에서 제공하는 금융 상품 정보를 제공하는 오픈 API
        

### 오픈 API 특징 및 주의사항

- 악성 사용자가 무수한 계정을 생성해 API 에 요청을 보내는 경우를 방지하기 위해 오픈 API 는 **API KEY** 를 활용하여 사용자를 확인
    - 사용자 인증 혹은 회원가입을 하면 서버에서 API KEY를 발급
    - 서버에 요청할 때 마다 해당 API KEY 를 함께 보내 정상적인 사용자인 것을 확인 받는다.
- API KEY 를 가지고 있는 악성 사용자가 단시간에 무수한 요청을 보내는 상황을 방지하기 위하여 일부 오픈 API 는 **사용량이 제한**되어 있다.
    - 사용량이 초과될 경우 요금이 청구될 수 있다.

## 날씨 데이터 수집

### JSON

- API가 반환하는 데이터는 어떻게 생겼을까?

### API 가 사용하는 데이터 형식 - JSON

- JavaScript Object Notation 의 약자로 자바스크립트 객체 표기법
- 데이터를 저장하거나 전송할 때 많이 사용되는 **경량의 텍스트 기반의 데이터 형식**
- 통식 방법이나 프로그래밍 문법이 아니라 단순히 데이터를 표현하는 표현 방법 중 하나
- 특징
    - 데이터는 중괄호({}) 로 둘러싸인 키-값 쌍의 집합으로 표현됨
    - 키 = 문자열 / 값 = 다양한 데이터 유형을 가질 수 있다.
    - 값은 쉼표 (,)로 구분됨
    
    ```python
    import json  # 내장 모듈
    
    # json 데이터
    json_data = '''
    {
    	"name": "홍길동",
    	"age": 28,
    	"city": "서울",
    	"hobbies": [
    		"공부하기",
    		"복습하기"
    	],
    	"isStudent": true
    }
    '''
    
    # 문자열을 딕셔너리로 변환 json.loads()
    data = json.loads(json_data)
    
    # JSON 데이터에서 원하는 데이터만 가져오기
    name = data.get('name')
    
    print(name)
    ```
    
    - 파이썬은 JSON을 활용하는 기능을 가지고 있음
    - 참고
        - 파싱 (Parsing)
            
            : 데이터를 의미 있는 구조로 분석하고 해석하는 과정
            
            (데이터를 원하는 형태로 변환)
            
        - json.loads()
            
            : JSON 형식의 문자열을 파싱하여 Python Dictionary로 변환
            

### Openweathermap API

- 기상 데이터 및 날씨 정보를 제공하는 오픈 API
- 전세계 날씨 데이터를 가져와 날씨, 일일 및 시간 별 예보 등 다양한 정보를 얻을 수 있다
- API 사용량 제한