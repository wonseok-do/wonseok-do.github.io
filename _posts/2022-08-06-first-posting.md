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

안녕하세요! 오늘부터 주특기 React 3주차가 시작되었습니다. 3주차에서는 1주차, 2주차와는 달리

개인 과제 프로젝트가 아니라 팀 과제 프로젝트를 하게 되었습니다. 첫 미니프로젝트할 때 이후로

계속 개인 프로젝트를 하다가 처음으로 팀 프로젝트를 하게 되어서 조금 떨리기도 하고 기대도 많이 되었습니다. 팀 프로젝트를 하게 되면 깃헙도 사용해야 되기 때문에 많이 걱정이 되었습니다.

그러나 팀원분들 중에 한분이 깃헙을 사용할 줄 아셔서 조금씩 물어보면서 나아갔습니다.

한분이 Repository 만들고 나머지분들이 clone을 합니다. 그리고 각자의 branch를 만들어서 branch에 각자가 맡은 페이지를 완성하고 나중에 main으로 merge하는 방향으로 계획을 세웠습니다.

<aside>
💡 yarn create react-app .   //  . 은 만든 폴더에 react를 만듭니다.

</aside>

<aside>
💡 git clone --branch [TAG] [REPO_URL] // 미리 만들어둔 branch에 클론을 합니다.

</aside>

<aside>
💡 git branch 작성명 //  branch(작성명)을 만듭니다.

</aside>

<aside>
💡 git checkout 작성명 //  branch(작성명)에 적용합니다.

</aside>

<aside>
💡 git add .     //  모든 파일을 add합니다.

</aside>

<aside>
💡 git commit -m “내용”   //  내용을 커밋합니다.

</aside>

<aside>
💡 git push origin 작성명  //   branch(작성명)에 내용을 올립니다.

</aside>

대충 이런 순으로 해봤습니다. 조금이나마 정리를 해둬서 다음에도 용이하게 쓸 수 있을 거 같습니다.

정말 어렵네요 ㅠㅠ 아직 초기 단계이니 많이 부딪혀 보고 깨지고 잘 쓸 수 있도록 해야겠습니다.

이번 프로젝트 예시가 todo-list인데요. 처음에 어떤 식으로 짤 지 회의를 하다 그냥 예시처럼 만들어 보자 라는 결과가 나왔는데요. 제가 맡은 부분은 리스트를 추가하는 페이지를 만드는 거였습니다.

Redux를 사용해서 만들었었는데, 이번 주차는 툴킷을 사용하라고 하더군요.. 아직 저는 리덕스 조차 제대로 사용하지 못하는데 툴킷까지 사용하려고 하니 좀 막막해서 리덕스로 프로젝트를 하자고 팀원분들께 양해를 구했습니다. 그러나 매니저님께 이런 상황을 말씀드렸는데 매니저님께서는 툴킷을 사용해보라고 하셔서 결국 리덕스만든 건 지우고 툴킷으로 새로 만들 거 같습니다.

아직 학습자료를 보지 못해서 툴킷을 어떻게 사용하는 지 공부를 하지 못했습니다. 아마 내일부터

빡세게 학습자료보면서 툴킷을 사용하는 법에 대해 익힐 거 같네요. 기대 반 걱정 반이네요 ^^

마지막으로 api명세서와 와이어프레임을 조금씩 만들어보았습니다. 아무리 생각해도 1주차, 2주차에도 todo-list를 만들었는데 이왕이면 제가 좋아하고 색다른 걸 만들고 싶다는 생각이 들더군요!

안에 틀은 todo-list와 비슷하지만 겉에 주제는 제가 좋아하는 만화로 했습니다. 아직 팀원분들한테는 시간이 너무 늦어 말하지는 못했지만, 어느정도 틀을 짜고 말해주는 게 서로 편할 거 같아 윤곽만 잡고 내일 팀원들이랑 상의할 거 같네요 ^^

Api명세서

| 기능             | method | url                | request                    | response                       | 비고                                   |
| ---------------- | ------ | ------------------ | -------------------------- | ------------------------------ | -------------------------------------- |
| 게시물 추가      | Post   | /Api/post          | {username, title, content} | {username, title, content}     |                                        |
| 게시물 수정      | Put    | /api/post/{postid} | {title, content}           | 데이터 받을 필요 없음          | 새로고침되면서 알아서 데이터 수정이 됨 |
| 게시물 삭제      | Delete | /api/post/{postid} | {postid}                   | msg: 게시물이 삭제 되었습니다. |                                        |
| 게시글 전체 조회 | Get    | /api/post          |                            | {get post :게시물의 정보}      | 게시물의 정보들을 받아옴               |
|                  |        |                    |                            |                                |                                        |
|                  |        |                    |                            |                                |                                        |

백엔드분의 도움을 받아 작성해보았습니다. 모든 기능을 추가한 것은 아니지만, 어떻게 돌아가는지? 이런 것에 대해 쪼~~~~~~~~~~~~~~~~오끔 이해하게 되었네요.. 많이 어렵더군요.. ㅠ

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/d4c615a5-a90c-42c1-a13a-abfa7b17a6fe/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220805%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220805T191656Z&X-Amz-Expires=86400&X-Amz-Signature=fb8b0389dfed0298c8aa5145ac4416527cb385a8ed20e631b7f4ba1aa9d31d4c&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

와이어프레임도 간략하게 만들어보았습니다. 처음으로 만들다 보니 부족한 것들도 많고, 추가 기능들도 더 필요할 거 같네요. 부족한 것들은 팀원들과 상의해서 추가하려고 합니다.

이번 프로젝트도 화이팅해서 잘 마무리할 수 있도록 열심히 공부하겠습니다!!!
