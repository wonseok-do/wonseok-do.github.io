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

오늘은 멘토님께 mvp 이후 한 것들을 점검받고 질의응답 시간을 가졌습니다.

여러 질문들이 있었지만 가장 큰 것은 메모이제이션, 레이지로딩, 테스트 코드 등이였습니다

아무래도 일일이 수작업을 통해 테스트하는 것은 무리가 있어 테스트 코드를 하면서

어떤 게 문제가 있는 지 파악을 해야 한다는 점이였고 함수를 왜 잘 짜야 하는 지에 대해서도 알 수

있는 기회가 됩니다. 그리고 성능쪽으로도 더 좋아져야 하구요.. 이제 곧 프로젝트가 끝나는 기간이

2주정도 밖에 남지 않아 추가적인 페이지도 한, 두개 정도만 늘리고 나머지는 버그와 성능 개선쪽에

시간을 투자할 것 같네요. 기능도 중요하지만 성능이 잘 되어야 한다고 생각해서 그 쪽에 더 초점을 둘 것 같습니다. 멘토 시간이 끝나고 저희끼리 회의를 하였구요.. 하루에 한번씩 회의를 하는데

쉽지 않네요 ㅎㅎ 특히 오늘이 좀 많이 지쳤습니다 ㅠㅠ 쉬고 싶다는 마음이 굴뚝같았지만 뭔가라도

하나라도 더 하고 쉬어야겠다고 생각이 들어 아직 페이지에 추가되지 않은 기능을 한 가지 추가하기로 했습니다. 그것은 좋아요 기능인데요 전체 레시피에서는 좋아요 기능이 되었지만, 상세 페이지에서는 좋아요 기능이 없어서 제가 그것을 구현하겠다고 하였고 했습니다 ㅎㅎ 처음 해보는 거라 많이 힘들었네요 ㅠㅠ 전체 레시피에서 좋아요 기능을 짠 것을 보면서 작업했습니다. 잘 못하면 어떡하지 라는 생각이 많이 들긴 했는데 어떻게든 구현이 되었네요 ㅎㅎ

```jsx
// recipeDetail.jsx
const timer = 1800;
const [needLoginModal, setNeedLoginModal] = useState(false);
const modalProps = {
  needLoginModal,
  setNeedLoginModal,
  timer,
};
// recipeTitle.jsx
const { needLoginModal, setNeedLoginModal, timer } = modalProps;
// console.log(needLoginModal);
const [like, setLike] = useState(isLiked);
const userLogin = Boolean(localStorage.getItem("refreshToken"));

// const { userLogin, needLogginModal, setNeedLogginModal, timer } = modalProps;
// console.log(userLogin);
const likeCard = async () => {
  // 로그인이 안되어 있다면 모달창을 띄우고 함수를 종료합니다.
  if (!userLogin) {
    if (!needLoginModal) {
      setNeedLoginModal(true);
      setTimeout(() => {
        setNeedLoginModal(false);
      }, timer);
    }
    return;
  }
  let contentType = "application/json";
  //like가 false일때는 좋아요 안눌러진상태
  if (like === false) {
    try {
      await api(contentType)
        .patch(`/recipes/${recipeId}/like`)
        .then((res) => {
          setLike(!like);
          console.log(res);
        });
    } catch (err) {
      console.log(err);
    }
  } else {
    try {
      await api(contentType)
        .patch(`/recipes/${recipeId}/dislike`)
        .then((res) => {
          setLike(!like);
          console.log(res);
        });
    } catch (err) {
      console.log(err);
    }
  }
};
{
  like === false ? (
    <img className="like_btn" src={dislikes} onClick={likeCard} />
  ) : (
    <img className="like_btn" src={likes} onClick={likeCard} />
  );
}
```

처음에는 like라는 state값을 지정을 안하고 recipe에 있는 데이터를 통해서 거기에 있는 데이터로

boolean 값으로 했지만, 렌더링이 될때에만 좋아요가 변했습니다.. 거기서 좀 많이 막혔는데요

팀원분의 도움으로 state값을 정하고 그렇게 했더니 잘 바뀌었네요.. 거의 다 했는데 좀 많이 아쉬웠습니다 ㅠㅠ 마무리가 조금 아쉬웠네요 그리고 로그인을 안한 상태에서는 좋아요를 누르게 되면 모달이 뜨게 구현하였구요. 마무리가 살짝 아쉽긴 했지만 처음 한 기능인데 이 정도면 만족스럽네요

더 분발해야겠습니다. 오늘 하루도 잘 마무리가 되었네요 더 화이팅하겠습니다 화이팅!!
