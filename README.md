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

\*6-4-
