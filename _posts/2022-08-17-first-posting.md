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

항해 6주차를 맞이하면서 벌써 5일이 지났습니다 ㅠㅠㅠ 시간이 엄청 빠르게 지나가네요..

처음으로 백엔드분들과 팀 프로젝트를 하게 되었는데요. 시작했을 때 프론트엔드와 백엔드에서

분리해서 작업하면 좀 더 쉽게 팀 프로젝트를 완성하지 않을까 싶었지만 그렇지 않더군요…

하루하루 열심히 TIL 적으면서 하려고 했지만 핑계 아닌 핑계지만… 제 실력이 너무 너무 부족해서

하루종일 서칭하고 물어보고 하는 시간들이 너무나도 빨리 지나가서… TIL 적을 시간이 없었습니다..

오늘 조~~금 정리가 되어서 적는 시간이 생겨 적게 되었습니다! 와이어프레임을 하고 그것으로

구역을 나눠 하기로 정했습니다. 정하는 방식은 사다리타기로 했는데 로그인과 회원가입이 걸렸습니다. 해본 적이 없어서 막막하긴 했지만 일단 뷰 먼저 어느정도 그려놓고 기능을 구현하는 방식으로 했습니다.

```jsx
const RegisterPage = () => {
  const navigate = useNavigate();
const [userId, setUserId] = useState("");
  const [password, setPassword] = useState("");
  const [confirmPassword, setConfirmPassword] = useState("");
  const [nickname, setnickname] = useState("");

  const [data, setData] = useState({
    email: "",
    password: "",
    nickname: "",
  });

  const [userIdError, setUserIdError] = useState(false);
  const [passwordError, setPasswordError] = useState(false);
  const [confirmPasswordError, setConfirmPasswordError] = useState(false);
  const [nicknameError, setnicknameError] = useState(false);
  const [checkEmail, setCheckEmail] = useState({ email: "" });
  const [checknickname, setChecknickname] = useState({ nickname: "" });
  const [dupEmail, setDupEmail] = useState(false);
  const [dupnickname, setDupnickname] = useState(false);

  //이메일 정규식
  const onChangeUserId = (e) => {
    const userIdRegex = /^[a-zA-Z0-9+-_.]+@[a-zA-Z0-9-]+.[a-zA-Z0-9-.]+$/;
    if (!e.target.value || userIdRegex.test(e.target.value))
      setUserIdError(false);
    else setUserIdError(true);
    setUserId(e.target.value);
    setData({ ...data, email: e.target.value });
    setCheckEmail({ email: e.target.value });
  };
  //비밀번호 정규식
  const onChangePassword = (e) => {
    const passwordRegex =
      /^(?=.*[A-Za-z])(?=.*\d)(?=.*[@!%*#?&])[A-Za-z\d@!%*#?&]{8,13}$/;
    if (!e.target.value || passwordRegex.test(e.target.value))
      setPasswordError(false);
    else setPasswordError(true);

    if (!confirmPassword || e.target.value === confirmPassword)
      setConfirmPasswordError(false);
    else setConfirmPasswordError(true);
    setPassword(e.target.value);
    setData({ ...data, password: e.target.value });
  };
  const onChangeConfirmPassword = (e) => {
    if (password === e.target.value) setConfirmPasswordError(false);
    else setConfirmPasswordError(true);
    setConfirmPassword(e.target.value);
    // setData({ ...data, confirmPassword: e.target.value });
  };
  //닉네임정규식
  const onChangenickname = (e) => {
    const nicknameRegex = /^[a-zA-Zㄱ-힣0-9-_.]{2,12}$/;
    if (!e.target.value || nicknameRegex.test(e.target.value))
      setnicknameError(false);
    else setnicknameError(true);
    setnickname(e.target.value);
    setData({ ...data, nickname: e.target.value });
    setChecknickname({ nickname: e.target.value });
  };
  //이메일중복확인
  const onCheckEmail = async () => {
    const res = await axios
      .post("http://taesik.shop/api/user/dup/email", checkEmail)
      .then((res) => {
        if (res.data.result) {
          alert("사용가능한 이메일이야");
          setDupEmail(true);
        } else {
          alert("이미 있어");
        }
      });
  };
  //닉네임중복확인
  const onChecknickname = async () => {
    const res = await axios
      .post("http://taesik.shop/api/user/dup/nickname", checknickname)
      .then((res) => {
        if (res.data.result) {
          alert("사용가능한 닉네임이야");
          setDupnickname(true);
        } else {
          alert("이미 있어");
        }
      });
  };
...
}
```

백엔드분과 정규식을 어떻게 할 건지 맞춰보고 진행을 했습니다. 정규식 사용과 어떻게 값을 지정해야 할지 너무 막막해서 서칭을 정말 많이 했습니다. 어느 정도 코드를 따와서 어떤 식으로 돌아가는지 알아보려고 코드를 뚫어지게 계속 봤었네요.. 제 손으로 짜는 코드가 거의 없어서.. 이렇게 해도 되나 싶을 정도로 고민이 많아졌어요 ㅠㅠ 제 자신이 이 정도밖에 안되는 거 같아서 뭔가 한심한 거 같네요.. 대충 로그인과 회원가입 기능이 얼추 완성은 되었는데요 아직 에러가 뜨거나 하는 부분들도 있어서 계속해서 조금씩 수정을 해봐야 할 거 같습니다. 이제 이틀 정도 남았는데요. 그때까지 팀원분들과 무사히 잘 마무리할 수 있도록 더 노력하겠습니다.. 실전 프로젝트까지 얼마 남지 않아서.. 남은 기간 동안 더 잘해질 수 있을까 생각이 들지만 그래도 잘 안되더라도 열심히 노력하겠습니다!! 화이팅!
