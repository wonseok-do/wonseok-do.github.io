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

오늘은 회원가입 페이지에서 카테고리를 추가하는 작업을 하려고 했는데요.

어떻게 데이터값을 클릭했을 때 추가하고, 다시 취소했을 때 삭제할 지에 대해서 찾아봤습니다

처음에는 간단하게 state값을 줘서 토글로 만들려고 했지만 그 이후가 문제라서.. 어떤 방법이

있을까 찾아봤는데 new Set()이라는 게 있네요. 이것을 사용하면 input type을 checkbox로 두고

check가 되었을 때 onChange함수를 통해서 state값에 new Set()을 넣고 add 하거나 delete할 수 있습니다 이것을 조금 시도해봤는데 로직을 이상하게 짜서인지.. 데이터 값이 안들어오고.. div 값만 들어오게 되는데요.. 뭔가 꼬인 것 같네요.. ㅠㅠ 원래는 react hook form으로 해보려고 했는데 막상 해보려니 음…… 생각만 많아지고 어떻게 시도해야 할 지 몰라서.. 음 모르겠네요 ㅠㅠ

그래서 일단 다른 방법으로 할 수 있는 방법까지 해보고 그 다음에 해보려고 합니다.

뭔가 조금 더 잘 짜면.. 구현할 수 있을 것 같은데요.. 음.. 내일 다시 한 번 더 시도해보려고 합니다.

화이팅!!
