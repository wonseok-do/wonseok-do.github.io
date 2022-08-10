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

팀 과제 프로젝트를 하면서 정말 힘든 시간을 보내고 있습니다… Redux하나로도 힘들었었는데 이번에는 toolkit, json-server, axios, thunk까지 하려니 막막하더군요.. 그래서 일단 학습자료를 먼저 봐야겠다 싶어서 봤지만 이해가 잘 안되었습니다. 강의밖에 답이 없겠다 싶어서 강의도 열심히 봤지요..

강의 보고 학습자료 보고 이것만 반복했었던 거 같아요 그래도 월요일에 React 세션이 있어서 조금이나마 숨통이 트였습니다.. 정말 쪼~~~~~~~~~오금이요. 그걸 보고 그 전에 Redux으로 작성했었던 것을 toolkit으로 바꿔봤습니다. 정말 힘들었지만 어떻게든 되더군요.. 카피라도 열심히 하면서요..

```jsx
// redux/config/cofigStore

import { configureStore } from "@reduxjs/toolkit";
import posts from "../modules/postsSlice";

const store = configureStore({
    reducer:{ posts, },
});

export default store

// redux/modules/postsSlice.js
import { createSlice } from "@reduxjs/toolkit";

const initialState = {
  posts:[
     {
       id: 1,
       title: "react",
         body: "안녕하세요",
     }
  ],
};

export const postsSlice = createSlice({
  name: "posts",
  initialState,
  reducers: {
     addPost: (state,action) => {
         state.posts = [...state.posts, action.payload];
    },
  },
});

export const { addPost } = postsSlice.actions;

export default postsSlice.reducer;

configStore.js
counterSlice.js 뼈대 만들기
configStore.js -> reducer추가
counterSlice.js -> reducers 작성 -> export
useSelector()
useDispatch()
reducers -> state.~~~
```

강의를 보면서 조금씩 정리해보았습니다… toolkit으로 말이죠!!!

```jsx
//Redux
const ADDTODO = "todo/ADDTODO";

export function addTodo(todo) {
  return { type: ADDTODO, todo };
}

const initialState = {
  todos: [
    {
      id: 1,
      userName: "아무개",
      title: "밥 먹자",
      comment: "어디에서 먹을까요?",
    },
  ],
};

export default function reducer(state = initialState, action) {
  switch (action.type) {
    case "todo/ADDTODO": {
      return { ...state, todos: [...state.todos, action.todo] };
    }
    default:
      return state;
  }
}
```

```jsx
//toolkit
import { createSlice } from "@reduxjs/toolkit";
import axios from "axios";

const initialState = {
  posts_list: [],
};

export const postsSlice = createSlice({
  name: "posts",
  initialState,
  reducers: {
    addPosts: (state, action) => {
      console.log(action);
      state.posts_list = [...state.posts_list, action.payload];
    },
  },
});

export const { addPosts } = postsSlice.actions;

export default postsSlice.reducer;
```

thunk도 해봤습니다

```jsx
export const getTodosThunk = createAsyncThunk("getTodos", async  (payload,api)=>{
  // 중간 작업
  const data = await  axios.get("url")

                                                                           try{
                                                                                   const data = await axios.get(
  //api.dispatch();                                                                   "url");
  //console.log(api.getState())                                                 return api.fulfillWithValue(data.data);
  api.fulfillWithValue();  //  dispatch , 요청이 성공했을때만         }  catch  (e)   {
                                                                                return  api.rejectWithValue(e);

  console.log(data.data)                                                    }
  // dispatch(원래 하려고했던 디스패치)
// 스토어에 넣어야지요
});

extraReducers: {
  [getTodosThunk.fulfilled]: (state, action) => {
    console.log(action)
   state.todos = action.payload
 },
  [getTodosThunk.rejected]: (state, action) => {
   console.log(action)
 }
}

reducers안에 값을 넣어야 하지만, 안에 만들어진 action creator는 사용가능  thunk 즉 밖에서 만들어진 thunk 함수는
reducers 사용 불가능 -> extraReducers 사용

useEffect(()=>{
   dispatch(getTodosThunk()
```

정리한 것들을 적용해봤지만 에러들이 미친듯이 터지더군요.. json-server하고 axios도 사용했습니다.

```jsx
import { createSlice, createAsyncThunk } from "@reduxjs/toolkit";
import axios from "axios";

const initialState = {
  posts_list: [],
  isLoading: false,
  error: null,
};

export const _getPosts = createAsyncThunk(
  "posts/getPosts",
  async (payload, thunkAPI) => {
    try {
      const data = await axios.get("http://localhost:3001/posts_list");
      console.log(data);
      return thunkAPI.fulfillWithValue(data.data);
    } catch (error) {
      console.log(error);
      return thunkAPI.rejectWithValue(error);
    }
  }
);
export const _addPosts = createAsyncThunk(
  "posts/addPosts",
  async (posts_list, thunkAPI) => {
    try {
      const data = await axios.post(
        "http://localhost:3001/posts_list",
        posts_list
      );
      return thunkAPI.fulfillWithValue(data.data);
    } catch (error) {
      return thunkAPI.rejectWithValue(error);
    }
  }
);

export const postsSlice = createSlice({
  name: "posts",
  initialState,
  reducers: {
    addPosts: (state, action) => {
      console.log(action);
      state.posts_list = [...state.posts_list, action.payload];
    },
  },
  extraReducers: {
    [_getPosts.pending]: (state) => {
      state.isLoading = true;
    },
    [_getPosts.fulfilled]: (state, action) => {
      state.isLoading = false;
      console.log("fulfilled 상태", state, action); //promise가 fulfilled일 때 dispatch
      state.posts_list = action.payload;
    },
    [_getPosts.rejected]: (state, action) => {
      state.isLoading = false;
      state.error = action.payload;
    },
    [_addPosts.fulfilled]: (state, action) => {
      state.posts_list = action.payload;
    },
  },
});

export const { addPosts } = postsSlice.actions;

export default postsSlice.reducer;
```

정말 힘들었습니다. 거의 다 복붙밖에는 없지만.. 이 흐름을 이해하는데 시간을 많이 투자했네요

중간에 map이 기능을 하지않는다는 에러메시지도 계속 떠서 useState를 추가하기도 했구요.

```jsx
import React, { useEffect } from "react";
import { useSelector, useDispatch } from "react-redux";
import { useNavigate } from "react-router-dom";
import styled from "styled-components";
import { _getPosts } from "../redux/modules/postsSlice";

const Posts = () => {
  const [boolen, setBoolen] = React.useState(true); // useState값을 지정 후 useEffect에 false값을 넣어줌
  const navigate = useNavigate();
  const dispatch = useDispatch();
  const { posts_list, isLoading, error } = useSelector((state) => state.posts);
  console.log(posts_list);
  useEffect(() => {
    setBoolen(false);
    dispatch(_getPosts());
  }, [dispatch]);
```

이제 오류도 해결하고 추가버튼을 눌러서 json-server와 연결한 덕에 추가한 페이지들이 날라가지 않게 해주었습니다. 수정하고 삭제버튼을 추가해야겠네요!! 많이 부족하지만.. 더 더 더 열심히 하겠습니다.. 밤새고 작업하니 너무 힘드네요 ㅠㅠㅠ 화이팅!
