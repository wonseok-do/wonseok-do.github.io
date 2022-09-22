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

오늘은 로그인 페이지와 비밀번호 찾기 페이지에서 회원가입 페이지와 같이 alert을

모달창으로 수정하였습니다. 이번에도 onSubmit 이슈가 있었는데요

alert을 사용했을 때는 error가 되었어도 상관이 없었지만, setError를 추가해서 그런지

error 한 번 뜨게 되면 작동이 바로 멈추네요.. 으아아아ㅏ앙

도저히 해결 방법을 찾지 못해 onClick으로 빼서 만들었습니다. 문제가 뭐야!!!!!!!!!

```jsx
// Login.jsx
const clickLogin = async () => {
  if (errors.email) {
    setEmailFailure(true);
    setTimeout(() => {
      setEmailFailure(false);
    }, 1000);
    return;
  }
  if (errors.password) {
    setPwFailure(true);
    setTimeout(() => {
      setPwFailure(false);
    }, 1000);
    return;
  }
  const data = { email: watch("email"), password: watch("password") };
  const queryStringData = Object.keys(data)
    .map((k) => encodeURIComponent(k) + "=" + encodeURIComponent(data[k]))
    .join("&");
  console.log(queryStringData);
  const contentType = "application/x-www-form-urlencoded";
  try {
    const res = await api(contentType).post(
      "/auth/signin",
      queryStringData
      // {
      //   headers: { "Content-Type": "application/x-www-form-urlencoded" },
      // }
    );
    console.log(res);
    localStorage.setItem("accessToken", res.data.accessToken);
    localStorage.setItem("refreshToken", res.data.refreshToken);
    setLoginSuccess(true);
    navigate("/recipe", {
      state: { message: `${data.email}\n로그인 되었습니다.` },
    });
  } catch (err) {
    console.log(err);
    // alert(err.response.data.message);
    setError("loginError", { message: err.response.data.message });
    setLoginError(true);
    setTimeout(() => {
      setLoginError(false);
    }, 1000);
  }
};
///
<StButton
  onClick={clickLogin}
  disabled={
    loginSuccess ||
    loginError ||
    watch("email") === "" ||
    watch("email") === undefined ||
    watch("password") === ""
  }
>
  계속하기
</StButton>;
```

다음에는 input에 있는 내용들이 있을 때 한 번에 지울 수 있는 버튼을 만들면 좋겠다고 하셔서

구현했습니다. input에 아무것도 없이 비어있을 때는 버튼이 없었다가 한 글자라도 나오게 되면

버튼이 나오도록 구현했습니다.

```jsx
// Login.jsx
<label>이메일</label>
        <div className="register_input_box">
          {watch("email")?.length >= 1 && (
            <img
              className="input_label_icon"
              src={cancelBtn}
              alt="리셋 버튼"
              onClick={() => resetField("email")}
            />
          )}
          <StInput
            type="text"
            placeholder="이메일 주소를 입력해 주세요"
            autoComplete="off"
            maxLength={100}
            {...register("email", {
              required: true,
              pattern: {
                value:
                  /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,3}))$/,
                message: "이메일 형식에 맞지 않습니다.",
              },
            })}
          />
        </div>
```

react hook form에 있는 resetField를 사용하여 register에서 설정한 name값을 넣어주게 되면

그 안에 있는 값이 리셋됩니다. 회원가입 페이지나 비밀번호 찾기 페이지에서도 비슷하게 구현했습니다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/34d88ea3-ad69-45e0-a4db-c0a34622e416/Untitled.png)

오늘 그래도 목표한 것들을 해결해서 다행이라고 생각합니다!! 그리고 저희 조가 가장 도움이

된 조로 뽑히게 되어 치킨 쿠폰을 받았습니다!!!! 진짜 저희 팀원분들 고생많으셨습니다

이제 얼마 남지 않은 기간 동안 더 힘내서 잘 끝마치도록 하겠습니다!!! 화이팅!!!!!
