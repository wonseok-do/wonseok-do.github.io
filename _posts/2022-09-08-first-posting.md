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

API가 나오게 돼서 axios를 사용해 데이터를 주고 받아 보는 작업을 해봤습니다. 회원가입 페이지에서 여러개의 컴포넌트로 나누었고 그것을 그 안에 데이터를 가져와서 사용해야 하기 때문에 어떻게 시작을 해야할 지 좀 막막했습니다. useState를 사용해야 되나 여러가지 고민을 좀 하다가

react-hook-form에 있는 useForm()에서 setValue와 getValues를 찾아보고 이것을 사용해야겠다 싶어서 한번 사용해봤습니다.

```jsx
//Email.jsx
const { register, errors, watch, setValue, getValues } = props;

const confirmEmailVerifyCode = async () => {
  try {
    const res = await axios.get(
      `http://~~~~~/api/auth/confirm-email?email=${watch(
        "email"
      )}&email-verify-code=${watch("Number")}`,
      { headers: { "Content-Type": "application/x-www-form-urlencoded" } }
    );
    const token = res.data.emailVerifyToken;
    console.log(token);
    setValue("emailVerifyToken", token);
    console.log(getValues("emailVerifyToken"));
    alert(res.data.message);
  } catch (err) {
    console.log(err);
    alert("이미 인증이 완료되었습니다");
  }
};
const sendEmailVerifyCode = async () => {
  try {
    const res = await axios.get(
      `http://~~~~~/api/auth/send-email?email=${watch("email")}`,
      {
        headers: { "Content-Type": "application/x-www-form-urlencoded" },
      }
    );
    console.log(res.data.message);
    alert(res.data.message);
  } catch (err) {
    console.log(err);
  }
};
```

```jsx
//Register.jsx
...
const onSubmit = async () => {
    const form = new FormData();
    form.append("imageValue", getValues("image")[0]);
    if (level === 3) {
      try {
        console.log(getValues("image")[0]);
        const res = await axios.post(
          `http://~~~~~/api/auth/signup?nickname=${getValues(
            "nickname"
          )}&email=${getValues("email")}&password=${getValues(
            "password"
          )}&nicknameVerifyToken=${getValues(
            "nicknameVerifyToken"
          )}&emailVerifyToken=${getValues("emailVerifyToken")}`,
          form,
          { headers: { "Content-Type": "multi-part/form-data" } }
        );
        console.log(res);
        alert(res.data.message);
        navigate("/signIn");
      } catch (err) {
        console.log(err);
      }
    }
  };
```

api명세서에서 경로와 content-type등 어떻게 해결해야 되나 고민을 정말 많이 했는데요.

경로같은 경우는 각 컴포넌트안에서는 watch()로 해결을 했고, 전체 폼에서는 그 값들을 가져와야 하기 때문에 getValues()를 사용했습니다. 그리고 이메일과 닉네임은 각각의 토큰 값이 있어 이 값들을 지정해야 하는데 setValue를 사용해서 값을 넣고 다시 getValues를 사용해서 값을 가져왔습니다.

이렇게 하는 것이 맞는 방법인지는 솔직히 잘 모르겠습니다. 그래도 vscode에 있는 확장프로그램에서 mysql를 통해 데이터가 제대로 들어가는 것까지는 확인했습니다. 매번 코드를 짜면서 잘하고 있는 지에 대한 자신이 없네요.. 더 열심히 공부해야겠습니다

```jsx
//Login.jsx
...
const onSubmit = async () => {
    const data = { email: watch("email"), password: watch("password") };
    const queryStringData = Object.keys(data)
      .map((k) => encodeURIComponent(k) + "=" + encodeURIComponent(data[k]))
      .join("&");
    console.log(queryStringData);
    try {
      const res = await axios.post(
        "http://~~~~~/api/auth/signin",
        queryStringData,
        {
          headers: { "Content-Type": "application/x-www-form-urlencoded" },
        }
      );
      console.log(res);
      console.log(res.data.accessToken);
      localStorage.setItem("accessToken", res.data.accessToken);
      localStorage.setItem("refreshToken", res.data.refreshToken);
      alert(res.data.message);
      navigate("/");
    } catch (err) {
      console.log(err);
    }
  };
```

로그인 같은 경우는 data를 querystring으로 만들었고 localstorage에 accessToken과 refreshToken을 넣었습니다. axios interceptors를 이용해야 하는데요. 이거는 조금 더 공부해봐야 알 것 같네요.

이렇게나마 조금씩 데이터를 넣고 하는 방법을 해보았는데요. 힘들었지만 정말 좋았습니다!!!

더욱더 힘내서 잘해보도록 하겠습니다 화이팅!!!!
