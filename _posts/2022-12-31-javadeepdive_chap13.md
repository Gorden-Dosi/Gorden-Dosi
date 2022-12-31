# Chapter 13. 스코프

---

### 1. 스코프란 Scope

스코프(유효범위)는 자바 스크립트를 포함한 모든 프로그래밍 언어의 기본적이며 중요한 개념이다.

다른 언어의 스코프와는 구별되는 특징이 있고, 각각의 var, let, const 키워드로 선언한 변수의 스코프는 다르게 동작며, 스코프는 변수와 함수에 깊은 관련이 있다.

```
//예제 1
function add(x, y) {
  // 매개변수는 함수 몸체 내부에서만 참조할 수 있다.
  // 즉, 매개변수의 스코프(유효범위)는 함수 몸체 내부다.
  console.log(x, y); // 2 5
  return x + y;
}

add(2, 5);

// 매개변수는 함수 몸체 내부에서만 참조할 수 있다.
console.log(x, y); // ReferenceError: x is not defined
```

변수는 코드의 가장 바깥 영역 뿐 아니라 코드 블록이나 함수 몸체 내에서도 선언할 수 있고 이때 코드 블록이나 함수는 중첩될 수 있다.

---

<aside>
<img src="https://www.notion.so/icons/playback-pause_red.svg" alt="https://www.notion.so/icons/playback-pause_red.svg" width="40px" /> **모든 식별자(변수 이름, 함수 이름, 클래스 이름 등)는 자신이 선언된 위치에 의해 다른 코드가 식별자 자신을 참조할 수 있는 유효 범위가 결정된다. 이를 스코프라고 한다. === 스코프는 식별자가 유효한 범위**

</aside>

```jsx
//예제 2
var var1 = 1; // 코드의 가장 바깥 영역에서 선언한 변수

if (true) {
  var var2 = 2; // 코드 블록 내에서 선언한 변수
  if (true) {
    var var3 = 3; // 중첩된 코드 블록 내에서 선언한 변수
  }
}

function foo() {
  var var4 = 4; // 함수 내에서 선언한 변수

  function bar() {
    var var5 = 5; // 중첩된 함수 내에서 선언한 변수
  }
}

console.log(var1); // 1
console.log(var2); // 2
console.log(var3); // 3
console.log(var4); // ReferenceError: var4 is not defined
console.log(var5); // ReferenceError: var5 is not defined
```

```jsx
// 예제 5 - 동 스코프 내에서 var의 중복 선언 허용
function foo() {
  var x = 1;
  // var 키워드로 선언된 변수는 같은 스코프 내에서 중복 선언을 허용한다.
  // **아래 변수 선언문은 자바스크립트 엔진에 의해 var 키워드가 없는 것처럼 동작한다.**
  var x = 2;
  console.log(x); // 2
}
foo();
```

```jsx
// 예제 6 - 동 스코프 내에서 let의 중복 선언 불가
function bar() {
  let x = 1;
  // **let이나 const 키워드로 선언된 변수는 같은 스코프 내에서 중복 선언을 허용하지 않는다.**
  let x = 2; // SyntaxError: Identifier 'x' has already been declared
}
bar();
```

### 2. **스코프의 종류**

| 구분 | 설명 | 스코프 | 변수 | 참조 가능 범위 |
| --- | --- | --- | --- | --- |
| 전역 | 코드의 가장 바깥 영역 | 전역 스코프 | 전역 변수 | 전역 |
| 지역  | 함수 몸체 내부 | 지역 스코프 | 지역 변수 | 자신의 지역과 
하위지역 스코프 |

![IMG_7205D11372AA-1.jpeg](Chapter%2013%20%E1%84%89%E1%85%B3%E1%84%8F%E1%85%A9%E1%84%91%E1%85%B3%20439c546cc27d4341be1307b45d8be1ce/IMG_7205D11372AA-1.jpeg)

### 3. 스코프 체인 scope chain

함수는 전역과 함수 몸체 내부에서 정의가 가능하다. 이를 ‘함수의 중첩’이라고 하고,

몸체 내부에 정의한 함수를 ‘**중첩 함수**nested function’, 이를 포함하는 함수를 

‘외부 함수outer function’라고 한다.

스코프 체인은 함수의 중첩으로 인한 계층적 연결된 구조를 말한다.

<aside>
<img src="https://www.notion.so/icons/playback-pause_gray.svg" alt="https://www.notion.so/icons/playback-pause_gray.svg" width="40px" /> 스코프 체인에서 변수를 참조할 때 자바스크립트 엔진은 스코프 체인을 통해 별수를 참조하는 코드의 스코프에서 시작하여 상위 스코프 방향으로 이동하며 선언된 ‘**변수를 검색**identifier resolrution’한다.

</aside>

![IMG_A05DF097E568-1.jpeg](Chapter%2013%20%E1%84%89%E1%85%B3%E1%84%8F%E1%85%A9%E1%84%91%E1%85%B3%20439c546cc27d4341be1307b45d8be1ce/IMG_A05DF097E568-1.jpeg)

1) 스코프 체인에 의한 변수 검색

 **하위 → 상위 스코프로 검색만 가능
 상위 스코프에서 유효한 변수는 하위 스코프에서 자유롭게 참고 가능하지만 
 하위 스코프에서 유효한 변수를 상위 스코프에서 참조 불가.**

2) 스코프 체인에 의한 함수 검색

 **검색 방식은 변수와 다르지 않다.**

12장 함수에서와 같이 함수는
  **함수 이름과 동일한 식별자를 암묵적으로 생성 및 할당** →  런타임 시작 → 함수 검색
의 순서로 동작한다.

따라서 스코프는 ‘**변수와 함수와 관계없이 식별자를 검색하는 규칙’**이라고 표현하는 것이 적합하다.

### 4. 함수 레벨 스코프

지역은 함수의 몸체 내부를 말하고, 지역은 지역 스코프를 만든다는 의미는
**코드 블록이 아닌 함수에 의해서만 지역스코프가 생성된다는 것이다.**

```jsx
//예제7
var x = 1;

if (true) {
  // var 키워드로 선언된 변수는 함수의 코드 블록(함수 몸체)만을 지역 스코프로 인정한다.
  // 함수 밖에서 var 키워드로 선언된 변수는 코드 블록 내에서 선언되었다 할지라도 모두 전역 변수다.
  // 따라서 x는 전역 변수다. 이미 선언된 전역 변수 x가 있으므로 x 변수는 중복 선언된다.
  // 이는 의도치 않게 변수 값이 변경되는 부작용을 발생시킨다.
  var x = 10;
}

console.log(x); // 10
```

```jsx
// 예제8
var i = 10;

// for 문에서 선언한 i는 전역 변수다. 이미 선언된 전역 변수 i가 있으므로 중복 선언된다.
for (var i = 0; i < 5; i++) {
  console.log(i); // 0 1 2 3 4
}

// 의도치 않게 변수의 값이 변경되었다.
console.log(i); // 5
```

위는 전역에 선언된 변수와 같은 식별자를 지역에 중복된 식별자로 선언한다면 
지역에 선언했더라도 전역 변수로 동작한다는 예외상황이다.

### 5. 렉시컬 스코프Lexical scope

```jsx
var x = 1; // x 전역스코프 정의

function foo() { // foo 함수 정의
  var x = 10;
  bar(); // bar 함수 정의
}

function bar() {
  console.log(x);
}

foo(); // ?
bar(); // ?
```

- 프로그래밍에서 상위 스코프가 결정되는 방식은 2가지이다.
- 함수를 어디서 호출했는지에 따라 함수의 상위 스코프를 결정한다.
   = 동적 스코프dynamic scope // 전역스코프와 foo함수의 지역스코프
- 함수를 어디서 정의했는지에 따라 함수의 상위 스코프를 결정한다.
   = 정적 스코프lexical scope 혹은 정적 스코프static scope // foo함수의 지역스코프

<aside>
<img src="https://www.notion.so/icons/playback-pause_red.svg" alt="https://www.notion.so/icons/playback-pause_red.svg" width="40px" /> 자바스크립트는 **‘렉스컬 스코프’**이므로 함수를 어디서 정의했는지에 따라 상위 스코프를 정의한다.

</aside>

렉시컬 스코프는 클로저와 깊은 관계가 있어 24장에서 자세한 설명 추가 예정.