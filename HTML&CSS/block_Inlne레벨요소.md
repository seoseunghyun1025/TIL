## HTML Ep06 - Block 레벨 요소와 Inline 레벨 요소

### div vs span
- 둘 다 영역을 나누는 컨테이너 태그 (시맨틱 태그 아님)
- `<div>`: 영역을 나누고 다른 태그를 담는 박스
- `<span>`: 특정 글자나 문장에만 스타일을 줄 때

### Block vs Inline
- 모든 HTML 태그에는 기본 `display` 값이 있음 → `block`이면 블록 요소, `inline`이면 인라인 요소
- 대표 예시: `div`는 블록, `span`은 인라인

| | Block (`div`, `p` 등) | Inline (`span`, `a` 등) |
|---|---|---|
| 차지하는 공간 | 가로 한 줄 전체 | 내용만큼만 |
| 배치 | 세로로 쌓임 | 가로로 나란히 |
| `width`, `height` | 적용됨 | 적용 안 됨 (위아래 `margin`도 안 됨) |

> - CSS `display` 값을 바꾸면 block ↔ inline 전환 가능
>   (`div`에 `display: inline` → 크기 지정 안 먹힘 / `span`에 `display: block` → 블록처럼 동작)
> - 다 외울 필요 없음. 대신 이 차이를 알면 나중에 레이아웃이 깨졌을 때 원인 찾기 쉬움
> - 개발자 도구 → Computed 탭에서 태그의 `display` 값 확인 가능