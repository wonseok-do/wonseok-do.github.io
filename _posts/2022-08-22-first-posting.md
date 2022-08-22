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

클론코딩주차 시작한지 벌써 4일이 지났습니다.. 하루하루 정신적으로 힘든 나날들이였네요..

이번 조에 배치된 팀원분들이 다 잘하는 분들이셔서 옆에 있을 때 제가 작아지고 있는 기분이 계속 들었습니다. 스트레스 받지 말아야지 하는 생각을 해보았지만 잘 안되고 비교하지 않으려고 해도 그게 쉽지가 않네요.. 제가 맡은 기능도 제대로 구현하지 못하니 더 답답하구요.. 그 분들이라면 금방 끝났을텐데.. 계속해서 의기소침해지고 정말 힘드네요.. 그래도 포기할 생각은 없습니다. 이렇게 빨리 포기할거라면 시작조차 안했을테니깐요.. 버티는 거라면 자신있지만.. 그저 하루하루 뭐하나 이룬 거 없이 시간만 축내고 있지 않나 이 생각이 드네요.. 그래도 매니저님들의 조언으로 정말 큰 기능하나 구현하지 못하더라도 아주 사소한 거 정~말 사소한 거 하나라도 이루어내고 내 것으로 만들어야겠다라는 생각을 하게 되었습니다. 너무 많은 것을 배우고 가지려고 과하게 욕심을 가졌었던 것 같습니다.

진짜 남들한테는 아무것도 아닌 정말 보잘거 없는 기능일지라도 저한테는 엄청난 시간이 걸리는 것이기에 이 기능 하나라도 구현할 수 있도록 노력할 것이고, 조금씩 성장하겠습니다. 곧 있으면 실전프로젝트가 시작되는데 너무 큰 욕심내지 않고 간단한 기능이라도 해도 최선을 다해 만들면서 조금씩 조금씩 제 영역을 넓혀 제가 할 수 있는 한에서 최대한 노력하려고 합니다. 지금 정말 보잘것 없지만 정말 잘하고 싶네요.. 이렇게 좀 내려놓으니 한결 편하네요.. 아직 힘들지만요 ㅎㅎ

제가 메인페이지구역을 맡았고 게시글 전체 조회를 하는데요. 무한 스크롤을 하자는 의견이 있어 오늘 하루종일 서칭을 해보았지만 비슷한 글을 읽어도 읽어도 이해가 잘 안되군요.. 저녁에 중간 점검이 있었는데요 그때 매니저님이 어려운 부분이기도 하니 페이지네이션부터 해보는 게 어떻겠냐고 조언하셔서 페이지네이션을 구현하였습니다. 기능 대부분은 카피로 이루어진거지만 그 안에 기능들이 어떻게 돌아가는 지 그거에 초점을 두었습니다.

```jsx
const [limit, setLimit] = useState(4);
  const [page, setPage] = useState(1);
  const offset = (page - 1) * limit;
//
<label>
        페이지 당 표시할 게시물 수:&nbsp;
        <select
          type="number"
          value={limit}
          onChange={({ target: { value } }) => setLimit(Number(value))}
        >
          <option value="4">4</option>
          <option value="8">8</option>
          <option value="12">12</option>
        </select>
      </label>
//
{postList.slice(offset, offset + limit).map((post) => {
...
}
//
<footer>
        <Pagination
          total={postList.length}
          limit={limit}
          page={page}
          setPage={setPage}
        />
      </footer>
```

```jsx
//src/Pagination
import styled from "styled-components";

function Pagination({ total, limit, page, setPage }) {
  const numPages = Math.ceil(total / limit);

  return (
    <>
      <Nav>
        <Button onClick={() => setPage(page - 1)} disabled={page === 1}>
          &lt;
        </Button>
        {Array(numPages)
          .fill()
          .map((_, i) => (
            <Button
              key={i + 1}
              onClick={() => setPage(i + 1)}
              aria-current={page === i + 1 ? "page" : null}
            >
              {i + 1}
            </Button>
          ))}
        <Button onClick={() => setPage(page + 1)} disabled={page === numPages}>
          &gt;
        </Button>
      </Nav>
    </>
  );
}
export default Pagination;

const Nav = styled.nav`
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 4px;
  margin: 16px;
`;

const Button = styled.button`
  border: none;
  border-radius: 8px;
  padding: 8px;
  margin: 0;
  background: black;
  color: white;
  font-size: 1rem;

  &:hover {
    background: tomato;
    cursor: pointer;
    transform: translateY(-2px);
  }
  &[disabled] {
    background: grey;
    cursor: revert;
    transform: revert;
  }
  &[aria-current] {
    background: deeppink;
    font-weight: bold;
    cursor: revert;
    transform: revert;
  }
`;
```

offset과 slice, limit로 한 페이지에 몇개의 게시글이 들어가며 그것을 어떻게 반복할 것인지에 대해 알아보면서 공부하니깐 흥미를 느꼈고 재밌었습니다. 무한스크롤은 하루종일봐도 이해를 거의 못했었는데 이것은 그나마 조금은 이해가 되어서 코드작성할 때나 코드를 봤을 때 기분이 무척 좋았습니다. 아직 완벽하게 이해한 것은 아니지만 몇 번 더 써보면 좀 나아질 거 같습니다. 그래도 오늘 이렇게 하나라도 배워가서 너무 좋네요.. 정말 정말 부족한 저이지만 조금씩 조금씩 진짜 한발자국씩이라도 이렇게 나아가겠습니다 화이팅!!!!
