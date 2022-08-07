---
layout: single
title: "클래스형 컴퍼넌스와 함수형 컴퍼넌스"
categories: coding
tag: [python, jekyll, blog]
toc: true
author_profile: false
sidebar:
  nav: "docs"
# search: false
---

## 🤩 이벤트 리스너(eventListener)란?

이벤트 리스너는 DOM객체에서 이벤트가 발생할 경우 해당 이벤트 처리핸들러를 추가할 수 있는 오브젝트입니다
이벤트 리스너를 이용하면 특정 DOM에 위에 말한 JavaScript이벤트가 발생할 때 특정 함수를 호출합니다
이벤트 리스너 등록하기 : 특정 DOM요소에 이벤트 리스너를 등록할 때는 addEventListener를 사용
DOM객체.addEventListener(이벤트명,실행할함수명,옵션);
이벤트 리스너 삭제하기 : 더 이상 해당 이벤트 리스너가 필요 없다고 하면 반드시 추가된 이벤트 리스너는 반드시 삭제해주어야 합니다
이벤트 리스너를 삭제할 땐 removeEventListener을 이용
DOM객체.removeEventListener(이벤트명,실행했던 함수명);

## 😆 클래스형 컴포넌트란?

클래스형 컴포넌트 : class로 정의하고 render() 함수에서 jsx 코드를 반환합니다

클래스형 컴포넌트 라이프 사이클 메서드

![클래스형 컴퍼넌트](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/31b292fd-c708-4310-ae4a-7bfe4ae4c37e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220807%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220807T134648Z&X-Amz-Expires=86400&X-Amz-Signature=b16d9019e26f17ca192d608098d84362976cc428aaaa5d9d395e6de596085c58&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

출처: [http://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/](http://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/)

**constructor** 는 컴포넌트의 생성자 메서드입니다. 컴포넌트가 만들어지면 가장 먼저 실행되는 메서드입니다.

**getDerivedStateFromProps** 는 props 로 받아온 것을 state 에 넣어주고 싶을 때 사용합니다. 컴포넌트의 props나 state가 바뀌었을때도 이 메서드가 호출합니다.

**shouldComponentUpdate** 메서드는 컴포넌트가 리렌더링 할지 말지를 결정하는 메서드입니다.

**render**은 컴포넌트를 렌더링하는 메서드, 컴포넌트 내에 엘리먼트 요소들(HTML, React 사용자 정의 태그)을 화면 상에 그리는 동작을 의미합니다.

**getSnapshotBeforeUpdate** 는 컴포넌트에 변화가 일어나기 직전의 DOM 상태를 가져와서 특정 값을 반환하면 그 다음 발생하게 되는 componentDidUpdate 함수에서 받아와서 사용을 할 수 있습니다.

**componentDidMount** 은 \*\*\*\*컴포넌트의 첫번째 렌더링이 마치고 나면 호출되는 메서드입니다.

**componentDidUpdate** 는 리렌더링이 마치고, 화면에 우리가 원하는 변화가 모두 반영되고
난 뒤 호출되는 메서드입니다. 3번째 파라미터로 getSnapshotBeforeUpdate 에서 반환한 값을 조회 할 수 있습니다.

**componentWillUnmount()** : 컴포넌트가 DOM상에서 제거될 때에 호출
컴포넌트가 마운트 해제되어 제거되기 직전에 호출, 컴포넌트 인스턴스가 마운트 해제되고 나면, 절대로 다시 마운트 되지 않습니다
언마운트 라는 것은, 컴포넌트가 화면에서 사라지는 것, 언마운트에 관련된 생명주기메서드

## 🙄 함수형 컴포넌트란?

함수형 컴포넌트 : function으로 정의하고 return문에 jsx코드를 반환합니다.

함수형 컴포넌트 라이프 사이클 메서드

![함수형 컴퍼넌트](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbF6rTe%2FbtrEvNPPvFs%2FkfuXlK3dGF4bJUpKXQcjH1%2Fimg.png)

[출처] [https://wavez.github.io/react-hooks-lifecycle/](https://wavez.github.io/react-hooks-lifecycle/)

### 함수형 컨포넌트에서 라이프 사이클 사용법

클래스형 컴포넌트에서는 state(상태)를 사용할 수 있으며 각종 라이프 사이클 및 메서드
를 이용하여 컴포넌트가 마운트 혹은 언마운트 될 때 추가 작업을 수행시키는 등 조작을 할 수 있었지만 함수형 컴포넌트에서는 불가능하다. 그렇기에 Hook이라는 것이 등장했습니다.

Hook은 함수 컴포넌트에서 React state와 생명주기 기능(lifecycle features)을 “연동(hook into)“할 수 있게 해주는 함수입니다. Hook은 class 안에서는 동작하지 않습니다. 대신 class 없이 React를 사용할 수 있게 해주는 것입니다.

### 함수형 컴포넌트에서는 event listener를 해제할 때 어떻게 해야할까요?

React class에서는 흔히 componentDidMount에 구독(subscription)을 설정 componentWillUnmount에서 이를 정리(clean-up)합니다.

함수형 컴포넌트에서는 Effect Hook을 사용하면 됩니다. Effect Hook, 즉 useEffect는 함수 컴포넌트 내에서 이런 side effects를 수행할 수 있게 해줍니다. useEffect Hook을 componentDidMount와 componentDidUpdate, componentWillUnmount가 합쳐진 것으로 생각해도 좋습니다.
구독(subscription)의 추가와 제거를 위한 코드는 결합도가 높기 때문에 useEffect는 이를 함께 다루도록 고안되었습니다. effect가 함수를 반환하면 React는 그 함수를 정리가 필요한 때에 실행시킬 것입니다. 모든 effect는 정리를 위한 함수를 반환할 수 있습니다. 이 점이 구독(subscription)의 추가와 제거를 위한 로직을 가까이 묶어둘 수 있게 합니다. 구독(subscription)의 추가와 제거가 모두 하나의 effect를 구성하는 것입니다.

## 😛 참고

[Hook 개요 - React](https://ko.reactjs.org/docs/hooks-overview.html)

[25. LifeCycle Method](https://react.vlpt.us/basic/25-lifecycle.html)

[[JavaScript] 이벤트리스너(Event Listener)란? - 사용법 및 주의사항](https://ordinary-code.tistory.com/64)
