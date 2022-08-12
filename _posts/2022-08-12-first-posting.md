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

어제 map해결을 잘한 줄 알았지만, 다시 또 에러가 발생했다.. 에러에 대해 잘못 접근한 거 같습니다..

기술매니저님의 도움으로 해결했습니다….

```jsx
// 해결전
[_addPosts.fulfilled]: (state, action) => {
      state.posts_list = action.payload
};

// 해결후
[_addPosts.fulfilled]: (state, action) => {
      state.posts_list = [...state.posts_list, action.payload];
};
```

map을 돌리려면 배열로 돌려야 하는데 위에 해결 전 경우 객체로 만들어져서 map에러가 뜨는 것입니다. map에러가 떴을 때 객체이기 때문에 안된다는 거까지는 유추했지만, 어떤 것이 객체가 되었는지 찾지를 못해서 다른 걸 건드려 그냥 해결되었던 것처럼 보였던 것이였네요.. console를 잘 활용하지 못한 것이 아쉽네요.. 더 열심히 찍어봐야겠습니다! 이제 delete를 구현해봤습니다

```jsx
// 수정
export const _delPosts = createAsyncThunk(
  "posts/delPosts",
  async (id, thunkAPI) => {
    try {
      await axios.delete(`http://localhost:3001/posts_list/${id}`);
      console.log(id);

      //   thunkAPI.dispatch(_getPosts(id));   // 수정전
      return thunkAPI.fulfillWithValue(id);   // thunkAPI.fulfillWithValue(data.data)
    } catch (error) {                         //   여기서 data 값을 찾을 수가 없다.
      return thunkAPI.rejectWithValue(error);
    }
  }
);

[_delPosts.fulfilled]: (state, action) => {
      console.log(action.payload);
      state.posts_list = state.posts_list.filter(
        (post) => post.id !== action.payload
      );
    },
```

위에서 data를 찾을 생각을 안하고 그냥 생각없이 코드를 치다보니 오류가 계속 떴었고 삭제 버튼을 눌렀을 때 바로 사라지는 것이 아니라 새로고침을 눌러야만 사라졌습니다.

기술매니저님의 조언으로 console를 찍어보면서 data가 없다는 것을 찾았고 id값을 찾으면서 위에 보이는 것처럼 고쳤습니다. 그렇게 하고 나니 고쳐졌네요.. 새로고침을 누르지 않고 하려고

thunkAPI.dispatch()를 사용했었습니다. 제가 로직을 잘못 활용하고 이해해서 이렇게 된 거 같네요

그래서 기술매니저님께서 저 식이 어떤 식으로 되는 지에 대해 정리해보라고 하셨고 정리를 해보았지만 자신이 없네요… 먼저 thunk함수를 사용하고 async, await를 사용하는데 axios.delete()안에 있는

‘url/:id’ 삭제버튼을 클릭버튼 눌렀을 때 전체 배열에서 같은 id값을 삭제합니다.

함수가 끝났을 때 filter를 통해 새로운 배열을 만듭니다! 이렇게 정리를 해보았습니다…

처음 배우기도 했고 그 전에 배웠던 것들도 아직 정리가 덜 되어서 많이 힘드네요 ㅠㅠ

수정기능도 추가하려고 했지만…. 제가 어떻게 해야할 지 갈피도 못잡고 제대로 이해하지도 못해서

에러도 많이 뜨고 새로고침하면 데이터도 다 날라가고.. 수정을 했지만 나머지는 날라가고 수정한

것만 있는 등.. 정말 힘들었고 구현을 결국 못했습니다..며칠을 밤새면서 했지만 결과가 좋지 않아

멘탈이 와르르 무너졌네요 너무 힘들어요 ㅠㅠㅠㅠㅠㅠㅠㅠㅠㅠㅠㅠ

이제 팀 프로젝트가 마무리 되었지만… 제가 좀 더 잘했다면 어땠을까 하는 생각이 드네요

내일부터 백엔드와 같이 하는 프로젝트를 시작하는데요 걱정이 너무 많이 드네요

더 더 더 열심히 하겠습니다!!!!!!!!!!!!!!!!!!! 화이팅!!!
