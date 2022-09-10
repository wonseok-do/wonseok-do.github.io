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

어제 생각했었던 에러들을 수정해보려고 했지만 잘 안됐습니다 ㅠㅠ

일단 디자이너님과 얘기를 나누고 뒤로가기 버튼을 눌렀을 때 처음부터 회원가입을 하는 방향으로

수정하였습니다. 그리고 뒤로가기 했을 때 이메일과 닉네임 토큰을 리셋시켜야 하는데요 이 부분을

고치려고 했지만 잘 안되었네요 ㅠㅠ

```jsx
const before = () => {
  if (level === 0) {
    navigate("/signIn");
  } else {
    // const emailToken = getValues("emailVerifyToken");
    // reset("emailVerifyToken");
    // reset("Number");
    // reset(getValues("email"));
    reset({ emailVerifyToken: undefined });
    // setValue("emailVerifyToken", undefined);
    // resetField("emailVerifyToken");
    // console.log(getValues("emailVerifyToken"));
    setLevel(0);

    // resetField(getValues("emailVerifyToken"));
    // console.log(getValues("emailVerifyToken"));
  }
};
React.useEffect(() => {
  if (level !== 0) {
    before();
  }
}, []);
```

react-hook-form에 있는 reset, resetField 등 함수들을 사용했지만 콘솔에는 undefined가 찍히더라도 서버자체에서는 토큰 값이 남아있기 때문에 유저가 회원가입을 다시 처음부터 했을 때 이미 인증해버린 아이디하고 닉네임을 사용할 수 없다는 게 문제가 되는데요. 저는 여기자체에서 해결하고 싶었지만 서버에 남아있는 토큰을 어떻게 해결할 수가 없어 백엔드분들하고 상의를 해봐야겠네요

중간에 setValue나 getValues등 여러가지 방면으로 생각해봤지만 도저히 답을 찾을 수가 없었네요

그리고 마지막에는 다시 처음부터 시작할 때 렌더링이 되어야겠다 싶어서 useEffect()를 사용했습니다 처음에는if (level !== 0) 이 조건문을 넣지 않아서 로그인에서 회원가입으로 넘어갈 때 계속해서 렌더링이 되어 로그인페이지에만 머무르게 되었어서 조건문을 넣어줬습니다

일단 임시라도 이 정도까지 해봤는데요. 백엔드분들과 빨리 얘기를 해서 다음 단계로 넘어갈 수 있게 하려고 합니다. 오늘은 뭔가 생각만 하고 저것만 끄적이다가 시간이 다 지나갔는데요 ㅠㅠㅠ 이래도 되나 싶을 정도로 고민만 하고 한 게 없는 것 같아서 속상하네요.. ㅠ 더 열심히 하도록 하겠습니다 화이팅!!!!!!!!!!!!!!!!
