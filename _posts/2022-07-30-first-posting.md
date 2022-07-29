---
layout: single
title: "상대 경로"
categories: coding
tag: [python, jekyll, blog]
toc: true
author_profile: false
sidebar:
  nav: "docs"
# search: false
---

Module not found: Can't resolve '파일' in '경로’에 대한 오류가 계속 떠서 경로에 대한 오류인가

싶어서 경로를 바꿨지만, 제대로 된 경로를 입력하지 않아서 오류를 고치지 못했다.

그래서 상대 경로에 대해서 검색했고 어느 정도 정리를 하게 되었다.

상대 경로를 풀어서 보면 ‘현재 위치한 곳을 기준’으로 해서 ‘그곳의 위치’이다.

```
/ : 루트   ./ : 현재 위치   ../ : 현재 위치의 상단 폴더
```

```
 1  '/'    -> 가장 최상의 디렉토리로 이동한다.(Web root)
 2  './'   -> 파일이 현재 디렉토리를 의미한다.
 3  '../'  -> 상위 디렉토리로 이동한다.- 만약 두단계 상위 디렉토리로 이동하려면
   '../../' 이렇게 사용하면 된다.

```

새로 만든 파일이 count_ex이다.

count_ex > src > modules > counter.js : A파일이라고 정하고,

count_ex > src > redux > modules > config > configStore.js : B파일이라고 정해보자

B파일에서 A파일을 import 하려고 한다. import counter(A파일) from ‘경로’를 입력해보자

경로를 찾기 위해선 B파일을 기준으로 A파일을 찾는다.

A파일과 B파일을 비교해보면, count_ex > src >~~~~~~~이후로 달라진다.

src까지 가려면 위로 3단계 이동해야 하기 때문에 ../../../ 사용하면 된다.

결국, import counter from “../../../modules/counter”; 가 된다.
