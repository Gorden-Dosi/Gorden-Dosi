---
layout: post
title:  Day 21 JS Koans
---
# Day 21 JS Koans 회고

expert 함수 사용

<aside>
💡 Koans란 **看話禪 //**
 간화선 불교에서 유래된 단어로, 결론을 내리기 전에 이게 왜 맞는지 깊게 고민한다는 의미를 가지고 있다고 합니다.

</aside>

NPM을 이용한 과제를 통해 Koans를 하고 회고한다.

1. 어떻게 test가 작동되는 지, 작동 원리를 터득했다.
2. type 에 대한 문제

```jsx
console.log(1 + '1') // '11'
console.log(123 - '1') // 122
console.log(1 + true) // 2
console.log('1' + true) // '1true'
```

문자열과 숫자의 암묵적 타입변환에 대해 생각해 볼수 있는 문제였다.

1. const 변수 선언 에 대한 문제
[https://google.github.io/styleguide/jsguide.html#features-use-const-and-let](https://google.github.io/styleguide/jsguide.html#features-use-const-and-let)
링크로 자세히 볼수 있었다.
2.  함수 선언문과 표현식 함수의 호이스팅 비교를 직접적인 실험을 통해 명확히 알수 있었고
또한 스코프 영역 역시 테스트를 통해 확실히 확인이 가능했다.
그러나 클로저 함수의 정의와 배열내 인덱스 순서와 개념, 객체의 순서와 인덱스 개념은 헛갈려서
계속해서 공부해야 할 듯하다.
[https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures) ⇒ 클로저의 정의
3. 화살표 함수 - 화살표 함수의 대략적인 사용법을 알 수 있었다.

```
// function 키워드를 생략하고 화살표 => 를 붙입니다
    const add = (x, y) => {
      return x + y
    }
   // add(10, 20) ;30

    // 리턴을 생략할 수 있습니다
    const subtract = (x, y) => x - y
   // subtract(10, 20) ;-10

    // 필요에 따라 소괄호를 붙일 수도 있습니다
    const multiply = (x, y) => (x * y)
    //multiply(10, 20) ;200

    // 파라미터가 하나일 경우 소괄호 생략이 가능합니다
    const divideBy10 = x => x / 10
    // divideBy10(100) ; 10
```

1. 원시 자료형과 참조 자료형의 차이를 알 수 있었다.
원시 자료형 - 이름(혹은 식별자?)에 정보저장
참조 자료형 - 이름(혹은 식별자?)에 주소 저장, 별도 공간에 정보 저장.
2. 배열의 인덱스 순서가 헛갈려서 추가적으로 검색을 해야했다.

```jsx
function () {
    const arr = ['peanut', 'butter', 'and', 'jelly'];

    arr.slice(1) // [ 'butter', 'and', 'jelly' ]);
    arr.slice(0, 1) // ['peanut']);
    arr.slice(0, 2) // ['peanut', 'butter']);
    arr.slice(2, 2) // []);
    arr.slice(2, 20) // ['and', 'jelly']);
    arr.slice(3, 0) // []);
    arr.slice(3, 100) // ['jelly']);
    arr.slice(5, 1) // []);
```

1. 객체의 사용법과 특징을 할수 있었다.
참조자료형으로서 추가하고 지우는 개념을 다시 상기할수 있었다.
[https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/this](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/this) ⇒ this의 개념
[https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/this](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/this)
⇒****Copying Objects in JavaScript****
[https://medium.com/watcha/깊은-복사와-얕은-복사에-대한-심도있는-이야기-2f7d797e008a](https://medium.com/watcha/%EA%B9%8A%EC%9D%80-%EB%B3%B5%EC%82%AC%EC%99%80-%EC%96%95%EC%9D%80-%EB%B3%B5%EC%82%AC%EC%97%90-%EB%8C%80%ED%95%9C-%EC%8B%AC%EB%8F%84%EC%9E%88%EB%8A%94-%EC%9D%B4%EC%95%BC%EA%B8%B0-2f7d797e008a)
⇒****깊은 복사와 얕은 복사에 대한 심도있는 이야기****
2. 전개 문법(spread syntax) 문법 및 사용법을 확인 할 수 있었다.
3. 구조 분해 할당(Destructing Assignment)에 관해서 느낄 수 있었다.

Koans를 하며 내가 몰랐던 부분을 더 확실히 알고 자세히 알고 싶은 개념과 용법을 찾아보고 싶어졌다.

1) 배열, 객체 그리고 인덱스에 대해서
2) 원시 자료형과 참조 자료형의 변수 선언방식과 정보 저장방식, 그리고 식별자와 이름의 차이
3) 객체와 전개 문법, 구조 분해 할당의 추가적인 예시

추가로 찾아보면 좋을것
[https://ko.javascript.info/strict-mode](https://ko.javascript.info/strict-mode)  ⇒ 엄격모드 설명
[https://ko.javascript.info/var#ref-21](https://ko.javascript.info/var#ref-21) ⇒ 즉시 실행 함수 표현식(IIFE)
[https://poiemaweb.com/es6-block-scope#13-호이스팅](https://poiemaweb.com/es6-block-scope#13-%ED%98%B8%EC%9D%B4%EC%8A%A4%ED%8C%85) ⇒ 변수 호이스팅과 TDZ(Temporal Dead Zone)

[https://www.chaijs.com/api/bdd/](https://www.chaijs.com/api/bdd/)
