---
layout: post
title: Firefly - BeesBeesBees
---

# Firefly - BeesBeesBees

이번 과제는 ****BeesBeesBees이다.
아직 이해가 부족한 prototype과 클래스, 상속에 관해서 재미있게 이해할 수 있었던 과제이다.****

grub (유충) → bee(그냥 벌) → forager bee (일벌 중식량 징발자벌?) → honey maker bee(일벌중 꿀생산하는 벌) 로 4단계 동안 상속에 대해 실습을 해보는 것이다.
단순히 글과 함께 이론으로 보는 것으로는 전혀 이해가 되지 않았는 데, 과제를 통해 대략적인 프로토 타입을 체득할수 있었다.

```jsx
class Grub { //유충
  // TODO..

  constructor( age, color, food ){
    //this는 인스턴스를 의미
    this.age = 0;
    this.color = 'pink';
    this.food = 'jelly';
  }
  
  eat(){
    return `Mmmmmmmmm ${this.food}`
  }
  // 함수는 this를 사용하지 않아도 됨.
  
}
// es5 에서는
// Grub.prototype functtion eat() .... 
module.exports = Grub; // 모듈에 대해 깊은 탐색이 필요
```

우선 유충을 상위 클래스로 만들어 주고 상속될 요소를 constructor를 통해 지정해준다.

```jsx
const Grub = require('./Grub'); // 해당 문법에 대한 확인 필요

class Bee extends Grub{
  constructor(age, color, food, job){
   super(food)//this보다 위에 있어야 참조오류가 생기지 않음. super()로도 사용 가능, 
  this.age = 5; // 덮어쓰기 해주는 과정
  this.color = 'yellow';
  this.job = 'Keep on growing';
  }
}

module.exports = Bee;
```

extends - super 문법으로 요소들이 상속될 수 있도록 한다.

```jsx
const Bee = require('./Bee');

class ForagerBee extends Bee{
  // TODO..
  constructor(age, job, color, food, canFly, treasureChest){
    super(color, food) // super() 로 사용가능
    this.age = 10;
    this.job = 'find pollen';
    this.canFly = true;
    this.treasureChest = [];
  }

  forage(str){
    if(str === 'pollen'){
      return this.treasureChest.push('pollen');
    }else if(str === 'flowers'){
      return this.treasureChest.push('flowers');
    }else if(str === 'gold'){
      return this.treasureChest.push('gold');
    }
    //this.treasureChest.push(str) -- return을 붙이면 안됨
  }
}

module.exports = ForagerBee;
```

 push, pop, shift, unshift 에 경우 return 과 함께 사용하면 의도와 다른값이 나오므로 주의를 해야한다.

//어째서인지 확인해야 함.

```jsx
const Bee = require('./Bee');

class HoneyMakerBee extends Bee{
  // TODO..
  constructor(age, job, color, food, honeyPot){
    super(color, food) // super()도 가능
    this.age = 10;
    this.job = 'make honey';
    this.honeyPot = 0;
  }
  makeHoney(){
    return this.honeyPot += 1;
  }
  giveHoney(){
    return this.honeyPot -= 1;
  }
}
```

확실히 return 을 사용하고 this.honeyPot++ 를 사용하니 제대로 작동이 잘 되지 않았다. 

이번 과제를 통해 프로토 타입에 대한 이해도를 높일 수 있었지만 다른 예제들과 문법적인 부분을 다시 살펴봐야 할것 같다.