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

회원가입 페이지에서 버튼의 위치가 변하지 않고 일정하게 있었으면 좋겠다고 하셔서

props로 값을 변경해서 위치를 통일 시켰습니다 ㅠㅠ 요소에서 일일이 다 확인하고

위치 계산하고 수정하고 했네요..ㅎㅎ 어떻게든 되어서 다행이네요 ㅠ

onClick을 했을 때 한 번만 보내야 되는데 빨리 클릭하게 되면 중복해서 보내게 됩니다

이것을 해결하려고 했는데 이 방법이 맞는지는 모르겠네요.. 일단은 됩니다..

onSubmit에서는 isSubmitting로 버튼에 disabled 걸어놓으면 되지만, onClick은 안됨원하는 방향으로 해결 방법을 찾지 못해 다르게 생각함 → 클릭을 했을 때 setTimeout으로 1초로 설정해두어 최소한 1초라는 시간 동안에 중복클릭을 못하는 것을 방지 → state값도 추가

```jsx
// Register.jsx
const [check, setCheck] = useState(false);

const completionRegister = async () => {
  setCheck(true);
  setTimeout(() => {
    setCheck(false);
  }, 1000);
  let contentType = "multi-part/form-data";
  //request(body)-> image 보내기
  const form = new FormData();
  form.append(
    "imageValue",
    getValues("image") === undefined ? null : getValues("image")[0]
  );
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
      navigate("/sign-up/complete");
    }, 1000);
  } catch (err) {
    console.log(err);
  }
};
<StButton
  onClick={completionRegister}
  disabled={
    check ||
    (level === 3 && watch("image") === undefined) ||
    (level === 3 && watch("image")?.length === 0) ||
    completion
  }
>
  계속하기
</StButton>;
```

클릭하자마자 state값을 변경하여 disabled을 걸어 클릭하지 못하게 만들었습니다

이런 방법이 맞는 지 의문이지만 일단 되니깐요.. 음.. 모르겠네요..

그리고 회원가입 중에 프로필 이미지가 비었을 때 기본 이미지가 보여야 하는데 보이지 않는

에러가 발생해 그것도 수정했습니다

```jsx
React.useEffect(() => {
  if (image && image.length > 0) {
    const file = image[0];
    setImagePreview(URL.createObjectURL(file));
  }
  if (image?.length === 0) {
    setImagePreview("");
  }
  console.log(image);
}, [image]);
```

useEffect에 이미지가 없을 때도 추가하였습니다. 이제 배포하고 마켓팅해야 돼서 에러 부분들을

고치는 데 시간을 거의 다 소비하고 있습니다. 저보다 팀원분들이 더 고생을 하고 있어서 저도

더 분발해야겠습니다!! 오늘도 이렇게 잘 해결해서 좋습니다!! 계속해서 화이팅하겠습니다!!
