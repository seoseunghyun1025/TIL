## HTML Ep08_1 - Form 태그 & input 태그

### `<form>`: 사용자 입력 양식을 감싸는 태그
- 로그인, 회원가입, 게시판 글쓰기처럼 사용자에게 데이터를 입력받는 양식
- 입력받는 데이터 하나하나를 폼 데이터 또는 필드라고 부름
- 주요 속성
  - `action`: 양식 데이터를 처리할 서버 쪽 주소
  - `method`: 제출할 때 쓰는 HTTP 메서드 (저장, 수정은 보통 POST)
### `<label>`: 입력 필드가 무엇인지 설명하는 태그
- 연결하는 방법은 두 가지
  1. `<label>` 안에 `<input>`을 넣기
  2. `<label for="id">`와 `<input id="id">`처럼 for 값과 id 값을 맞추기

### `<fieldset>` + `<legend>`
- `fieldset`: 폼 안의 데이터를 그룹으로 묶음 (예: 개인정보, 사업자정보)
- `legend`: 그룹의 제목

### `<input type="...">` 종류
- `email`: 제출할 때 이메일 형식인지 자동으로 검사
- `tel`: 모바일에서 숫자 키패드가 올라옴
- `url`: 제출할 때 URL 형식인지 검사
- `number`: 숫자만 입력 가능, 증가/감소 버튼이 생김
- `range`: 슬라이더로 범위 값을 입력
- `date` / `month` / `week`: 날짜 / 월 / 몇 번째 주
- `time`: 시간
- `file`: 파일 업로드, `multiple`을 붙이면 여러 개 선택 가능
- `hidden`: 화면에는 보이지 않고 서버로 값만 보냄 (`name`, `value`와 함께 사용)
- `password`: 입력값이 가려짐(마스킹)

### 자주 쓰는 속성
- `required`: 필수 입력. 비어 있으면 제출할 때 막힘
- `min` / `max`: number, range, date, time에서 최솟값과 최댓값 제한

### 폼 데이터 속성
- `readonly`: 읽기 전용. 값을 수정할 수 없지만 제출하면 서버로 **전송됨**
- `disabled`: 수정할 수 없고 흐리게 표시됨. 사용하지 않는 데이터라는 뜻이라 서버로 **전송되지 않음**
- `autofocus`: 페이지에 들어오면 해당 필드에 커서가 자동으로 놓임
- `placeholder`: 값이 비어 있을 때 보여주는 안내 문구 (예: "URL을 입력해주세요"). 입력을 시작하면 사라짐

> readonly와 disabled는 둘 다 수정이 안 됨. 차이는 서버로 값이 가는지(readonly) 안 가는지(disabled)

### `checkbox` / `radio`
- `type="checkbox"`: 여러 개 중 **2개 이상** 선택 가능
  - 실습: "좋아하는 색을 모두 고르세요" → red, orange, yellow, green, blue
- `type="radio"`: 여러 개 중 **하나만** 선택 가능
  - 실습: 배송 방법 → free / paid
  - `name`이 다르면 둘 다 체크되는 문제가 생김. 같은 그룹은 **`name`을 똑같이** 지정해야 함 (예: `name="delivery"`)
- 제출하면 각 항목의 `value`가 서버로 전송됨
- `label for`와 `input id`를 맞추면 글자를 클릭해도 선택됨

```html
<input type="radio" id="free" name="delivery" value="free">
<label for="free">무료</label>
<input type="radio" id="paid" name="delivery" value="paid">
<label for="paid">유료</label>
```

### `<textarea>`: 여러 줄 입력 (예: 자기소개)
- `rows`: 보이는 줄 수 (10 → 5로 바꾸면 높이가 줄어듦)
- `cols`: 보이는 칸(열) 수 (30 → 15로 바꾸면 너비가 줄어듦)
- 기본값은 `value` 속성이 아니라 **태그 사이의 내용**에 넣음

```html
<textarea rows="5" cols="15">나는 짐코딩입니다</textarea>
```

### `<select>` + `<option>`: 여러 옵션 중 고르기
- `<select>` 안에 `<option>`을 여러 개 넣어 사용
- 서버로 전송되는 것은 option 사이의 텍스트가 아니라 **`value`** 값
  - 예: `<option value="apple_10kg">사과 10kg</option>` → `apple_10kg`가 전송됨
- `selected`: 처음부터 선택되어 있을 옵션 지정
- `multiple`(select에 지정): 여러 개 선택 가능, 모양도 목록형으로 바뀜
  - Shift + 클릭: 연속 범위 선택
  - Ctrl(Mac은 Cmd) + 클릭: 떨어진 항목 따로 선택

### `<datalist>`: 검색이 되는 선택 목록
- select처럼 옵션을 고르지만, `<input>`과 함께 쓰는 점이 다름
- **input의 `list` 값과 datalist의 `id` 값을 반드시 맞춰야 함**
- input 기반이라 입력하면서 옵션을 **검색**할 수 있음

```html
<input list="fruits">
<datalist id="fruits">
  <option value="사과">
  <option value="바나나">
</datalist>
```

### `<button type="...">`
- `submit`: 폼 데이터를 form의 `action` 주소로 전송
  - **type을 안 쓰면 기본값이 submit**
  - 실습에서 404 페이지가 뜬 이유: action에 적은 주소에 서버 프로그램이 없어서
- `reset`: 폼 안의 입력값을 모두 처음 상태로 되돌림
- `button`: 기본 동작이 없음. 주로 JavaScript를 실행할 때 사용
  - 예: `onclick="alert('Hello World')"` → 클릭하면 경고창이 뜸 (이벤트는 JS에서 자세히 배움)
- button 태그는 form 안뿐 아니라 필요한 곳 어디에나 쓸 수 있음

### Form 전체 정리
- `<form>`: 폼을 정의하는 영역이자 필드(폼 데이터)를 담는 컨테이너
- `<input>`: 필요한 데이터 종류에 맞는 type으로 입력받음
- 그 외: `textarea`, `select`, `datalist`, `button`
- 받으려는 데이터와 사용자가 편하게 쓸 수 있는 컨트롤을 기준으로 알맞은 요소를 고르기

> 모든 폼 태그와 속성을 외울 필요 없음. 자주 쓰는 건 실제로 만들다 보면 자연스럽게 외워지고, 기억나지 않으면 구글이나 MDN에서 찾아보기