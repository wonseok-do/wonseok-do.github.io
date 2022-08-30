---
layout: single
title: "로그인 초안"
categories: coding
tag: [python, jekyll, blog]
toc: true
author_profile: false
sidebar:
  nav: "docs"
# search: false
---

## 로그인 페이지 react-hook-form 사용

```jsx
import React from "react";
import styled from "styled-components";
import { useForm } from "react-hook-form";
import { Link } from "react-router-dom";

const Login = () => {
  const {
    register,
    handleSubmit,
    watch,
    reset,
    formState: { isSubmitting, isDirty, errors },
  } = useForm();
  const onSubmit = (data) => console.log(data);

  return (
    <Stdiv>
      <Stform onSubmit={handleSubmit(onSubmit)}>
        <label>이메일</label>
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
        />
        {errors.email && <p>{errors.email.message}</p>}
        <label>비밀번호</label>
        <input
          type="password"
          placeholder="**********"
          maxLength={15}
          {...register("password", {
            required: "비밀번호는 필수 입력입니다",
            pattern: {
              value: /^.*(?=^.{8,15}$)(?=.*\d)(?=.*[a-zA-Z])(?=.*[!@#]).*$/,
              message:
                "비밀번호는 문자, 숫자, 특수문자(!@#) 각 1개씩 포함하며 8글자 이상, 15글자 이하입니다",
            },
          })}
        />
        {errors.password && <p>{errors.password.message}</p>}
        <button type="submit" disabled={isSubmitting}>
          로그인
        </button>
      </Stform>
      <Link to="/signUp">회원가입</Link>
    </Stdiv>
  );
};

export default Login;

const Stdiv = styled.div`
  width: 350px;
`;
const Stform = styled.form`
  display: flex;
  flex-direction: column;
  & p {
    color: #bf1650;
  }
`;
```

version6 → version7 register 활용

<input name="email" ref={register} /> => 이 부분이 우선 바뀌었습니다. ref={register} 로 하지 않고
<input name="email" { ...register("email) } /> 이렇게 하면 동작합니다. 그리고 register() 의 값으로 value 를 넣어주기 때문에 name 속성이 꼭 필요한 게 아니라면, name 속성을 입력하지 않고

{ ...register("email") } 로 제어할 수 있습니다. name 속성의 값과 상관없이 watch() 안에 들어오는 value 는 register() 의 value 입니다.

추가로 register 옵션은 { ...register("email", { required: true }) } 이렇게 됩니다. pattern 등을 추가하여

정규식을 활용할 수 있고, errors를 통해 정규식에 맞지 않으면 errors메시지도 띄울 수 있게 합니다.

**watch**

console.log(watch(”name”) , <input {…register(”name”)}/> 콘솔에 name값이 출력됩니다.

**formstate:{ isSubmitting }**
중복 제출 방지
button -> disabled 속성에 isSubmitting 추가합니다.
버튼을 눌렀을 때 제출처리가 끝날 때까지 비활성화가 됩니다.
끝났을 경우 다시 활성화합니다.
