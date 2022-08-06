---
layout: single
title: "TIL"
categories: coding
tag: [python, jekyll, blog]
toc: true
author_profile: false
sidebar:
  nav: "docs"
# search: false
---

오늘은 학습자료와 React 심화반 강의를 봤습니다. Toolkit을 보긴 했지만, 아직 써보질 못해서 잘

모르겠네요. 아마 내일 강의를 어느 정도 보게 되면 toolkit을 써보지 않을까 하네요.

리덕스 툴킷에 대한 것을 정리를 조금 해보았습니다.

리덕스 툴킷 : 우리가 이전에 배운 리덕스를 개량한 것
리덕스를 사용하기 위해 작성했던 duck 패턴의 요소들이 전체적인 코드의 양을 늘림
코드는 더 적게, 그리고 리덕스를 더 편하게 쓰기 위한 기능들을 흡수해서 만든 것

Action Value와 Action Creator를 이제 직접 생성 x
Action Value, Action Creator, Reducer가 하나로 합쳐짐
slice라는 API를 사용 이것을 사용하면 위에 3개를 각각 만들필요 x
slice를 이용하면, Reducer, Action Value, Action Creator를 한번에 구현할 수 있다.

```jsx
const counterSlice = createSlice({
   name: "",  // 이 모듈의 이름
   initialState : {},  // 이 모듈의 초기상태 값
   reducers : {}, // 이 모듈의 Reducer 로직
})

export const counterSlice = createSlice({
  name: "counter",
  initialState,
  reducers : {  // 리듀서 안에 만든 함수 자체가 리듀서 로직이자, Action creator가 된다
  addNumber: (state,action) => {
   state.number = state.number + action.payload;
   },
   minusNumber = (state, action) => {
   state.number = state.number - action.payload;
 },
},
});
export const {addNumber, minusNuber} = counterSlice.actions;
export default counterSlice.reducer;

configStore :
import {createstore} from "redux" -> import {configureStore} from "@reduxjs/toolkit"
combineReducers -> configureStore
store :
const store = configureStore ({
   reducer: {
   counter,
 },
});
```

**Devtools**도 조금 공부해보았습니다.

Redux Devtools
현재 프로젝트의 state 상태라던가, 어떤 액션이 일어났을 때 그 액션이 무엇이고,
그것으로 인해 state가 어떻게 변경되었는지 등 리덕스를 사용하여 개발할 때
아주 편리하게 사용할 수 있다
툴킷을 사용하면, 별도의 설정없이 devtools를 사용할 수 있다.
내장된 주요 패키지 : thunk, devtools, immer 등

**HTTP 프로토콜?**

HTTP는 통신 프로토콜입니다.
프로토콜이란 상호 간에 정의한 규칙을 의미 특정 기기 안에 데이터를 주고받음
웹에서는 브라우저와 서버 간에 데이터를 주고 받기 위한 방식
HTTP 프로토콜은 상태가 없는 (stateless) 프로토콜
상태가 없다는 말은 데이터를 주고 받기 위한 각각의 데이터 요청이 서로 독립적으로 관리가 된다
이전 데이터 요청과 다음 데이터 요청이 서로 관련이 없다
별도의 추가 정보 관리 x, 다수의 요청 처리 및 서버의 부하를 줄일 수 있음
기본 포트는 80번
데이터를 주고받기 위해서는 요청(Request)을 보내고 응답(Response)을 받음
브라우저에서 서버로 Request, 서버에서 브라우저로 Response
클라이언트란 요청을 보내는쪽, 웹 관점에서는 브라우저를 의미함
서버란 요청을 받는 쪽 의미, 데이터를 보내주는 원격지의 컴퓨터를 의미

URL(Uniform Resource Locators)
서버에 자원을 요청하기 위해 입력하는 영문 주소
url 구조
[http://www.domain.com:1234/path/to/resource?a=b&x=y](http://www.domain.com:1234/path/to/resource?a=b&x=y)
pro host port resource path query

HTTP 요청 메서드
요청하는 데이터에 특정 동작 수행하려면 HTTP 요청 메서드를 이용
GET : 존재하는 자원에 대한 요청 // 조회
POST : 새로운 자원을 생성 // 생성
PUT : 존재하는 자원에 대한 변경 // 변경
DELETE : 존재하는 자원에 대한 삭제 // 삭제

HTTP 상태 코드
서버에서 설정해주는 응답 정보
200(성공), 404(실패)로 크게 2가지로 나뉜다

**Promise**
자바스크립트 비동기 처리에 사용되는 객체
비동기 처리란
자바스크립트의 비동기 처리란 특정 코드의 연산이 끝날 때까지 코드의 실행을 멈추지 않고
다음 코드를 먼저 실행하는 자바스크립트의 특성을 의미
비동기 처리의 가장 흔한 사례는 제이쿼리의 ajax입니다.
보통 화면에 표시할 이미지나 데이터를 서버에서 불러와 표시해야 하는데
이때 ajax통신으로 해당 데이터를 서버로부터 가져올 수 있다.
특정 로직의 실행이 끝날 때까지 기다려주지 않고 나머지 코드를 먼저 실행하는 것이 비동기 처리
비동기 처리가 필요한 이유 : 화면에서 서버로 데이터를 요청했을 때 서버가 언제 그 요청에 대한
응답을 줄지도 모르는데 마냥 다른 코드를 실행 안하고 기다릴 순 없기 때문
또 다른 비동기 처리 사례
setTimeout() : Web API의 한 종류
코드를 바로 실행하지 않고 지정한 시간만큼 기다렸다가 로직을 실행
ex)
console.log('Hello')
setTimeout(function() {
console.log('Bye');
}, 3000); // 3000은 3초를 의미 시간을 지정
console.log('Hello Again')
위에서 순서대로 찍히는 것이 아니다.
비동기가 아니라면 Hello -> 3초뒤 Bye -> Hello Again
비동기이기에 Hello -> Hello Again -> 3초가 지났으면 Bye

콜백 함수로 비동기 처리 방식의 문제점 해결하기
위와 같은 문제를 해결하기 위해서 콜백(callback)함수를 이용하면 된다.
콜백 함수 동작 방식 예제
식당 자리 예약과 같다.
일반적으로 맛집을 가면 사람이 많아 자리가 없어 대기자 명단에 이름을 쓴 다음에
자리가 날 때까지 주변 식당을 돌아다니거나 쇼핑을 합니다.
만약 식당에서 자리가 생기면 전화로 자리가 났다고 연락이 옵니다.
그 전화를 받는 시점이 콜백 함수가 호출되는 시점과 같습니다.
자리가 났을 때만 연락이 오기 때문에 미리 가서 기다릴 필요도 없고, 직접 식당 안에 들어가서
자리가 비어 있는 지 확인할 필요도 없습니다. 자리가 준비된 시점, 즉 데이터가 준비된
시점에서만 저희가 원하는 동작(자리에 앉는다, 특정 값을 출력한다 등) 을 수행할 수 있습니다.

**콜백 지옥 (Callback hell)**
콜백 지옥은 비동기 처리 로직을 위해 콜백 함수를 연속해서 사용할 때 발생하는 문제
서버에서 데이터를 받아와 화면에 표시하기까지 인코딩, 사용자 인증 등을 처리해야 하는 경우가 있습니다.
만약 이 모든 과정을 비동기로 처리해야 한다고 하면 콜백 안에 콜백을 계속 무는 형식으로
코딩을 하게 되는데 이러한 코드 구조는 가독성도 떨어지고 로직을 변경하기도 어렵습니다.
이와 같은 코드 구조를 콜백 지옥이라고 합니다.
해결 방법
Promise나 Async를 사용하는 방법이 있습니다
코딩 패턴으로만 콜백 지옥을 해결하려면 콜백 함수를 분리해주면 됩니다.

이제 Promise를 공부해 봅시다.
Promise는 자바스크립트 비동기 처리에 사용되는 객체
주로 서버에서 받아온 데이터를 화면에 표시할 때 사용
프로미스의 3가지 상태(states)
상태란? 프로미스의 처리 과정을 의미 new Promise()로 프로미스를 생성하고 종료될 때까지
3가지 상태를 갖습니다
Pending(대기) : 비동기 처리 로직이 아직 완료되지 않은 상태
Fulfilled(이행) : 비동기 처리가 완료되어 프로미스가 결과 값을 반환해준 상태
Rejected(실패) : 비동기 처리가 실패하거나 오류가 발생한 상태
Pending(대기)
new Promise() 메서드를 호출하면 대기 상태가 됩니다.
new Promise();
메서드를 호출할 때 콜백 함수 선언할 수 있고, 콜백 함수의 인자는 resolve, reject입니다
new Promise(function(resolve, reject) {
//
});
**Fulfilled(이행)**
콜백 함수의 인자 resolve를 아래와 같이 실행하면 이행상태가 됩니다
new Promise(function(resolve, reject) {
resolve();
});
그리고 이행 상태가 되면 아래와 같이 then()을 이용하여 처리 결과 값을 받을 수 있습니다.
function getDate() {
return new Promise(function(resolve, reject) {
var date = 100;
resolve(data);
});
} // resolve()의 결과 값 data를 resolvedData로 받음
getData().then(function(resolvedData) {
console.log(resolvedData); // 100
});
Rejected(실패)
new Promise()로 프로미스 객체를 생성하고 reject를 사용하여 아래와 같이 호출하면
실패(Rejected) 상태가 됩니다
new Promise(function(resolve, reject) {
reject();
});
실패 상태가 되면 실패한 이유(실패 처리의 결과 값)를 catch()로 받을 수 있습니다.
function getData() {
return new Promise(function(resolve, reject) {
reject(new Error("Request is failed"));
});
}
// reject()의 결과 값 Error를 err에 받음
getData().then().catch(function(err) {
console.log(err); // Error : Request is failed
});

여러 개의 프로미스 연결하기 (Promise Chaining)
여러 개의 프로미스를 연결하여 사용할 수 있다.
then()메서드를 호출하고 나면 새로운 프로미스 객체가 반환됩니다.
function getData() {
return new Promise({
// ...
});
}
// then()으로 여러개의 프로미스를 연결한 형식
getData()
.then(function(data) {
// ...
})
.then(function() {
//...
})
.then(function() {
// ...
});
ex)
new Promise(function(resolve, reject) {
setTimeout(function() {
resolve(1); // setTimeout()을 이용해 2초 후에 resolve(0를 호출
}, 2000);
})
.then(function(result) {
console.log(result); // 1 // resolve()가 호출되면 프로미스가 대기 상태에서 이행상태로 넘어감
return result + 10; 첫번째 .then()의 로직으로 넘어감
}) 첫번째와 마찬가지로 계속해서 그 다음 .then()으로 넘겨줌
.then(function(result) { 최종적으로 .then()에서 31값을 출력
console.log(result); // 11
return result + 20;
})
. then(function(result) {
console.log(result); // 31
});

프로미스의 에러 처리 방법

1. then()의 두 번째 인자로 에러를 처리하는 방법
   getData().then(
   handleSuccess,
   handleError
   );
2. catch()를 이용하는 방법
   getData().then().catch();
   프로미스의 reject() 메서드가 호출되어 실패 상태가 된 경우에 실행
   가급적 catch()로 에러를 처리하는 게 더 효율적

**async & await**
자바스크립트의 비동기 처리 패턴 중 가장 최근에 나온 문법
기존의 비동기 처리 방식인 콜백 함수와 프로미스의 단점을 보완하고 개발자가 읽기
좋은 코드를 작성할 수 있게 도와줍니다.
ex)
async function logName() {
var user = await fetchUser('[domain.com/users/1](http://domain.com/users/1)'); // fetchUser() 서버에서 데이터를 받아노는 HTTP통신코드라고 가정
if ([user.id](http://user.id/) === 1) {
console.log([user.name](http://user.name/));
}
}
async & await 기본 문법
async function 함수명() {
await 비동기*처리*메서드\_명();
}
먼저 함수의 앞에 async 라는 예약어를 붙입니다. 그러고 나서 함수의 내부 로직 중
HTTP 통신을하는 비동기 처리 코드 앞에 await를 붙입니다.
async await 문법을 이용하면 기존의 비동기 처리 코드 방식으로 사고하지 않아도 되는 장점이 있다.

async & await 예외 처리
예외를 처리하는 방법은 바로 try catch입니다.
프로미스에서 에러 처리를 위해 .catch()를 사용했던 것처럼 async에서는 catch{}를 사용

이 정도 공부해봤습니다. 아직 잘 모르겠네요! 더 더 더 열심히 공부해보겠습니다!

공부하면서도 부족한 것들이 너무 많다는 것을 느꼈습니다!!!!! 더욱 더 화이팅하겠습니다!

### 😂 참고

[자바스크립트 Promise 쉽게 이해하기](https://joshua1988.github.io/web-development/javascript/promise-for-beginners/)

[자바스크립트 async와 await](https://joshua1988.github.io/web-development/javascript/js-async-await/)

[자바스크립트 비동기 처리와 콜백 함수](https://joshua1988.github.io/web-development/javascript/javascript-asynchronous-operation/)

[프런트엔드 개발자가 알아야하는 HTTP 프로토콜 Part 1](https://joshua1988.github.io/web-development/http-part1/)
