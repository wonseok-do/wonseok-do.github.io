---
layout: single
title: "TIL(error)"
categories: coding
tag: [python, jekyll, blog]
toc: true
author_profile: false
sidebar:
  nav: "docs"
# search: false
---

오늘은 한 것들을 합쳐서 에러를 잡기로 하였습니다. 일단 제가 한 부분에서는 pagination에러가 나더군요.. 프론트쪽에서 해결하는 방식으로 만들어서 그런가봅니다.. 원래 백엔드와 같이 했어야 했는데 제가 아직 잘 몰라서 이렇게 처리하는 방식으로 만들어버렸네요 실전 프로젝트에서 하게 된다면 꼭 백엔드와 같이 만들어서 해결해보고 싶습니다.

Error

```jsx
//페이지가 아무것도 없을 때 <>버튼이 눌림
//해결 : button->disabled에 numPage === 0을 추가 0이 되는 경우가 페이지수가 0인 경우밖에 없음
...
const numPages = Math.ceil(total / limit);

<Button
          onClick={() => setPage(page + 1)}
          disabled={page === numPages}
        >
          &gt;
        </Button>
...
<Button
          onClick={() => setPage(page + 1)}
          disabled={page === numPages || numPages === 0}
        >
          &gt;
        </Button>
```

```jsx
//맨밑에 고정되어 있어야하는데 위에 고정됨
//해결 : 전체 div에 display : flex,
//flex-direction : column -> Pagination을 감싸고 있는 div에 flex:1;을 추가
...
<div
      style={{
        position: "relative",
        height: "100%",
        padding: "0 2rem",
        display: "flex",
        flexDirection: "column",
      }}
  <StContainer>
...
  </StContainer>
    >
...
</div>
const StContainer = styled.div`
  display: flex;
  flex-direction: column;
  position: relative;
  flex: 1;
`;
```

flex : 1에 대해서 공부를 해야겠습니다. 아직 css도 많이 어렵네요… 분발해야겠습니다!

```jsx
//페이지 당 표시할 게시물 수를 4,8,12로 했는데
//더미데이터로 페이지 9개를 넣고 페이지 당 표시할 게시물 수 8로 한다면
//마지막 페이지(2)에서 페이지 당 표시할 게시물 수를 12로 바꿨을 때 비어있는 현상 발생
//해결 : 바뀔때마다 강제로 페이지1로 가게끔하면 어떨까하다가
//select안에서 onChange가 일어날 때 setPage(1)를 추가해보았더니 해결이 되었습니다
...
<select
          type="number"
          value={limit}
          onChange={({ target: { value } }) =>

            setLimit(Number(value));
          }
        >
          <option value="4">4</option>
          <option value="8">8</option>
          <option value="12">12</option>
        </select>
...
<select
          type="number"
          value={limit}
          onChange={({ target: { value } }) => {
            setPage(1);
            setLimit(Number(value));
          }}
        >
          <option value="4">4</option>
          <option value="8">8</option>
          <option value="12">12</option>
        </select>
```

완벽하게 고쳤다고는 할 수 없지만 이렇게나마 고칠 수 있어서 다행이네요.. 더 열심히 하겠습니다!
