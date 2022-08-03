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

오늘 드디어 리액트 기초반 강의 5주차를 마무리 했습니다. 그동안 버킷리스트를 만드는 작업을

했는데요. 이번 5주차 강의에서는 그동안 만들었던 버킷리스트에 firestore를 적용하는 법에 대해서

배웠습니다.

firestore에서 데이터를 가지고 올 때 비동기 통신을 하게 되는데 리덕스에서 비동기 통신을 할 때

필요한 미들웨어를 사용하게 됩니다.

**미들웨어란?** 리덕스 데이터를 수정할 때 **[액션이 디스패치 되고 → 리듀서에서 처리]** 하던 과정에서
미들웨어는 이 과정 사이에 미리 사전 작업을 할 수 있도록 하는 중간 다리 같은 거예요!
즉! **[액션이 일어나고 → 미들웨어가 할 일 하기 → 리듀서에서 처리]** 이 순서로 처리하게 됩니다!

강의에서는 redux-thunk라는 미들웨어를 사용했습니다. redux-thunk는 **객체 대신 함수를 생성하는 액션 생성함수**를 작성할 수 있게 해줍니다!

```jsx
// configStore.js redux-thunk 추가
import { createStore, combineReducers, applyMiddleware, compose } from "redux";
import bucket from "./modules/bucket";
import thunk from "redux-thunk";

const middlewares = [thunk];
const rootReducer = combineReducers({ bucket });
const enhancer = applyMiddleware(...middlewares);

const store = createStore(rootReducer, enhancer);

export default store;
```

load, create, delete, update를 추가했습니다.

```jsx
// app.js
import { useDispatch, useSelector } from "react-redux";
import {
  createBucket,
  loadBucketFB,
  addBucketListFB,
} from "./redux/modules/bucket";
import Progress from "./Progress";
import { db } from "./firebase";
import {
  collection,
  doc,
  getDoc,
  getDocs,
  addDoc,
  updateDoc,
  deleteDoc,
} from "firebase/firestore";
...
const text = React.useRef(null);
  const dispatch = useDispatch();
  const is_loaded = useSelector((state) => state.bucket.is_loaded);

  React.useEffect(() => {
    dispatch(loadBucketFB());
  }, []);

  const addBucketList = () => {
    // 스프레드 문법! 기억하고 계신가요? :)
    // 원본 배열 list에 새로운 요소를 추가해주었습니다.
    // setList([...list, text.current.value]);
    // dispatch(createBucket({ text: text.current.value, completed: false }));
    dispatch(addBucketListFB({ text: text.current.value, completed: false }));
  };
...
<button onClick={addBucketList}>추가하기</button>
```

```jsx
// bucket.js
// middlewares
export const loadBucketFB = () => {
  return async function (dispatch) {
    const bucket_data = await getDocs(collection(db, "bucket"));
    console.log(bucket_data);

    let bucket_list = [];
    bucket_data.forEach((bucket) => {
      console.log(bucket.data());
      bucket_list.push({ id: bucket.id, ...bucket.data() });
    });
    console.log(bucket_list);
    dispatch(loadBucket(bucket_list));
  };
};
```

더 많이 있지만, 간추리는 게 힘들어서 이 정도로만 하겠습니다. 위에 코드와 비슷하게 해서 짰습니다. 파이어베이스랑 통신 → 필요하다면 리듀서 고치고 → 불러다 쓰기 이런 순입니다.
