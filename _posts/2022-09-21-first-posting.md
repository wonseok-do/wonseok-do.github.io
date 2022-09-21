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

mvp가 끝나고 스파르톤을 한 이후로 밤을 샜더니 몸 상태가 급격히 안좋아져서

작업을 많이 하지 못했습니다ㅠㅠ 팀원들께 정말 죄송하네요.. 죄송하다고 여러번 말씀드렸습니다ㅠ

이제 회원가입 페이지에서 alert 창 대신에 모달창으로 구현했습니다

이거 구현하려고 머리를 쥐어싸맸습니다.. 도저히 비동기에서 어떻게 message를 가져와야할 지

생각을 많이 해봤지만.. 도저히 못 찾은 그때.. React hook form에 있는 setError로 어떻게 되지

않을까? 싶어서 시도했는데 어찌어찌 구현은 되었네요.. ㅠㅠ 이게 맞는건 지.. 의문스럽지만

일단 되어서 다행이네요! sweetalerts를 사용하면 생각보다 손쉽게(?) 구현할 수 있겠지만..

팀원이 만들어준 모달을 사용해서 구현하고 싶기도 했고, 라이브러리 없이도 구현이 가능하다면

최대한 라이브러리를 안 쓰는 방향으로 하고 싶었기에 이렇게 시도를 해봤습니다..

```jsx
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
      // {
      //   headers: { "Content-Type": "application/x-www-form-urlencoded" },
      // }
    );
    console.log(res.data.message);
    setCheckEmail(true);
    // alert(res.data.message);
    setCheckNumber(true);
    setMinutes(3);
    setSeconds(0);
    setCheckTimer(true);
    setEmailSuccess(true);
    setTimeout(() => {
      setEmailSuccess(false);
    }, 1000);
    return;
  } catch (err) {
    console.log(err);
    // alert(err.response.data.message);
    setCheckEmail(false);
    setCheckTimer(false);
    setCheckNumber(false);

    setError("emailError", { message: err.response.data.message });

    // setValue("emailError", err.response.data.message);
    // console.log(setError);
    setFailure(true);
    setTimeout(() => {
      setFailure(false);
    }, 2000);
    return;
  }
};
///
{
  failure && <ToastMessage text={errors?.emailError?.message} timer={2000} />;
}
```

onClick했을 때 setError에 message와 이름을 넣고 ToastMessage(모달)에서 메시지가 나오게끔 구현했습니다. 코드가 지저분해진 것 같기도 하고.. 잘 모르겠네요 ㅎㅎ.. 이게 맞나?

이거 구현하겠다고 머리를 이리저리 굴리면서.. 에휴.. 힘든 나날들을 보냈었는데 구현돼서 홀가분하네요. 닉네임 등 다른 부분들도 저거랑 비슷하게 구현했습니다

이제 완성하고 나서 보니 onSubmit이 안되더라고요? 확인해봤더니 중간에 error(이미 가입한 이메일, 인증 번호 틀림, 중복된 닉네임 등)이 나오게 되면 onSubmit이 작동을 안되네요..

이것을 수정하려고 구글링을 해봤지만 결국 답을 찾을 수가 없었습니다. 이유조차 찾을 수가 없었네요.. 결국 onSubmit에 있는 기능들을 빼서 버튼에 onClick을 추가하고 기능을 옮겨서 해결하였습니다

```jsx
const onSubmit = async (data) => {
  console.log(data);
  // let contentType = "multi-part/form-data";
  // //request(body)-> image 보내기
  // const form = new FormData();
  // form.append(
  //   "imageValue",
  //   getValues("image") === undefined ? null : getValues("image")[0]
  // );
  // //마지막 페이지, 이메일, 닉네임 토큰이 있을 때에만 onSubmit사용
  // if (level === 3) {
  //   try {
  //     const res = await api(contentType).post(
  //       `/auth/signup?password=${getValues(
  //         "password"
  //       )}&nicknameVerifyToken=${getValues(
  //         "nicknameVerifyToken"
  //       )}&emailVerifyToken=${getValues("emailVerifyToken")}`,
  //       form
  //       // { headers: { "Content-Type": "multi-part/form-data" } }
  //     );
  //     console.log(res);
  //     alert(res.data.message);
  //     // setCompletion(true);
  //     navigate("/signUp/complete");
  //   } catch (err) {
  //     console.log(err);
  //   }
  // }
};
const completionRegister = async () => {
  let contentType = "multi-part/form-data";
  //request(body)-> image 보내기
  const form = new FormData();
  form.append(
    "imageValue",
    getValues("image") === undefined ? null : getValues("image")[0]
  );
  //마지막 페이지, 이메일, 닉네임 토큰이 있을 때에만 onSubmit사용
  try {
    const res = await api(contentType).post(
      `/auth/signup?password=${getValues(
        "password"
      )}&nicknameVerifyToken=${getValues(
        "nicknameVerifyToken"
      )}&emailVerifyToken=${getValues("emailVerifyToken")}`,
      form
      // { headers: { "Content-Type": "multi-part/form-data" } }
    );
    console.log(res);
    // alert(res.data.message);
    setCompletion(true);
    setTimeout(() => {
      navigate("/signUp/complete");
    }, 1000);
  } catch (err) {
    console.log(err);
  }
};
///
<StButton
  onClick={completionRegister}
  disabled={
    (level === 3 && watch("image") === undefined) ||
    (level === 3 && watch("image")?.length === 0) ||
    isSubmitting ||
    completion
  }
>
  계속하기
</StButton>;
```

어떻게든 onSubmit에서 실행되게끔 하려고 했지만, 도저히 방법을 찾지 못해서 onClick으로 해결했습니다.. 이렇게 해보니 실행은 되네요.. 이유를 알고 싶네요 ㅠㅠ

그래도 어찌저찌해서 실행이 되고 완성(?)에 가까워지고 있는 것 같아서 좋습니다. 2주? 3주? 이 정도밖에 남지 않았는데요.. 남은 기간동안 더 화이팅하도록 하겠습니다! 우리 팀원분들 최고 !! 화이팅!
