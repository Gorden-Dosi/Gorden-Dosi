---
layout: post
title: Javascript deepdive 스터디 Chapter 7.
---

모던 자바스크립트 Deep Dive
자바스크립트의 기본 개념과 동작 원리

7장 연산자
1. 산술 연산자
2. 할당 연산자
3. 비교 연산자
4. 삼항 조건 연산자
5. 논리 연산자
6. 쉼표 연산자
7. 그룹 연산자
8. typeof 연산자
9. 지수 연산자
10. 그 외의 연산자
11. 연산자의 부수효과
12. 연산자의 우선순위
13. 연산자의 결합순서


연산자의 정의
연산자(operator)는 하나 이상의 표현식을 대상으로 산술, 할당, 비교, 논리, 타입, 지수 연산(operation) 등을 수행해 하나의 값을 만든다. 이때 연산의 대상을 피연산자(operand)라 한다. 피연산자는 값으로 평가될 수 있는 표현식
이어야 한다. 그리고 피연산자와 연산자의 조합으로 이뤄진 연산자 표현식도 값으로 평가될 수 있는 표현식
이다.
예)
산술 연산자
5 * 4 // - 20
// 문자열 연결 연산자
'My name is + 'Lee' // - 'My name is Lee'
17 할당 연산자
color = 'red' // - 'red'
11 비교 연산자
3 > 5 // - false
// 논리 연산자
true && false // - false
// 타입 연산자
typeof 'Hi' // string

1. 산술 연산자
1)이항 산술 연산자 - 두개의 값을 연산, (피연산자의 값을 변경하는) 부수효과는 없다. ( +,-,*,/,%)
2)단항 산술 연산자 - 하나의 피연산자를 산술연산
 부수효과 O - > ++, —
 부수효과 X -> -(피연산자), +(피연산자)
3) 문자 연결 연산자 - 하나 이상의 피연산자가 문자열인 경우 문자끼리 연결하는 연산자로 동작
 예외 ) 불리언 타입의경우 압묵적 타입 변환으로 false = 0, true = 1로 변환하여 연산


2. 할당 연산자
할당 연산자(assignment operator)는 우항에 있는 피연산자의 평가 결과를 좌항에 있는 변수에 할당한다.

= ,   += ,   -=,     *=,    /=,     %=  
var x;
x = 10;
console.log(x); // 10
x += 5; // x = x + 5;
console.log(x); // 15
x -= 5; // x = x - 5;
console.log(x); // 10
x *= 5; // x = x * 5;
console.log(x); // 50
x /= 5; // x = x / 5;
console.log(x); // 10
x %= 5; // x = x % 5;
console.log(x); // 0
var str = 'My name is ‘;

// 문자열 연결 연산자
str += 'Lee'; // str = str + 'Lee';
console.log(str); // 'My name is Lee’

할당문은 값으로 평가되는 표현식의 문으로서 할당된 값으로 평가된다.

3. 비교 연산자.
동등/ 일치 비교 연산자

  비교 연산자는 ==,===,!=, !== 가 있으며 부수 효과는 없고 예제는 다음과 같다.

==  / 동등 비교(느슨) / x == y  / x와 y의 값이 같음.
=== / 일치 비교 (엄격) / x === y / x와 y의 값과 타입이 같음
!= / 부동등 비교(느슨) / x != y  / x와 y의 값이 다름.
!== / 불일치 비교(엄격)  / x !== y / x와 y의 값과 타입이 다름

NaN의 경우 예외로
NaN === NaN; // false  의 값이 나오므로 주의가 필요하다.

2) 대소 관계비교  연산자
>, <. >=, <=

4. 삼항 조건 연산자
삼항 조건 연산자는 첫 번째 피연산자가 true로 평가되면 두 번째 피연산자를 반환하고, 첫 번째 피연산자가
false로 평가되면 세 번째 피연산자를 반환한다. 즉, 삼항 조건 연산자는 두 번째 피연산자 또는 세 번째 피
연산자로 평가되는 표현식이다.
예)
var x = 2
// 2 % 2는 이고 좋은 false로 암묵적 타입 변환된다.
var result = x % 2 ? '홀수' : '짝수';
console.log(result); // 짝수
( 이해도가 부족해 추후 내용 추가 예정)

5. 논리연산자
|| - 논리합(OR)
&& - 논리곱(AND)
! - 부정(NOT)

6. 쉽표연산자. (추가예정)

7. 그룹연산자
괄호로 싸인 부분부분부터 연산. 연산자 우선순위가 가장 높다.

 10 * 2 + 3 // -> 23
 10 * ( 2 + 3 ) // -> 50


8. typeof 연산자
7가지 문자열 “ string”, “number”, “boolean”, “undefined”, “symbol”, “object”, “function”  중 하나를 반환한다
null 은 반환하지 않고 “object”로 반환하며 === 일치 연산자로 확인하는 것이 좋다. 7개 타입 데이터는 정확히 일치하지 않는다.
선언하지 않은 식별자는 referenceError가 발생하지 않고 undefined를 반환한다.

9. 지수 연산자.
ES7에서 도입된 지수 연산자는 좌항의 피연산자를 base로, 우항의 피연한자를 지수(pxponent)로 거듭제곱하여 숫자값을 반환한다.
2 ** 2; // 4
지수 연산자가 도입되기 이전에는
math.pow(2,2); // 4 를 사용했다.
음의 제곱을 계산하려면 괄호로 base를 묶어야한다.

10. 그 외의 연산자
추후 등장 예정인 연산자
?.   ///   옵셔널 체이닝 연산자
??  ///   null 병합 연산자
delete ///   프로퍼티 삭제
new   ///   생성자함수를 호출할 때 사용하여 인스턴스를 생성
instanceof    ///   좌변의 객체가 우변의 생성자함수와 연결된 인스턴스인지 판별
in  ///   프로퍼티 존재 확인


11. 연산자의 부수효과
보통 다른 코드에 영향을 주지 않고 새로운 값을 생성하지만.
할당 연산자(=), 증가/감소 연산자(++/--), delete 연산자는 부수 효과가 있다.

var x;
// 할당 연산자는 변수 값이 변하는 부수 효과가 있다. 이는 X 변수를 사용하는 다른 코드에 영향을 준다.
x = 1;
console.log(x); // 1
11 증가/감소 연산자(++/-)는 피연산자의 값을 변경하는 부수 효과가 있다.
// 피연산자 x의 값이 재할당되어 변경된다. 이는 X 변수를 사용하는 다른 코드에 영향을 준다.
x++;

12. 연산자 순위

1  //  ()
2 // new(매개변수 존재... [] (프로퍼티 접근) () 함수 호출), ?. (옵셔널 체이닝 연산자)
3 // new(매개변수 미존재)
4 // X++, X—
5 // !X, +X, -X, ++x, --x, typeof, delete
6 // **(이항 연산자 중에서 우선순위가 가장 높다)
7 // *, /, %
8 // +, -
9 // <, <=, >, >=, in, instanceof
10 // ==, ! =,===, !==
11 // ??(null 병합 연산자 )
12 //  &&
13 //  ||
14 // ? ... : …
15 // 할당 연산자(=+=, −=...)
16// ,


13. 연산자 결합순서
결합 순서
좌항→ 우항 // +, -, /, %, <, <=, >, >=, &&, ||, .. [], (), ??, ?.. in, instanceof
우항 → 좌항 // ++, -- 할당 연산자(=+= −=...…), X, +x, −x, ++X, −−x, typeof, delete, ? ... : ..….

이번 장도 역시 암기를 해야 할 듯합니다.
일부 부분은 필요할 때마다 참고를 할수 있도록 하는 것도 필요하다고 합니다.

2022.12.27