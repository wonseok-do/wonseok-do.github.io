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

이번에는 부트스트랩처럼 이미 다 만들어진 ui를 사용해봤습니다.

머테리얼 ui는 우리가 styled-components를 쓰던 것처럼 사용할 수 있어요.
공식 문서([https://material-ui.com/](https://material-ui.com/))에서 어떻게 생겼는 지 보고 사용 해봅시다!

`yarn add @mui/material @emotion/react @emotion/styled`

위에 코드를 cra프로젝트에 설치하고 사용했습니다.

정말 예쁜 기능들이 많았는데요 그 중에서 button 기능을 사용해봤습니다.

```jsx
import Button from "@mui/material/Button";
```

`<Button variant="outlined" color="error">`

이렇게 사용하면 됩니다. import 하고 적용하면 끝!

또 다른 기능도 이용해 봤는데요. 로딩하는 동안에 이미지 나올 수 있도록 구현해보았습니다.

```jsx
import React from "react";
import styled from "styled-components";
import { Eco } from "@material-ui/icons";

const Spinner = (props) => {
  return (
    <Outter>
      <Eco
        style={{
          color: "#673ab7",
          fontSize: "150px",
        }}
      />
    </Outter>
  );
};

const Outter = styled.div`
  background: #e5d6ff;
  width: 100vw;
  height: 100vh;
  position: fixed;
  top: 0px;
  left: 0px;
  display: flex;
  align-items: center;
  justify-content: center;
`;

export default Spinner;
```

Eco가 있는데 아이콘을 불러서 사용합니다. 다양한 아이콘들이 많이 있습니다. 취향에 맞게 사용하시면 될 것 같아요!

아직 많은 기능들을 사용해보지 않아서.. 잘 모르지만.. React 2주차 개인 프로젝트를 만들면서

시간이 남는다면 조금씩 기능들을 추가해서 사용해 볼 생각입니다. 재미있을 거 같아요!
