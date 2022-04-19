# Restful API

### Restful API에 대해 아는대로 설명해주세요.

<br>

---

<br>

## Anwer

### 요약

- Rest : 웹에 존재하는 모든 자원(이미지, 동영상, DB 자원)에 고유한 URI를 부여해 활용하는것 HTTP URI를 통해 자원을 명시하고 HTTP Method를 통해 해당 자원에 대한 CRUD Opetaion을 적용

- Rest 구성 요소 : 자원(URI),행위(Method),표현(서버가 응답으로 보내주는 자원의 상태)

- RESTful : Rest의 형식을 따른 시스템

- RESTful API 디자인 가이드

  1. URI는 정보의 자원을 표현해야 한다

  2. 자원에 대한 행위는 HTTP Method(GET,POST,PUT,DELETE)로 표현한다.

## <br>

### REST의 개념

> ### **Representational State Transfer**의 약자
>
> 자원을 이름(자원의 표현)으로 구분하여 해당 자원의 상태(정보)를 주고 받는 모든 것을 의미 _(자원: 해당 소프트웨어가 관리하는 모든것)_
>
> 웹의 기존 기술과 HTTP 프로토콜을 그대로 활용하기 때문에 웹의 장점을 최대한 활용할 수 있는 아키텍처 스타일

<img width="75%" src="https://user-images.githubusercontent.com/48541850/163925203-2e9eac26-c09b-4364-b7c9-59ca098f4eb9.png">

**REST의 구체적인 개념**

- HTTP URI를 통해 자원을 명시, HTTP Method를 통해 자원에 대한 CRUD Operation을 적용하는 것을 의미
- 자원 기반의 구조(ROA,Resource _Oriented Architecture_) 설계의 중심에 Resource(자원)가 있고 HTTP Method를 통해 Resource를 처리하도록 설계된 아키텍처

**API(Application Programming Interface)란**

데이터와 기능의 집합을 제공하여 컴퓨터 프로그램간 상호작용을 촉진하며, 서로 정보를 교환가능 하도록 하는 것

<br>

**CRUD Opeartion**
| 명령 | 역할 (HTTP Method) |
| ------ | ----------------------- |
| Create | 생성 (POST) |
| Read | 조회 (GET) |
| Update | 수정(PUT) |
| Delete | 삭제 (DELETE) |
| HEAD | header 정보 조회 (HEAD) |

### REST 구성

- **자원** (RESOURCE) : URI
- **행위** (Verb): HTTP METHOD
- **표현** (Representations) : 서버가 응답으로 보내주는 자원의 상태

(_URI는 식별하고, URL은 위치를 가르킨다_)

### REST의 특징

**1. 클라이언트 / 서버 구조**

- 자원이 있는 Server, 지원을 요청하는 Client의 구조를 가진다.

**2. 무상태 (Stateless)**

- HTTP Stateless 프로토콜 이므로 REST 역시 무상태성을 가짐. 클라이언트의 Context를 서버에 저장하지 않음.

**3. 캐시 처리 가능**

- 웹 표준 HTTP 프로토콜을 그대로 사용하므로 웹에서 사용하는 기존의 인프라를 그대로 활용 가능.

**4. 계층화**

- API서버는 순수 비즈니스 로직을 수행하고 그 앞단에 사용자 인증, 암호화, 로드밸런싱 등을 하는 계층을 추가하여 구조상의 유연성을 줄 수 있다.

**5. 인터페이스 일관성**

- URI로 지정한 자원에 대한 조작을 통일되고 한저엊ㄱ인 인터페이스로 수행한다. HTTP 표준에만 따른다면 모든 플랫폼에서 사용 가능

**6. 자체 표현 구조**

- 동사(Method) + 명사(URI)로 이루어져있어 어떤 메서드에 무슨 행위를 하는지 알 수 있으며 REST API 자체가 매우 쉬워서 API 메세지 자체만 보고도 API를 이해할 수 있음

<br>

### REST의 장단점

| 장점                               | 단점          |
| ---------------------------------- | ------------- |
| 쉬운 사용                          | 메소드의 한계 |
| 클라이언트-서버 역할의 명확한 분리 | 표준이 없음   |
| 특정 데이터 표현을 사용 가능       |               |

### REST API 디자인 가이드

❗️ **매우 중요**

> **1. URI는 정보의 자원을 표현해야 한다**
>
> **2. 자원에 대한 행위는 HTTP Method(GET,POST,PUT,DELETE)로 표현한다.**

<img width="70%" src="https://user-images.githubusercontent.com/48541850/163947184-a924bed0-42ee-4d2a-a467-d2dc62ae52c8.png">

<br>

#### **REST API 중심 규칙 예시**

- ❗️잘못된 예시

  ```
  GET /members/delete/1
  ```

- ✅ 올바른 예시
  ```
  DELETE /members/1
  ```
  _(자원에 대한 행위는 HTTP Method(GET,POST,PUT,DELETE)로 표현한다)_

<br>

### URI 설계시 주의 사항

1. **슬래시 구분자(/)는 계층 관계를 나타내는 데 사용**

   ```
   http://restapi.example.com/houses/apartments
   http://restapi.example.com/animals/mammals/whales
   ```

<br>

2. **URI 마지막 문자로 슬래시(/)를 포함하지 않는다**.

   URI에 포함되는 모든 글자는 리소스의 유일한 식별자로 사용되어야 하며 URI가 다르다는 것은 리소스가 다르다는 것이고, 역으로 리소스가 다르면 URI도 달라져야 합니다.

   REST API는 분명한 URI를 만들어 통신을 해야 하기 때문에 혼동을 주지 않도록 URI 경로의 마지막에는 슬래시(/)를 사용하지 않습니다.

   ```
   http://restapi.example.com/houses/apartments/ (X)
   http://restapi.example.com/houses/apartments  (0)
   ```

<br>

3. **하이픈(-)은 URI 가독성을 높이는데 사용**

   URI를 쉽게 읽고 해석하기 위해, 불가피하게 긴 URI경로를 사용하게 된다면 하이픈을 사용해 가독성을 높일 수 있습니다.

<br>

4. **밑줄(\_)은 URI에 사용하지 않는다**.

   글꼴에 따라 다르긴 하지만 밑줄은 보기 어렵거나 밑줄 때문에 문자가 가려지기도 합니다. 이런 문제를 피하기 위해 밑줄 대신 하이픈(-)을 사용하는 것이 좋습니다.(가독성)

<br>

5. **URI 경로에는 소문자가 적합하다.**

   URI 경로에 대문자 사용은 피하도록 해야 합니다. 대소문자에 따라 다른 리소스로 인식하게 되기 때문입니다.

   RFC 3986(URI 문법 형식)은 URI 스키마와 호스트를 제외하고는 대소문자를 구별하도록 규정하기 때문이지요.

   ```
   RFC 3986 is the URI (Unified Resource Identifier) Syntax document
   ```

<br>

6. **파일 확장자는 URI에 포함시키지 않는다.**

   ```
   http://restapi.example.com/members/soccer/345/photo.jpg (X)
   ```

   REST API에서는 메시지 바디 내용의 포맷을 나타내기 위한 파일 확장자를 URI 안에 포함시키지 않습니다. Accept header를 사용하도록 합시다.

   ```
   GET / members/soccer/345/photo HTTP/1.1 Host: restapi.example.com Accept: image/jpg
   ```

<br>

### 기타 참고 사항

리소스간의 관계를 표현하는 방법

    ```
    /리소스명/리소스 ID/관계가 있는 다른 리소스명

    ex) GET : /users/{userid}/devices (일반적으로 소유 ‘has’의 관계를 표현할 때)
    ```

자원을 표현하는 Collection과 Document

    ```
    http:// restapi.example.com/sports/soccer/players/13

    (sports, players 컬렉션과 soccer, 13(13번인 선수)를 의미하는 도큐먼트)
    ```

## 참고

- [[Network] REST란? REST API란? RESTful이란?](https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html)
- [NHN Cloud - REST API 제대로 알고 사용하기](https://meetup.toast.com/posts/92)
- [REST란?](https://hckcksrl.medium.com/rest%EB%9E%80-c602c3324196)
