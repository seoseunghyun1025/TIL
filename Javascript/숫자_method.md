# TIL: 숫자와 Math 메소드 (Number, Math)

## 1. 진법 변환: `toString(n)`
- 숫자를 문자열로 바꾼다. 괄호 안에 숫자를 넣으면 그 진법으로 변환한다.

```js
let num = 10;
num.toString();   // "10"
num.toString(2);  // "1010"

let num2 = 255;
num2.toString(16); // "ff" (색상 표현에 자주 씀)
```

## 2. Math 내장 객체
- 수학 관련 프로퍼티와 메소드를 가진 내장 객체다.
- `Math.PI`: 원주율

### 올림 / 내림 / 반올림

```js
let num1 = 5.1;
let num2 = 5.7;

Math.ceil(num1);  // 6  올림
Math.floor(num2); // 5  내림
Math.round(num1); // 5  반올림
Math.round(num2); // 6
```

## 3. 소수점 자릿수 다루기
**방법 1: 곱하고 반올림한 뒤 나누기**

```js
let userRate = 30.1234;
Math.round(userRate * 100) / 100; // 30.12
```

**방법 2: `toFixed(n)`로 소수점 n자리까지 반올림 (더 간단)**

```js
userRate.toFixed(2);  // "30.12"
userRate.toFixed(0);  // "30"         0이면 정수 부분만 남음
userRate.toFixed(6);  // "30.123400"  자릿수보다 크면 0으로 채움
```

> ⚠️ `toFixed()`는 **문자열을 반환**한다. 그래서 `Number()`로 숫자로 바꾼 뒤 작업하는 경우가 많다.

```js
Number(userRate.toFixed(2)); // 30.12
```

## 4. `isNaN()`
- `NaN`인지 판별한다.
- `NaN`은 자기 자신과도 같지 않다고 판단하기 때문에, NaN인지 검사하는 방법은 `isNaN()`뿐이다.

```js
let x = Number('x'); // NaN
x == NaN;    // false
x === NaN;   // false
NaN == NaN;  // false
isNaN(x);    // true
```

## 5. `parseInt()` / `parseFloat()`
- `parseInt()`: 문자열을 정수로 바꾼다. `Number()`와 달리 **문자가 섞여 있어도 동작**한다.
  - 읽을 수 있는 데까지 읽다가 문자를 만나면 거기까지의 숫자를 반환한다.
  - 숫자로 시작하지 않으면 `NaN`을 반환한다.
  - 두 번째 인수로 **진법**을 지정할 수 있다.
- `parseFloat()`: `parseInt()`와 같지만 **소수점까지** 반환한다. `parseInt()`는 소수점 이하를 버린다.

```js
let margin = '10px';
parseInt(margin); // 10
Number(margin);   // NaN

let redColor = 'f3';
parseInt(redColor);     // NaN
parseInt(redColor, 16); // 243

parseInt('11', 2);      // 3  (2진수 → 10진수)

let padding = '18.5%';
parseInt(padding);   // 18
parseFloat(padding); // 18.5
```

## 6. `Math.random()`
- 0 이상 1 미만의 랜덤 숫자를 만든다.

```js
// 1 ~ 100 사이 랜덤 정수
Math.floor(Math.random() * 100) + 1;
```

| 단계 | 의미 |
|---|---|
| `Math.random()` | 예: 0.6789 |
| `* 100` | 뽑을 숫자의 개수 (5로 바꾸면 1~5) |
| `Math.floor()` | 소수점 이하를 버림 → 0~99 |
| `+ 1` | 0이 나올 수 있으니 1을 더해 1~100으로 맞춤 |

## 7. 기타 Math 메소드

```js
Math.max(1, 4, -1, 5, 10); // 10  최댓값
Math.min(1, 4, -1, 5, 10); // -1  최솟값
Math.abs(-1);              // 1   절댓값 (absolute)
Math.pow(2, 10);           // 1024 거듭제곱 (power)
Math.sqrt(16);             // 4   제곱근 (square root)
```

## 정리
- 쇼핑몰 가격 계산이나 통계 지표를 만들 때 꼭 필요하다.
- 결과가 문자열인지 숫자인지(`toString`, `toFixed`) 꼭 확인하자.