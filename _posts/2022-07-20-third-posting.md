---
layout: single
title: "React 과제2"
categories: coding
tag: [python, jekyll, blog]
toc: true
author_profile: false
sidebar:
  nav: "docs"
# search: false
---

# JavaScript의 객체와 불변성이란?

---

JavaScript는 객체 기반 프로그램 언어이다. JavaScript를 구성하고 있는 거의 모든 것이 객체이다.

원시형 타입의 값을 제외한 나머지 타입의 값(함수, 배열 ,정규 표현식 등)은 모두 객체이다.

원시형 타입과 객체형 타입이 있는데 원시형 타입은 단 하나의 값만을 나타내고, 객체형 타입은 다양한 값을 하나의 단위로 구성한 복합적인 자료구조이다. 즉, 원시형 타입의 값은 변경 불가능한 값, 객체형 타입의 값은 변경 가능한 값이라고 보면 된다.

불변성(Immutability)이란 말 그대로 변하지 않는 것을 의미한다. 즉, 불변 데이터는 한번 생성되고 나면 그 뒤에는 변할 수 없다.

## 🤑기본형 데이터와 참조형 데이터

**기본형 타입**(Primative Type)은 객체가 아닌 데이터 유형을 말하며 값을 그대로 할당하고 메모리상에 고정된 크기로 저장, 원시 데이터값 자체를 보관한다. 메모리영역 안에서 변경 불가능하며, 변수에 할당할때 완전히 새로운 값이 만들어져 재할당된다.

기본형 타입 : Boolean, String, Number, null, undefined, Symbol

**참조형 타입**(Reference Type)은 변수에 할당할 때 값이 아닌 데이터의 주소를 저장한다.

참조형 타입 : Object, Array, map, else, function RegExp

## 🙄불변 객체를 만드는 방법

JavaScript에서 const, Object.freeze()를 사용하여 불변 객체를 만들 수 있다. 그러나 const만 사용하게 되면 객체 재할당이 불가능하지만 객체의 속성은 변경가능하게 된다. 또한 Object.freeze()만 사용하게 되면 동결된 객체를 반환하지만 객체의 재할당은 가능하게 된다.

그렇기에 const와 Object.freeze()를 조합하면 객체의 재할당과 객체의 속성 둘 다 변경 불가능하게 만들어 불변 객체가 된다.

## 😍얕은 복사와 깊은 복사

얕은복사(shallow copy)는 원본객체는 하나인 상태에서, 참조값만 복사한다.
깊은복사(deep copy)는 원시값처럼 완전한 복사본을 만든다.

# 호이스팅과 TDZ는 무엇일까?

---

### 스코프, 호이스팅, TDZ

**스코프**(scope)란 변수에 접근할 수 있는 범위이며 그중에서 전역 스코프(global scope)는 전역에 선언되어 있어 어느 곳에서든지 해당 변수에 접근할 수 있고 지역 스코프(local scope)는 해당 지역에서만 접근할 수 있어 지역을 벗어난 곳에선 접근할수없다.

호이스팅이란 함수의 선언부가 유효 범위의 최상단으로 끌어올려지는 현상이며, 변수에 어떤 값이 할당되기 전인 선언된 상태만 끌어 올려진다. 변수의 선언과 초기화를 분리한 후, 선언만 코드의 최상단으로 옮긴다.

TDZ(Temporal dead zone)이란 선언과 초기화 사이이며, 선언 전에 변수를 사용하는 것을 허용하지 않는다

### 함수 선언문과, 함수 표현식에서 호이스팅 방식의 차이

함수 선언식은 함수 선언을 function으로 시작하는데 선언된 함수는 나중 사용을 위해 저장되며, 함수를 실행하려면 함수 이름을 호출한다.

함수 표현식은 정의한 function을 별도의 변수에 할당한다.

함수 선언식은 코드를 구현한 위치와 관계없이 자바스크립트의 특징인 호이스팅에 따라 브라우저가 자바스크립트를 해석할 때 맨 위로 끌어 올려진다. 함수 표현식은 함수 선언과는 달리 끌어 올려지지 않는다. 함수 표현식을 정의하기 전에는 사용할 수 없다.

### var, let, const, function 원리

var 키워드를 이용한 변수 선언은 선언 단계와 초기화 단계가 동시에 진행한다.

let 키워드로는 변수 중복 선언이 불가하지만, 재할당은 가능하다. let 키워드로 선언한 변수는 선언 단계와 초기화 단계가 분리되어 진행된다.

const가 let과 다른 점이 있다면, 반드시 선언과 초기화를 동시에 진행되어야 한다. const도 let과 마찬가지로 재선언이 불가하며, 더 나아가 재할당도 불가하다.

function키워드로 선언한 모든 식별자는 호이스팅이 된다.

### 실행 컨텍스트와 콜 스택

실행 컨텍스트(Execution Context)는 scope, hoisting, this, function, closure 등의 동작원리를 담고 있는 자바스크립트의 핵심원리이며 실행 가능한 코드가 실행되기 위해 필요한 환경이라고 말할 수 있다. 그리고 3가지 프로퍼티(variable object, scope chain, this value)를 소유한다.

콜 스택이란 자바스크립트 코드가 실행되며, 생성되는 실행 컨텍스트를 저장하는 자료구조이다.

### 스코프체인, 변수 은닉화

스코프 체인은 해당 코드의 유효 범위(in scope) 안에 있는 변수를 정의하는 객체의 체인, 리스트이며식별자 유효범위 안에서부터 바깥으로 차례로 검색해 나가는 것이다.

변수은닉화(variable shadowing)란 \*\*\*\*inner함수에서 a 변수를 선언함으로써 전역 공간의 a 변수 접근을 막는다

### 실습 과제

- 콘솔에 찍힐 b 값을 예상해보고, 어디에서 선언된 “b”가 몇번째 라인에서 호출한 console.log에 찍혔는지, 왜 그런지 설명해보세요.
  주석을 풀어보고 오류가 난다면 왜 오류가 나는 지 설명하고 오류를 수정해보세요.

```jsx
let b = 1;

function hi () {

const a = 1;

let b = 100;

b++;

console.log(a,b);

}

//console.log(a); //  전역에 선언된 게 없기때문에 오류
											오류를 수정하기 위해서는 function안에 있는 const a = 1을
											let b = 1 밑으로 꺼낸다.

console.log(b);   //  let b = 1이 전역에서 선언했기에 b = 1 출력

hi();             //   function으로 함수선언을 하였고 let은 재할당이 되기에
												안에 있는 let b = 100으로 재할당되었다.
												그래서 a = 1, b = 100 출력

console.log(b);   //   let b = 1이 전역에서 선언했기에 b = 1 출력
```
