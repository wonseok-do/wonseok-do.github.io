---
layout: single
title: "React 과제"
categories: coding
tag: [python, jekyll, blog]
toc: true
author_profile: false
sidebar:
  nav: "docs"
# search: false
---

# JavaScript의 자료형과 JavaScript만의 특성

---

## 😀느슨한 타입(loosely typed의 동적(dynamic)언어

JavaScript는 느슨한 타입의 동적이면서 JavaScript의 변수는 어떤 특정 타입과 연결되지 않는다.

그래서 모든 타입의 값으로 할당(및 재할당)이 가능하다.

```jsx
let haha = 50; // haha 숫자(Number)
haha = "bar"; // 문자열(String)
haha = true; // Boolean
```

## 😋JavaScript의 형변환

JavaScript의 형변환에는 엔진이 필요에 따라 자동으로 데이터 타입을 변환하는 암시적 변환과

개발자가 의도를 가지고 데이터 타입을 변환하는 명시적 변환이 있다.

산술연산자(+, -, \*, %)중에서 더하기는 숫자와 문자열이 같이 되어있을 때 숫자보다 문자열이 우선시 되어 숫자형을 문자형으로 변환하여 연산해준다. 그 외에는 숫자형이 문자형보다 우선시 되어 숫자형이 문자형으로 변환되지 않는다.

명시적 변환에는 문자열이 아닌 값을 문자열로 바꾸어주는 **[](https://t1.daumcdn.net/cfile/tistory/990D9A3A5B8290210D)String(),** 숫자가 아닌 값을 숫자로 바꾸어주는 **Number()**이 있으며 숫자가 아닌 것 같은 값에는 NaN(Not A Number)으로 변환된다. 어떤 값이 있는 것 같은 뉘앙스를 가진 값에는 true, 아니면 false으로 변환하는 **Boolean()**이 있다.

## 😂==, ===

JavaScript를 사용하게 되면 ==, === 뭐가 다르지? 하고 생각할 때가 많다.

==, ===의 주된 차이점은 == 연산자를 사용하여 서로 다른 유형의 두 변수[값]을 비교하고,

=== 연산자는 값뿐만 아니라 자료형도 비교한다는 점이다.

```jsx
0 == false; // ==이여서 true

0 === false; // 여기서는 false
console.log(typeof 0); // 0의 유형이 number
console.log(typeof false); // false의 유형이 boolean이기에 유형이 달라서 false
```

## 😎느슨한 타입의 동적 언어의 문제점, 보완방법

JavaScript의 객체는 너무나도 동적이여서, 언제라도 속성을 추가, 삭제, 수정할 수 있다.

그렇기에 JavaScript는 함수형 프로그래밍을 지원하는데도 불구하고 불변성을 지원하지 않는다.

IDE나 단에서 타입체크를 못하게 되어 잘 못쓴 타입을 잡지못하고 에러가 발생한다. 그래서 보완하는 방법에는 정적 타입의 언어 TypeScript정도가 있다.

## 😤undefined와 null의 미세한 차이

null과 undefined는 자료형이면서 동시에 값인 독특한 특징이 있다. 그렇지만 빈 값이냐, 값을 할당하지 않았냐에 따라 null과 undefined로 나뉘게 된다.

**null**은 의도적으로 명확하게 비어있다는 것을 명시적으로 밝힐 때 할당하는 값이다.

**undefined**은 값을 할당하지 않아 암시적으로 알려줄 때 확인되어지는 값이다.

ex) null : 화장실에 휴지걸이만 있는 것, undefined : 휴지걸이에 휴지심만 있는 것
