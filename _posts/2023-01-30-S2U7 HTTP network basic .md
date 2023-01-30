---
layout: post
title: S2U7 HTTP/ network basic
---

HTTP 와 네트워크의 기초

— Client Server Architecture === 2 tier Architecture
Client ←→ Server

— 3 tier Architecture
Client ←→ Server ←→ Data Base

**오늘 공부할 내용은 2 tier Architecture 이다.**

HTTP - **H**yper**T**ex**T** **P**rotocol >> Protocol → 서버와의 통신을 위한 규약

이를 통해 통신을 한다면 HTTP Message를 주고 받게 되고, 이를 통해 API(Application Programming Interface 의사소통을 위한 내용)가 포함되어 있는 내용이 오고 갑니다.

HTTP 요청 메서드
[https://developer.mozilla.org/ko/docs/Web/HTTP/Methods](https://developer.mozilla.org/ko/docs/Web/HTTP/Methods)

참고 - OSI 7 Layers

**URL과 URI**

URI → Uniform Resource Identifier
scheme, hosts, url-path 로 이루어짐
[https://www.google.com/webhp](https://www.google.com/webhp)

URL → Uniform Resource Locator
scheme, hosts, url-path ++ query, fragment

[https://www.google.com/search?q=uri&sxsrf=AJOq](https://www.google.com/search?q=uri&sxsrf=AJOqlzVYh7oOQONRvRj5yANIjs8XYiNQ7g%3A1675080351818&source=hp&ei=n7LXY7rrLsqQhwPunbOoDA&iflsig=AK50M_UAAAAAY9fAr5--AxDvyQIaIfUHWtB2ypXMqVhd&ved=0ahUKEwj6ttnKoO_8AhVKyGEKHe7ODMUQ4dUDCAk&uact=5&oq=uri&gs_lcp=Cgdnd3Mtd2l6EAMyBwgjECcQnQIyBAgAEEMyBwguENQCEEMyBAgAEEMyBAgAEEMyBAgAEEMyCggAEIAEEBQQhwIyBQgAEIAE)…..

URI은 URL보다 많은 요소를 가지고 있는 상위  개념이다.

scheme : 통신 프로토콜 지정 `http` 또는 `https` 등
host : 웹 페이지, 이미지, 동영상 등의 파일이 위치한 웹 서버, 도메인 또는 IP // `www.google.com`
port : 대상(서버)에 접근하기 위한 통로 // `:80, :443`
url-path : 접근할 대상(서버)의 경로에 대한 상세 정보, 웹 서버의 루트 디렉토리로부터 웹 페이지, 이미지, 동영상 등의 파일이 위치까지의 경로[https://www.google.com/`doodles/national-liberation-day-of-korea-2022`](https://www.google.com/doodles/national-liberation-day-of-korea-2022)
query : 접근할 대상에 전달하는 추가적인 정보 (파라미터) // 웹 서버에 전달하는 추가 질문 //`q=JavaScript`
fragment : 메인 리소스 내에 존재하는 서브 리소스에 접근할 때 이를 식별하기 위한 정보

DNS - Domain name system

HTTP Messages

요청(Requests)과 응답(Responses) 두 가지 유형이 있음

HTTP Messages는 두 가지로 나뉘나 구조는 유사하다

start line / status line : start line에는 요청이나 응답의 상태를 나타냅니다. 항상 첫 번째 줄에 위치
응답에서는 status line이라고 부릅니다.
HTTP headers : 요청을 지정하거나, 메시지에 포함된 본문을 설명하는 헤더의 집합
empty line : 헤더와 본문을 구분하는 빈 줄
body : 요청과 관련된 데이터나 응답과 관련된 데이터 또는 문서를 포함합니다. 요청과 응답의 유형에 따라 선택적으로 사용
start line과 HTTP headers를 묶어 요청이나 응답의 헤드(head)라고 하고, [payload](https://ko.wikipedia.org/wiki/%ED%8E%98%EC%9D%B4%EB%A1%9C%EB%93%9C_(%EC%BB%B4%ED%93%A8%ED%8C%85))는 body라고 칭한다.

****Stateless // 무상태성은 HTTP의 큰 특징. 이전에 한 작업을 기억(저장)하지 못하기 때문에 쿠키 혹은 세션을 이용해 이전 자료를 기억****

**AJAX** - **A**synchronous **J**avaScript **A**nd **X**MLHttpRequest

이전 웹페이지는 **X**MLHttpRequest만을 사용해 전체 페이지를 다시 불러오는 방식으로 정보를 가져옴.
그러나 AJAX를 이용해 SPA(Fetch 등을 사용)을 만들어 필요한 부분만 새로고침이 가능해졌다.

AJAX의 장점

- 서버에서 HTML을 완성하여 보내주지 않아도 일부 웹페이지만을 업데이트하고 렌더링을 할수 있다.
- 이전에는 브라우저마다 다른 방식으로 AJAX를 사용했으나, XHR이 표준화되면서부터 브라우저에 상관없이 AJAX 사용가능
- AJAX를 사용하면 필요한 일부분만 렌더링하기 때문에 빠르고 더 많은 상호작용이 가능한 애플리케이션을 만들 수 있습니다.
- 더 작은 대역폭(네트워크 통신 한 번에 보낼 수 있는 데이터의 크기)
- 이전에는 서버로부터 완성된 HTML 파일을 받아와 렌더링을 했기에 한 번에 보내야 하는 데이터의 크기가 컸지만 AJAX는 필요한 데이터를 텍스트 형태(JSON, XML 등)로 보내면 되기 때문에 비교적 데이터의 크기가 작다.

AJAX의 단점

- Search Engine Optimization(SEO)에 불리
    
    AJAX 방식의 웹 애플리케이션은 한 번 받은 HTML을 렌더링 한 후, 서버에서 비동기적으로 필요한 데이터를 가져와 렌더링을 하는데 검색 엔진 프로그램의 경우 HTML파일만을 보고 데이터 크롤링을 하기 때문에 검색엔진에 정보를 가져가기 어렵다.
    
- 뒤로가기 버튼 문제
    
    AJAX는 ****Stateless하기때문에**** 뒤로가기 등의 기능을 구현하기 위해서는 별도로 History API를 사용해야 한다.
    
    SSR(Server Side Rendering) - 서버에서 렌더링해서 클라이언트에게 제공
    
    CSR(Client Side Rendering) - 서버에서 정보만 다운로드해서 클라이언트(브라우저)에서 렌더링
    
    SSR 장점 - SEO에 유리, TTV - time to view가 짧다.
    SEO은 HTML 우선이기 때문에 이미 랜더링된 HTML을 보내줄수 있어 좋다.
    자바스크립트(상호작용)보다 글을 우선 랜더링할수 있어서 신문과 같이 바로 출력할수 있을 때 좋다.
    SSR 단점 - 자바스크립트를 나중에 받기 때문에 빠른소통은 어렵다.
    CSR - 자바스크립트를 포함한 모든자료 한 번 에 다운
    CSR 장점 - TTI - time to interaction와 TTV의 간극이 짧다. - 자바 스크립트를 우선 받기 때문에 빠른 상호작용이 가능하다.
    CSR 단점 - 자바스크립트 파일이 크다면 로딩시간이 길다.
    첫 페이지를 보여주는 데 늦음 그래서 코드 스플리팅(필요한 자바스크립트만 받아옴)
    
    기초 부분이기 때문에 가벼운 이론과 용어 정리가 많은 수업이었다.