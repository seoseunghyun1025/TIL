## CSS Ep03_1 - 폰트(Font) 스타일

### 글꼴 관련 속성
- `font-family`: 글꼴 종류. 쉼표로 여러 개를 쓰면 앞의 글꼴이 없을 때 다음 글꼴을 적용함
- `font-size`: 글자 크기 (예: `28px`)
- `font-style: italic`: 기울임꼴(이탤릭체)
- `font-weight`: 글자 굵기
  - 키워드: `bold`, `bolder`, `lighter`
  - 숫자: `100`(가장 얇음) ~ `900`(가장 두꺼움)
- `font-variant: small-caps`: 소문자를 작은 대문자로 바꿈

```css
.title { font-size: 28px; }
.italic { font-style: italic; }
.bold { font-weight: bold; }
.small-caps { font-variant: small-caps; }
```

> 개발자 도구에서 요소를 선택하고 `font-family` 값을 바꿔 보면 글꼴이 바뀌는 걸 바로 확인할 수 있음

### 웹폰트 (Google Fonts)
- 사용자 컴퓨터에 설치되어 있지 않아도 온라인에서 내려받아 적용하는 글꼴
- 적용 순서
  1. Google Fonts에서 언어를 Korean으로 고르고 글꼴 선택 (실습: 나눔고딕)
  2. `@import` 코드를 복사해 `<style>` 맨 첫 줄에 붙여 넣기 (`<link>` 태그로 넣는 방법도 있음)
  3. 안내된 `font-family` 값을 복사해서 적용

```css
@import url('구글 폰트에서 복사한 주소');
html { font-family: 'Nanum Gothic', sans-serif; }
```

### 단위
- 글자 크기뿐 아니라 `width`, `height` 같은 크기를 정할 때도 씀

| 단위 | 기준 | 예시 |
|---|---|---|
| `px` | 화면의 픽셀 크기 | `20px` = 20픽셀 |
| `rem` | 최상위 요소(`html`)의 글자 크기 | html이 16px이면 `2rem` = 32px |
| `em` | 자기 자신의 글자 크기 (보통 부모에게서 상속받은 값) | 부모가 10px이면 `2em` = 20px |
| `vw` | 뷰포트(브라우저에 보이는 화면) 너비의 % | 화면 너비가 1200px이면 `50vw` = 600px |
| `vh` | 뷰포트 높이의 % | 화면 높이가 1600px이면 `50vh` = 800px |

> rem은 어디서 쓰든 html 기준이라 값이 일정하고, em은 부모 글자 크기에 따라 결과가 달라짐. vw와 vh는 화면 크기가 바뀌면 함께 늘어나고 줄어듦

#### 꿀팁: 클래스 붙여 쓰기
```css
.rectangle.width { width: 20vw; background-color: yellow; }
```
- `.rectangle.width`처럼 띄어쓰기 없이 붙이면 **두 클래스를 모두 가진 요소**를 선택함 (띄어 쓰면 자손 결합자가 됨)

## CSS Ep03_2 - 폰트(Font) 스타일 (이어서)

### 글자 색상 `color`
| 표기법 | 예시 | 설명 |
|---|---|---|
| 키워드 | `blue`, `red`, `transparent` | 색 이름으로 지정. `transparent`는 완전히 투명함 |
| RGB(A) | `rgb(255, 0, 0)`, `rgba(255, 0, 0, 0.5)` | 앞의 세 값은 빨강·초록·파랑, 네 번째 값은 투명도 |
| 16진수 | `#ff0000`, `#ff000080` | 두 자리씩 빨강·초록·파랑, 마지막 두 자리는 투명도 |

```css
.title { color: blue; }
.title { color: rgba(0, 0, 255, 0.5); } /* 반투명 파랑 */
```

> 투명도 값은 0에 가까울수록 투명해짐. 실무에서는 RGB나 16진수를 주로 씀
> 개발자 도구에서 색상 박스를 누르면 팔레트로 색을 고를 수 있음. 색상 값을 클릭할 때마다 RGB, 16진수 같은 다른 표기법으로 바뀜

### 텍스트 정렬 `text-align`
```css
.text-center { text-align: center; } /* 가운데 */
.text-right  { text-align: right; }  /* 오른쪽 */
.text-left   { text-align: left; }   /* 왼쪽 */
```

### 줄 간격 `line-height`
```css
html { font-size: 16px; }
.paragraph { line-height: 1.8; } /* 글자 크기의 1.8배 */
```
- `27px`처럼 고정값을 쓸 수도 있고, `em`이나 단위 없는 숫자로 글자 크기의 몇 배인지 정할 수도 있음

### 자간 / 단어 간격 / 들여쓰기
```css
.paragraph {
  letter-spacing: 2px;  /* 글자 사이 간격 */
  word-spacing: 1px;    /* 단어 사이 간격 */
  text-indent: 80px;    /* 문단 첫 줄 들여쓰기 */
}
```

### 대소문자 변환 `text-transform`
```html
<span class="text-transform">Korea</span>
```
```css
.text-transform { text-transform: uppercase; } /* KOREA */
.text-transform { text-transform: lowercase; } /* korea */
```

### 텍스트 장식 `text-decoration`
```css
a { text-decoration: none; }  /* a 태그 기본 밑줄 제거 */
/* line-through: 취소선, overline: 윗줄 */
```
> 주로 a 태그의 기본 밑줄을 없앨 때 많이 씀

### 텍스트 그림자 `text-shadow`
```css
.text-shadow { text-shadow: 10px 10px 10px black; }
/*                          x축  y축  번짐  색상 */
```
- 첫 번째 값은 가로(x축) 이동, 두 번째 값은 세로(y축) 이동. 음수를 쓰면 반대로 감 (예: y가 `-30px`이면 위로 올라감)
- 세 번째 값은 번짐 정도로, 클수록 더 흐려짐. 네 번째 값은 그림자 색

### 리스트 스타일 `list-style`
```css
ul { list-style: none; }   /* 앞의 점 모양 제거 */
ul { list-style: circle; } /* 속이 빈 동그라미 */
```

> 💡 강사 조언: 속성을 억지로 외울 필요는 없음. 자주 쓰다 보면 자연스럽게 익숙해지니까, 문법을 외우기보다 HTML과 CSS로 간단한 버튼이나 UI, 홈페이지를 직접 만들어 보는 게 훨씬 도움이 됨