# Evenet Loop

### 1. Event Loop에 대해서 설명해주세요.

### 2. 마이크로 태스크 큐와 태스크 큐에 대해서 설명해주세요.

<br>

# Anwer

## 요약

### 1. Event Loop란

> 싱글 스레드인 JS의 메인 스레드를 관리하는 관리자
>
> 실행 영역인 Call Stack과 콜백 함수가 담기는 Callback Queue를 관리한다.

1. 싱글 스레드인 자바스크립트의 경우 엔진이 메모리 할당을 담당하는 Memory Heap과 코드가 호출되어 스택으로 쌓이는 Call Stack으로 이루어져 있는데 이때 콜 스택에 쌓인 순서대로 코드를 실행하고 제거하게 된다.

2. 이때 비동기 작업의 경우 Web API에게 넘겨주게 된다.
3. Web API는 비동기 작업을 수행하고 콜백 함수를 이벤트 루프를 통해 Call에게 넘겨준다.
4. 이벤트 루프는 Call Stack이 비어있으면 Call를 확인하고 Call에 존재하는 콜백 함수를 Call Stack에 밀어넣어준다.
5. Call Stack에 쌓인 콜백 함수가 실행되고 Call Stack에서 제거된다.

<br>

### 2. 마이크로 태스크 큐 & 태스크 큐

우선 순위 : 마이크로 태스크 큐 > 태스크 큐

- 태스크 큐 : **setTimeout**, setInterval, setImmediate, requestAnimationFrame, I/O, UI 렌더링
- 마이크로 태스크 큐 : **Promise**, process.nextTick, Object.observe, MutationObserver

<br>

---

<br>

## 들어가기 전

- **프로세스**

  - 운영체제가 프로그램의 실행을 위해 프로그램에 메모리를 할당하는 단위

- **스레드**

  - 프로세스가 할당받은 메모리를 실행하는 단위. 하나의 프로세스가 여러 스레드로 나뉠 수 있다.

- **task queue**

  - 콜 스택에 들어가기 전에 setTimeout, 사용자 이벤트 콜백 등이 저장되는 큐

- **microtask queue**

  - Promise.then 콜백이 저장되는 큐

---

<br>

## Event Loop

### 브라우저의 기본 구조

> JS는 단일 스레드 프로그래밍 언어
>
> Call Stack이 하나라는 뜻 (멀티가 되지 않고 하나씩 하나씩 처리한다는 의미)

<br>

<img width="500" alt="JS 엔진" src="https://user-images.githubusercontent.com/48541850/162141123-f21f7ec2-1461-4cc0-a60b-19a0c0a2582a.png"/>

- **JS 엔진**

  > 자바스크립트는 단일 스레드 (sigle thread) 프로그래밍 언어인데, 이 의미는 Call Stack이 하나라는 뜻

  - Memoery Heap : 메모리 할당이 일어나는 곳
  - Call Stack : 코드가 실행될 때 쌓이는 곳 , stack 형태로 쌓임

- **Web API**

  > 브라우저에서 제공하는 API

  - DOM, Ajax, Timeout 등이 있다
  - Call Stack에서 실행된 비동기 함수는 Web API를 호출하고, Web API는 콜백함수를 Callback Queue에 밀어 넣는다

- **Callback Queue**

  > 비동기적으로 실행된 콜백함수가 보관 되는 영역

  - setTimout (1st)
  - addEventListener (2nd)

- **Event Loop**

  > Call Stack과 Callback Queue의 상태를 체크하여, **Call Stack이 빈 상태가 되면, Callback Queue의 첫번째 콜백을 Call Stack으로 밀어넣는다**.

<br>

### 콜 스택

<img width="400" alt="콜스택 과정" src="https://media.vlpt.us/post-images/jakeseo_me/fc418e50-456c-11e9-83dd-8359947fc569/callstack.gif"/>

> 콜스택 과정

<br>

<img alt="콜스택 에러 이미지" width="400" src="https://media.vlpt.us/post-images/jakeseo_me/ce05cad0-472c-11e9-b667-3db1122c69c1/failedStack.png"/>

> 브라우저 콘솔에서 가끔 긴 빨간색 에러 스택들을 본 기억이 있을 것이다.
>
> 보통 그것들은 콜스택의 현재 상태를 나타낸다.
>
> 그리고 실패한 함수를 스택처럼 top부터 bottom까지 나타낸다.

### Event Loop 의 동작

<img src="https://media.giphy.com/media/41qMCw6byUsNjqeie0/giphy.gif?cid=790b76110b521df01c236df35e6f56e004135ad84c50bd9e&rid=giphy.gif&ct=g" />

- T : task queue
- rAF : requestAnimationFrame
- S : Style (렌더 트리 생성)
- L : Layout
- P : Paint

1. 초기 콜 스택에 쌓여있는 task를 모두 처리

   > 처음 html을 가져오고 script 태그를 만나는 순간을 생각해보자.
   >
   > 브라우저 렌더링 과정에 들어가기 전에 동작을 잠깐 멈추고 자바스크립트 코드를 읽기 시작한다.
   >
   > 자바스크립트 코드가 DOM 트리를 수정할 수 있기 때문이다.
   >
   > 이 과정에서 코드들이 콜 스택에 올라가 동작을 수행하게 되고 Promise나 setTimeout과 같은 비동기 관련 콜백들이 queue에 등록된다.

2. Promise.then 콜백이 microtask queue에 등록되어 있다면 실행

   > 처음 콜 스택에 있는 코드들이 모두 실행되고 난 후부터는 Promise가 가장 높은 우선순위를 차지한다.
   >
   > Promise.then 콜백이 등록된 microtask queue는 특징이 하나 있는데, queue에 등록된 모든 콜백이 처리될 때까지 계속 수행한다는 것이다.

3. 화면 갱신이 필요하다면 렌더링 파이프라인으로 이동 (requestAnimationFrame(rAF))

   > 화면 갱신이 필요하다면 이라고 했는데 이는 이벤트 루프가 판단하는 것이다.
   >
   > 사용자가 스크롤 이동을 했거나, 어떤 요소를 클릭했거나 등등 화면을 갱신해야 될 필요가 있다면 렌더링 파이프라인으로 이동한다. (그림 1에서 오른쪽 path)
   >
   > 여기서 자바스크립트 코드 상에 rAF api를 사용하면 이벤트 루프가 모니터 주사율(Hz)에 맞춰 렌더링 파이프라인으로 들어가려고 노력한다.
   >
   > (싱글 스레드이기 때문에 반드시 주기가 지켜지는 것은 아님) 보통은 모니터 주사율이 60Hz기 때문에 화면 갱신 속도도 60fps이고 이는 1프레임이 16ms 정도 나와야 함을 의미한다.
   >
   > 여기서 1프레임이란, 렌더링 파이프라인에 진입했을 때부터 다음 파이프라인 진입까지를 의미한다.

4. task queue에 있는 콜백을 하나씩 실행. (setTimeout)

   > 이제 드디어 setTimeout과 사용자 이벤트 콜백의 시간이다.
   >
   > 그런데 queue에 있는 콜백을 하나씩 실행한다는 것은 무슨 뜻일까.
   >
   > Promise와는 다르게 task queue는 콜백을 하나 실행하고 이벤트 루프를 놓아주어 다른 동작을 수행할 수 있도록 한다는 것이다.
   >
   > 앞서 Promise의 예시와 같이 재귀적으로 setTimeout 콜백을 task queue에 집어넣어도, 브라우저는 정상 작동한다.

## 참고

- [자바스크립트 개발자라면 알아야 할 33가지 개념 #1 콜스택 (번역)](https://velog.io/@jakeseo_me/2019-03-15-2303-%EC%9E%91%EC%84%B1%EB%90%A8-rmjta5a3xh)

- [T.I.L 이벤트루프란 무엇인가? [21.03.23]](https://velog.io/@wnstjr0317/T.I.L-%EC%9D%B4%EB%B2%A4%ED%8A%B8%EB%A3%A8%ED%94%84%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80)

- [자바스크립트 비동기 처리 과정과 RxJS Scheduler](https://sculove.github.io/post/javascriptflow/)

- [](https://velog.io/@thms200/Event-Loop-%EC%9D%B4%EB%B2%A4%ED%8A%B8-%EB%A3%A8%ED%94%84)
