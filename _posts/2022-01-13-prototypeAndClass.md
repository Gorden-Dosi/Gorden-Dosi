---
layout: post
title: Prototype과 class
---
# Prototype과 class

JavaScript는 프로토타입(Prototype == 원형 객체原型客體 원래 모형을 유지한 객체) 기반 언어
prototype은 자신을 만들어낸 객체의 원형
[https://developer.mozilla.org/ko/docs/Learn/JavaScript/Objects/Object_prototypes](https://developer.mozilla.org/ko/docs/Learn/JavaScript/Objects/Object_prototypes)

[https://developer.mozilla.org/ko/docs/Learn/JavaScript/Objects/Classes_in_JavaScript#ecmascript_2015_클래스](https://developer.mozilla.org/ko/docs/Learn/JavaScript/Objects/Classes_in_JavaScript#ecmascript_2015_%ED%81%B4%EB%9E%98%EC%8A%A4)

****Array(배열) 클래스와 인스턴스, 그리고 프로토타입의 관계****

![스크린샷 2023-01-13 오후 3.00.28.png](Prototype%E1%84%80%E1%85%AA%20class%2055685a0bf86c48d6a35f2e2f470d665b/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-01-13_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_3.00.28.png)

prototype: 내가 원형일 때 존재함.
-함수 객체만 가지고 있다.
-생성자를 가지는 원형으로 선언 가능

__**proto__** : 나의 원형을 가리킴

모든 객체가 가지고 있다.
하나의 링크라고 할 수 있다.

— 이러한 prototype 프로퍼티를 통해 생성자 함수는 인스턴스에게 프로토타입 객체에 있는 
  데이터, 메소드를 상속한다. (인스턴스는 사용 가능하다.)
— 인스턴스 객체의 key에 접근할 때, 해당 객체에게 key가 없다면 그 다음으로 
  상위 프로토타입 속성에서 key가 있는지 확인한다.
— 없다면 그것을 찾기 위해 더 상위의 프로토타입(부모)에서 찾는다. 이것을 프로토타입 체인이라고 한다.

#프로토 타입에 대해서는 더 많은 이해가 필요해 내용 추가 예정입니다.