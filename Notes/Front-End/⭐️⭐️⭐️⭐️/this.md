# this

### this의 용법 아는대로 설명해주세요.

<br>

---

<br>

## Anwer

## This

    자신이 속한 객체 또는 자신이 생성할 인스턴스를 가리키는 자기 참조 변수(self-reference variable)입니다.

### this 바인딩이란?

바인딩이란 식별자(변수)와 값(원시 값 또는 객체)을 연결하는 과정을 의미한다.

예를 들어, 변수 선언은 변수 이름(식별자)과 확보된 메모리 공간의 주소를 바인딩하는 것이다.

this 바인딩은 this(키워드로 분류되지만 식별자 역할을 한다)와 this가 가리킬 객체를 바인딩하는 것이다.

<br>

### this 용법

- 기본 바인딩 (전역 객체)
- 암시적 바인딩
- 명시적 바인딩
- new 바인딩

| 함수 호출 방식                                             | this 바인딩                                                            |
| ---------------------------------------------------------- | ---------------------------------------------------------------------- |
| 일반 함수 호출                                             | 전역 객체(window/ global)                                              |
| 콜백 함수 호출                                             | 전역 객체(window/ global)                                              |
| 내부 함수 호출                                             | 전역 객체(window/ global)                                              |
| 메서드 호출                                                | 메서드를 호출한 객체                                                   |
| 생성자 함수                                                | 호출 생성자 함수가 (미래에) 생성할 인스턴스                            |
| Function.prototype.apply/call/bind 메서드에 의한 간접 호출 | Function.prototype.apply/call/bind 메서드에 첫 번째 인수로 전달한 객체 |

## 참고

- [zerocho : 자바스크립트의 this는 무엇인가?](https://www.zerocho.com/category/JavaScript/post/5b0645cc7e3e36001bf676eb)
- [자바스크립트 this의 4가지 동작 방식](https://yuddomack.tistory.com/entry/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-this%EC%9D%98-4%EA%B0%80%EC%A7%80-%EB%8F%99%EC%9E%91-%EB%B0%A9%EC%8B%9D)
