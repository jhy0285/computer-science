# JSON

## JSON이란?
JSON(JavaScriptObjectNotation)은 **javascript 객체 문법**으로
구조화된 **문자(텍스트) 기반의 데이터 교환 형식**을 말합니다. 

python, javascript, java등 여러언어에서 데이터교환형식으로 쓰이며, 객체문법으로 표현하는 것
말고도 배열, 문자열도 표현 가능합니다.

형식은 중괄호({}) 안에 Key : Value 형식으로 들어가는 형식입니다.

[JSON 구조 참조](https://www.json.org/json-en.html)

아래는 JSON에 대한 대표적인 특징과 설명입니다.


### 1. 키 충돌이 일어날 경우, 선언시의 제일 밑에있는(제일최근에 입력한) </br></br> Value 값이 살아남는다.
중복키 떄문에 키 충돌이 일어날 경우, 선언시의 제일 밑에있는(제일최근에 입력한)
 Key : Value 쌍이 살아남습니다.

```json
{
 "name" : "kundol",
 "name" : "King",
 "age" : 30
}
```
위에 예시에서는 name이라는 키 값이 중복되는데,
이때 밑에있는 쌍인 "name" : "King" 쌍이 살아남습니다.

### 2. 자바스크립트 객체와의 차이점
JSON은 기본적으로 자바스크립트 객체 문법을 기반으로 하기 떄문에, 유사한 점이 많지만, 차이점도 존재합니다.

1. 자바스크립트객체에서 키(KEY)값은 따옴표 없이 쓸 수 있지만, <br/> JSON에서는 반드시 쌍따옴표를 붙여야 합니다.
```json
JS object의 경우
{   
    name : "Young Jin",
    age : 25
};
//따옴표 없이 KEY값 선언 가능
        
JSON의 경우
{   
    "name" : "Young Jin",
    "age" : 25
};
//반드시 쌍따옴표만으로 KEY값 선언 가능
```
2. 자바스크립트객체에서 문자열 값은 어떠한 형태의 따옴표도 사용 가능('' ,"" 모두가능) 
하지만 <br/>  JSON에서는 반드시 쌍따옴표로 감싸야 합니다.
```json
JS object의 경우
{   
    name : "Young Jin",
    gender : 'male'
};
//문자열 선언시 '', "" 모두가능
        
JSON의 경우
{   
    "name" : "Young Jin",
    "age" : "male"
};
//문자열 선언시 반드시 ""만 가능
```
3. javascript object와 유사합니다만 undefined, 메서드 등을 포함할 수 없습니다. <br/> 
즉, 문자열(string), 숫자(number), 불리언(boolean), 배열(array), 객체(object), null 은 가능합니다.
```json
### JS object ###
let person = {
  "name": "John",
  "age": 30,
  "isStudent": false,
  "hobbies": ["reading", "sports"],
  "address": {
    "city": "New York",
    "zipcode": "10001"
  },
  "sayHello": function() {
    console.log("Hello!");
  },
  "sayBye" : undefined
};
//JSobject에 경우 sayHello 라는 메서드와 sayBye라는 undefined를  값으로 가지고 있음

### JSON ###
let person = {
  "name": "John", //String 가능
  "age": 30, //number 가능
  "isStudent": false, //boolean 가능
  "hobbies": ["reading", "sports"], //array 가능
  "address": { //object가능
    "city": "New York",
    "zipcode": "10001"
  },
    // 그러나 메서드, undefined는 사라짐
};
//즉, JSON으로 변환 할 경우 sayHello, sayBye 사라짐
```
그리고 예시에는 없지만 JSON은 null도 값으로 가질 수 있습니다!

### 3. 직렬화와 역직렬화
1. 직렬화(Serialization)
- 직렬화는 데이터 구조나 객체를 파일이나 네트워크를 통해 **전송 가능한 형태로 변환**하는 과정을 의미합니다.
- 이 과정에서 객체는 바이트 스트림, 텍스트 문자열 또는 다른 형태로 변환됩니다
- 예를들어 JS진영에서는 JS object를 JSON String으로 변환(직렬화)해서 HTTP통신에 사용합니다.
```javascript
//JavaScript 객체선언
const data = {
 name: 'Alice',
 age: 25,
 isStudent: true,
};

// JavaScript 객체를 JSON 문자열로 변환(직렬화)합니다.
const jsonData = JSON.stringify(data);

// 출력 : '{"name":"Alice","age":25,"isStudent":true}'
console.log(jsonData)
```
- Python 진영에서는 key : value의 해쉬테이블인 Dictionary 타입의 자료형을 </br> JSON String으로 변환(직렬화)해서 HTTP통신에 사용합니다.
```python
import json

# 요청에 포함할 JSON 데이터 (Python 사전 형태)
data = {
    "name": "Alice",
    "age": 25,
    "isStudent": True,
}

# Python 사전을 JSON 문자열로 직렬화
json_data = json.dumps(data)

# 출력 : '{"name": "Alice", "age": 25, "isStudent": true }'
print(json_data)
```

2. 역직렬화(Deserialization)
- 역직렬화는 직렬화된 데이터를 다시 원래의 데이터 구조나 객체로 변환하는 과정입니다.
- 예를 들어 JS진영에서는 JSON데이터를 JS object 파일로 변환(역직렬화)해서 사용합니다.
```javascript
// JSON 문자열 선언
const jsonString = '{"name": "Alice", "age": 25, "isStudent": true}';

// JSON 문자열을 JavaScript 객체로 역직렬화
const parsedData = JSON.parse(jsonString);

// 역직렬화된 데이터 사용
console.log(parsedData.name);        // 출력: Alice
console.log(parsedData.age);         // 출력: 25
console.log(parsedData.isStudent);   // 출력: true
```
- 파이썬에서는 JSON데이터를 key : value의 해쉬테이블인 dict 형식으로 변환(역직렬화)해서 사용합니다.
```python
import json

# JSON 형식의 문자열
json_string = '{"name": "Alice", "age": 25, "isStudent": true}'

# JSON 문자열을 파이썬의 데이터 구조로 역직렬화
data = json.loads(json_string)

# 역직렬화된 데이터 사용
print(data['name'])  # 출력: Alice
print(data['age'])   # 출력: 25
print(data['isStudent'])  # 출력: True
```

### 4. 재귀적인 구조를 가지고 있다.

당연하지만, key : value 쌍에서 이 value 값이 다시 
key : value 쌍일 수 있고, 이는 계속 재귀적으로 가능하다.


```json
  {
    "name" : {
        "firstname" : "no",
        "lastname" : "hongchul"
    },
    "age" : 30
  }
//name안에 firstname, lastname처럼 재귀적으로 선언 가능
```
### 5. Array 형식으로도 가능하다
JSON 데이터를 배열형식으로 여러개 가질수 있는데, 이를 
JSON Array라고 한다.
```json
[
 {
  "name" : {
   "firstname" : "no",
   "lastname" : "hongchul"
  },
  "age" : 30
 },
 
 {
  "name" : {
   "firstname" : "cho",
   "lastname" : "youngjin"
  },
  "age" : 35
 },
],
// 배열형식으로 여러 JSON 객체 가질수 있음
```

# XML

## XML이란?
XML(Extensible Markup Language)은 데이터를 저장하고 전송하기 위해 마크업 언어를 쓰는 데이터 교환 형식입니다.

### 1. 마크업 이란?

마크업은 문서나 데이터의 구조를 표현하기 위해 일정한 규칙에 따라 특정 **표시나 태그를 사용**하여 문서를 작성하는 것입니다

마크업을 사용하는 MarkUp Language로는 대표적으로 HTML과 XML이 있습니다.

### 2. XML 구성
XML은 
1. 프롤로그 : XML문서의 버전과 인코딩을 지정하는 부분입니다.
2. 루트요소(단 하나만) : XML 문서의 최상위 요소이며, 하나의 단일한 루트 요소만을 가집니다.
3. 하위 요소들 : 루트 요소 안에 포함되는 구조화된 데이터의 요소들입니다. </br> 각각은 또 다른 하위 요소들을 포함할 수도 있습니다.

이렇게 구성되어 있습니다.
```xml
<!-- 프롤로그(Prologue) -->
<?xml version="1.0" encoding="UTF-8"?>
<!-- 루트 요소 -->
<OSTList> 
    <!-- 하위 요소들 -->
    <OST1>
        <!-- 내용 -->
     <name>마녀 배달부 키키</name> 
     <song>따스함에 둘러쌓인다면</song>
    </OST1>
 
    <!-- 하위 요소들 -->
    <OST2>
        <!-- 내용 -->
     <name>하울의 움직이는 성</name> 
     <song>세계의 약속</song>
    </OST2>
 
</OSTList>
```

### 3. HTML과 XML 비교
- HTML의 용도는 데이터를 표시 / XML은 데이터를 저장 및 전송이 목적입니다.
- HTML에는 미리 정의된 태그가 있지만 사용자는 XML에서 고유한 태그를 만들고 정의 가능 합니다.
- XML은 대/소문자를 구분하지만 HTML은 구분하지 않습니다.</br> 즉 XML에서
```<book>``` 대신 ```<Book>```으로 태그를 작성하면 XML 구문 분석기에서 오류가 발생합니다

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<meta name="viewport" content="width=device-width,
initial-scale=1.0">
<title>Document</title>
</head>
<body>
<p></p>
<div></div>
</body>
</html>
```
HTML은 위처럼 ```<head>``` , ```<body>```,```<p>``` , ```<div>``` 처럼 미리 정의된 태그만을 사용해야 됩니다.

### 4. sitemap.xml
xml은 대표적으로 sitemap.xml에 쓰입니다.

sitemap.xml은 웹 사이트의 구조와 콘텐츠를 검색 엔진에 제공하기 위한 파일입니다.

이 파일은 웹 페이지의 계층 구조, 각 페이지의 중요도, 최근 업데이트된 페이지 등을 검색 엔진에 알려주는 역할을 합니다.

sitemap.xml을 작성하는 이유는 아래와 같은 이유들이 있습니다.

- 검색엔진에게 사이트맵을 알려줌으로서  SEO(검색 엔진 최적화)에 이점을 줄수 있습니다.
 >(SEO 하는 이유) : 구글이라는회사에 데이터베이스에 저의 서비스의 페이지들이 저장되어있다.</br>
    => 이 저장된 정보들을 바탕으로 뭔가를 검색했을떄 어떤 알고리즘을 통해서
  노출되는것이다 </br>=> 이떄 알고리즘을 우리가 건들수는 없으니 검색이 잘되도록 최적화 시키는 노력을 하는 것이다.

- 사이트가 매우 크거나 서로 링크가 종속적으로 연결되지 않은 경우 크롤러가 일부 페이지를
  누락하는 일이 있는데 </br>
  이를 sitemap.xml이 방지하고 모든 페이지들을 크롤링할 수 있도록
  해줍니다.

### 5. JSON과 XML 비교

일반적으로 JSON이 XML보다 용량 측면에서 더 가볍습니다. 

이는 JSON이 불필요한 태그를 사용하지 않고 데이터를 더 간결하게 표현하기 때문입니다.

JSON은 데이터를 효율적으로 표현하기 위해 중괄호와 배열 등의 간단한 구조를 사용하며,

이로 인해 더 적은 용량을 차지합니다. 

XML은 태그들로 감싸인 구조로 데이터를 표현하기 때문에 일반적으로 JSON보다 용량이 더 크게 나타날 수 있습니다.

JSON
```json
{
"지브리OST리스트" : [
    {
      "name" : "마녀 배달부 키키",
      "song" : "따스함에 둘러쌓인다면"
    },
    {
       "name" : "하울의 움직이는 성",
       "song" : "세계의 약속"
    }
  ]
}
```

XML
```xml
<?xml version="1.0" encoding="UTF-8"?>
<OSTList>
 <OST>
  <name>마녀 배달부 키키</name> <song>따스함에 둘러쌓인다면</song>
 </OST>
 <OST>
  <name>하울의 움직이는 성</name> <song>세계의 약속</song>
 </OST>
</OSTList>
```

위의 예시처럼 같은 내용의 데이터를 가지고 있어도 XML이 열고 닫는 태그가 추가되서 일반적으로 더 무겁습니다.