---
layout: post
title: React_State&Props
---
# React_State&Props

React를 사용할때 중요한 개념인 State와 props에 대한 공부를 과제와 함께했다.
리액트의 컴포넌트 간의 단방향 데이터 흐름의 핵심이라고 할 수 있는데, 

state는 현재 컴포넌트에서 생성, 변할 수 있는 데이터 라고 할수 있고
props는 상위 컴포넌트에서 상속받은 읽기전용의 객체 값으로 변하지 않는 값(상위 컴포넌트 값을 변경하지 못하게 하여side effect 방지를 위해)이라고 할수 있다.

이에 대해서 실습을 통해 알아보겠다.

```jsx
//index.js

import React from 'react'; // import로 react 받음
import ReactDOM from 'react-dom'; // import로 react-dom 받음(실행)
import App from './App'; //import로 app.js 파일의 정보 받음

import dummyTweets from './static/dummyData'; // 더미데이터를 받음

ReactDOM.render(
  <App dummyTweets={dummyTweets} />,
  document.getElementById('root')
); //react dom 으로 랜더링을 함
```

```jsx
//app.js

import React from 'react'; // import로 react 받음
import { BrowserRouter, Routes, Route } from 'react-router-dom';
// 리액트 돔의 BrowserRouter, Routes, Route 정보를 사용할수 있도록 선언

import Sidebar from './Sidebar';//import로 Sidebar.js 파일의 정보 받음
import Tweets from './Pages/Tweets';//import로 Tweets.js 파일의 정보 받음
import MyPage from './Pages/MyPage';//import로 MyPage.js 파일의 정보 받음
import About from './Pages/About';//import로 About.js 파일의 정보 받음

import './App.css'; //import로 App.css 파일의 정보 받음
import './global-style.css';//import로 global-style.css 파일의 정보 받음

const App = (props) => {
  return (
    <BrowserRouter> // 위에 선언한 리액트 돔을 태그를 이용해 사용
      <div className="App">
        <main>
          <Sidebar /> // 사이드 바를 앱의 하위 컴포넌트로 선언
          <section className="features">
            <Routes> // Routes 태그를 사용해 Route태그를 사용가능하게 묶음
              <Route path="/" element={<Tweets />}></Route>
              <Route path="/mypage" element={<MyPage />}></Route>
              <Route path="/about" element={<About />}></Route>
                    // Route path태그를 사용해 각 요소를 연결
            </Routes>
          </section>
        </main>
      </div>
    </BrowserRouter>
  );
};

// ! 아래 코드는 수정하지 않습니다.
export default App; // app 을 외부로 보냄
```

```jsx
//sidebar.js

import React from 'react'; // react 에서 정보 받음
import { Link } from 'react-router-dom'; // dom을 사용해 link를 사용할 준비

const Sidebar = () => {
  return (
    <section className="sidebar">
      <Link to="/"> // link to를 사용해 각 링크와 연결
        <i className="far fa-comment-dots"></i>
      </Link>
      <Link to="/about">
        <i className="far fa-question-circle"></i>
      </Link>
      <Link to="/mypage">
        <i className="far fa-user"></i>
      </Link>
    </section>
  );
};

export default Sidebar; // Sidebar 을 외부로 보냄
```

```jsx
//footer.js

import React from 'react'; // import로 react 받음

const Footer = () => {
  return (
    <footer>
      <img id="logo" src={`${process.env.PUBLIC_URL}/codestates-logo.png`} />
      Copyright @ 2022 Code States
    </footer>
  );
};

export default Footer; // Footer 를 외부로 보냄
```

```jsx
//about.js

import React from 'react'; // react 사용준비
import Footer from '../Footer'; //import로 Footer.js 파일의 정보 받음
import './About.css'; //import로 About.css 파일의 정보 받음

const About = (props) => {
  return (
    <section className="aboutTwittler">
      <div className="aboutTwittler__container">
        <div className="aboutTwittler__wrapper">
          <div className="aboutTwittler__detail">
            <p className="aboutTwittler__detailName">React Twittler Info</p>
          </div>
        </div>
      </div>
      <div className="aboutTwittler__content">
        <i className="fas fa-users"></i>
        <p>나만의 Twittler 소개페이지를 꾸며보세요.</p>
      </div>
      <Footer /> // Footer 를 About 컴포넌트의 하위 컴포넌트로 선언
    </section>
  );
};

export default About; // About 를 외부로 보냄
```

```jsx
//mypage.js

import React from 'react'; // react 사용준비
import Footer from '../Footer';//import로 Footer.js 파일의 정보 받음
import Tweet from '../Components/Tweet';//import로 Tweet.js 파일의 정보 받음
import './MyPage.css'; //import로 MyPage.css 파일의 정보 받음
import dummyTweets from '../static/dummyData'; //import로 dummyTweets 파일의 정보 받음

const MyPage = () => {
  const filteredTweets = dummyTweets.filter(
    (tweet) => tweet.username === 'parkhacker'
  ); // filter를 통해 원하는 정보만 추출하는 함수선언

  return (
    <section className="myInfo">
      <div className="myInfo__container">
        <div className="myInfo__wrapper">
          <div className="myInfo__profile">
            <img src={filteredTweets[0].picture} /> //추출된 정보 중 사진을 출력
          </div>
          <div className="myInfo__detail">
            <p className="myInfo__detailName">
              {filteredTweets[0].username} Profile // 추출된 정보중 이름을 출력
            </p>
            <p>28 팔로워 100 팔로잉</p>
          </div>
        </div>
      </div>
      <ul className="tweets__mypage">
        {filteredTweets.map((tweet) => {
          return <Tweet key={tweet.id} tweet={tweet} />;
        })} // map을 통해 추출한 정보를 전체 출력
      </ul>
      <Footer /> // Footer를 MyPage의 하위 컴포넌트로 선언
    </section>
  );
};

export default MyPage;// MyPage 를 외부로 보냄
```

```jsx
//Tweets.js
import React, { useState } from 'react'; // state를 조작하는 방법중 useState사용 준비
import Footer from '../Footer';//import로 Footer.js 파일의 정보 받음
import Tweet from '../Components/Tweet';//import로 Tweet.js 파일의 정보 받음
import './Tweets.css';//import로 Tweets.cs 파일의 정보 받음
import dummyTweets from '../static/dummyData'; //import로 Footer.js 파일의 정보 받음
import shortid from 'shortid';//import로 정보 받음???

const Tweets = () => {
  const [username, setUsername] = useState('parkhacker'); 
  const [msg, setMsg] = useState('');
  const [tweets, setTweets] = useState(dummyTweets);
  const [filteredTweets, setFilteredTweets] = useState(dummyTweets);
  const [isFiltered, setIsFiltered] = useState(false);
  const [currentUsername, setCurrentUsername] = useState('default');
  //구조분해 할당으로 useState 사용(state 변수 선언)

  const handleButtonClick = (event) => {
    const tweet = {
      id: shortid(),
      username: username,
      picture: 'https://randomuser.me/api/portraits/men/98.jpg',
      title: 'new Tweet',
      content: msg,
      createdAt: new Date().toLocaleDateString('ko-KR'),
      updatedAt: new Date().toLocaleDateString('ko-KR'),
    };
    const newTweets = [tweet, ...tweets];
    setTweets(newTweets);
  };// 버튼클릭으로 실행되는 함수

  const handleChangeUser = (event) => {
    setUsername(event.target.value)
  }

  const handleChangeMsg = (event) => {
    setMsg(event.target.value)
  }

  const handleFilterTweet = (event) => {
    if (event.target.value === 'default') {
      setTweets(tweets);
      setIsFiltered(false);
    } else {
      const filtered = tweets.filter(
        (tweet) => tweet.username === event.target.value
      );
      setIsFiltered(true);
      setFilteredTweets(filtered);
    }
    setCurrentUsername(event.target.value);
  }; 

  const handleDeleteTweet = (username, deleteIndex) => {
    if (isFiltered) {
      alert('필터 시 삭제 불가합니다.')
      return;
    }
    const restTweets = tweets.filter((tweet, idx) => idx !== deleteIndex);
    setTweets(restTweets);
  };

  const handleAllTweetButton = (event) => {
    setIsFiltered(false);
    // setTweets(tweets);
    setCurrentUsername('default');
  };

  const tweetsRenderer = (tweet, idx) => {
    return (
      <Tweet
        key={tweet.id}
        tweet={tweet}
        handleDeleteTweet={handleDeleteTweet}
        idx={idx}
      />
    );
  }

  return (
    <React.Fragment>
      <div className="tweetForm__container">
        <div className="tweetForm__wrapper">
          <div className="tweetForm__profile">
            <img src="https://randomuser.me/api/portraits/men/98.jpg" />
          </div>
          <div className="tweetForm__inputContainer">
            <div className="tweetForm__inputWrapper">
              <div className="tweetForm__input">
                <input
                  type="text"
                  value={username}
                  onChange={handleChangeUser}
                  placeholder="your username here.."
                  className="tweetForm__input--username"
                ></input>
                <textarea
                  value={msg}
                  onChange={handleChangeMsg}
                  placeholder="your tweet here.."
                  className="tweetForm__input--message"
                ></textarea>
              </div>
              <div className="tweetForm__count" role="status">
                <span className="tweetForm__count__text">
                  {'total: ' + tweets.length}
                </span>
              </div>
            </div>
            <div className="tweetForm__submit">
              <div className="tweetForm__submitIcon"></div>
              {/* TODO : 작성한 트윗을 전송할 수 있는 button 엘리먼트를 작성하세요. */}
              <button className="tweetForm__submitButton" onClick={handleButtonClick}>
                Tweet
              </button>//submit버튼 태그
            </div>
          </div>
        </div>
      </div>
      <div className="tweet__selectUser">
        <select value={currentUsername} onChange={handleFilterTweet}>
          <option value="default">
            -- click to filter tweets by username --// 아래 내용은 과제와 내용이 달라 확인필요
          </option>

          {tweets.reduce((acc, cur) => {
            const isNotUnique = acc.reduce((a, c) => {
              if (c.username === cur.username) {
                return true
              }
              return a === true ? true : false
            }, false)

            return isNotUnique ? acc : [...acc, cur]
            }, []).map((tweet) => {
            return (
              <option key={tweet.id} value={tweet.username}>
                {tweet.username}
              </option>
            );
          })}
        </select>
        {currentUsername !== 'default' ? (
          <button onClick={handleAllTweetButton}>
            <i className="far fa-caret-square-left"></i>
          </button>
        ) : (
          <div></div>
        )}
      </div>
      <ul className="tweets">
        {isFiltered ? filteredTweets.map(tweetsRenderer) : tweets.map(tweetsRenderer)}</ul>
      <Footer />
    </React.Fragment>
  );
};

export default Tweets;
```

```jsx
//tweet.js

import React from 'react';
import './Tweet.css';

const Tweet = ({ tweet, handleDeleteTweet, idx }) => {
  const parsedDate = new Date(tweet.createdAt).toLocaleDateString('ko-kr');
  // 날짜 데이터 정제
  return (
    <li className="tweet" id={tweet.id}>
      <div className="tweet__profile">
        <img src={tweet.picture} />
      </div>
      <div className="tweet__content">
        <div className="tweet__userInfo">
          <div className="tweet__userInfo--wrapper">
            <span className="tweet__username">{tweet.username}</span>
            <span className="tweet__createdAt">{parsedDate}</span>
          </div>
          <div className="tweet__userInfo--buttonWrapper">
            <button
              className="tweet__deleteButton"
              onClick={() => handleDeleteTweet(tweet.username, idx)}
            >
              <i className="far fa-trash-alt"></i>
            </button>
          </div>
        </div>
        <div className="tweet__message">{tweet.content}</div>
      </div>
    </li>
  );
};

export default Tweet;
```

이번 과제를 하면서 리액트는 HTML을 쉽게 만들어주면서 깊이들어가면 어렵다는 것을 느꼈다…