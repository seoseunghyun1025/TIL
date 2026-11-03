## CSS Ep02 - 선택자(Selector)
- 선택자: CSS로 꾸밀 HTML 태그를 고르는 방법. 태그를 선택한 다음 색상, 크기 등 스타일을 적용함

### 1. 기본 선택자 (Ep02_1)

#### 전체 선택자 `*`
- 문서 안의 **모든 요소**를 선택함
- 주로 브라우저 기본 스타일을 초기화할 때 사용함

```css
* {
  margin: 0;
  padding: 0;
}
```

#### 타입(태그) 선택자 `태그명`
- 태그 이름으로 선택함. 해당 태그는 **전부** 적용됨

```css
h2 { color: green; }
p {
  color: gray;
  font-weight: 400;   /* 글자 두께 */
  text-align: center; /* 왼쪽/가운데/오른쪽 정렬 */
}
```

#### 클래스 선택자 `.클래스명`
- class 속성 값으로 선택함
- 같은 클래스를 **여러 요소에 중복**해서 쓸 수 있음
- 클래스명은 자유롭게 짓되, 역할이 드러나게 지으면 가독성이 좋아짐

```html
<span class="red-text">동해</span>
<span class="blue-text">남산</span>
```
```css
.red-text { color: red; }
.blue-text { color: blue; }
```

#### ID 선택자 `#아이디명`
- id 속성 값으로 선택함
- id는 문서 안에서 **유일해야 함** (중복 불가, 요소 하나만 선택)

```css
#title {
  font-size: 40px;
  color: darkgray;
  background-color: ...;
}
```

> 클래스는 여러 번 쓸 수 있고, ID는 한 번만 쓸 수 있음

### 2. 속성 선택자 (Ep02_2)
- HTML 요소의 **속성**이 있는지, 또는 속성 **값**이 무엇인지에 따라 요소를 선택함

#### `[속성]`: 속성이 있으면 선택
```css
h2[class] { font-size: 30px; }  /* class 속성이 있는 h2만 */
a[target] { color: green; }     /* target 속성이 있는 a만 */
[target] { color: green; }      /* 태그 없이 속성만 써도 됨 */
```

#### `[속성="값"]`: 값이 정확히 일치
```css
h2[class="naver-title"] { color: green; }
```

#### `[속성*="값"]`: 값을 포함 (문자열 일부)
```css
a[href*="www"] { text-decoration: none; }  /* 밑줄 제거 */
```

#### `[속성^="값"]`: 값으로 시작
```css
h2[class^="google"] { color: blue; }
```

#### `[속성$="값"]`: 값으로 끝남
```css
a[href$="facebook.com"] { color: red; }
```

#### `[속성~="값"]`: 공백으로 구분된 값 중 해당 **단어**가 있음
- class처럼 값을 여러 개 지정했을 때 사용
```css
h2[class~="title"] {
  color: blue;
  font-weight: 300;
}
```

> `*=`는 문자열 안에 글자가 포함되어 있으면 선택하고, `~=`는 공백으로 구분된 단어 하나가 정확히 있어야 선택함

### 3. 그룹 선택자 & 결합자 (Ep02_3)

#### 그룹 선택자 `A, B`
- 쉼표로 여러 선택자를 묶어 같은 스타일을 한 번에 적용함
```css
h1, h2 { text-align: center; }
```

#### 결합자: 요소 사이의 관계로 선택
- **형제 요소**: 같은 부모 아래 같은 단계에 있는 요소들

```html
<section>
  <ul>
    <li>...</li>        <!-- section의 자손, ul의 자식 -->
  </ul>
  <span>구글</span>     <!-- section의 자식 -->
</section>
```

##### 자손 결합자 `A B` (띄어쓰기)
- A 안에 있는 **모든 하위 요소** B를 선택함 (깊이 상관없음)
```css
section li { color: blue; }    /* ul 안에 있어도 선택됨 */
section span { color: red; }
```

##### 자식 결합자 `A > B`
- A의 **바로 아래(1단계)** 에 있는 B만 선택함
```css
section > li { color: yellow; }      /* ❌ li는 ul 안에 있어서 적용 안 됨 */
ul > li { color: yellow; }           /* ⭕ */
section > ul > li { color: blue; }   /* ⭕ 단계별로 이어 쓰기 가능 */
```

##### 일반 형제 결합자 `A ~ B`
- A **뒤에 나오는** 형제 B를 모두 선택함 (A보다 앞에 있는 B는 선택 안 됨)
```css
p ~ span { color: red; }
```

##### 인접 형제 결합자 `A + B`
- A **바로 다음에** 붙어 있는 형제 B 하나만 선택함
```css
p + code { font-size: 30px; }
.first + li { color: blue; }   /* class="first"인 li 바로 다음 li */
```

| 결합자 | 기호 | 선택 범위 |
|---|---|---|
| 자손 | `A B` | A 안의 모든 B |
| 자식 | `A > B` | A 바로 아래의 B |
| 일반 형제 | `A ~ B` | A 뒤에 나오는 형제 B 전부 |
| 인접 형제 | `A + B` | A 바로 다음 형제 B 하나 |

> 실무에서는 기본 선택자, 그룹 선택자, 자손·자식 결합자를 가장 많이 씀. 형제 결합자는 외우지 말고 쓰다 보면 익숙해짐. 의사 클래스(고급 선택자)는 CSS 후반부에서 다룸