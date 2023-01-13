---
layout: post
title: class와 instance
---

# class와 instance

JavaScript는 객체지향 언어이기 때문에 객체를 구분하는 용어의 차이를 잘 알아야 한다.
청사진(설계도), blueprint에 해당하는 객체를 class,
blueprint를 바탕으로 한 인스턴스 객체(instance object)를 줄여서 instance라고 칭합니다.

```jsx
ES5dp에서는 클래스를 함수로 정의
function Phone(brand, name, color){
 // 인스턴스가 만들어질 때 실행되는 코드
}

ES6 에서는 class 키워드를 통해서도 정의 가능.
class Phone{
  constructor( brand, name, color ) {
   // 인스턴스가 만들어질 때 실행되는 코드
  }
}

new 키워드로도 클래스의 인스턴스 생성가능.
let iphone = new Phone('apple','iphone','midNight');
let galaxy = new Phone('samsung','galaxy','phantomWhite');
let pixel = new Phone('google','pixel','lemongrass');
```

속성과 메소드

| 속성 | 메소드 |
| --- | --- |
| brand
name
color
battery level
AP clock pulse | recharge()
running()
setapp() |

모바일 폰의 속성은 브랜드, 모델명, 색상, 배터리상태 등이 있을 있습니다.
메서드는 쉽게 말해 ‘객체에 이미 포함된 함수’입니다. 배터리 충전, 프로그램 실행,
프로그램 실행 등이 메서드 입니다.

```jsx
ES5
function Phone( brand, name, color ) {
  this.brand = brand;
  this.name = name;
  this.color = color;
 }

ES6
class Phone{
  constructor( brand, name, color ) {
  this.brand = brand;
  this.name = name;
  this.color = color;
 }
}
```

this는 인스턴스 객체를 의미한다. parameter로 넘어온 요소를 인스턴스 생성시 지정하는 값이며

this에 할당한다는 것은 인스턴스에 해당 요소를 부여하겠다는 의미입니다.

```jsx
ES5
function Phone( brand, name, color ) { /* 생략 */ }
Phone.prototype.recharge = function() {
  // 충전을 구현하는코드 
}
Phone.prototype.running = function() {
 // 앱 실행을 구현하는 코드
 }

ES6
class Phone{
  constructor( brand, name, color ) { /* 생략 */ }
   recharge() {
 }
   running() {
 }
```

 ES5 - prototype 키워드를 사용해야 메서드를 정의할수 있음.
 ES6 - 생성자 함수와 함께 class 키워드 안쪽에 묶어서 정의.

| prototype | 모델의 청사진을 만들때 쓰는 원형 객체(original form) |
| --- | --- |
| constructor | 인스턴스가 초기화 될때 실행하는 생성자 함수 |
| this | 함수가 실행될 때 해당 scope마다 생성되는 고유한 실행 context(execution context)
new 키워드로 인스턴스를 생성했을 때는 해당 인스턴스가 this값이 됨. |

```jsx
let galaxy = new Phone('samsung','galaxy','phantomWhite')
galaxy.color; //'phantomWhite'
prototype.recharge(); // 갤럭시가 충전을 시작합니다.

let arr = [ 'A', 'B', 'C' ];
arr.length; // 3
arr.push('course'); 새 element 추가 
// 배열과 비슷한 객체지향 Array 인스턴스

let arr = new Array[ 'A', 'B', 'C' ];
arr.length; // 3
arr.push('course'); 새 element 추가 
```