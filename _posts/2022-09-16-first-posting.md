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

자잘한 에러와 모달 창을 구현해보았습니다. 일단 급한 건 회원가입 페이지에서 뒤로 가기 버튼을 눌렀을 때 모달 창을 띄워야 하는데요. 그것을 먼저 구현하고 나머지도 구현했습니다.

### **회원가입 페이지의 뒤로가기 버튼에 모달 창 추가**

**수정 전**

```jsx
const before = () => {
  if (level === 0) {
    navigate("/signIn");
  } else {
    reset({ emailVerifyToken: undefined });
    reset({ nicknameVerifyToken: undefined });
    setLevel(0);
    alert("뒤로가기 버튼을 누를 시 이메일 인증부터 새로 하셔야 합니다.");
  }
};
```

**수정 후**

-import(모달) 및 state 값 추가

-버튼 (before) 기능을 분리

-모달 버튼 추가

```jsx
import ConfirmBox from "../components/elements/modal/ConfirmBox";
...
const [modal, setModal] = useState(false);
...
const before = () => {
    if (level === 0) {
      navigate("/signIn");
    } else {
      setModal(true);
    }
  };
  const resetRegister = () => {
    setTimeout(() => {
      reset({ emailVerifyToken: undefined });
      reset({ nicknameVerifyToken: undefined });
      setLevel(0);
      setModal(false);
    }, 1000);
  };
  const cancelModal = () => {
    setTimeout(() => {
      setModal(false);
    }, 1000);
  };
{modal && (
        <ConfirmBox
          text={"뒤로가기 버튼을 누를시\n이메일 인증부터 새로 하셔야 합니다."}
          confirmButtonText={"새로하기"}
          backgroundShadow={true}
          onComfirmed={resetRegister}
          onDenied={cancelModal}
        />
      )}
```

figma로 나온 회원가입 페이지 - 이메일, 닉네임 부분에서 버튼을 수정

**수정 전**

![https://user-images.githubusercontent.com/108975442/190639043-4ac285f6-8c3c-4f7f-a7ff-6e2873242296.png](https://user-images.githubusercontent.com/108975442/190639043-4ac285f6-8c3c-4f7f-a7ff-6e2873242296.png)

**수정 후**

![https://user-images.githubusercontent.com/108975442/190639129-36995486-650c-47bc-bea6-5b36c0a371b4.png](https://user-images.githubusercontent.com/108975442/190639129-36995486-650c-47bc-bea6-5b36c0a371b4.png)

![https://user-images.githubusercontent.com/108975442/190639151-3f168274-13b8-4a45-a5fe-f83f6535705a.png](https://user-images.githubusercontent.com/108975442/190639151-3f168274-13b8-4a45-a5fe-f83f6535705a.png)

```
  const [checkNumber, setCheckNumber] = useState(false);
  const [checkNumberCode, setCheckNumberCode] = useState(false);
  const [checkEmailCode, setCheckEmailCode] = useState(false);
  const [checkNumber, setCheckNumber] = useState(false);
  const [checkNumberCode, setCheckNumberCode] = useState(false);
  const [checkEmailCode, setCheckEmailCode] = useState(false);
...
//인증번호 발송
  const sendEmailVerifyCode = async () => {
    let contentType = "application/x-www-form-urlencoded";
    if (errors.email) {
      setToast(true);
      setTimeout(() => {
        setToast(false);
      }, 1000);
      return;
    }
    try {
      const res = await api(contentType).get(
        `/auth/send-email?email=${getValues("email")}`
      );
      console.log(res.data.message);
      setCheckEmail(true);
      alert(res.data.message);
      setCheckNumber(true);
      setMinutes(3);
      setSeconds(0);
      setCheckTimer(true);
    } catch (err) {
      console.log(err);
      alert(err.response.data.message);
      setCheckEmail(false);
      setCheckTimer(false);
      setCheckNumber(false);
    }
  };
  //입력번호 확인
  const confirmEmailVerifyCode = async () => {
    let contentType = "application/x-www-form-urlencoded";
    try {
      const res = await api(contentType).get(
        `/auth/confirm-email?email=${getValues(
          "email"
        )}&email-verify-code=${getValues("Number")}`
      );
      const token = res.data.emailVerifyToken;
      console.log(token);
      setValue("emailVerifyToken", token);
      console.log(getValues("emailVerifyToken"));
      setCheckEmailCode(true);
      setCheckNumberCode(true);
      alert(res.data.message);
    } catch (err) {
      console.log(err);
      alert(err.response.data.message);
      setCheckNumberCode(false);
    }
  };
const next = async () => {
    //에러가 날 경우 알림띄우기
    if (errors.email && level === 0) {
      alert("이메일을 제대로 입력해주세요!");
      return;
    }
    if (errors.password && level === 1) {
      alert("비밀번호를 제대로 입력해주세요");
      return;
    }
    if (errors.password_confirm && level === 1) {
      alert("비밀번호가 일치하지 않습니다");
      return;
    }
    if (errors.nickname && level === 2) {
      alert("닉네임을 제대로 입력해주세요");
      return;
    }
    //닉네임 중복확인
    if (level === 2) {
      const contentType = "application/x-www-form-urlencoded";
      try {
        const res = await api(contentType).get(
          `/auth/confirm-nickname?emailVerifyToken=${getValues(
            "emailVerifyToken"
          )}&nickname=${getValues("nickname")}`
        );
        const token = res.data.nicknameVerifyToken;
        // console.log(res);
        setValue("nicknameVerifyToken", token);
        console.log(getValues("nicknameVerifyToken"));
        alert(res.data.message);
      } catch (err) {
        console.log(err);
        alert(err.response.data.message);
        return;
      }
    }
    setLevel((prev) => prev + 1);
  };
...
{!checkNumber ? (
          <StButton
            onClick={sendEmailVerifyCode}
            disabled={watch("email") === undefined || watch("email") === ""}
          >
            이메일 인증번호 발송
          </StButton>
        ) : !checkEmailCode ? (
          <StButton
            onClick={confirmEmailVerifyCode}
            disabled={
              watch("Number")?.length <= 5 || getValues("Number") === undefined
            }
          >
            인증번호 확인
          </StButton>
        ) : level === 3 ? (
          <StButton
            disabled={
              (level === 3 && watch("image") === undefined) ||
              (level === 3 && watch("image")?.length === 0) ||
              isSubmitting
            }
          >
            계속하기
          </StButton>
        ) : (
          <StButton
            onClick={next}
            disabled={
              (level === 0 && watch("email") === undefined) ||
              (level === 0 && watch("email") === "") ||
              (level === 0 && watch("emailVerifyToken") === undefined) ||
              (level === 1 && watch("password") === "") ||
              (level === 1 && watch("password_confirm") === "")
            }
          >
            계속하기
          </StButton>
        )}

```

- 기존의 이메일 버튼과 닉네임 버튼을 회원가입 페이지로 가져옴
- state 값 추가
- 버튼을 삼항연산자를 사용하여 쓰임에 맞게 보이게 함

기존의 버튼기능만 옮겨서 갖다쓰면 끝날 줄 알았지만, 상황에 맞게 버튼을 바꿔줘야 하기 때문에

삼항연산자도 여러번 쓰는데 너무 힘들었습니다. 생각보다 쉽지 않더군요. 그래도 이제 어느정도

구상했던 것에 맞춰지고 있는 것 같아서 좋네요. 자잘한 것들도 고치면서 더 힘내보도록 하겠습니다

화이팅!!!!!!!!!!!
