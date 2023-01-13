# javascript-fronf-end-dev2

\*6-3-20. 선택 레슨: react-helmet으로 페이지 제목 설정하기
우리가 만든 프로젝트에서 한 가지 아쉬운 점이 있다면

각 페이지에 들어갔을 때 페이지 제목이 바뀌지 않는다는 건데요.

아래 스크린샷들에서 주소창 위에 제목이 보이시나요?

홈페이지

카탈로그 페이지

페이지를 이동하더라도 제목이 “Codethat”으로 그대로 유지되고 있습니다.

이 제목은 public 폴더의 index.html 파일에 있는 <title> 태그에 지정된 건데요.

개발자 도구를 열어서 보면 보이는 HTML 코드에서 head 태그 안에 있는 title 태그가 바로 그것이죠.

<html lang="ko">
  <head>
    <meta charset="utf-8" />
    <title>Codethat</title>
    ...
  </head>
  <body>
    <div id="root" class="container">
      ...
    </div>
    <script src="/static/js/bundle.js"></script>
    <script src="/static/js/vendors~main.chunk.js"></script>
    <script src="/static/js/main.chunk.js"></script>
  </body>
</html>
자바스크립트로 페이지 제목을 바꾸려면 아래처럼 document.title 값을 수정하면 됩니다.

document.title = 'Codethat - 커뮤니티';
그런데 이 코드의 문제점은 페이지 제목이 어떻게 바뀌는지 알려면,

관련된 코드를 차례대로 읽어봐야 한다는 단점이 있죠. 눈에 잘 띄지도 않고요.

이것보다 좀 더 편리하게 리액트스러운 방법으로 제목을 바꿀 수 있는 방법이 있습니다.

바로 react-helmet 이라는 라이브러리를 사용하는 건데요.

import { Helmet } from 'react-helmet';
import Button from '../components/Button';
import Container from '../components/Container';
import Lined from '../components/Lined';
import styles from './HomePage.module.css';
import landingImg from '../assets/landing.svg';

function HomePage() {
return (
<>
<Helmet>

<title>Codethat - 코딩이 처음이라면, 코드댓</title>
</Helmet>
<div className={styles.bg} />
<Container className={styles.container}>
<div className={styles.texts}>
<h1 className={styles.heading}>
<Lined>코딩이 처음이라면,</Lined>
<br />
<strong>코드댓</strong>
</h1>
<p className={styles.description}>
11만 명이 넘는 비전공자, 코딩 입문자가 코드댓 무제한 멤버십을
선택했어요.
<br />
지금 함께 시작해보실래요?
</p>
<div>
<Button>지금 시작하기</Button>
</div>
</div>
<div className={styles.figure}>
<img src={landingImg} alt="그래프, 모니터, 윈도우, 자물쇠, 키보드" />
</div>
</Container>
</>
);
}

export default HomePage;
사용법은 정말 간단합니다.

예를 들면 위 코드처럼 Helmet 이라는 컴포넌트로 감싼 다음에,

안에다가 <title> 태그를 배치하면 이 컴포넌트가 렌더링 될 때

HTML의 <title> 태그를 덮어쓸 수 있습니다.

이름이 헬멧인 이유는 <head> 태그에 덮어쓰기 때문이죠 😆.

관심있으신 분들은 아래 사이트를 방문해서 사용법을 참고해서 적용해보면 좋을 것 같습니다!

react-helmet - npm

\*6-3-21. 싱글 페이지 애플리케이션(SPA) 이해하기

\*클라이언트 사이드 렌더링(CSR): 웹브라우저에서 자바스크립트로 웹 페이지를 만드는 것
클라이언트: 웹 브라우저
렌더링: HTML 페이지를 만드는 것

\*싱글 페이지 애플리케이션(SPA):하나의 HTML 문서안에서 자바스크립트로 여러 페이지를 보여주는 사이트

싱글 페이지: 하나의 HTML 문서
애플리케이션: 여러 페이지를 보여주는 사이트

\*6-3-22. 리액트를 렌더링하는 방식
앞에서 우리는 클라이언트사이드 렌더링에 대해 배워봤습니다. 클라이언트 사이드 렌더링이란 웹 브라우저에서 자바스크립트로 HTML을 만들고, 이걸로 화면을 보여주는 거였는데요. 이걸 꼭 웹 브라우저에서 할 필요는 없습니다.

리액트 팀에서는 렌더링을 자유롭게 할 수 있도록 리액트를 개발했는데요. 리퀘스트를 받으면 서버가 렌더링 해서 리스폰스로 보내줄 수도 있고, 아예 미리 HTML 파일로 만들어 두었다가 리스폰스로 보내줄 수도 있는데요. 심지어는 리액트 코드를 HTML이 아니라 모바일 애플리케이션의 화면을 렌더링 하는 데 사용할 수도 있습니다.

이번 노트에서는 어떤 방식의 렌더링이 있는지 살펴볼 건데요. 이 개념들은 꼭 리액트에서만 사용하는 건 아니니까 알아두시면 두고두고 유용할 겁니다. 그리고 이런 렌더링을 활용한 리액트 기술 세 가지를 소개해드릴게요. 많은 개발자들이 실제 프로덕트를 개발하는 데 사용하는 기술들이니까, 앞으로 리액트를 공부하는데 참고하시면 좋을 것 같습니다.

대표적인 렌더링의 종류
클라이언트사이드 렌더링(Client-side Rendering)
— 웹 브라우저에서 자바스크립트로 HTML을 만드는 것

리액트로 할 수 있는 가장 기본적인 방식의 렌더링입니다. 리액트로 작성한 코드는 자바스크립트로 변환이 가능한데요. 참고로 이런 변환을 트랜스파일링이라고 부릅니다. 관련된 내용을 다시 보고 싶으시다면 "React 웹 개발 시작하기 - 브라우저는 어떻게 리액트를 알아들을까?" 를 참고해주세요.

클라이언트사이드 렌더링은 자바스크립트로 변환된 리액트 코드를 웹 브라우저에서 실행해서 HTML을 만드는 걸 말합니다.

서버사이드 렌더링(Server-side Rendering)
— 서버에서 HTML을 만들고 리스폰스로 보내주는 것

백엔드 서버에서 리퀘스트를 받으면 상황에 맞는 HTML을 만들어서 리스폰스로 보내주는 방식을 '서버사이드 렌더링'이라고 합니다. 서버에서 HTML을 만든다는 뜻이죠.

이번 토픽에서는 배우지 않지만, 리액트에서도 서버사이드 렌더링을 할 수 있는 기능들을 제공합니다. 이렇게 하면 이미 렌더링 된 것이 웹 브라우저에 도착하니까 훨씬 빨리 화면을 띄워줄 수 있고,검색 엔진에서 좋은 점수를 받아서 검색했을 때 사이트가 잘 노출될 수 있다는 장점이 있습니다.

이런 내용들은 나중에 자세히 살펴볼 기회가 있을 테니까, 여기서는 '서버에서 HTML을 만들어서 보내준다'는 것만 확실히 알고 넘어갑시다.

정적 사이트 생성(Static Site Generation)
— 미리 HTML 파일을 만들어서 서버를 배포하는 것

서버에서 렌더링 하는 것도 좋지만, 데이터가 거의 바뀌지 않는다면 매번 새로 만드는 건 낭비가 아닐까요? 그래서 미리 HTML 파일로 만들고 이걸 서버를 배포하는 방법을 사용하는데, 이런 방식을 '정적 사이트 생성'이라고 합니다. 서버에서는 리퀘스트가 들어오면 HTML 파일을 읽어서 리스폰스로 보내주는 건데요.

'정적 사이트 생성'에서 정적이라는 말의 의미는 HTML을 파일로 만든다는 겁니다. 개발자가 새로 배포하지 않는다면 서버에서 보내주는 HTML이 달라지지 않는다는 의미죠. 용어가 생소해 보이지만, 쉽게 생각해서 리액트 코드로 HTML 파일을 만든다고 생각하면 됩니다.

물론 자바스크립트를 쓸 수 있기 때문에 정적으로 생성된 사이트에서도 동적인 데이터를 가져와 페이지를 보여줄 수 있답니다.

렌더링을 활용한 리액트 기술 세 가지
Next.js
— 리액트 서버사이드 렌더링을 편하게

Nextjs Example

Next.js 기본 예제 프로젝트 모습

우선 가장 먼저 소개할 기술은 Next.js 라는 기술입니다. 리액트에서는 서버사이드 렌더링을 하는 기능들을 제공하고 있지만, 아주 기본적인 방법만 제공합니다. 때문에 매번 작성해야 하는 코드의 양도 많고 복잡합니다. 그래서 개발자들은 서버사이드 렌더링을 대신 구현해주는 기술들을 만들기 시작했는데요. Next.js는 그렇게 만들어진 기술들 중에서 가장 인기 있는 기술입니다.

2021년을 기준으로 말하자면 리액트로 서버사이드 렌더링을 구현하는 경우 대부분 Next.js를 사용한다고 보면 됩니다. 심지어 리액트 공식 사이트에서도 Next.js를 추천하는데요. 특히 리액트 라우터랑은 다르게 HTML 파일을 나누듯이 자바스크립트 파일을 나눠 놓으면 곧바로 페이지로 사용할 수 있다는 장점도 있습니다.

리액트에서 서버사이드 렌더링을 써보고 싶으시다면 Next.js를 공부해보시는 걸 추천드릴게요.

공식 사이트: https://nextjs.org/

Gatsby
— 리액트로 정적 사이트 만들기

Gatsby Example

gatsby-starter-blog 프로젝트의 모습

두 번째로 소개할 기술은 Gatsby라는 기술입니다. 예전에 프로젝트를 배포하기 전에 npm run build 명령어로 프로젝트를 빌드했던 거 기억나시나요? 빌드라는 건 리액트로 작성된 소스코드들을 브라우저가 알아들을 수 있도록 만드는 걸 말하는데요. Gatsby는 리액트 코드를 미리 렌더링 해서 프로젝트를 빌드할 때 HTML 파일로 만듭니다. 위에서 이런 방식을 정적 사이트 생성이라고 했었죠? Gatsby를 사용하면 리액트로 만든 사이트를 빌드해서 손쉽게 HTML 파일로 만들 수 있습니다.

회사 소개 사이트나 동아리 홈페이지 혹은 포트폴리오 사이트 같이 정적인 사이트를 리액트로 만들고 싶으시다면 Gatsby를 사용하는 걸 강력 추천드릴게요.

공식 사이트: https://www.gatsbyjs.com/

React Native
— 모바일 앱의 화면도 리액트로

React Native Example

리액트 네이티브에서 텍스트와 버튼을 배치한 예시

마지막으로 소개할 기술은 React Native입니다. 자바스크립트로 된 리액트 코드는 서버나 클라이언트에서 HTML로 변환됩니다. 하지만 꼭 HTML만 만들어야 할까요? 모바일 앱을 개발할 수도 있지 않을까요? 모바일 화면에서 쓰는 것들을 미리 컴포넌트로 만들어두면 충분히 가능할 거 같습니다.

React Native는 이런 아이디어에서 출발한 기술입니다. 리액트로 작성한 코드를 모바일 앱으로 만들 수 있게 해 주는데요. 리액트 코드로 개발하면 웹과 안드로이드와 iOS 앱에서 사용하는 공통적인 코드를 한 번에 개발할 수 있다는 장점이 있습니다.

여러 플랫폼의 서비스를 빠르게 개발할 수 있기 때문에 많은 스타트업에서 React Native를 활용하고 있답니다. 이번 기회에 React Native를 배워서 모바일 앱도 만들어보는 건 어떨까요!

공식 사이트: https://reactnative.dev/

\*6-4-01. Styled Components란?
혹시 React 프로젝트에 CSS를 적용하면서 답답함을 느낀 적 있지 않으신가요? 이런 답답함을 느꼈다면 잘하고 계신 겁니다. CSS를 React 프로젝트에 그대로 적용하는 건 여러 면에서 불편한 게 맞으니까요.

React를 오랫동안 사용해 온 개발자들도 똑같은 고민을 해왔습니다. 그리고, 문제를 해결하기 위해 새로운 기술들을 만들었습니다. 그중에서도 가장 인기 있는 기술이 바로 Styled Components입니다. 어떤 건지 일단 코드부터 한 번 볼게요.

import styled from 'styled-components';

const Button = styled.button`  background-color: #ededed;
  border: none;
  border-radius: 8px;`;

function App() {
return (

<div>
<h1>안녕 Styled Components!</h1>
<Button>확인</Button>
</div>
);
}

export default App;
<Styled Components로 Button이라는 컴포넌트를 만든 예시 코드>

위 코드에서 Button이라는 변수는 React 컴포넌트인데요. 우리가 익숙하게 보던 React 컴포넌트를 만드는 방식과 조금 다르죠? 일반적인 방법과 다르게 CSS 코드로 컴포넌트가 만들어졌네요. 여기가 바로 Styled Components가 적용된 부분입니다.

React는 JSX라는 문법으로 태그를 작성해 태그에 해당하는 컴포넌트를 만듭니다. 그렇게 만든 컴포넌트에 스타일을 적용하려면 해당 태그를 타겟한 CSS 코드를 따로 작성해야 하죠. 이런 방식에는 여러 가지 불편한 점이 있습니다.

하지만, Styled Components는 컴포넌트를 만들면서 바로 해당 컴포넌트의 스타일을 작성합니다. 마치 JSX로 컴포넌트를 만드는 것처럼 리액트스럽게 CSS를 쓰는 방식인 거죠. 이렇게 컴포넌트 중심으로 스타일을 지정하는 방식은 편리할 뿐만 아니라, 개발 속도도 빨리지게 하고, 심지어 재밌습니다. 아마 이번 수업을 듣고 나면 여러분은 Styled Components의 엄청난 팬이 되어 있으실 거예요.

다음 레슨에서는 본격적인 설명에 들어가기 앞서, React에서 CSS를 쓸 때 실제로 어떤 불편한 점이 있는지 좀 더 구체적으로 알아보겠습니다. 그리고, Styled Components가 이 문제들을 어떻게 해결하는지도 간단하게 알아볼게요.

\*6-4-02. 기존 방식의 문제점
React 프로젝트에서 CSS를 쓸 때 어떤 불편함이 있는지, Styled Components가 그 불편함을 어떻게 해결해 주는지 한번 알아보겠습니다.

CSS 클래스 이름이 겹치는 문제
아래 두 컴포넌트, App.js와 Dashboard.js를 예로 들어볼게요.

App.js

import Dashboard from './Dashboard';
import App.css;

function App() {
return (

<div className="container">
<Dashboard> ... </Dashboard>
</div>
);
}

export default App
App.css

.container {
background-color: #000000;
}
Dashboard.js

import Dashboard.css;

function Dashboard({ children }) {
return (

<div className="container">
{children}
</div>
);
}

export default Dashboard;
Dashboard.css

.container {
font-size: 16px;
}

App.js에 App이라는 컴포넌트를 만들고 클래스 이름을 .container로 지었습니다. Dashboard.js에는 Dashboard라는 컴포넌트를 만들고, 해당 컴포넌트에서의 클래스 이름도 .container로 지었습니다. 그렇게 만들어진 Dashboard 컴포넌트는 App 컴포넌트 안에 배치했습니다.

각 컴포넌트의 스타일링 코드도 살펴보죠. Dashboard.js에서는 Dashboard.css만 불러와서 컴포넌트의 font-size를 16px로 지정하고 있습니다. App.js에서는 App.css만 불러와서 컴포넌트의 background-color를 #000000로 지정하고 있네요. 각 컴포넌트에 따로 스타일을 지정하기 위한 의도인 거 같습니다.

하지만, 위 코드는 의도와는 다르게 동작합니다. 두 컴포넌트 모두에서 App.css에 있는 스타일과 Dashboard.css에 있는 스타일이 모두 적용되는데요. 이는 사용된 클래스 이름이 전역적인 특성을 가지기 때문입니다. 참고로, 클래스 이름이 전역적이라는 건 한 컴포넌트에서 사용한 클래스 이름을 다른 모든 컴포넌트에서도 사용할 수 있다는 뜻입니다.

클래스 이름은 모든 곳에서 사용할 수 있기 때문에, import 해오지 않은 CSS 파일에서도 같은 클래스 이름이 사용된 부분이 있으면 그곳의 스타일이 함께 적용됩니다. 이렇게 의도하지 않은 방식으로 스타일이 적용되는 걸 막기 위해 클래스 이름은 겹치지 않도록 조심해야 합니다.

페이스북 메인 화면 (출처: [Facebook](https://www.facebook.com/))

페이스북 메인 화면 (출처: Facebook)

규모가 작은 프로젝트에서는 클래스 이름을 겹치지 않도록 짓는 게 어렵지 않습니다. 하지만, 프로젝트가 커지면 굉장히 힘든 일이 되는데요. 페이스북 프로젝트에서는 약 5만여 개가 넘는 컴포넌트를 사용한다고 합니다. 이런 프로젝트에서 겹치지 않는 클래스 이름을 짓는다는 건 거의 불가능에 가깝다고 봐야겠죠.

const StyledApp = styled.div`  background-color: #000000;`;

const Dashboard = styled.div`  font-size: 16px;`;

function App() {
return (
<StyledApp>
<Dashboard> ... </Dashboard>
</StyledApp>
);
}

Styled Components는 이 문제를 아주 간단하게 해결했습니다. 클래스 이름을 아예 쓰지 않는 건데요. CSS 코드로 React 컴포넌트를 바로 만드니까 애초에 클래스 이름이 겹칠 일이 없습니다.

재사용하는 CSS 코드를 관리하기 어렵다
머티리얼 디자인의 그림자 디자인 (출처: [구글 머티리얼 디자인](https://material.io/design/environment/light-shadows.html))
머티리얼 디자인의 그림자 디자인 (출처: 구글 머티리얼 디자인)

사이트를 만들다 보면 자주 쓰는 CSS 코드가 생기기 마련입니다. 예를 들면 그림자 같은 게 있는데요. 그림자는 다양한 곳에서 자주 쓰지만 스타일의 종류는 몇 가지로 정해져 있습니다. 이렇게 자주 재사용되는 스타일은 각 종류 별로 클래스를 만들어 놓고 여러 컴포넌트에서 가져다 쓰면 편리하겠죠.

CSS만으로도 이렇게 개발하는 게 가능합니다. 하지만, CSS만으로는 재사용되는 코드를 잘 관리하는 게 어렵습니다. 아래 예시를 통해 살펴볼게요.

src/App.js

import Dashboard from './Dashboard';
import Card from './Card';
import App.css;

function App() {
return (

<div className="container">
<Dashboard>
<Card> ... </Card>
</Dashboard>
</div>
);
}

export default App
src/App.css

.shadow20 {
box-shadow: 0 10px 15px rgba(0, 0, 0, 0.2);
}

.shadow40 {
box-shadow: 0 10px 15px rgba(0, 0, 0, 0.4);
}
src/Card.js

import Card.css;

function Card({ children }) {
return (

<div className="container shadow20">
</div>
);
}

export default Card;

App 컴포넌트 안에 Dashboard를 배치하고, 그 안에 Card 컴포넌트를 배치하는 코드입니다. App.css 파일에 .shadow20이라는 클래스를 만들어 두고 이걸 Card 컴포넌트에서 썼습니다(클래스 이름은 전역적이기 때문에 이렇게도 사용할 수 있습니다).

여기서 문제는, App.css 코드에 정의된 shadow20만을 보고는 이게 어디에서 사용되는 스타일인지 알기 어렵다는 건데요. JavaScript와 달리 CSS 코드는 VSCode 같은 코드 에디터에서 추적하기 어렵기 때문에 직접 텍스트로 하나하나 검색을 해야 합니다. 스타일이 재사용 되는 곳이 점점 더 많아질수록 코드를 유지 보수 할 때 관리가 더 힘들어지겠죠.

src/shadows.js

import { css } from 'styled-components';

const shadow20 = css`  box-shadow: 0 10px 15px rgba(0, 0, 0, 0.2);`;

const shadow40 = css`  box-shadow: 0 10px 15px rgba(0, 0, 0, 0.4);`;
src/Card.js

import { shadow20 } from '../shadows';

const Card = styled.div`  ${shadow20}
  ...(다른 CSS 코드)`;

export default Card;

Styled Components에서는 스타일 재사용이 필요한 상황에서 클래스가 아니라 JavaScript 변수를 만듭니다. 위 예시 코드에서 shadow20은 JavaScript 변수인데요. JavaScript라서 언제 어디서 쓰고 있는지 에디터를 통해 확인하기 쉽고, 이름을 바꾸거나 삭제를 하는 것도 코드 에디터를 통해 쉽게 할 수 있습니다.

\*6-4-03. 03. Hello Styled
설치
우선 Create React App을 사용해서 프로젝트를 생성해주세요.

npm init react-app 프로젝트명

생성한 프로젝트 폴더 안에서 아래 명령어로 Styled Components를 설치해 줍니다.

npm install styled-components

참고로 이번 수업은 Styled Components 버전 5를 기준으로 배울 예정입니다. 올바로 설치되었다면 package.json 파일에 아래와 같이 추가됩니다. 맨 앞의 숫자가 5로 시작하면 버전 5입니다.

{
...
"dependencies": {
...
"styled-components": "^5.3.5"
},
}
Hello Styled!
간단한 코드를 한번 써 볼게요.

src/Button.js

import styled from 'styled-components';

const Button = styled.button`  background-color: #6750a4;
  border: none;
  color: #ffffff;
  padding: 16px;`;

export default Button;

src/App.js

import Button from './Button';

function App() {
return (

<div>
<Button>Hello Styled!</Button>
</div>
);
}

export default App;

실행했을 때 아래 스크린샷처럼 보이면 성공입니다.

Untitled

개발자 도구로 HTML 코드를 살펴보면 아래처럼 Styled Components가 알아서 클래스 이름을 만들고 스타일을 적용해 준 걸 볼 수 있죠.

<div id="root">
  <div>
    <button class="sc-bczLRJ hrAeCU">Hello Styled!</button>
  </div>
</div>
코드 살펴보기
이제 코드를 하나씩 살펴보면서 이해해 봅시다.

styled 불러오기
import styled from 'styled-components';
styled-components의 default import로 styled를 가져오면 됩니다. 대부분의 작업은 styled 함수를 사용합니다.

컴포넌트 만들기
Styled Components에서는 클래스 대신에 컴포넌트를 만드는데요. 가장 기본적인 컴포넌트를 만드는 방식을 살펴보겠습니다. 아래 코드는 <button> 태그에 스타일을 지정한 컴포넌트를 만드는 코드입니다.

const Button = styled.button`  background-color: #6750a4;
  border: none;
  color: #ffffff;
  padding: 16px;`;

styled.tagname의 tagname 부분에는 스타일을 적용할 HTML 태그 이름을 씁니다. 그리고, 바로 뒤에 템플릿 리터럴 문법으로 CSS 코드를 적습니다.

이런 JavaScript 문법을 처음 보는 분들이 있을 텐데요, 지금은 그냥 이런 문법으로 쓰는구나 하고 넘어가셔도 괜찮습니다. 태그 함수라는 걸 사용한 건데, 이게 왜 함수이고 어떻게 동작하는지는 토픽 마지막에 Styled Components의 미니 버전을 직접 만들면서 자세히 파헤쳐 볼게요. 일단 지금은 문법만 확실히 알고 넘어갑시다.

템플릿 리터럴 안에는 우리에게 익숙한 CSS 문법이 있죠? CSS 코드를 그대로 복사 붙여넣기 해서 편하게 쓸 수 있습니다.

컴포넌트 사용하기
<Button>Hello Styled!</Button>
styled.tagname으로 만든 컴포넌트는 일반적인 React 컴포넌트처럼 JSX로 사용하면 됩니다.

\*6-4-04. Nesting 문법
이번 레슨에서는 Styled Components에서 지원하는 Nesting이라는 문법을 배워보겠습니다. Nesting은 CSS 규칙 안에서 CSS 규칙을 만드는 걸 말하는데요. Nesting을 활용하는 두 가지 방법인 & 선택자와 컴포넌트 선택자에 대해 알아보겠습니다.

& 선택자
& 선택자를 사용해서 앞에서 만든 버튼 컴포넌트를 호버하거나 클릭했을 때 배경색이 바뀌도록 해볼게요.

4-1

src/Button.js

import styled from 'styled-components';

const Button = styled.button`
background-color: #6750a4;
border: none;
color: #ffffff;
padding: 16px;

&:hover,
&:active {
background-color: #463770;
}
`;

export default Button;

Nesting에서 &는 부모 선택자를 의미합니다. 위 코드에서는 버튼 컴포넌트의 클래스를 뜻하는 건데요. 기존 CSS 코드로 표현해 본다면, 버튼 컴포넌트가 .Button이라는 클래스 이름을 쓸 때 &:hover는 .Button:hover와 같은 의미입니다. 어렵지 않죠?

.Button {
background-color: #6750a4;
border: none;
color: #ffffff;
padding: 16px;
}

.Button:hover,
.Button:active {
background-color: #463770;
}
컴포넌트 선택자
Styled Components에선 클래스 이름을 쓰지 않는데요. 그럼 컴포넌트 안에 있는 또 다른 컴포넌트를 선택하고 싶으면 어떻게 해야 할까요?

버튼 안에 아이콘을 배치하는 상황으로 예를 들어볼게요. 버튼 텍스트 왼쪽에 아이콘을 배치하고 그 사이에 마진을 4px만큼 주려고 합니다. 아래 이미지처럼요.

4-2

Styled Components로 Icon과 StyledButton 컴포넌트를 각각 만들고, StyeldButton 안에 Icon을 배치할 건데요. 이때 StyledButton 컴포넌트 안에서 Icon 컴포넌트를 선택해 별도로 margin-right: 4px라는 속성을 지정하려고 합니다.

이럴 경우, 컴포넌트를 선택자로 쓰고 싶을 때는 ${Icon}같이 컴포넌트 자체를 템플릿 리터럴 안에 넣어주면 됩니다.

import styled from 'styled-components';
import nailImg from './nail.png';

const Icon = styled.img`  width: 16px;
  height: 16px;`;

const StyledButton = styled.button`
background-color: #6750a4;
border: none;
color: #ffffff;
padding: 16px;

& ${Icon} {
margin-right: 4px;
}

&:hover,
&:active {
background-color: #463770;
}
`;

function Button({ children, ...buttonProps }) {
return (
<StyledButton {...buttonProps}>
<Icon src={nailImg} alt="nail icon" />
{children}
</StyledButton>
);
}

export default Button;

자손 결합자(Descendant Combinator)로 쓴 & ${Icon} { ... } 부분을 기존 CSS로 표현해 본다면 아래처럼 나타낼 수 있습니다. 버튼 안에 있는 태그 중에 Icon 컴포넌트에 해당하는 태그를 찾아서 스타일을 적용하는 거죠.

.StyledButton {
...
}

.StyledButton .Icon {
margin-right: 4px;
}

특히, &와 자손 결합자를 사용하는 경우에는 &를 생략할 수 있습니다. 즉 ${Icon}만 써도 똑같이 동작합니다. 보통 간편하게 많이 쓰니까, 자손 결합자로 Nesting 할 때는 아래처럼 쓰는 걸 권장합니다.

const StyledButton = styled.button`
background-color: #6750a4;
border: none;
color: #ffffff;
padding: 16px;

${Icon} {
margin-right: 4px;
}

&:hover,
&:active {
background-color: #463770;
}
`;

참고로 Nesting은 여러 겹으로 할 수도 있는데요. 예를 들어서 아래 코드처럼 Nesting된 규칙 안에서 규칙을 만들 수도 있습니다.

const StyledButton = styled.button`
...
&:hover,
&:active {
background-color: #7760b4;

    ${Icon} {
      opacity: 0.2;
    }

}
`;
4-3

&:hover, &:active { ... } 안에 있는 ${Icon} 선택자를 CSS 코드로 표현해 보면 아래와 같습니다.

.StyledButton:hover .Icon,
.StyledButton:active .Icon {
opacity: 0.5;
}

\*6-4-04. Nesting 문법
이번 레슨에서는 Styled Components에서 지원하는 Nesting이라는 문법을 배워보겠습니다. Nesting은 CSS 규칙 안에서 CSS 규칙을 만드는 걸 말하는데요. Nesting을 활용하는 두 가지 방법인 & 선택자와 컴포넌트 선택자에 대해 알아보겠습니다.

& 선택자
& 선택자를 사용해서 앞에서 만든 버튼 컴포넌트를 호버하거나 클릭했을 때 배경색이 바뀌도록 해볼게요.

4-1

src/Button.js

import styled from 'styled-components';

const Button = styled.button`
background-color: #6750a4;
border: none;
color: #ffffff;
padding: 16px;

&:hover,
&:active {
background-color: #463770;
}
`;

export default Button;

Nesting에서 &는 부모 선택자를 의미합니다. 위 코드에서는 버튼 컴포넌트의 클래스를 뜻하는 건데요. 기존 CSS 코드로 표현해 본다면, 버튼 컴포넌트가 .Button이라는 클래스 이름을 쓸 때 &:hover는 .Button:hover와 같은 의미입니다. 어렵지 않죠?

.Button {
background-color: #6750a4;
border: none;
color: #ffffff;
padding: 16px;
}

.Button:hover,
.Button:active {
background-color: #463770;
}
컴포넌트 선택자
Styled Components에선 클래스 이름을 쓰지 않는데요. 그럼 컴포넌트 안에 있는 또 다른 컴포넌트를 선택하고 싶으면 어떻게 해야 할까요?

버튼 안에 아이콘을 배치하는 상황으로 예를 들어볼게요. 버튼 텍스트 왼쪽에 아이콘을 배치하고 그 사이에 마진을 4px만큼 주려고 합니다. 아래 이미지처럼요.

4-2

Styled Components로 Icon과 StyledButton 컴포넌트를 각각 만들고, StyeldButton 안에 Icon을 배치할 건데요. 이때 StyledButton 컴포넌트 안에서 Icon 컴포넌트를 선택해 별도로 margin-right: 4px라는 속성을 지정하려고 합니다.

이럴 경우, 컴포넌트를 선택자로 쓰고 싶을 때는 ${Icon}같이 컴포넌트 자체를 템플릿 리터럴 안에 넣어주면 됩니다.

import styled from 'styled-components';
import nailImg from './nail.png';

const Icon = styled.img`  width: 16px;
  height: 16px;`;

const StyledButton = styled.button`
background-color: #6750a4;
border: none;
color: #ffffff;
padding: 16px;

& ${Icon} {
margin-right: 4px;
}

&:hover,
&:active {
background-color: #463770;
}
`;

function Button({ children, ...buttonProps }) {
return (
<StyledButton {...buttonProps}>
<Icon src={nailImg} alt="nail icon" />
{children}
</StyledButton>
);
}

export default Button;

자손 결합자(Descendant Combinator)로 쓴 & ${Icon} { ... } 부분을 기존 CSS로 표현해 본다면 아래처럼 나타낼 수 있습니다. 버튼 안에 있는 태그 중에 Icon 컴포넌트에 해당하는 태그를 찾아서 스타일을 적용하는 거죠.

.StyledButton {
...
}

.StyledButton .Icon {
margin-right: 4px;
}

특히, &와 자손 결합자를 사용하는 경우에는 &를 생략할 수 있습니다. 즉 ${Icon}만 써도 똑같이 동작합니다. 보통 간편하게 많이 쓰니까, 자손 결합자로 Nesting 할 때는 아래처럼 쓰는 걸 권장합니다.

const StyledButton = styled.button`
background-color: #6750a4;
border: none;
color: #ffffff;
padding: 16px;

${Icon} {
margin-right: 4px;
}

&:hover,
&:active {
background-color: #463770;
}
`;

참고로 Nesting은 여러 겹으로 할 수도 있는데요. 예를 들어서 아래 코드처럼 Nesting된 규칙 안에서 규칙을 만들 수도 있습니다.

const StyledButton = styled.button`
...
&:hover,
&:active {
background-color: #7760b4;

    ${Icon} {
      opacity: 0.2;
    }

}
`;
4-3

&:hover, &:active { ... } 안에 있는 ${Icon} 선택자를 CSS 코드로 표현해 보면 아래와 같습니다.

.StyledButton:hover .Icon,
.StyledButton:active .Icon {
opacity: 0.5;
}

\*6-4-07. 다이나믹 스타일링
이번에는 크기를 조절하는 size, 둥근 모양을 지정하는 round라는 Prop을 추가해 버튼 컴포넌트의 크기와 모양을 조절하는 예시를 만들어 볼게요. 그 과정을 통해 다이나믹한 스타일링을 하는 법에 대해 알아보도록 하겠습니다. 우선 완성된 코드부터 봅시다.

src/Button.js

import styled from 'styled-components';

const SIZES = {
large: 24,
medium: 20,
small: 16,
};

const Button = styled.button`  background-color: #6750a4;
  border: none;
  border-radius: ${({ round }) => round ?`9999px`:`3px`};
color: #ffffff;
font-size: ${({ size }) => SIZES[size] ?? SIZES['medium']}px;
padding: 16px;

&:hover,
&:active {
background-color: #463770;
}
`;

export default Button;
src/App.js

import styled from 'styled-components';
import Button from './Button';

const Container = styled.div`  ${Button} {
    margin: 10px;
  }`;

function App() {
return (
<Container>

<h1>기본 버튼</h1>
<Button size="small">small</Button>
<Button size="medium">medium</Button>
<Button size="large">large</Button>
<h1>둥근 버튼</h1>
<Button size="small" round>
round small
</Button>
<Button size="medium" round>
round medium
</Button>
<Button size="large" round>
round large
</Button>
</Container>
);
}

export default App;
7-1

앞에서 잠깐 살펴봤지만, 템플릿 리터럴 안에는 달러와 중괄호(${ ... })를 사용해서 JavaScript 코드를 집어넣을 수 있습니다. 이런 걸 표현식 삽입법(Expression Interpolation)이라고 부르는데요. 표현식 삽입법을 사용하면 Styled Components에서 Prop에 따라 컴포넌트의 스타일을 다르게 보여줄 수 있습니다. JSX에서 Prop이나 State에 따라 HTML 태그를 다르게 보여주는 것과 비슷하죠. 코드를 좀 더 자세히 살펴보면서 설명드릴게요.

${ ... } 안에 값(변수) 사용하기
가장 기본적인 사용법은 JavaScript 변수를 그대로 넣는 방식입니다. 아래 예시처럼 우리가 평소에 템플릿 문자열을 만들 때 사용하는 방식이라고 생각하시면 됩니다.

const a = 1;
const b = 2;
const str = `${a} 더하기 ${b}는 ${a + b} 입니다.`;

아래 예시 코드에서 ${SIZES['medium']} 부분은 숫자 20을 뜻하기 때문에, font-size: ${SIZES['medium']}px;는 font-size: 20px;란 코드가 됩니다.

const SIZES = {
large: 24,
medium: 20,
small: 16
};

const Button = styled.button`  ...
  font-size: ${SIZES['medium']}px;`;
${ ... } 안에 함수 사용하기
다음으로, Prop에 따라 스타일을 다르게 적용하는 함수를 넣으려고 하는데요. 함수의 파라미터로는 Props를 받고, 리턴 값으로는 스타일 코드를 리턴하면 됩니다. 참고로 이건 템플릿 리터럴의 기능이 아니라 Styled Components가 내부적으로 처리해 주는 겁니다.

const SIZES = {
large: 24,
medium: 20,
small: 16
};

const Button = styled.button`  ...
  font-size: ${(props) => SIZES[props.size]}px;`;

만약에 구조 분해(Destructuring)하면 아래처럼 쓸 수도 있겠죠.

font-size: ${({ size }) => SIZES[size]}px;

그런데 여기서 size Prop이 값이 없거나 잘못된 값이면 어떻게 될까요? Styled Components에서는 undefined 값을 빈 문자열로 처리해 주기 때문에 font-size: px 같은 잘못된 CSS 코드가 됩니다. 그래서 가능하면 기본 값을 정해주는 게 좋은데요. 여러 가지 방법이 있겠지만, 아래와 같은 식으로 널 병합 연산자(Nullish coalescing operator)를 사용할 수도 있습니다.

font-size: ${({ size }) => SIZES[size] ?? SIZES['medium']}px;
논리 연산자 사용하기
함수를 사용할 때 많이 사용하는 패턴 중 하나는 논리 연산자를 사용하는 겁니다. 예를 들어서, round라는 Prop이 참일 때 컴포넌트의 모서리를 둥글게 만드는 예제를 살펴볼게요.

const Button = styled.button`  ...
  ${({ round }) => round &&`
border-radius: 9999px;
`}
`;

round 값이 참이면 그 뒤에 값까지 계산하기 때문에 border-radius: 9999px이라는 문자열이 리턴돼서 적용됩니다. 반대로, round 값이 거짓이면 그냥 false가 리턴돼서 아무런 값도 적용되지 않습니다. React에서 JSX로 조건부 렌더링 하는 것과 비슷하죠?

삼항 연산자 사용하기
마찬가지로 자주 쓰는 패턴입니다. round 가 참이면 완전히 둥근 모서리를 보여주고, 거짓이면 3px 정도로 살짝 부드럽게 깎인 모서리를 보여주고 싶다면 아래와 같이 삼항 연산자로 쓸 수 있습니다.

border-radius: ${({ round }) => round ? `9999px` : `3px`};

\*6-4-09. 스타일 재사용: 상속
HTML 태그에 스타일링하는 건 styled.tagname을 사용해서 할 수 있었습니다. 그런데, JSX 문법으로 직접 만든 컴포넌트나, Styled Components를 사용해 이미 만들어진 다른 컴포넌트에 스타일을 입히려면 어떻게 해야 할까요? 이런 상황에서는 상속을 사용하면 됩니다. 그 방법에 대해서 한번 알아볼게요.

styled() 함수
Styled Components로 만들어진 컴포넌트를 상속하려면 styled() 함수를 사용하면 됩니다. 코드부터 살펴볼게요.

src/Button.js

import styled from 'styled-components';

const SIZES = {
large: 24,
medium: 20,
small: 16,
};

const Button = styled.button`
background-color: #6750a4;
border: none;
color: #ffffff;
font-size: ${({ size }) => SIZES[size] ?? SIZES['medium']}px;
padding: 16px;

${({ round }) =>
round
? `  border-radius: 9999px;`
: `  border-radius: 3px;`}

&:hover,
&:active {
background-color: #463770;
}
`;

export default Button;
src/App.js

import styled from 'styled-components';
import Button from './Button';

const SubmitButton = styled(Button)`
background-color: #de117d;
display: block;
margin: 0 auto;
width: 200px;

&:hover {
background-color: #f5070f;
}
`;

function App() {
return (

<div>
<SubmitButton>계속하기</SubmitButton>
</div>
);
}

export default App;
9-1

Button 컴포넌트의 스타일을 상속해서 새로운 버튼 SubmitButton을 만들고, App 컴포넌트 안에 SubmitButton을 배치하는 상황입니다.

코드를 보면 SubmitButton 컴포넌트를 만들 때 styled(Button)이라고 썼죠? 이렇게 하면 SubmitButton이 Button의 스타일을 상속받게 됩니다. Button 컴포넌트에 SubmitButton의 스타일이 상속됐기 때문에, 마찬가지로 글씨는 흰색으로 보이고 있죠.

상속이라는 단어가 어렵게 느껴질 수도 있는데요, 다른 컴포넌트의 스타일을 가져와서 원하는 대로 사용할 수 있는 것이라고 이해하시면 됩니다. 예시 코드에서 SubmitButton도 Button 의 스타일 전부를 상속하고, 몇 가지 스타일만 추가해 원하는 컴포넌트를 만들고 있습니다.

JSX로 직접 만든 컴포넌트에 styled() 사용하기
styled.tagname으로 만든 컴포넌트는 바로 styled() 함수를 사용할 수 있지만, 그렇지 않은 컴포넌트는 따로 처리가 필요합니다. 예를 들어, 약관을 보여주는 TermsOfService라는 컴포넌트가 있다고 해 볼게요.

src/TermsOfService.js

function TermsOfService() {
return (

<div>
<h1>㈜코드잇 서비스 이용약관</h1>
<p>
환영합니다.
<br />
Codeit이 제공하는 서비스를 이용해주셔서 감사합니다. 서비스를
이용하시거나 회원으로 가입하실 경우 본 약관에 동의하시게 되므로, 잠시
시간을 내셔서 주의 깊게 살펴봐 주시기 바랍니다.
</p>
<h2>제 1 조 (목적)</h2>
<p>
본 약관은 ㈜코드잇이 운영하는 기밀문서 관리 프로그램인 Codeit에서
제공하는 서비스를 이용함에 있어 이용자의 권리, 의무 및 책임사항을
규정함을 목적으로 합니다.
</p>
</div>
);
}

export default TermsOfService;

TermsOfService는 JSX 문법을 직접 사용해서 바로 컴포넌트가 만들어졌는데요. 이 컴포넌트를 styled() 함수로 감싸보겠습니다.

src/App.js

import styled from 'styled-components';
import Button from './Button';
import TermsOfService from './TermsOfService';

const StyledTermsOfService = styled(TermsOfService)`  background-color: #ededed;
  border-radius: 8px;
  padding: 16px;
  margin: 40px auto;
  width: 400px;`;

const SubmitButton = styled(Button)`
background-color: #de117d;
display: block;
margin: 0 auto;
width: 200px;

&:hover {
background-color: #f5070f;
}
`;

function App() {
return (

<div>
<StyledTermsOfService />
<SubmitButton>계속하기</SubmitButton>
</div>
);
}

export default App;
9-2

styled()로 지정한 스타일이 적용되지 않습니다. StyledTermsOfService에 지정한 배경색이랑 너비가 적용이 안 된 거 같네요. 왜 그럴까요?

Styled Components는 내부적으로 className을 따로 생성합니다. 그리고, 자체적으로 생성된 className이 있는 부분에 styled() 함수의 스타일이 입혀지죠.

그런데, JSX 문법으로 직접 만든 컴포넌트는 styled() 함수가 적용될 className에 대한 정보가 없는데요. styled() 함수에서 지정한 스타일이 입혀질 부분이 어딘지 알 수 없으니 스타일이 적용되지 않은 거죠.

이렇게, Styled Components를 사용하지 않고 직접 만든 컴포넌트는 className 값을 Prop으로 따로 내려줘야 styled() 함수를 사용할 수 있습니다. 이런 식으로요.

src/TermsOfService.js

function TermsOfService({ className }) {
return (

<div className={className}>
...
</div>
);
}
9-3

직접 만든 컴포넌트에 className Prop을 따로 내려주는 건 syled() 함수가 적용될 부분의 className을 별도로 정해주는 거라고 이해하시면 됩니다. 위 코드의 경우엔, <div> 태그에 className을 내려줬기 때문에 styled(TermsOfService)에서 작성한 코드는 TermsOfService 안에 있는 <div> 태그에 적용됩니다.

정리하자면, 스타일 상속을 하려면 styled() 함수를 사용하면 되는데, styled.tagname으로 만든 컴포넌트는 styled() 함수로 바로 상속하면 되고, Styled Components를 사용하지 않고 직접 만든 컴포넌트에는 클래스 이름을 내려준 후에 styled() 함수로 상속해야 합니다. 어렵지 않죠?

\*6-4-10. 스타일 재사용: css 함수
가끔 중복되는 CSS 코드들을 변수처럼 저장해서 여러 번 다시 사용하고 싶을 때가 있습니다. 그런 상황에서 주로 사용되는 css 함수에 대해 배워보겠습니다.

Button 컴포넌트와 Input 컴포넌트에 같은 글자 크기를 갖도록 하는 상황을 생각해 볼게요. size라는 Prop으로 small, medium, large 각각에 지정된 크기를 전달하면 16, 20, 24 픽셀로 글자 크기를 지정하려 합니다. 가장 단순한 방법은 아래처럼 똑같은 코드를 두 번 작성하는 형태가 되겠죠.

import styled from 'styled-components';

const SIZES = {
large: 24,
medium: 20,
small: 16
};

const Button = styled.button`  ...
  font-size: ${({ size }) => SIZES[size] ?? SIZES['medium']}px;`;

const Input = styled.input`  ...
  font-size: ${({ size }) => SIZES[size] ?? SIZES['medium']}px;`;

하지만, 이렇게 반복되는 코드는 한 곳에서 지정하고 여러 군데서 활용하는게 더 바람직할 거 같은데요. 이럴 때 css 함수를 사용하면 됩니다.

import styled, { css } from 'styled-components';

const SIZES = {
large: 24,
medium: 20,
small: 16
};

const fontSize = css`  font-size: ${({ size }) => SIZES[size] ?? SIZES['medium']}px;`;

const Button = styled.button`  ...
  ${fontSize}`;

const Input = styled.input`  ...
  ${fontSize}`;

일반적인 템플릿 리터럴을 쓰는 게 아니라 css라는 태그 함수를 붙여서 쓴다는 점을 주의 깊게 봐주세요. Props를 받아서 사용하는 함수가 들어있기 때문에 반드시 css 함수를 사용해야 합니다.

만약에 아래 코드처럼 함수를 삽입하지 않는 단순한 문자열이라면 일반적인 템플릿 리터럴을 써도 되는데요.

const boxShadow = `  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);`;

하지만, 이런 경우에도 항상 css 함수를 사용하도록 습관화하는 걸 권장 드립니다.

const boxShadow = css`  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);`;

\*6-4-01. 글로벌 스타일

\* {
box-sizing: border-box;
}

body {
font-family: 'Noto Sans KR', sans-serif;
}

CSS를 작성하다 보면, 모든 컴포넌트에 적용하고 싶은 코드가 생기는 경우가 있습니다. 대표적으로 폰트나 box-sizing: border-box 같은 코드가 그렇습니다. 물론 이런 코드를 css 함수를 사용해서 변수로 만들고 사용할 수도 있겠죠. 하지만, 모든 컴포넌트에 일일이 값을 넣어주는 건 너무 귀찮은 일입니다. 이럴 땐 글로벌 스타일 컴포넌트를 사용하면 되는데요. 글로벌 스타일 컴포넌트를 최상위 컴포넌트에서 렌더링 하면 글로벌 스타일이 항상 적용된 상태가 되도록 할 수 있습니다.

예를 들어서 사이트 전체에 폰트와 box-sizing을 지정하는 코드를 넣어 볼게요.

import { createGlobalStyle } from 'styled-components';

const GlobalStyle = createGlobalStyle`

\*{
box-sizing: border-box;
}

body {
font-family: 'Noto Sans KR', sans-serif;
}
`;

function App() {
return (
<>
<GlobalStyle />

<div>글로벌 스타일</div>
</>
);
}

export default App;

createGlobalStyle이라는 함수는 다른 Styled Components 함수들과 마찬가지로 템플릿 리터럴 문법으로 사용합니다. 이 함수는 <style> 태그를 컴포넌트로 만드는 건데요. 실제로 <style> 태그가 저 위치에 생기는 건 아니고, Styled Components가 내부적으로 처리해서 <head> 태그 안에 우리가 작성한 CSS 코드를 넣어 줍니다. 개발자 도구에서 한 번 확인해 보세요!

\*6-4-03. 애니메이션
키프레임이란?

공이 튀어 오르는 애니메이션 (출처: 위키피디아)

영상과 애니메이션은 여러 개의 사진을 연속으로 보여주면서 마치 움직이는 듯한 효과를 만들어 냅니다. 이때 연속으로 보여주는 한 장 한 장의 이미지를 프레임이라고 하는데요. 과거에는 애니메이션을 만들 때 프레임 각각을 모두 만들었지만, 요즘에는 움직임의 기준이 되는 프레임만 만들고 그 사이의 프레임들을 자동으로 채워 넣는 방식을 주로 사용합니다. 이때 '움직임의 기준이 되는 프레임'을 '키프레임'이라고 부릅니다.

CSS에서 키프레임은 CSS 애니메이션을 만들 때 기준이 되는 지점을 정하고, 적용할 CSS 속성을 지정하는 문법을 뜻합니다. 예를 들어서, 아래 HTML/CSS 코드는 .ball이라는 <div> 태그를 위아래로 움직이는 애니메이션인데요. 시작 지점에서는 기본값인 translateY(0%)를 적용하고, 애니메이션의 중간 시점에서는 translateY(100%)를 적용한 다음, 마지막에는 기본값인 translateY(0%) 을 적용하고 있습니다.

<div class="ball"></div>
@keyframes bounce {
  0% {
    transform: translateY(0%);
  }

50% {
transform: translateY(100%);
}

100% {
transform: translateY(0%);
}
}

.ball {
animation: bounce 1s infinite;
background-color: #ff0000;
border-radius: 50%;
height: 50px;
width: 50px;
}
보시면 @keyframes로 키프레임 애니메이션을 선언한 다음에, 그걸 animation 속성에서 이름으로 쓰고 있죠? 이 부분을 잘 기억해 주세요.

keyframes 함수
그렇다면, Styled Components에서는 키프레임 애니메이션을 어떻게 넣을 수 있을까요? 예시로 플레이스 홀더 애니메이션을 만들어보며 함께 알아봅시다.

플레이스홀더 애니메이션은 사이트에서 보여줄 내용을 로딩하는 동안 내용이 들어갈 자리에 미리 네모나 동그라미 같은 걸 보여주면서, 애니메이션으로 로딩 중이라는 걸 보여주는 걸 말합니다. (부트스트랩의 예시)

플레이스홀더 애니메이션을 HTML/CSS 코드로 간단히 만들어보면 아래와 같습니다.

<div class="placeholder">
  <div class="placeholder-item a"></div>
  <div class="placeholder-item b"></div>
  <div class="placeholder-item c"></div>
</div
@keyframes placeholder-glow {
  50% {
    opacity: 0.2;
  }
}

.placeholder {
animation: placeholder-glow 2s ease-in-out infinite;
}

.placeholder-item {
background-color: #888888;
height: 20px;
margin: 8px 0;
}

.a {
width: 60px;
height: 60px;
border-radius: 50%;
}

.b {
width: 400px;
}

.c {
width: 200px;
}

여기서 placeholder-glow라는 애니메이션 코드는 애니메이션의 중간인 50% 시점에 0.2의 불투명도로 만드는 건데요. 불투명도의 기본값이 1이니까, 불투명도가 0.2로 낮아졌다가 다시 1로 높아지는 애니메이션이 됩니다.

이 코드를 Styled Components 버전으로 다시 써 볼게요. @keyframes는 keyframes라는 함수를 쓰면 되는데요. styled 함수와 마찬가지로 템플릿 리터럴로 사용하는 태그 함수입니다. 여기서 특히 keyframes로 만든 애니메이션을 ${placeholderGlow}처럼 템플릿 리터럴에 삽입하는 형태로 사용했다는 점을 유심히 봐주세요.

src/Placeholder.js

import styled, { keyframes } from 'styled-components';

const placeholderGlow = keyframes`  50% {
    opacity: 0.2;
  }`;

export const PlaceholderItem = styled.div`  background-color: #888888;
  height: 20px;
  margin: 8px 0;`;

const Placeholder = styled.div`  animation: ${placeholderGlow} 2s ease-in-out infinite;`;

export default Placeholder;
src/App.js

import styled from 'styled-components';
import Placeholder, { PlaceholderItem } from './Placeholder';

const A = styled(PlaceholderItem)`  width: 60px;
  height: 60px;
  border-radius: 50%;`;

const B = styled(PlaceholderItem)`  width: 400px;`;

const C = styled(PlaceholderItem)`  width: 200px;`;

function App() {
return (

<div>
<Placeholder>
<A />
<B />
<C />
</Placeholder>
</div>
);
}

export default App;

참고로, keyframes 함수가 리턴하는 변수는 단순한 문자열이 아니라 JavaScript 객체입니다. 크롬 개발자 도구로 살펴보면 아래처럼 id, 이름, 작성한 CSS 규칙의 내용 등이 값으로 들어가 있는걸 알 수 있는데요. 리턴되는 값이 이런 객체이기 때문에 반드시 styled 함수나 css 함수를 통해 사용해야 한다는 것을 주의해주세요.

{
id: "sc-keyframes-bEnYbJ"
inject: ƒ (e, t)
name: "bEnYbJ"
rules: "\n 50% {\n opacity: 0.2;\n }\n"
toString: ƒ ()
}

\*6-4-05. 테마
ThemeProvider로 테마 설정 사용하기
테마 기능을 만들기 위해서는 현재 테마로 설정된 값을 사이트 전체에서 참조할 수 있어야 합니다. React에서는 이런 상황에서 Context라는 걸 사용하는데요. Styled Components에서도 Context를 기반으로 테마를 사용할 수 있습니다. Context를 내려주는 컴포넌트로 ThemeProvider라는 걸 사용하면 되죠.

예시로 메인 색상을 파랑, 노랑, 빨강으로 설정할 수 있는 테마를 만들어 보겠습니다.

App.js

import { ThemeProvider } from "styled-components";
import Button from "./Button";

function App() {
const theme = {
primaryColor: '#1da1f2',
};

return (
<ThemeProvider theme={theme}>
<Button>확인</Button>
</ThemeProvider>
);
}

export default App;

ThemeProvider라는 Context Provider를 사용해서 theme이라는 객체를 내려줍니다. 이렇게 하면 ThemeProvider 안에 있는 Styled Components로 만든 컴포넌트에서는 Props를 사용하듯이 theme이라는 객체를 쓸 수 있습니다.

예를 들어서 Button 컴포넌트에서 theme 값을 써 볼게요. Prop 값을 사용하듯이 theme이라는 값을 쓰면 되는데요. 기존에 있던 배경색 대신에 아래처럼 함수를 삽입해서 테마 값을 사용합니다. 어렵지 않죠?

src/Button.js

const Button = styled.button`  background-color: ${({ theme }) => theme.primaryColor};
  /* ... */`;

만약에 여러 테마를 선택하게 하고 싶다면 useState 를 활용해서 테마를 바꿔주면 됩니다.

import { useState } from 'react';
import { ThemeProvider } from 'styled-components';
import Button from './Button';

function App() {
const [theme, setTheme] = useState({
primaryColor: '#1da1f2',
});

const handleColorChange = (e) => {
setTheme((prevTheme) => ({
...prevTheme,
primaryColor: e.target.value,
}));
};

return (
<ThemeProvider theme={theme}>
<select value={theme.primaryColor} onChange={handleColorChange}>

<option value="#1da1f2">blue</option>
<option value="#ffa800">yellow</option>
<option value="#f5005c">red</option>
</select>
<br />
<br />
<Button>확인</Button>
</ThemeProvider>
);
}

export default App;

그런데, 만약 테마 설정 페이지를 만든다고 하면 테마 값을 일반적인 컴포넌트에서 참조할 필요도 생길 텐데요. 그럴 때는 ThemeContext를 불러오면 됩니다. 이 값은 React Context이기 때문에 useContext로 씁니다.

import { useContext } from 'react';
import { ThemeContext } from 'styled-components';

// ...

function SettingPage() {
const theme = useContext(ThemeContext); // { primaryColor: '#...' }
}

\*6-4-07. 상황별 유용한 팁
버튼 모양 링크가 필요할 때
19-1

사이트를 개발하다보면 모양은 버튼이지만 역할은 링크인 경우가 있습니다. 예를 들어 페이스북의 로그인 페이지에 있는 "Create new account" 버튼은 모양은 버튼이지만 "Log In"이랑 달리 <a> 태그로 되어 있고, 클릭하면 회원가입 페이지로 이동합니다.

버튼의 스타일 코드는 버튼 컴포넌트에 있을텐데, 이걸 <a> 태그 버전으로도 만들어야 하는 걸까요? 이렇게 반복되는 스타일링 코드를 어떻게 관리하면 좋을까요? 이럴 때 간편하게 사용할 수 있는게 바로 as 라는 Prop 입니다. 예를 들어서 아래와 같이 Button 이라는 컴포넌트가 <button> 태그로 만들어져 있을 때, 이걸 <a> 태그로 바꿔서 사용할 수 있습니다.

const Button = styled.button`  /* ... */`;

as 로 태그 이름을 내려주면 해당하는 태그로 사용할 수 있습니다. 굳이 버튼 모양의 링크 컴포넌트를 만들 필요가 없겠죠?

<Button href="https://example.com" as="a">
  LinkButton
</Button>
원치 않는 Props가 전달될 때
아래처럼 Prop을 Spread 문법을 사용해서 <a> 태그로 전달하는 Link 컴포넌트가 있다고 해 봅시다. 그리고 StyledLink 라는 걸 만들어서 underline 이라는 불린 Prop으로 스타일링 해 볼게요.

import styled from 'styled-components';

function Link({ className, children, ...props }) {
return (
<a {...props} className={className}>
{children}
</a>
);
};

const StyledLink = styled(Link)`  text-decoration: ${({ underline }) => underline ?`underline`:`none`};
`;

function App() {
return (
<StyledLink underline={false} href="https://codeit.kr">
Codeit으로 가기
</StyledLink>
);
}

export default App;

위 코드를 실행하면 이런 경고가 뜹니다.

react-dom.development.js:86 Warning: Received `false` for a non-boolean attribute `underline`.

If you want to write it to the DOM, pass a string instead: underline="false" or underline={value.toString()}.

If you used to conditionally omit it with underline={condition && value}, pass underline={condition ? value : undefined} instead.
at a
at Link (http://localhost:3000/static/js/bundle.js:26:5)
at O (http://localhost:3000/static/js/bundle.js:44495:6)
at App

이 오류는 React에서 알려주는 오류인데요. HTML 태그에 underline 이라는 속성을 지정했는데, 그 속성의 값이 문자열이 아니라서 생긴 오류입니다. <a> 태그에는 underline 이라는 속성이 없죠. 이 문제의 근본적인 원인은 <a {...props} className={className}> 이 부분인데요. Spread를 하는 과정에서 의도하지 않은 underline Prop까지 내려간 것이 원인입니다.

underline Prop이 전달되는 순서를 정리해 보면 이렇습니다.

StyledLink 컴포넌트에서 underline 이라는 Prop을 받는다
StyledLink 가 스타일링하고 있는 Link 컴포넌트에 underline Prop이 전달된다
Link 컴포넌트에서 Spread 문법을 통해 <a> 태그에 underline Prop이 전달된다.
이럴 때는 구조 분해 코드를 조금 고쳐서 underline을 제외하면 원치 않는 Prop이 전달되는 걸 막을 수 있습니다.

function Link({ className, children, underline, ...props }) {
return (
<a {...props} className={className}>
{children}
</a>
);
};

그런데 생각해보면 underline 이라는 Prop은 Link 에서 쓰려고 만든 게 아니라 StyledLink 컴포넌트에서만 쓰려고 만든 건데, Link 에 Prop으로 전달되는게 좀 더 근본적인 문제인 거 같습니다. 이럴 때 아예 Prop이 전달되지 않게 만드는 방법이 있습니다. 바로 Transient Prop이라는 걸 사용하는 건데요.

Transient Prop을 사용하면 Styled Components로 스타일링하는 컴포넌트에서만 Prop을 사용하고, 스타일링의 대상이 되는 컴포넌트에는 Prop이 전달되지 않도록 할 수 있습니다(참고로, Transient는 "일시적인, 순간적인"이라는 뜻입니다).

아래의 코드는 StyledLink 컴포넌트 안에서만 Prop을 사용하고 Link에는 전달하지 않는 예시입니다. Transient Prop을 만들려면 앞에다 $ 기호를 붙여주면 됩니다. 아래 코드에서 $underline Prop은 StyledLink 안에서만 사용되고, Link 로 전달되지는 않습니다.

import styled from 'styled-components';

function Link({ className, children, ...props }) {
return (
<a {...props} className={className}>
{children}
</a>
);
};

const StyledLink = styled(Link)`  text-decoration: ${({ $underline }) => $underline ?`underline`:`none`};
`;

\*6-4-09. Styled Components 파헤치기
이번 레슨에서는 태그 함수(Tagged Function)라는 걸 사용해서 Styled Components와 비슷한 함수를 만들어 볼 건데요. 그 과정을 통해 Styled Components의 편리한 문법이 어떻게 만들어진건지 한번 파헤쳐 보도록 하겠습니다.

우선 처음엔 문자열을 리턴하는 함수부터 만들어 보고, 여기서 값을 삽입하는 방법을 구현해 보고요, 최종적으로는 컴포넌트를 리턴하는 함수로 만들어 볼게요.

태그 함수(Tagged Function)
태그 함수(Tagged Function)는 템플릿 리터럴 문법을 사용해서 실행할 수 있는 함수입니다. 일단 코드부터 먼저 볼게요.

function h1(strings, ...values) {
return [strings, values];
}
const result = h1`color: pink;`;
console.log(result); // [['color: pink;'], []]

보시면 h1 이라는 함수는 첫 번째 파라미터로 strings, 그리고 나머지 파라미터들을 values 배열로 받는데요. 이 함수를 템플릿 리터럴로 실행한 거 보이시나요? 이렇게 일반적인 형태로 함수를 선언하고, 템플릿 리터럴로 실행하면 특정한 형태로 파라미터가 전달됩니다.

어떤식으로 전달되는지 확인해보려고 일단 console.log 로 출력해봤는데요. strings 에는 입력한 문자열이 배열로 나오네요. values 는 빈 배열로 출력됩니다.

이번에는 템플릿 리터럴에 값을 삽입하고 출력해보죠.

function h1(strings, ...values) {
return [strings, values];
}
const backgroundColor = 'black';
const result2 = h1`  background-color: ${backgroundColor};
  color: pink;`;
console.log(result2);
// [['\n  background-color: ', ';\n  color: pink;\n'], ['black']]

strings 에는 값이 삽입되는 부분 앞뒤의 문자열들이 잘려서 배열로 들어가 있고, values에는 삽입된 값들이 배열로 들어가 있습니다. 이것이 태그 함수의 기본적인 동작입니다. 이걸 사용해서 CSS 스타일이 생성된 리액트 컴포넌트를 만드는 것이 Styled Components의 핵심 아이디어입니다.

간단하게 <style> 태그를 렌더링하는 컴포넌트를 만들어 볼게요. 실제 Styled Components는 더 복잡하고 정교하게 만들어졌겠지만, 저희는 좀 더 간단한 버전으로 만들어 보겠습니다.

function h1(strings, ...values) {
// React 컴포넌트를 만든다
function Component({ children }) {
// 템플릿 리터럴에서 받은 값을 CSS 코드로 만든다
let style = '';
for (let i = 0; i < strings.length; ++i) {
style += strings[i];
if (values[i]) {
style += values[i];
}
}

    // CSS 코드에 따라 클래스 이름을 만든다
    const className = `my-sc-${style.length}`;

    // `<style>` 태그로 만든 CSS 코드를 렌더링한다
    return (
      <>
        <style>{`.${className} {${style}}`}</style>
        <h1 className={className}>{children}</h1>
      </>
    );

}
return Component;
}

const backgroundColor = 'black';
const StyledH1 = h1`  background-color: ${backgroundColor};
  color: pink;`;

function App() {
return <StyledH1>Hello World</StyledH1>;
}

export default App;
Untitled

위 코드에서 Component 라는 부분이 약간 헷갈릴 수 있는데, 컴포넌트 함수를 선언하는 부분이라고 이해하시면 됩니다. 태그 함수 안에서 컴포넌트를 만들고 이걸 리턴하는 건데요. 이 컴포넌트는 우리가 태그 함수에서 집어넣은 CSS 코드를 <style> 태그에 렌더링하는 컴포넌트입니다.

내부적으로 사용할 클래스 이름도 만들었는데요. 여기선 단순하게 CSS 코드 길이를 가지고 클래스 이름을 생성했습니다(my-sc${style.length} 부분). Styled Components에서는 내부적으로 클래스네임을 알아서 생성해주기 때문에 우리가 클래스 이름을 신경 쓸 필요가 없었죠.

여기서 마지막으로 함수를 삽입하는 예시도 한번 만들어 봅시다. 단순히 strings 와 values 배열을 합쳐주는 게 아니라, React 컴포넌트의 Props를 활용하는 함수가 삽입되는 경우를 처리할 건데요.

function h1(strings, ...values) {
// React 컴포넌트를 만든다
function Component({ children, ...props }) {
// 템플릿 리터럴에서 받은 값을 CSS 코드로 만든다
let style = '';
for (let i = 0; i < strings.length; ++i) {
style += strings[i];
// 삽입된 값이 함수이면 props를 가지고 실행한 값을 CSS에 넣는다.
if (typeof values[i] === 'function') {
const fn = values[i];
style += fn(props);

        // 그 외에 값이 존재하면 CSS에 문자열로 넣는다.
      } else if (values[i]) {
        style += values[i];
      }
    }

    // CSS 코드에 따라 클래스 이름을 만든다
    const className = `my-sc-${style.length}`;

    // `<style>` 태그로 만든 CSS 코드를 렌더링한다
    return (
      <>
        <style>{`.${className} {${style}}`}</style>
        <h1 className={className}>{children}</h1>
      </>
    );

}
return Component;
}

const backgroundColor = 'black';
const StyledH1 = h1`  color: pink;
  ${({ dark }) => dark && 'background-color: black;'}`;

function App() {
return <StyledH1 dark>Hello World</StyledH1>;
}

export default App;

이번에는 Component 함수 안에서 CSS 코드를 생성하는 부분에 함수를 처리하는 부분이 추가되었습니다. 위 코드가 실행되는 순서를 하나씩 생각해 볼게요.

템플릿 리터럴로 태그 함수 h1 을 실행해서, StyledH1 이라는 컴포넌트가 만들어진다.
App 컴포넌트를 렌더링하면 StyledH1 컴포넌트도 렌더링한다.
StyledH1 컴포넌트에서는 CSS 코드를 생성해서 <style> 태그로 넣는다. 이때 함수로 삽입된 값(${({ dark }) => dark && 'background-color: black;'} 부분)은 함수이기 때문에, Props를 가지고 실행해서 CSS로 만든다. 우리 코드에서는 dark 라는 값이 있기 때문에, CSS에는 background-color: black; 이라는 값으로 반영된다.

하하하하하하하하하하한
