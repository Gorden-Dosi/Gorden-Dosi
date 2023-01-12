---
layout: post
title: JS Section 2 Unit 1 higher order function
---


# Section 2 Unit1 고차함수

처음 고차함수라는 말을 들었을 때, 함수도 못하는데 고차함수라니… 막막했었다.
하지만 천천히 하다보니 조금은 이해가 간다.

1. 일급 객체는 일급이라는 말과 같이 다른 요소보다 우선 순위이고 다음과 같은 특징이 있다.

- 변수에 할당(assignment) 할 수 있다.
- 다른 함수의 전달인자(argument)로 전달될 수 있다.
- 다른 함수의 결과로서 리턴될 수 있다.

그리고 함수를 변수에 할당할 수 있기 때문에, 함수를 배열의 요소나 객체의 속성값으로 저장할 수 있어  함수를 데이터(string, number, boolean, array, object)처럼 다룰 수 있다.
2. 고차 함수(higher order function)는 함수를 전달인자(argument)로 받을 수 있고, 함수를 리턴할 수 있는 함수이다.(커리함수라고도 부른다.)
3. 콜백함수(callback function)는 다른 함수(caller)의 전달인자(argument)로 전달되는 함수이다.
4. 내장 고차함수

1) filter
참인 값만 출력

```jsx
let [1,2,3]
let result = arr.filter(function(element){
return element % 2 !==0 
});

result; // [ 1 , 3]
```

2) map
요소 값을 재구성 ( maping )

```jsx
let [1,2,3]
let result = arr.map(function(element){
return element * 2
});

result; // [ 2, 4, 6 ]
```

3) reduce
요소 값끼리 연산

```jsx
let [1,2,3]
let result = arr.reduce(function( accumulation, current, index){
  accumulation + current;
return accumulation;
}, 1);

result; // 7
```

1. 고차함수의 중요성
복잡한 코드를 함수로 간단하게 표현할수 있다.
가독성이 좋아진다.
등등
2. 고차함수의 추상화
추상의 개념에서 0과 1은 단지 개념일 뿐이라서 개념전달을 용이하기 위한 기호일 뿐이다.
이때 추상화된 개념을 생각에서 추상화라는 그래도 명확하지 않지만 생각보다 
명확한 개념으로 전달이 가능하다.

그리고 우선 Prototype의 경우 객체에 내장되어 있는 메소드를 말한다. 
console 창에서 확인하는 방법이 있는걸로 아는데 추후 추가 하겠습니다.
