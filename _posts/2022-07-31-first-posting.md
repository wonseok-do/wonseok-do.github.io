---
layout: single
title: "WIL"
categories: coding
tag: [python, jekyll, blog]
toc: true
author_profile: false
sidebar:
  nav: "docs"
# search: false
---

벌써 항해99를 시작한 지, 3주차가 지나고 4주차가 시작되었네요……….. 정말 시간이 빠릅니다..

하루하루 정신없이 보내서.. 공부한 것들이 머릿속에 잘 남았을지.. 그것도 걱정이네요…

주특기 이제 막 1주차가 끝나고 2주차 시작하는데 1주차에서 프로젝트를 만들고 하는 것들이 너무 어렵고 힘들었습니다. React… 공부해야 할 것들이 정말 많네요.. 시간 분배도 잘 못해서.. 체력적으로 많이 부족한데.. 운동 열심히 해서 남은 항해 기간 잘 마무리할 수 있도록 노력해야겠습니다!

밑에 있는 것들은 WIL 키워드입니다.

## 🙄 Props란?

props : component가 부모 component로부터 데이터를 받아온 데이터

이전에는 setProps, replaceProps로 props를 변경할 수 있었지만, 이제는 더 이상 사용되지 않습니다. 따라서, 함수 컴포넌트나 클래스 컴포넌트 모두 컴포넌트의 자체 props를 수정해서는 안됩니다. 모든 React컴포넌트는 자신의 props를 다룰 때 반드시 순수 함수처럼 동작해야 합니다.

## 😎 State란?

state : component가 가지고 있는 데이터

state는 한 컴포넌트에서만 사용하는 정보를 주로 넣어놓고 생성, 수정하는 데이터입니다.

생성도 수정도 오직 해당 컴포넌트 내에서만 이뤄집니다.

state 가 변경되면 컴포넌트를 다시 렌더링 해야합니다.

## 😁 리렌더링 발생 조건

- props가 바뀔 때
- state가 바뀔 때
- 부모 컴포넌트가 업데이트 되었을 때(=리렌더링했을 때)
- 또는, 강제로 업데이트 했을 경우! (forceUpdate()를 통해 강제로 컴포넌트를 업데이트할 수 있습니다.)

### 😶 참고

[React.state ,props 하는일과 차이점](https://velog.io/@s2s2hyun/React.state-props-%ED%95%98%EB%8A%94%EC%9D%BC%EA%B3%BC-%EC%B0%A8%EC%9D%B4%EC%A0%90)

[props](https://itprogramming119.tistory.com/entry/React-props-%EC%B4%9D%EC%A0%95%EB%A6%AC-%EB%B0%8F-%EC%98%88%EC%A0%9C?category=1203905)

[Components와 Props - React](https://ko.reactjs.org/docs/components-and-props.html)
