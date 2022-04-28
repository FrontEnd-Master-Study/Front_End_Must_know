# Execution Context

### 1. 실행 문맥에 대해서 설명해주세요.(자주 물어보진 않지만 알아둘 것)

<br>

---

<br>

## Anwer

### 🙋‍♀️ 실행 문맥에 대해서 설명해주세요

<br>

### 💁 대답

    실행 문맥은 자바스크립트가 실행되는 문맥으로 추상적인 개념입니다.
    문맥에 따라서 자바스크립트 엔진이 순서와 범위 등 코드를 실행하는데 필요한 정보를 파악합니다.
    하나의 실행문맥이 하나의 실행 구역이기도 합니다.

1.  > 실행 컨텍스트는 소스코드를 실행하는 데 필요한 환경을 제공하고 코드의 실행 결과를 실제로 관리하는 영역이다.
    >
    > 식별자(변수, 함수, 클래스 등의 이름)를 등록하고 관리하는 스코프와 코드 실행 순서 관리를 구현한 내부 메커니즘으로, 모든 코드는 실행 컨텍스트를 통해 실행되고 관리된다.

2.  > 실행 컨텍스트는 전역 컨텍스트와 함수 컨텍스트 두 종류가 있으며,
    >
    > 전역 컨텍스트는 가장 기본이 되는 실행 컨텍스트로 자바스크립트 코드가 처음 실행되면 생성됩니다. 코드 전체의 정보를 가지고,
    >
    > 함수 컨텍스트는 함수가 호출되면 함수 컨텍스트가 실행됩니다.

3.  > 실행 컨텍스트는 **실행컨텍스트 스택**과 **렉시컬 환경**으로 구성됩니다.
    >
    > 실행 컨텍스트 스택은 코드의 실행 순서를 관리하는 자료구조로 LIFO구조로 들어오는 코드를 관리합니다 .
    >
    > 렉시컬 환경은 스코프를 구분하여 식별자를 등록하고 관리하는 저장소 역할을 하는 렉시컬 스코프의 실체입니다.

---

## Execution context

    실행 컨텍스트는 소스코드를 실행하는 데 필요한 환경을 제공하고 코드의 실행 결과를 실제로 관리하는 영역이다.
    모든 코드는 실행 컨텍스트를 통해 실행되고 관리된다.

### **종류**

- 전역 컨텍스트 : 가장 기본이 되는 실행 컨텍스트 , 자바스크립트 코드가 처음 실행되면 생성
- 함수 컨텍스트 : 함수 호출시 생성

  <br>

### **컨텍스트의 4가지 원칙**

- 전역 컨텍스트 하나 생성 후, 함수 호출 시마다 컨텍스트가 생깁니다.
- 컨텍스트 생성 시 컨텍스트 안에 변수객체(arguments, variable), scope chain, this가 생성됩니다.
- 컨텍스트 생성 후 함수가 실행되는데, 사용되는 변수들은 변수 객체 안에서 값을 찾고, 없다면 스코프 체인을 따라 올라가며 찾습니다.
- 함수 실행이 마무리되면 해당 컨텍스트는 사라집니다.(클로저 제외) 페이지가 종료되면 전역 컨텍스트가 사라집니다.

<br>

### **실행 컨텍스트 구조**

![IMG_73379FD8F58A-1](https://user-images.githubusercontent.com/48541850/165704157-1ff4d40c-4db8-4428-841e-1fffe73075b9.jpeg)

---

#### 예시 코드)

```js
var name = "zero";
function wow(word) {
  console.log(word + " " + name);
}
function say() {
  var name = "nero";
  console.log(name);
  wow("hello");
}
say();
```

---

### 전역 컨텍스트

```
- arguments(함수의 인자) X
- variable : 해당 스코프의 변수들
- scope chain : 자기 자신인 전역 변수 객체
- this : 따로 설정 안되어있을시 window (new를 호출하여 변경 가능)
```

객체 형식으로 표현

```js
'전역 컨텍스트': {
변수객체: {
    arguments: null,
    variable: ['name', 'wow', 'say'],
},
scopeChain: ['전역 변수객체'],
this: window,
}
```

전역 실행 컨텍스트에 바인딩된 전역 렉시컬 환경
![image](https://user-images.githubusercontent.com/48541850/165708984-442b46ec-e351-4736-bf47-7d4281a810a2.png)

<br>

### 함수 컨텍스트

```
- arguments: 함수의 인자
- variable : 해당 스코프의 변수들
- scope chain : 자기 자신인 변수객체와 상위의 변수 객체
- this : 따로 설정 안되어있을시 window (new를 호출하여 변경 가능)
```

객체로 표현

- function say() 실행시

```js
'say 컨텍스트': {
  변수객체: {
    arguments: null,
    variable: ['name'], // 초기화 후 [{ name: 'nero' }]가 됨
  },
  scopeChain: ['say 변수객체', '전역 변수객체'],
  this: window,
}
```

- function wow() 실행시

```js
'wow 컨텍스트': {
  변수객체: {
    arguments: [{ word : 'hello' }],
    variable: null,
  },
  scopeChain: ['wow 변수객체', '전역 변수객체'],
  this: window,
}
```

함수 실행 컨텍스트에 바인딩된 함수 렉시컬 환경
![image](https://user-images.githubusercontent.com/48541850/165709013-059b5bb2-efd8-4e7e-9b9a-88ca87d94a0b.png)

## 참고

- [zerocho : 실행 컨텍스트](https://www.zerocho.com/category/JavaScript/post/5741d96d094da4986bc950a0)

- [[ES6] Javascript Execution Context(실행문맥, 실행컨텍스트)](https://velog.io/@kwonh/ES6-Javascript-Execution-Context%EC%8B%A4%ED%96%89%EB%AC%B8%EB%A7%A5-%EC%8B%A4%ED%96%89%EC%BB%A8%ED%85%8D%EC%8A%A4%ED%8A%B8)
