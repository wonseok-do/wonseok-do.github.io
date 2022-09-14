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

회원가입페이지에서 회원가입 이후에 단계적으로 설명하는(?) 페이지가 추가되어서 구현했습니다.

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/042cbae3-e7f5-4777-b115-87d29657972a/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220914%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220914T165141Z&X-Amz-Expires=86400&X-Amz-Signature=444d2d5dee9e670ade7931089cbcedda5bd1864c80ff6458cb0901106cde90f1&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

이미지 밑에 있는 o o o 이것을 단계가 지나갈 때마다 색이 바뀌어야 하는데 어떻게 구현해야 하는지에 대해 고민을 했습니다. 처음에는 프로그래스바로 구현을 할까 하다가 점점 더 복잡해지는 것 같아서 그냥 삼항연산자를 사용하여 조건에 맞을 때에만 검은색이 아닐 경우에는 회색이 나오도록 구현했습니다

```jsx
import React, { useState } from "react";
import { useNavigate } from "react-router-dom";

import styled from "styled-components";

import CompleteOne from "../components/RegisterComplete/CompleteOne";
import CompleteTwo from "../components/RegisterComplete/CompleteTwo";
import CompleteThree from "../components/RegisterComplete/CompleteThree";

const RegisterComplete = () => {
  const [level, setLevel] = useState(0);
  const navigate = useNavigate();
  const clickLevel = () => {
    setLevel((prev) => prev + 1);
    if (level === 2) {
      navigate("/signIn");
    }
  };

  return (
    <div>
      {level === 0 && <CompleteOne />}
      {level === 1 && <CompleteTwo />}
      {level === 2 && <CompleteThree />}
      <StCounts>
        {level === 0 ? (
          <StCount color="#393939"></StCount>
        ) : (
          <StCount color="#CDCDCD"></StCount>
        )}
        {level === 1 ? (
          <StCount color="#393939"></StCount>
        ) : (
          <StCount color="#CDCDCD"></StCount>
        )}
        {level === 2 ? (
          <StCount color="#393939"></StCount>
        ) : (
          <StCount color="#CDCDCD"></StCount>
        )}
      </StCounts>
      {level !== 2 ? (
        <StBtn onClick={clickLevel}>계속하기</StBtn>
      ) : (
        <StBtn onClick={clickLevel}>시작하기</StBtn>
      )}
    </div>
  );
};

export default RegisterComplete;

const StBtn = styled.button`
  position: absolute;
  width: 90%;
  height: 59px;
  top: 689px;
  color: #eee;
  background: #101010;
  border: 1px solid #101010;
  border-radius: 10px;
  left: 5%;
`;
const StCounts = styled.div`
  display: flex;
  position: absolute;
  top: 600px;
  left: 240px;
  gap: 30px;
`;
const StCount = styled.div`
  background: ${(props) => props.color};
  width: 20px;
  height: 20px;
  border-radius: 50%;
`;
```

일단 구현하는 것에만 집중했고 이것을 어떻게 조금 더 단순하게 코드를 줄일 수 있을 것 같은데

그것은 프로젝트가 어느정도 완성이 되면 그때 가서 수정해보려고 합니다.

그리고 비밀번호 찾기도 구현해보았는데요. 백엔드분들께서 api를 너무 잘해놓으셔서.. 전 그냥

데이터만 보내면 되었네요.. 백엔드분들 짱짱!!

```jsx
import React from "react";
import { useForm } from "react-hook-form";
import { useNavigate } from "react-router-dom";

import api from "../server/api";

import CheckEmail from "../components/resetPassword/CheckEmail";

import styled from "styled-components";

import arrowBack from "../assets/svg/arrow_back.svg";

const ResetPassword = () => {
  const contentType = "application/x-www-form-urlencoded";
  const navigate = useNavigate();
  const {
    register,
    watch,
    handleSubmit,
    getValues,
    formState: { errors, isSubmitting },
  } = useForm({ criteriaMode: "all", mode: "onChange" });

  const onSubmit = async () => {
    try {
      const res = await api(contentType).get(
        `/auth/send-password?email=${getValues("email")}`
      );
      console.log(res);
      alert(res.data.message);
      navigate("/signIn");
    } catch (err) {
      console.log(err);
      alert(err.response.data.message);
    }
  };
  const before = () => {
    navigate("/signIn");
  };

  return (
    <div>
      <StForm onSubmit={handleSubmit(onSubmit)}>
        <StSpanBox>
          <StArrowBack src={arrowBack} alt="뒤로가기" onClick={before} />
          <StSpanCenter>비밀번호 찾기</StSpanCenter>
        </StSpanBox>
        <CheckEmail register={register} errors={errors} />
        <StButton
          disabled={
            watch("email") === undefined ||
            watch("email") === "" ||
            isSubmitting
          }
        >
          계속하기
        </StButton>
      </StForm>
    </div>
  );
};

export default ResetPassword;

const StSpanBox = styled.div`
  display: flex;
  padding-top: 20px;
`;
const StArrowBack = styled.img`
  width: 25px;
  height: 25px;

  cursor: pointer;
`;
const StSpanCenter = styled.span`
  margin: auto;
  font-size: 20px;
`;
const StForm = styled.form`
  display: flex;
  flex-direction: column;
  & > div > label {
    margin-top: 20px;

    font-size: 30px;
    font-weight: bold;
  }
  & p {
    color: #bf1650;
  }
  & input {
    margin-top: 20px;
    margin-bottom: 20px;

    border: none;
    border-bottom: 3px solid #b4b3b3;

    font-size: 20px;
    :hover,
    :focus {
      outline: none;
      border-bottom-color: #000;
    }
    ::placeholder {
      color: #ddd;
    }
  }
`;
const StButton = styled.button`
  border-radius: 10px;

  margin-top: 250px;
  padding: 15px;

  background-color: #fff;
  border: 3px solid #eee;
  color: #a3a2a2;

  font-size: 18px;
  text-align: center;

  :disabled {
    pointer-events: none;
  }
  :hover {
    background-color: #000;
    border: none;
    color: #fff;
  }
`;
```

이메일에 임시 비밀번호가 발급이 되는데요. 발급한 것 밑에 완료(?)버튼이 있는데 그것을 누르게 되면 로그인페이지가 새 창으로 뜨게 되면서 비밀번호가 임시 비밀번호로 바뀌게 됩니다!

로그인을 할 때 기존 이메일과 임시 비밀번호를 입력하면 로그인이 되는 방식입니다.

그리고 마이 페이지에서 비밀번호를 수정할 수 있게 구현하려고 합니다. 일단 오늘은 이 정도까지 구현을 해보았습니다. 아직 부족한 게 많지만 기능 구현이 잘 되어가고 있어서 좋네요! 내일도 화이팅하겠습니다! 화이팅!!!!!!!!!!!!
