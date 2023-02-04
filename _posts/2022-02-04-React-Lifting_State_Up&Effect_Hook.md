---
layout: post
title:  React - Lifting State Up & Effect Hook
---

React State 끌어올리기와 Effect Hook을 과제를 통해 실습해봤다.

```jsx
// main.js
import Head from 'next/head';
import { useEffect, useState } from 'react';
import { getFlight } from '../api/FlightDataApi';
import FlightList from './component/FlightList';
import LoadingIndicator from './component/LoadingIndicator';
import Search from './component/Search';
import Debug from './component/Debug';
// 후반 테스트를 진행할 때 아래 import를 삭제합니다.
// import json from ('../resource/flightList');

export default function Main() {
  // 항공편 검색 조건을 담고 있는 상태
  const [condition, setCondition] = useState({
    departure: 'ICN',
  });
  const [flightList, setFlightList] = useState([]);
  const [isLoading, setIsLoading] = useState(true); // false 로 시작해도됨
  // 로딩 인디케이터는 인터넷에 이미 구현된 것 혹은 npm 라이브러리에서 다운받아 쓸수 있음

  // 주어진 검색 키워드에 따라 condition 상태를 변경시켜주는 함수
  const search = ({ departure, destination }) => {
    if (
      condition.departure !== departure ||
      condition.destination !== destination
    ) {
      console.log('condition 상태를 변경시킵니다');
      // TODO: search 함수가 전달 받아온 '항공편 검색 조건' 인자를 condition 상태에 적절하게 담아보세요.
      setCondition({
        departure : departure, // departure
        destination : destination //destination
      })
    }
  };

  // const filterByCondition = (flight) => {
  //   let pass = true;
  //   if (condition.departure) {
  //     pass = pass && flight.departure === condition.departure;
  //   }
  //   if (condition.destination) {
  //     pass = pass && flight.destination === condition.destination;
  //   }
  //   return pass;
  // };

  global.search = search; // 실행에는 전혀 지장이 없지만, 테스트를 위해 필요한 코드입니다. 이 코드는 지우지 마세요!

  // TODO: Effeck Hook을 이용해 AJAX 요청을 보내보세요.
  // TODO: 더불어, 네트워크 요청이 진행됨을 보여주는 로딩 컴포넌트(<LoadingIndicator/>)를 제공해보세요.
  useEffect(() => {
    setIsLoading(true); // 우선 로딩화면 보여주기
    getFlight(condition).then((filtered) => { //.then((data))도 가능
      setFlightList(filtered);
      setIsLoading(false); // 로딩끝난걸 보여주기
    });
  }, [condition]);

  // TODO: 테스트 케이스의 지시에 따라 search 함수를 Search 컴포넌트로 내려주세요.
  return (
    <div>
      <Head>
        <title>States Airline</title>
        <link rel="icon" href="/favicon.ico" />
      </Head>

      <main>
        <h1>여행가고 싶을 땐, States Airline</h1>
        <Search onSearch = {search} />
        <div className="table">
          <div className="row-header">
            <div className="col">출발</div>
            <div className="col">도착</div>
            <div className="col">출발 시각</div>
            <div className="col">도착 시각</div>
            <div className="col"></div>
          </div>
          {/* <FlightList list={flightList.filter(filterByCondition)} /> filter(filterByCondition)가 필요없는 이유는 정보를 바로 넣어주기 때문. */}
          {isLoading ? <LoadingIndicator /> : <FlightList list={flightList} />}
        </div>
//isLoading 은 삼항연산자로 useEffect 에서 나온 setIsLoading과 연결되어 로딩화면과 렌더링된 화면을 보여준다.

        <div className="debug-area">
          <Debug condition={condition} />
        </div>
        <img id="logo" alt="logo" src="codestates-logo.png" />
      </main>
    </div>
  );
}
```

```jsx
//Search.js

import { useState } from 'react';

function Search( {onSearch}) {
  const [textDestination, setTextDestination] = useState('');

  const handleChange = (e) => {
    setTextDestination(e.target.value.toUpperCase());
  };

  const handleKeyPress = (e) => {
    if (e.type === 'keypress' && e.code === 'Enter') {
      handleSearchClick();
    }
  };

  const handleSearchClick = () => {
    console.log('검색 버튼을 누르거나, 엔터를 치면 search 함수가 실행됩니다');

    // TODO: 지시에 따라 상위 컴포넌트에서 props를 받아서 실행시켜 보세요.
    onSearch({
      departure: "ICN",
      destination : textDestination,
    });
  };

  return (
    <fieldset>
      <legend>공항 코드를 입력하고, 검색하세요</legend>
      <span>출발지</span>
      <input id="input-departure" type="text" disabled value="ICN"></input>
      <span>도착지</span>
      <input
        id="input-destination"
        type="text"
        value={textDestination}
        onChange={handleChange}
        placeholder="CJU, BKK, PUS 중 하나를 입력하세요"
        onKeyPress={handleKeyPress}
      />
      <button id="search-btn" onClick={handleSearchClick}> 
        검색
      </button>
    </fieldset>
  );
}

export default Search;
```

```jsx
//flightDataApi.js

import flightList from '../resource/flightList';
import fetch from 'node-fetch';

//브라우저가 정상적으로 렌더링 되었을때
if (typeof window !== 'undefined') { // 로커ㄹ스토리지에 flight라는 프로퍼티명으로 JSON.stringigy(flightList)저장
  localStorage.setItem('flight', JSON.stringify(flightList));
}

// export function getFlight(filterBy = {}) {
//   // HINT: 가장 마지막 테스트를 통과하기 위해, fetch를 이용합니다. 아래 구현은 완전히 삭제되어도 상관없습니다.
//   // TODO: 아래 구현을 REST API 호출로 대체하세요.

//   let json = [];
//   if (typeof window !== 'undefined') {
//  // 로컬 스토리지에 있는 'flight'프로퍼팅 안에있는걸 가져오겠다
//     json = localStorage.getItem('flight');
//   }
//   const flight = JSON.parse(json) || []; // JSON을 객체로 반환.

//   return new Promise((resolve) => {
//     const filtered = flight.filter((flight) => {
//       let condition = true;
//       if (filterBy.departure) {
//         condition = condition && flight.departure === filterBy.departure;
//       }
//       if (filterBy.destination) {
//         condition = condition && flight.destination === filterBy.destination;
//       }
//       return condition;
//     });
// //의도적인 delay
//     setTimeout(() => {
//       resolve(filtered);
//     }, 500);
//   });
// }

export function getFlight(filterBy = {}) {
  let queryString = '';
  if (filterBy.departure) {
    queryString = queryString + `departure=${filterBy.departure}&`;
    //queryString = '?departure`;
  }
  if (filterBy.destination) {
    queryString = queryString + `destination=${filterBy.destination}`;
  }
  let endpoint = `http://ec2-13-124-90-231.ap-northeast-2.compute.amazonaws.com:81/flight?${queryString}`;
  return fetch(endpoint).then((resp) => resp.json());
  // return fetch(`http://ec2-13-124-90-231.ap-northeast-2.compute.amazonaws.com:81/flight?${queryString}').then((res)=> res.json)
}
```

본격적으로 리액트를 사용해봤다.
API를 받아오고 상태를 변경시키는 중요 리액트 개념을 실습해봐서 다른 것도 해보고 싶어졌다.