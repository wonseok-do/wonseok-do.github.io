---
layout: single
title: "회원가입 초안"
categories: coding
tag: [python, jekyll, blog]
toc: true
author_profile: false
sidebar:
  nav: "docs"
# search: false
---

회원가입 react-hook-form 사용

```jsx
import React from "react";
import styled from "styled-components";
import { useForm } from "react-hook-form";
import { useNavigate } from "react-router-dom";

const Register = () => {
  const navigate = useNavigate();
  const {
    register,
    watch,
    handleSubmit,
    formState: { errors, isSubmitting },
  } = useForm();
  const password = React.useRef();
  password.current = watch("password");

  const onSubmit = (data) => console.log(data);

  return (
    <StDiv>
      <StForm onSubmit={handleSubmit(onSubmit)}>
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
        <label>닉네임</label>
        <input
          placeholder="닉네임"
          minLength={2}
          maxLength={10}
          {...register("nickname", {
            required: "닉네임은 필수 입력입니다.",
            pattern: {
              value: /^(?=.*[a-zA-Z0-9가-힣])[a-zA-Z0-9가-힣]{2,10}$/,
              message: "닉네임은 2~10자이며, 한글, 영어, 숫자포함합니다.",
            },
          })}
        />
        {errors.nickname && <p>{errors.nickname.message}</p>}
        <label>비밀번호</label>
        <input
          type="password"
          placeholder="***********"
          minLength={8}
          maxLength={15}
          {...register("password", {
            required: "비밀번호는 필수 입력입니다.",
            pattern: {
              value: /^.*(?=^.{8,15}$)(?=.*\d)(?=.*[a-zA-Z])(?=.*[!@#]).*$/,
              message:
                "비밀번호는 문자, 숫자, 특수문자(!@#) 각 1개씩 포함하며 8글자 이상, 15글자 이하입니다",
            },
          })}
        />
        {errors.password && <p>{errors.password.message}</p>}
        <label>비밀번호 재확인</label>
        <input
          type="password"
          {...register("password_confirm", {
            required: "비밀번호 재입력은 필수입니다.",
            validate: (value) => value === password.current,
          })}
        />
        {errors.password_confirm && <p>{errors.password_confirm.message}</p>}
        {errors.password_confirm &&
          errors.password_confirm.type === "validate" && (
            <p>비밀번호가 일치하지 않습니다.</p>
          )}
        <button type="submit" disabled={isSubmitting}>
          완료
        </button>
        <button onClick={() => navigate("/signIn")}>취소</button>
      </StForm>
    </StDiv>
  );
};

export default Register;

const StDiv = styled.div`
  width: 350px;
`;
const StForm = styled.form`
  display: flex;
  flex-direction: column;
  & p {
    color: #bf1650;
  }
`;
```

앞선 로그인과 비슷합니다. 추가적으로 errors의 type에 따른 message를 띄우는 것과

password_confirm에서 useRef()사용과 watch사용입니다.

errors → message : {errors.password_confirm && errors.password_confirm.type === "validate" && (<p>비밀번호가 일치하지 않습니다.</p>)}

type 쓰는 경우 (2가지 이상의 errors를 추가) 그거에 맞는 것만 발생 -> 조건에 맞을 시 errors → message 가 없어집니다

**password_confirm의 validate: (value) => value === password.current만 쓸 경우 에러발생**

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/414d3d3f-43c5-4b5a-927e-4143d2e643a4/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220830%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220830T142637Z&X-Amz-Expires=86400&X-Amz-Signature=afc34a01b0dff7efc8e286b31ba939fdbf0b53822392fbc869f8e6822c55cea0&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

해결 : const password = React.useRef(); password.current = watch("password"); 추가

1. ref 생성
   const password = useRef();
2. watch를 이용하여 password 필드 값 가져오기
   password.current = watch("password");
3. 가져온 password 값을 ref.current에 넣어주기
   watch를 이용하여 password 값을 password.current에 넣는다
   <input {...register("password_confirm"{validate:(value)=>value===password.current})}/>
   input 안에서 validate의 value 값과 password.current 값 비교
