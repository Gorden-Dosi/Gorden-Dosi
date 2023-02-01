---
layout: post
title:  REST API 실습
---

이론을 바탕으로 Postman 을 사용하여 오픈된 API와 Key를 가져와 실습.

[https://web.postman.co/](https://web.postman.co/)

postman은 REST API 설계 개발, 테스팅을 할 수 있는 GUI 툴.

이전에 학습했던

GET, POST, PUT, DELETE를 사용해 실습.

root - endpoint 자리를 입력하고 postman 을 통해 응답이 오는가를 보는 간단한 과제.

github를 예로 
`root`는 [https://api.github.com](https://api.github.com/)
`endpoint`는 /{githubID}/messages

Get 메서드를 사용하다면 Get 사용 후 [https://api.github.com](https://api.github.com/)/{githubID}/messages 처럼 REST API의 양식에 맞추어 불러오고, 
POST 메서드를 사용한다면 같은 방식으로 POST사용 후 URI를 지정하고 [https://api.github.com](https://api.github.com/)/{githubID}/messages JSON 방식으로 RAW에 입력을 한다.

너무 짧아보이지만 반응한다는 것을 볼수있고 API와 key를 사용해볼수있는 실습이었다.