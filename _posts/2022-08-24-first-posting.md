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

오늘까지 코드를 짰던 것들을 합쳐보았는데요.. 중간에 에러가 났지만.. 팀원들이 해결하는 것을 보는 중에 저녁에 야자반이 있어서 끝까지 보질 못했다 ㅠㅠ 다 보고 싶었는데.. ㅠㅠ

야자반에서는 crud에 대해 설명을 다시 듣고 점검하는 시간을 가졌습니다.

```jsx
const [arr,setArr] = useState([{id:1,contents:"asdf",isComplete:false}])

const handleDeleteTodo = (id) => {
  setArr((prevArr)=>prevArr.filter((todo)=>todo.id!==id))
  setArr([...arr].filter((todo)=>todo.id!==id)

setArr 안에 prevArr은 그냥 이전에 값을 복사(?)하는 느낌으로 가져옴

const d = {key:{key:1}}
const e = JSON.parse(JSON.stringify(d));
e.key.key =2
console.log(d);
key의 값 변경 x

깊은 복사, 얕은 복사 알아둘 것

const e = {...d}
할 경우 key의 값이 변경
얕은 복사가 된 거임
안에 있는 key 주소 건드림

const d = {key:1}
const e = {...d}
e.key =2
console.log(d)
key의 값 변경 x

but
const e = d
key의 값 변경

const handleCompleteTodo = (id) => {
  setArr([...arr].map((todo)=>(todo.id===id? {...todo, isComplete:!todo.isComplete}:todo)))
}

const handleAddTodo = (id, contents) => {
  setArr([...arr, { id, contents, isComplete: false}])
}
```

매니저님이 알려주신 부분을 적으면서 다시 보니 전보다는 이해가 되네요.. 그러나 막상 쓸려고 하면 막막할 거 같아요 ㅠㅠㅠ 그리고 얕은 복사와 깊은 복사에 대해서도 간략히 설명해주셨는데요..

이것도 많이는 아니지만 조금이나마 정리가 된 거 같습니다. 이번에 배운 것들이 정말 많았어요..

정말 정말 뜻깊은 시간이였습니다. 그리고 마지막에는 멘토님이 오셔서 이것저것 설명해주시고 질의응답시간을 가졌는데요.. 질의응답중에서 생각을 많이 했었던 것들을 가져왔습니다.

README와 issues에 자신이 한 것을 잘 정리해둘 것
코드들을 작성할 때 왜 그 코드들을 썼는지 근거를 기반으로 해야함
근거 잘 생각해둘 것
무지성으로 코드짜지말 것
아무리 완성이 높은 프로젝트라도 뜯어보면 자신이 구현한 부분들이 정말 작기 때문에 그 사소한 거라도 근거가 있다면
그게 쌓여서 자신것이 됨
그리고 싸우지말 것

이 정도가 되겠네요. 오늘 코드를 많이 짜거나 하지는 못했지만 많은 것들을 배울 수 있어서 좋았습니다. 아 그리고 야자반시간 마지막에 정말 정말 궁금했던 redux사용에 대해 여쭤봤는데요..

페이지안에서 axios.get post, async와 await 등으로 다 해결할 수 있지않나? 굳이 slice페이지를 만들어서 미들웨어 thunk을 사용해야 할까? 이거에 대해서 질문을 드렸었는데 페이지안에서 해결할 수 있지만 컴포넌트를 나누고 이런 것들과 관련이 있었고 페이지안에서 dispatch로 간략히 쓸 수 있는 점 등 여러가지 이유가 있더라구요.. 그러나 현업에서 사용하지 않는 곳도 있다고 합니다. 그래도 redux는 기본이니 잘 익혀두라고 하시더군요.. 아직 redux을 많이 사용해보지 않아 어렵기도 하고 잘 쓰고 싶은데 그게 마음처럼 잘 되지는 않더군요.. 잘 쓸 수 있도록 더 열심히 공부하고 노력해야겠습니다. 클론코딩 얼마 남지 않았지만 남은 기간 동안 팀원분들께 민폐끼치지 않도록 더 열심히 하겠습니다 화이팅!!!!!
