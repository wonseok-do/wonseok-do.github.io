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

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/3d2d4caa-cf74-48b6-9036-a07544913ec9/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220831%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220831T175648Z&X-Amz-Expires=86400&X-Amz-Signature=e3b8b53c3d5f03efb9c82fc27884758e5ca9bf5a990285872628fbe4183f699d&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

오늘 디자이너분께서 회원가입 페이지를 새로 만들어주셔서 이거에 맞게 컴포넌트를 나눠야 할 것 같아서 나눠보았습니다.

```jsx
const [level, setLevel] = React.useState(0);
...
<StDiv>
      <StForm onSubmit={handleSubmit(onSubmit)}>
        <button onClick={before} disabled={level === 0}>
          &lt;
        </button>
        {level === 0 && <Email register={register} errors={errors} />}
        {level === 1 && (
          <Password register={register} errors={errors} watch={watch} />
        )}
        {level === 2 && (
          <Image register={register} errors={errors} watch={watch} />
        )}
        {level === 3 && <Nickname register={register} errors={errors} />}

        /
        /
        /
      </StForm>
    </StDiv>
```

이렇게 나눠보는 것은 첨이라 팀원분의 도움을 받고 나눠보았습니다. level에 따라서 그거에 맞는 것만 출력하게끔 하였습니다. 뒤로가기 버튼을 만들었을 때 데이터가 날아가지 않을까 했지만 부모 컴포넌트에서 관리하고 있어서 그런 걱정은 하지 않아도 되었네요.

```jsx
const next = () => {
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
  if (errors.image && level === 2) {
    alert("이미지를 추가해 주세요");
  }
  if (errors.nickname && level === 3) {
    alert("닉네임을 제대로 입력해주세요");
    return;
  }
  setLevel((prev) => prev + 1);
};
const before = () => {
  setLevel((prev) => prev - 1);
};
```

버튼을 만들어서 추가적으로 onClick을 했을 때 level을 추가하고 빼는 식으로 이메일, 패스워드 등 필요한 곳이 뜰 수 있게 하였고, 추가적으로 조건식을 넣어서 버튼을 누를 수 있게 하는 것과 알림을 뜨게 만들었습니다. 각각의 자식 컴포넌트에 props을 내려주어 useForm()을 사용할 수 있게 하였구요. 이렇게 조금씩 조금씩 컴포넌트를 나누고 조건식넣고 제 손으로 짜보니 기분이 매우 좋네요.

다른 것은 조금 괜찮았지만 이미지넣는 건 처음이다 보니 조금 해멨습니다.

```jsx
const Image = (props) => {
  const { register, errors, watch } = props;
  const [imagePreview, setImagePreview] = React.useState(
    "https://cdn.pixabay.com/photo/2015/10/05/22/37/blank-profile-picture-973460_1280.png"
  );
  const image = watch("image");

  React.useEffect(() => {
    if (image && image.length > 0) {
      const file = image[0];
      setImagePreview(URL.createObjectURL(file));
    }
  }, [image]);

  return (
    <StDiv>
      <label>프로필 이미지</label>
      <StImg src={imagePreview} />
      <input
        type="file"
        id="picture"
        {...register("image")}
        accept="image/*"
        style={{ display: "none" }}
      />
      {errors.image && <p>이미지를 추가해 주세요</p>}
      <div className="labelButton">
        <label htmlFor="picture">사진 선택</label>
      </div>
    </StDiv>
  );
};
```

state로 지정해주는 것과 register를 사용하여 useEffect()에서 이미지 미리보기 등을 구현할 때 생각보다 할만했습니다. URL.createObjectURL()를 사용하는 것도 신기했구요. 쉽게 url를 출력하다니..

input 에서 type=”file”로 추가하면 파일 추가? 라는 예쁘지 않은 버튼이 생기는데요. 그래서

display:”none” 주었고 버튼을 추가해서 onClick 함수를 사용하려고 했으나 image에 대한 current 값을 찾을 수가 없어 포기했습니다. 그래서 다른 방법을 찾다가 label을 사용해서 구현하게 되었습니다.

input 안에 있는 id 값을 label의 htmlFor 값에 넣으면 사용할 수 있는데요. 그것을 통해 눌렀을 때 파일 추가 기능을 사용할 수 있었습니다. 그러나 label만 덩그러니 있으면 예쁘지 않아 div로 감싸서 박스 형태로 만들어 구현해봤습니다. 오늘 시도해본 것들이 정말 많았는데요. 조금씩 조금씩 구현할 수 있어서 너무 좋았습니다. 이렇게 조금씩 나아가도록 하겠습니다. 화이팅!!!!!!!!!!!!!
