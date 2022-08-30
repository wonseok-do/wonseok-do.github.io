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

오늘 로그인과 회원가입 기능을 조금 구현해보았습니다. 이번에는 react-hook-form으로 만들었는데요. 처음 사용해보는 것이기에 react-hook-form 홈페이지나 유튜브, 블로그 등 여러 곳에서 찾아보면서 공부해보고 사용했습니다. 아직 이해 안되는 부분도 있고 많은 기능들을 다 알지 못하기에 일단 쓸 수 있는 것만 보고 사용했습니다.

**register**

쓰는 방법이 달라서 찾아보았더니 버전에 따라서 다른 것이였네요.

```jsx
//version6
<input name="email" ref={register}/>
//version7
<input {...register("email")}/>
```

그리고 register({required:true)} 등 안에 여러가지 기능들을 추가하여 사용할 수 있습니다 pattern 같은 것들을 사용해서 value 값에 정규식 표현을 추가하여 그거에 맞는 값을 출력할 수도 있습니다.

errors 메시지도 표현하기 쉬웠습니다.

```jsx
<input
  type="text"
  placeholder="test@email.com"
  autoComplete="off"
  maxLength={20}
  {...register("email", {
    required: "이메일은 필수 입력입니다.",
    pattern: {
      value: /\S+@\S+\.\S+/,
      message: "이메일 형식에 맞지 않습니다.",
    },
  })}
/>;
{
  errors.email && <p>{errors.email.message}</p>;
}
```

하나하나 state값을 주고 그것을 onChange에 넣어서 하던 것들이 이렇게 쉬워졌네요.. 그러나 완벽하게 사용하기에는 더 공부해야 할 것 같습니다. 아직 모르는 기능들도 너무 많구요…

**formstate:{ isSubmitting }**
중복 제출 방지
button -> disabled 속성에 isSubmitting 추가
버튼을 눌렀을 때 제출처리가 끝날 때까지 비활성화가 됨
끝났을 경우 다시 활성화

```jsx
<button type="submit" disabled={isSubmitting}>
  완료
</button>
```

**password_confirm 방법**

1. ref 생성
   const password = useRef();
2. watch를 이용하여 password 필드 값 가져오기
   password.current = watch("password");
3. 가져온 password 값을 ref.current에 넣어주기
   watch를 이용하여 password 값을 password.current에 넣는다
   <input {...register("password_confirm"{validate:(value)=>value===password.current})}/>
   input 안에서 validate의 value 값과 password.current 값 비교

```jsx
const password = React.useRef();
  password.current = watch("password");
...
<input
          type="password"
          {...register("password_confirm", {
            required: "비밀번호 재입력은 필수입니다.",
            validate: (value) => value === password.current,
          })}
        />
```

이렇게 새로운 기능들을 공부하고 사용하니 기분이 좋네요! 지금 팀원분들과 다 같이 으쌰으쌰하면서 열심히 공부하고 있습니다. 모르는 것들은 서로서로 알려주면서 말이죠! 지금보다 더 열심히 공부해서 팀원분들한테 민폐끼치지 않도록 하겠습니다!! 더 힘내보도록 하겠습니다 화이팅!!!!!!
