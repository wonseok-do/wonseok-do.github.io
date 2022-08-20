---
layout: single
title: "게시글 전체 조회"
categories: coding
tag: [python, jekyll, blog]
toc: true
author_profile: false
sidebar:
  nav: "docs"
# search: false
---

**게시글 전체 조회하기**

몇번이고 설명을 듣고 혼자서 해보려고 했지만.. 정말 아무것도 하지 못했다. 스스로가 정말 답답할 정도.. 팀원분들께 도움을 받고 조금씩 정리해보면서 이제라도 조금씩 해보려고 한다.. 아니 하고 싶다.. ㅠㅠ 먼저 json-server와 axios에 대해 알아야 한다.. 어렴풋이 알겠지만 막상 하려니 힘드네요..

여러가지 방법이 있겠지만은 알려주신 방법은 따로 폴더를 만들어서 사용한다고 한다. 구별하기 쉽게 하려고 한거 같다.

```jsx
// 새 폴더 만들 때 mkdir 파일명
// yarn init -y
// yarn add json-server
// package.json에 추가
"scripts": {
    "start": "json-server-auth --watch db.json --port 5000"
  }
//db.json 파일추가 -> 안에 내용 추가
{
  "post": [
    {
      "id": 0,
      "img": "https://upload.wikimedia.org/wikipedia/commons/thumb/a/ae/DaangnMarket_logo.png/800px-DaangnMarket_logo.png",
      "title": "사람입니다",
      "price": "10000",
      "nickname": "도원석",
      "location": "수도권",
      "likeCount": 0
    },
}
//yarn start
//postman으로 http://localhost:5000/post get 요청을 보내서 데이터 들어오는지 확인
```

```jsx
//게시글 전체 조회
const Home = () => {
  const [postList, setPostList] = useState([]);
  useEffect(() => {
    const getPosts = async () => {
      const res = await axios.get("http://localhost:5000/post");
      setPostList(res.data);
    };
    getPosts();
  }, []);
  console.log(postList);
  return (
    <StContainer>
      {postList.map((post) => {
        return (
          <StCard key={post.id}>
            <StImg>
              <img src={post.img} />
            </StImg>
            <StComment>
              <p>{post.title}</p>
              <p>{post.nickname}</p>
              <p>{post.price}</p>
              <p>{post.location}</p>
              <span>{post.likeCount}</span>
            </StComment>
          </StCard>
        );
      })}
    </StContainer>
  );
};
```

useEffect()을 통해 렌더링될 때 안에 실행하도록 한다. async, await를 사용하여 데이터를 받아오는데 문제없도록 한다. axios.get으로 데이터를 가져온다. 그 후 useState와 map함수로 데이터를 화면에 보일 수 있게 한다.

이렇게 정리를 해보았습니다. 정리(?)는 아닌가?… 이렇게 보면 기본적으로 배운 것들이고 뭔가 쉬운 듯하면서도 어렵고.. 막상 혼자하려니 정말 안되네요.. 이거 하나 제대로 못하는 제가 너무 답답하지만 그래도 포기하지 않고 열심히 해보겠습니다 화이팅!!
