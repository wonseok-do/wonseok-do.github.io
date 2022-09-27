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

이틀간 유저피드백을 받았는데요.. 정말 무시무시했습니다.. 제가 맡았던 회원가입, 로그인 페이지부터 문제가 생겨 진땀을 흘렸네요.. 일단 회원가입이 조금 힘들다는 말도 있었고, 오류가 떠서 안된다는 말도 있었습니다.. 프로필 사진 이슈문제.. 유효성검사 등 제대로 잘 안되더군요.. 그래도 이렇게

확인을 할 수 있어서 좋았습니다. 수정하고 다시 시도해보고 서버를 닫았다가 켰다가 많이 했네요..

일단 어느 정도 고치긴 했지만.. 다시 또 문제가 생기는 지는 기다려봐야 할 것 같습니다.

전체적으로 문제가 생각보다 많이 생기더군요.. 에러를 다 잡기는 힘들지만.. 그래도 최대한 잡을 수 있는 것들은 다 잡아보려고 합니다. 에러를 해결할 때까지는 많이 힘들었지만.. 막상 해결하고 나면 기분이 좋더군요. 이런 기분을 느끼면서 개발을 하는 것 같습니다. 쉽지 않은 길이지만 재밌네요

막상 에러 터지면 기분이 조금 안 좋긴 하지만 그래도 고치고 나면 뿌듯한 기분 드네요 헤헤

불과 3개월 전.. 처음 코딩을 했을 때는 아무것도 못하고 콘솔도 못찍고 했었는데.. 조금씩 에러를 해결하면서 아 이 정도는 성장했구나를 느낍니다.. 뭔가 한 글자 한 글자 적을 수 있다는 게 신기하네요

```jsx
const getProfile = async () => {
  const contentType = "application/json";
  try {
    const res = await api(contentType).get("/profile/my-profile");
    console.log(res.data.user);
    setProfiles(res.data.user);
  } catch (err) {
    console.log(err);
  }
};
useEffect(() => {
  getProfile();
}, []);
///
<input
  defaultValue={profiles?.nickname}
  {...register("nickname", {
    pattern: {
      value: /^(?=.*[a-zA-Z0-9])[a-zA-Z0-9]{2,10}$/,
      message: "닉네임은 2~10자이며, 영어, 숫자포함합니다.",
    },
  })}
  type="text"
/>;
///
const [imagePreview, setImagePreview] = React.useState(profiles?.imageUrl);

const image = watch("imageValue");

const profileImg = image?.length === 0 ? profiles?.imageUrl : imagePreview;

React.useEffect(() => {
  if (image && image.length > 0) {
    const file = image[0];
    setImagePreview(URL.createObjectURL(file));
  }
  if (image?.length === 0) {
    setImagePreview(profiles?.imageUrl);
  }
}, [image]);

return (
  <StProfileEditHeader>
    <StProfilePic
      profileImg={profileImg}
      onError={(e) => (e.target.src = profiles?.resizedUrl)}
    >
      <label htmlFor="picture">
        <img src={editIcon} alt="프로필 이미지 수정" />
      </label>
    </StProfilePic>
    <input
      type="file"
      id="picture"
      {...register("imageValue")}
      accept="image/*"
    />
  </StProfileEditHeader>
);
```

원래 토큰을 사용해서 프로필 수정을 했었는데요.. 프로필을 수정할 때 바로 적용이 안되고 다시 로그인을 해야 적용이 되었습니다. 그래서 새로운 api가 나왔습니다. 토큰을 사용하지 않고 그것을 사용해서 이것을 props로 보내서 사용하는 방법을 택했습니다. 닉네임이나 비밀번호 등 수정하는 것은 괜찮았지만 이미지같은 경우에는 쉽지가 않았네요.. 하필 vscode까지 작동이 제대로 안되는 오류가 발생해서.. 정말 힘들었습니다.. 그래도 어떻게든 해결하려고 콘솔 한 번 찍고 다시 껐다가 키고 다시 찍고 이렇게 반복하면서 값 찾고 해결했습니다. 이미지는 이미지의 길이가 0일 때 원래 프로필이미지가 나오게 만들고 바뀐 값이 나와야되는데 기본 이미지값이 나오지 않아서 그것만 해결하는데 시간이 많이 걸렸습니다. 그거하나만 해결하는데 6시간 넘게 걸린 것 같네요.. ㅠㅠ 그래도 해결해서 다행이네요. 해결못했으면….. 끔찍.. 하루하루가 참.. 힘드네요.. 몸관리하면서 잘 버티도록 하겠습니다.

팀원분들 조금 더 화이팅해요!!! 화이팅!!
