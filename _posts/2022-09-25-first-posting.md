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

요즘 잠이 너무 많이 자는 것 같다는 생각이 드네요.. 오늘도 아침 8시에 게더에 접속해

빠르게 공부하려고 했지만… 이미 10시가 넘어버린 상황………..

그래도 오늘 뭔가라도 해결해보려고 합니다. 댓글 페이지 보던 와중에 아직도 alert로 뜨길래

바로 모달로 수정하는 작업을 했습니다. 팀원분이 짜놓은 코드라.. 열심히 체킹체킹체킹..

```jsx
const [checkComment, setCheckComment] = useState(false);
///
{
  checkComment && <ToastMessage text={"댓글을 입력해주세요"} timer={1000} />;
}
///
if (comment === "" || comment === null) {
  setCheckComment(true);
  setTimeout(() => {
    setCheckComment(false);
  }, 1000);
  return;
}
```

상위 컴포넌트에서 state값을 지정하고 그걸 props로 내려준 다음에 alert 대신 모달로 구현했습니다!! 처음에는 모달하는 것조차 버거웠었는데 2번, 3번 계속 하다보니 이제는 조금 할만하네요 ㅎㅎ

생각보다 빨리 끝나서 다른 버그가 없나 찾아보다가 댓글 수정할 때 input값에 기존에 있던 내용이

들어있지 않아 defaultValue값을 넣어줘야 한다는 것을 보고 한 번 해봐야겠다는 생각이 들어 시도했습니다!! 걱정 두근두근..

```jsx
const {
  register,
  handleSubmit,
  watch,
  setValue,
  getValues,
  formState: { errors },
} = useForm({ defaultValues: {} });
///
console.log(comments);
///
{
  comments.map((comment) => {
    if (comment.commentId === editCommentId) {
      return (
        <div className="input_box" key={comment.commentId}>
          <input
            className="comment_input"
            type="text"
            name="content"
            defaultValue={comment.comment}
            {...register("comment")}
            placeholder="새로운 댓글을 입력해주세요"
          />
          {/* {comment.comment} */}

          <button className="comment_btn">확인</button>
        </div>
      );
    }
  });
}
```

react hook form을 사용하다 보니 useForm에서 defaultValues를 사용할 수 있습니다.

comment값을 찾기 위해 열심히 콘솔로 찍어보면서 값을 찾았습니다. 그리고 그것을 map을 돌리고 input에 넣어주면 끝!!! 이제는 콘솔로 값 찾아보는 것도 조금은 익숙해졌네요.. 시도해봤는데 못하면 어쩌지.. 걱정했었는데 걱정과는 다르게 잘 해결이 되었네요 ㅎㅎ 조금은 성장한 것 같아서 기분이 매우 좋습니다!!
