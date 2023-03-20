---
layout: post
title: react 번들링과 웹팩
---

react  webpack의 번들링은 많은 양의 파일을 묶어줌으로서  활용성 높은 웹의 사용성과  웹 응용프로그램의 파일 용량을 줄이기 위해 사용되는 기술이다.
이를 통해 빠른 로딩 속도와 높은 성능을 기대할 수 있다.
아래는 웹팩에 대한 설명이다.

---

Webpack이란 여러 개의 파일을 하나의 파일로 합쳐주는 모듈 번들러를 의미합니다. 모듈 번들러란 HTML, CSS, JavaScript 등의 자원을 전부 각각의 모듈로 보고 이를 조합해 하나의 묶음으로 번들링(빌드)하는 도구입니다.

---

웹 팩은 밑의 항목들로 구성을 하고 사용한다.

- Entry
- Output
- Loaders
- Plugins
- Mode
- Browser Compatibility

## **Target**

Webpack은 다양한 환경과 target을 컴파일합니다. target의 기본값은 web입니다. 적용하지 않으면 이 기본 값으로 적용됩니다. 이 부분에는 web 외에도 다양한 환경을 컴파일 할 수 있는데, esX를 넣으면 지정된 ECMAScript 버전으로 컴파일할 수 있습니다.

## **Entry(엔트리)**

일반적인 문맥에서 entry의 뜻은 “입구"입니다. 박물관 입구, 놀이동산 입구등의 문맥에서 사용되는 영어 단어입니다. webpack에서의 entry는 프론트엔드 개발자가 작성한 코드의 “시작점"으로 이해하면 편합니다. React도 index.js에서 HTML 엘리먼트 하나에 React 코드를 적용하는 것 부터 시작합니다. (실제 webpack을 사용하기도 했습니다.)

Entry 속성은 Entry point라고도 하며, webpack이 내부의 디펜던시 그래프를 생성하기 위해 사용해야 하는 모듈입니다. Webpack은 이 Entry point를 기반으로 직간접적으로 의존하는 다른 모듈과 라이브러리를 찾아낼 수 있습니다.

## **Output(출력)**

Output 속성은 생성된 번들을 내보낼 위치와 이 파일의 이름을 지정하는 방법을 webpack에 알려주는 역할을 합니다.

## **Loader(로더)**

Webpack은 기본적으로 JavaScript와 JSON 파일만 이해합니다. 그러나 loader를 사용하면 Webpack이 다른 유형의 파일을 처리하거나, 그들을 유효한 모듈로 변환해 애플리케이션에 사용하거나 디펜던시 그래프에 추가할 수 있습니다.

## **Plugins(플러그인)**

Plugins를 사용하면 번들을 최적화하거나 에셋을 관리하고, 또는 환경변수 주입 등의 광범위한 작업을 수행할 수 있게 됩니다.

## **Optimization(최적화)**

Webpack은 버전 4부터는 선택한 항목에 따라 최적화를 실행합니다.

최적화하기 위해 다양한 옵션이 지원이 되는데, 대표적으로 `minimize`와 `minimizer` 등을 사용합니다.

- minimize : `TerserPlugin` 또는 `optimization.minimize`에 명시된 plugins로 bundle 파일을 최소화(=압축)시키는 작업 여부를 결정
- minimizer : `defualt minimizer`을 커스텀된 `TerserPlugin` 인스턴스를 제공해서 재정의할 수 있습니다.