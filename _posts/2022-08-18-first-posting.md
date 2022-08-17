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

오늘은 정리해보는 시간을 가져보려고 합니다. 아직 정리가 덜 되어있긴 하지만요 ㅎㅎ..

일단 아이디, 닉네임 중복 체크에서 너무 많이 막혔는데 조금은 해결되어서 먼저 써보겠습니다.

```jsx
const [checkEmail, setCheckEmail] = useState({ email: "" });
const [checknickname, setChecknickname] = useState({ nickname: "" });
const [dupEmail, setDupEmail] = useState(false);
const [dupnickname, setDupnickname] = useState(false);

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
```

데이터를 보낼 이메일과 닉네임을 만든 후 url에 데이터를 보냈을 때 돌아오는 result 값이 true 일 경우 사용 가능하고 false일 경우 불가능하게 만들었습니다. 데이터를 보내는 것을 처음에 제대로 만들지 못하기도 했지만 만들지 않고 post했을 때 어떠한 값이 들어오는 지 console로 찍어보면서 하려고 했는데 console에서 계속 400에러가 떴습니다. 제가 잘못된 요청을 보내서 그런가보다하고 데이터를 어떻게 해서 보내지? 하고 서칭하면서 해보았지만 결국 찾을 수 없었고 팀원분들에게 도움을 청했습니다. 결국 제 잘못이 아닌 백엔드쪽에서 오류가 난 거였습니다… 그래도 해결해서 다행이였습니다. 물론 그걸 해결하려고 시간을 많이 소비하기는 했지만.. 팀원분들에게 민폐를 끼치지 않고 해결하려다 보니 이렇게 되었네요. 그래도 저는 괜찮았습니다. 팀원분들이 괜찮았을 지는 모르겠지만요… ㅠ

로그인에서 토큰을 통해 로그인과 로그아웃 기능을 만들어봤습니다. react-cookie를 사용했습니다.

```jsx
const [cookies, setCookie] = useCookies(["token"]);
const onSubmit = async () => {
  axios
    .post("http://taesik.shop/api/user/login", loginData)
    .then((result) => {
      let expires = new Date();
      expires.setMinutes(expires.getMinutes() + 60);

      console.log(result);

      setCookie("token", result.data.token, { path: "/", expires });
      dispatch(logIn());

      navigate("/");
    })
    .catch((e) => {
      console.log(e);
    });
};
//
const logOut = () => {
  removeCookie("token"); // 쿠키를 삭제
  navigate("/"); // 메인 페이지로 이동
};
```

setCookie를 통해 토큰을 쿠키에 들어갑니다. removeCookie를 통해 쿠키를 삭제하여 로그아웃을 구현하였습니다. token을 사용해서 포스트 작성 등을 할 때 작성, 수정을 할 수 있게 하려고 했지만 그것까지는 구현하지 못했습니다. 그러나 팀원분이 api.interceptors을 만들어서 토큰을 사용할 수 있게

구현했더군요.. 코드를 봤지만 제가 모르는 부분이 너무 많아 이해를 거의 못했습니다.. ㅠㅠ 저도 저렇게 쓸 수 있다면 좋았을텐데…^^;;

오늘은 이렇게 마무리하는 시간을 가졌지만.. 하다보니 현타가 와서.. 좀 정신적으로 힘들었습니다. 아 내가 한 부분이 많이 없구나 하고요.. 매니저님들과 상담도 많이 가졌습니다. 덕분에 힘이 좀 나네요 ㅎㅎ.. 기술매니저님과 상담을 하면서 에러부분도 조금씩 고쳐나갔습니다.

```jsx
const onCheckEmail = async () => {
  const res = await axios
    .post("http://taesik.shop/api/user/dup/email", checkEmail)
    .then((res) => {
      if (res.data.result) {
        alert("사용가능한 이메일이야");
        setDupEmail(true);
      }
    })
    .catch((res) => {
      console.log(res.response.data.result);
      if (res.response.status === 400) {
        alert("이미 존재하는 이메일이야");
      }
    });
};
const onChecknickname = async () => {
  const res = await axios
    .post("http://taesik.shop/api/user/dup/nickname", checknickname)
    .then((res) => {
      if (res.data.result) {
        alert("사용가능한 닉네임이야");
        setDupnickname(true);
      }
    })
    .catch((res) => {
      console.log(res);
      if (res.response.status === 400) {
        alert("이미 존재하는 닉네임이야");
      }
    });
};
//
await axios
  .post("http://taesik.shop/api/user/signup", data)
  .then((response) => {
    if (response.data.result === true) {
      navigate("/login");
    }
  })
  .catch((response) => {
    console.log("catch=", response.response.status);
    if (response.response.status === 400) {
      alert("다시 한 번 확인해봐");
    }
  });
```

맨 밑에 있는 부분에서 에러가 떴을 때 어떻게 alert을 띄워주는 지 설명해주셨고.. 그것을 바탕으로 제가 수정하고 싶은 부분들을 수정하였습니다. 잘 작동하네요 ㅎㅎ 매니저님 감사합니다!!!!

에러를 .then에서 실행하다 보니 실행이 안되었습니다. .then에서 오류나면 실행이 안되고, .catch를 통해 오류를 뜨게 합니다. try와 catch도 있는데요. try는 실행을 하지만 오류가 나면 catch로 넘어가 catch로 오류를 뜨게 합니다. 이 부분이 try와 then의 차이점이 아닌가 싶습니다. 아직 많이 사용해보지 않아서 미숙하지만.. 계속해서 에러를 달고 살아야 하는 만큼 잘 숙달할 수 있도록 노력해보겠습니다.. 오늘 하루 처음과 중간이 좋진 않았지만.. 끝이 생각보다 잘 마무리 된거 같아서 기분이 나쁘지는 않네요 내일 드디어 배포하는 날인데요 마지막까지 최선을 다해서 잘 마무리할 수 있도록 하겠습니다. 나 자신 그리고 우리 팀원들 화이팅!!!!
