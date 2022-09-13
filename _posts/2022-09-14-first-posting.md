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

그 전에 계속해서 고민했던 이메일과 닉네임 인증 관련해서 오늘 거의 다 해결되었습니다.

백엔드 깃헙 이슈에 올리고 백엔들분들과 얘기를 나누면서 해결하였습니다.

회원가입을 완료하지 못했을 경우 : 회원가입을 하다 중간에 새로고침이나 페이지 이탈 등 여러가지 상황

이럴 경우 토큰을 다 날리는 식으로 하였는데요. 그 대신 하루에 5번정도의 횟수를 정해두고 그 횟수를 초과했을 경우 24시간이 지난 후에 할 수 있도록 하였습니다. 그리고 인증 번호의 만료 시간을 두어 3분이 지나면 다시 인증번호를 재발급하도록 하게 하였습니다. 오늘 몇번의 테스트 결과 토큰값이 잘 없어져서 회원가입 하다가 다시 하게 되는 경우에 그 해당 이메일이 다시 인증이 되는 것을 확인하였지만 인증 번호 3분이 지났는데도 불구하고 인증 번호가 처리가 되는 문제가 발생하였습니다.

이 부분에 대해서 백엔드 이슈에 올렸고 백엔들분들께 말씀드렸습니다. 아마 내일쯤 해결이 될 것 같습니다. 그리고 인증 번호를 받고 3분이라는 시간이 지나는 것을 확인할 타이머도 추가하였습니다.

처음 구현하는 거여서 헤매기는 했지만 다행히 구현은 되었습니다.

```jsx
//Email.jsx
...
  const [minutes, setMinutes] = useState(3);
  const [seconds, setSeconds] = useState(0);
  const [checkTimer, setCheckTimer] = useState(false);
...
const sendEmailVerifyCode = async () => {
    try {
      const res = await api(contentType).get(
        `/auth/send-email?email=${getValues("email")}`
        // {
        //   headers: { "Content-Type": "application/x-www-form-urlencoded" },
        // }
      );
      console.log(res.data.message);
      setCheckEmail(true);
      alert(res.data.message);
      setMinutes(3);
      setSeconds(0);
      setCheckTimer(true);
    } catch (err) {
      console.log(err);
      alert(err.response.data.message);
    }
  };
...
<Timer
        minutes={minutes}
        setMinutes={setMinutes}
        seconds={seconds}
        setSeconds={setSeconds}
        checkTimer={checkTimer}
      />
```

```jsx
//Timer.jsx
import React, { useEffect } from "react";

const Timer = ({ minutes, setMinutes, seconds, setSeconds, checkTimer }) => {
  useEffect(() => {
    if (checkTimer === true) {
      const countdown = setInterval(() => {
        if (parseInt(seconds) > 0) {
          setSeconds(parseInt(seconds) - 1);
        }
        if (parseInt(seconds) === 0) {
          if (parseInt(minutes) === 0) {
            clearInterval(countdown);
          } else {
            setMinutes(parseInt(minutes) - 1);
            setSeconds(59);
          }
        }
      }, 1000);
      return () => clearInterval(countdown);
    }
  }, [minutes, seconds, checkTimer]);

  return (
    <div>
      <p>
        {minutes}:{seconds < 10 ? `0${seconds}` : seconds}
      </p>
    </div>
  );
};

export default Timer;
```

Timer.jsx에서 state를 하고 값을 처리할까 하다가 인증 번호를 재발급했을 때 타이머가 다시 3분이 되어야 하기 때문에 어떻게 초기화해야 할 지 몰라서 Email.jsx에서 버튼을 눌렀을 때 set값으로 3분을 넣어 구현하였습니다. Email.jsx에서 state값을 Timer.jsx에 보내는 식으로 만들었습니다.

setInterval이라는 함수가 타이머를 만들 때 유용하다는 것을 찾으면서 처음 알았습니다.

중간에 return () ⇒ clearInterval(countdown)이 빠질 경우 렌더링이 되면서 숫자가 올라갔다 내려갔다 하는 에러가 발생하게 됩니다. 다른 부분에서는 크게 어려웠던 것은 없었네요. 이렇게 타이머를 구현하게 되어서 좋았습니다. 오늘 하루도 한 건 해서 다행이네요! mvp까지 얼마 남지 않았는데요. 그때까지 남은 기능들도 마무리 잘할 수 있도록 노력하겠습니다. 화이팅!!
