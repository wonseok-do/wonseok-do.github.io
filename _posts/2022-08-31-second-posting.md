---
layout: single
title: "버튼 에러"
categories: coding
tag: [python, jekyll, blog]
toc: true
author_profile: false
sidebar:
  nav: "docs"
# search: false
---

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/877b9c09-6af2-4c10-8240-825fe5237027/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220831%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220831T175800Z&X-Amz-Expires=86400&X-Amz-Signature=6a610cc53f72b94096358ed69d2a87f957481d36a8a58bdfacac054bd2737ab4&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

회원가입 페이지에서 취소버튼을 눌러 로그인 페이지로 갔을 때 저렇게 에러가 발생하였다.

구글링을 해본 결과 form안에 있는 button에서 문제가 발생한 것을 확인하였다.

```jsx
//수정 전
<form onSubmit={handleSubmit(onSubmit)}>
  // // //
  <button type="submit" disabled={isSubmitting}>
    완료
  </button>
  <button onClick={() => navigate("/signIn")}>취소</button>
</form>
```

form안에 2개의 button중에서 하나의 button의 type이 정해지지 않아서 생기는 오류인 것 같았다.

```jsx
//수정 후
<form onSubmit={handleSubmit(onSubmit)}>
  // // //
  <button type="submit" disabled={isSubmitting}>
    완료
  </button>
  <button type="button" onClick={() => navigate("/signIn")}>
    취소
  </button>
</form>
```

정해지지 않은 button에 type을 지정하니 오류가 뜨지 않았다. 이렇게 해결했다.
