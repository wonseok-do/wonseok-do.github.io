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

이번 WIL주제가 라이프사이클(클래스형, 함수형) 그리고 React Hooks에 관한 것입니다.

그 전에 공부한 적이 있지만 다시 한번 더 보니 조금(?)은 그 전보다는 이해가 되는 거 같네요..

며칠동안 2시간~3시간밖에 잠을 못 자서.. 컨디션을 관리하지 못해 오늘 하루종일 잠만 잤네요 ㅠㅠ

공부를 거의 하지 못했지만, 이거라도 공부를 해야겠다는 생각이 들어서 열심히 보고 있습니다!

클래스형 컴포넌트 : class로 정의하고 render() 함수에서 jsx 코드를 반환합니다

클래스형 컴포넌트 라이프 사이클 메서드

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/31b292fd-c708-4310-ae4a-7bfe4ae4c37e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220807%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220807T134648Z&X-Amz-Expires=86400&X-Amz-Signature=b16d9019e26f17ca192d608098d84362976cc428aaaa5d9d395e6de596085c58&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

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

![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbF6rTe%2FbtrEvNPPvFs%2FkfuXlK3dGF4bJUpKXQcjH1%2Fimg.png)

[출처] [https://wavez.github.io/react-hooks-lifecycle/](https://wavez.github.io/react-hooks-lifecycle/)

### 함수형 컨포넌트에서 라이프 사이클 사용법

클래스형 컴포넌트에서는 state(상태)를 사용할 수 있으며 각종 라이프 사이클 및 메서드
를 이용하여 컴포넌트가 마운트 혹은 언마운트 될 때 추가 작업을 수행시키는 등 조작을 할 수 있었지만 함수형 컴포넌트에서는 불가능하다. 그렇기에 Hook이라는 것이 등장했습니다.

Hook은 함수 컴포넌트에서 React state와 생명주기 기능(lifecycle features)을 “연동(hook into)“할 수 있게 해주는 함수입니다. Hook은 class 안에서는 동작하지 않습니다. 대신 class 없이 React를 사용할 수 있게 해주는 것입니다.

---

라이프사이클을 다루는 것은 컴포넌트가 생겨나고, 변화하고, 없어지는 일련의 프로세스를
프로그래머가 통하는 것을 뜻함.
라이프사이클은 순차적으로 실행된다는 사실과 라이프사이클은
굉장히 효율적으로 업데이트 된다는점
처음 생성될 때, props나 state가 업데이트 되었을 때, 컴포넌트가 더이상
브라우저에 보여질 필요가 없을 때
컴포넌트가 로딩되기 시작하는 Mounting
constructor 클래스 생성자
초기 state를 정할수 있다
실제 로딩이 이루어지는 render
컴포넌트를 렌더링할때 필요한 메서드
처음 로딩이 끝난뒤에 수행되는 componentDidMount
컴포넌트의 업데이트 Updating
1.props가 바뀔 때
2.state가 바뀔 때 3.부모컴포넌트가 리렌더링 될때
4.this.forceUpdate로 강제로 렌더링을 트리거할때
컴포넌트의 삭제 Unmounting
componentWillUnmount
컴포넌트가 사라질 때에 수행되는 메소드

useEffect
useEffect Hook을 이용하여 컴포넌트가 렌더링 이후에 어떤일을 수행할 수 있다.
렌더링 이후 compunetDidMount, componentDidUpdate, componentWillMount 을 할 수 있다.

**React Hooks**

- useState
  컴포넌트의 state를 관리 할 수 있다
- useEffect
  렌더링 이후에 실행할 코드를 만들 수 있다.
- useContext
  부모컴포넌트와 자식 컴포넌트 간의 변수와 함수를 전역적으로 정의할 수 있다
- useReducer
  state(상태) 업데이트 로직을 reducer 함수에 따로 분리할 수 있다
- useRef
  컴포넌트나 HTML 요소를 래퍼런스로 관리할 수 있다.
- useMemo, useCallback
  의존성 배열에 적힌 값이 변할 때만 값, 함수를 다시 정의할 수 있다.

[https://defineall.tistory.com/900](https://defineall.tistory.com/900)

위에 사이트를 통해서 더 자세히 알 수 있습니다.

코드를 짜면서 위에 Hook을 사용하고 있지만은, 아직 많이 부족해서 쓰는 것이 힘드네요 ㅠㅠ

조금 더 열심히 공부해서 custom hook 만들어서 쓰고 싶습니다.

내일부터 다시 돌아오는 월요일이니 오늘 일찍 자고 다시 열심히 공부해야겠군요. 몸 관리도 열심히 해야겠습니다… 이 긴 여정을 잘 마무리하려면 말이죠..!
