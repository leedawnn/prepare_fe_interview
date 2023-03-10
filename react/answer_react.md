# prepare_frontend_interview

## React

- **리액트는 라이브러리인가요 프레임워크인가요?**
  - 리액트는 공식문서에 나와있듯이 라이브러리입니다.
  - **프레임워크와 라이브러리의 차이점은?**
    - 프레임워크는 개발 시 필수적인 코드나 알고리즘 등이 어느정도 구성되어 있는 뼈대를 제공하도록 만들어졌습니다. 라이브러리는 특정 기능에 대한 API(도구, 함수)를 모은 집합을 말합니다.
- **리액트를 사용하는 이유**
  - React는 기본적으로 컴포넌트 기반이기 때문입니다. 컴포넌트는 역할과 가능에 따라 따로 관리하기 편하고, 반복되는 부분을 대체할 수 있어서 코드 재사용성을 높여주기 때문입니다.
  - Virtual Dom으로 인해 빠른 렌더링이 가능하기 때문입니다.
  - SPA(싱글 페이지 애플리케이션)으로 서버의 자원을 아낄 수 있으며, 더 좋은 사용자 경험을 제공할 수 있기 때문입니다.
- **virtual DOM에 대해서 아나요?**
  - 리액트는 실제 DOM을 조작하는 대신, 이를 추상화한 virtual DOM을 사용합니다. 리액트에서 데이터가 변하여 실제 DOM을 업데이트 할 때는 세가지 절차를 밟습니다. 전체 UI를 virtual DOM에 리렌더링하고, 이전 내용과 현재 내용을 비교하여 바뀐 부분만 실제 DOM에 적용시킵니다.
  - DOM과 CSSOM의 차이점
    - DOM은 HTML 문서에 접근하기 위한 인터페이스입니다. CSSOM은 CSS 객체 모델로 자바스크립트가 CSS를 동적으로 조작할 수 있게 해줍니다.
- **React에서 함수 컴포넌트와 클래스 컴포넌트의 차이 🔥**
  - 클래스 컴포넌트는 객체지향 프로그래밍의 구조를 띄고 있으며, state를 초기화 하기 위해서는 constructor(생성자) 함수를 필요로 하기 때문에 함수 컴포넌트에 비해 코드가 길어지고, 사이즈가 커질 수 있습니다. 함수 컴포넌트는 클래스형 컴포넌트에 비해 Hooks를 사용하여 생성자 함수를 통해 state를 초기화 하지 않더라도 사용이 가능합니다(useState 등).
- **리액트에서 함수형 컴포넌트라고 부르지 않고 함수 컴포넌트라고 부르는 이유가 무엇인가요🔥**
  - 리액트에서 사용하는 함수 컴포넌트는 hook이 들어가고, 이 훅으로 사이드 이펙트를 빈번히 일으키기 때문에 순수함수를 지향하는 함수형 프로그래밍이라고 볼 수 없기 때문입니다.
- **props와 state의 차이🔥**
  - props: 컴포넌트 속성을 설정할 때 사용하는 요소입니다. props값은 해당 컴포넌트를 불러와 사용하는 부모 컴포넌트에서 설정할 수 있습니다.
  - state: 컴포넌트 내부에서 바뀔 수 있는 값을 의미합니다. props를 바꾸려면 부모 컴포넌트에서 바꿔야합니다.
- **Props가 컴포넌트간에 전달받는 것이라고 했는데 자식에서 부모로도 전달할 수 있는가 🔥**

  - 부모가 함수를 넣어 props로 자식에게 넘겨주면, 자식이 데이터를 파라미터로 넣어 호출하는 방식으로 전달할 수 있다.

  ```typescript
  import React, { useState } from 'react';

  function App() {
    return (
      <div className='App'>
        <Parent />
      </div>
    );
  }

  const Parent = (props) => {
    const [data, setData] = useState('initial data');

    return (
      <>
        <div>{data}</div>
        <Child setData={setData} />
      </>
    );
  };

  const Child = (props) => {
    return (
      <>
        <button onClick={() => props.setData('data from child')}>send data to parent</button>
      </>
    );
  };
  ```

- **FLUX에 대해서 아나요? 🔥🔥**
  - 단방향으로만 흐르는 데이터 흐름을 가진 아키텍쳐를 말합니다.  
    \* 참고 - [Flux 카툰 안내서](https://bestalign.github.io/translation/cartoon-guide-to-flux/)
- **리덕스에 대해서 아나요? 🔥**
  - 상태관리 라이브러리 중 하나이며, 리덕스는 Store라는 변수를 이용하여 전역 상태 관리를 합니다.
- **리덕스의 기본 원칙은? 🔥**
  1. 애플리케이션의 모든 상태는 하나의 저장소 안에 하나의 객체 트리 구조로 구성됩니다.
  2. state는 읽기 전용입니다.
  3. 순수 함수에 의해서 변경되어야 합니다.
- **React에서 state의 불변성을 유지하라는 말이 있는데 이에 대해 설명해달라 🔥**
  - 객체는 실제 데이터 값이 아닌 참조값을 가집니다. 그렇기 때문에 복사하여 동일한 참조 값을 가지는 객체 중 하나라도 변경된다면 모든 객체의 내부 값이 변경될 것 입니다. 이 때 spread 연산자를 통해 복사할 경우 A와 B는 같은 값을 가지더라도 새로운 객체를 할당 받은 상태가 되기 때문에 무결성을 유지할 수 있습니다.
- **리듀서 내부에서 불변성을 지키는 이유는? 전개 연산자의 단점을 해결할 수 있는 방법은 무엇인가 🔥**

  - 불변성을 지킴으로써 각각의 고유한 참조값을 가지는 객체를 복사해서 사용함으로써 어떤 함수가 호출됐을 때 같은 객체를 참조한다면 생길 수 있는 불필요한 리렌더링을 줄일 수 있습니다.
  - spread 연산자를 사용할 경우 1depth의 값에서만 깊은 복사를 실행하기 때문에, immer과 같은 라이브러리를 사용하여 불변성을 지키는 것이 좋습니다.

- **리액트 사용시에 부수효과(side effect)로 인해 생기는 문제점이 있다면 🔥**

  - state를 직접 조작하지 않는 방식으로 부수효과를 피해야합니다. state나 props가 변경될 때 리렌더링이 되기 때문에 의도치 않게 부수효과를 가진 함수들로 인해 불필요한 리렌더링이 잦아질 수 있기 때문입니다. 또한 Redux의 reducer는 순수함수여야만 하는데, store값을 변경하는 함수가 부수효과를 동반하지 않아야 store 내부의 값들이 안전하게 보호될 수 있습니다.

- **컴포넌트의 라이프 사이클 메서드 🔥**
  - 라이프사이클은 총 세 가지, 즉 마운트, 업데이트, 언마운트 카테고리로 나눕니다.

1. 마운트
   DOM이 생성되고 웹 브라우저상에 나타나는 것을 마운트라고 합니다.
   - componentDidMount : 컴포넌트가 웹 브라우저상에 나타난 후 호출하는 메서드
2. 업데이트
   컴포넌트는 다음과 같은 총 네 가지 경우에 업데이트합니다.

   - Props가 바뀔 때
   - state가 바뀔 때
   - 부모 컴포넌트가 리렌더링될 때
   - this.forceUpdate로 강제로 렌더링을 트리거할 때

   - componentDidUpdate : 컴포넌트의 업데이트(리렌더링) 작업이 끝난 후 호출하는 메서드입니다.

3. 마운트의 반대 과정, 즉 컴포넌트를 DOM에서 제거하는 것을 말합니다.
   - componentWillUnmount : 컴포넌트가 웹 브라우저사에서 사라지기 전에 호출하는 메서드

\* 참고 - [리액트의 라이프 사이클](https://kyun2da.dev/react/%EB%A6%AC%EC%95%A1%ED%8A%B8-%EB%9D%BC%EC%9D%B4%ED%94%84%EC%82%AC%EC%9D%B4%ED%81%B4%EC%9D%98-%EC%9D%B4%ED%95%B4/)

- **Hooks의 종류 🔥**
  Hooks는 리액트 버전 16.8에 새로 도입된 기능으로 함수 컴포넌트에서도 상태 관리를 할 수 있는 useState, 렌더링 직후 작업을 설정하는 useEffect 등의 기능을 제공하여 기존의 함수 컴포넌트에서 할 수 없었던 다양한 작업을 할 수 있게 해줍니다.

  - useState - 첫 번째 원소는 상태 값, 두 번째 원소는 상태를 설정하는 함수입니다. 이 함수에 파라미터를 넣어서 호출하면 전달받은 파라미터로 값이 바뀌고 컴포넌트가 리렌더링 됩니다.
  - useEffect
    - 리액트 컴포넌트가 렌더링될 때마다 특정 작업을 수행하도록 설정할 수 있는 Hook 입니다.
    - 마운트만 실행시키고 싶을 경우 : 두 번째 파라미터로 비어있는 배열을 넣어주면 된다.
      ```javascript
      useEffect(() => {
        console.log('마운트될 때만 실행됩니다.');
      }, []);
      ```
    - 특정 값이 업데이트될 때만 실행하고 싶을 경우 : 두 번째 파라미터로 전달되는 배열 안에 검사하고 싶은 값을 넣어주면 된다.
      ```javascript
      useEffect(() => {
        console.log(name);
      }, [name]);
      ```
  - useReducer
    - useReducer는 useState보다 더 다양한 컴포넌트 상황에 따라 다양한 상태를 다른 값으로 업데이트해 주고 싶을 때 사용하는 Hook입니다. 리듀서는 현재 상태, 그리고 업데이트를 위해 필요한 정보를 담은 액션 값을 전달받아 새로운 상태에 반환하는 함수입니다. 리듀서 함수에서 새로운 상태를 만들 때는 반드시 불변성을 지켜주어야 합니다.
  - useMemo
    - useMemo를 사용하면 함수 컴포넌트 내부에서 발생하는 연산을 최적화할 수 있습니다. 렌더링하는 과정에서 특정 값이 바뀌었을 때만 연산을 실행하고, 원하는 값이 바뀌지 않았다면 이전에 연산했던 결과를 다시 사용하는 방식입니다.
  - useCallback
    - useMemo와 상당히 비슷한 함수입니다. 주로 렌더링 성능을 최적화 해야하는 상황에서 사용하며, 이 Hook을 사용하면 만들어놨던 함수를 재사용할 수 있습니다. useCallback의 첫 번째 파라미터에는 생성하고 싶은 함수를 넣고, 두 번째 파라미터에는 배열을 넣으면 됩니다. 이 배열에는 어떤 값이 바뀌었을 때 함수를 새로 생성해야 하는지 명시해야합니다.
  - useRef
    - 바닐라 자바스크립트에서 DOM 요소를 조작하기 위해 querySelector나 getElementById 등을 사용했다면, 리액트에서는 useRef 훅 함수를 사용합니다. useRef는 .current 프로퍼티에 변경가능한 값을 담고있는 객체입니다. 또한, .current 프로퍼티를 변경하더라도 리렌더링을 유발하지 않습니다. ref 객체 안의 값은 리액트 생명주기에 독립적이기 때문입니다.
  - 커스텀 Hooks

- **useMemo와 useCallback의 차이를 아나요 🔥**

  - useMemo 함수는 메모이제이션된 값을 반환하고, useCallback 함수는 메모이제이션 된 함수를 반환합니다.

    > Memoization(메모이제이션) :
    > 프로그램 실행 시 이전에 계산한 값을 저장합니다.
    > 원하는 값이 바뀌지 않았다면 이전에 연산했던 결과를 다시 사용하는 방식입니다.

- **리액트에서 setState는 비동기 동작인가요 동기 동작인가요?**
  - setState는 비동기로 동작하는 Hook입니다. 만약 한 컴포넌트 안에서 여러 state값을 연속으로 바꿔주는 일이 생긴다면 불필요한 리렌더링이 발생하기 때문에 비효율적으로 동작하게 됩니다. 이에 대비하여 리액트는 setState를 비동기로 처리해서 컴포넌트 내의 비동기 함수를 처리하는 콜백큐가 다 비워지면 리렌더링하도록 설계되었습니다.
- **setState가 비동기 동작을 취했을 때 얻을 수 있는 이점은 무엇인가요?**
  - 불필요한 리렌더링을 막을 수 있습니다.
- **useLayoutEffect를 사용해보신 적 있나요**
  - 사용해본 적은 없으나 useLayoutEffect에 대해서는 설명할 수 있습니다. useEffect와 useLayoutEffect 훅의 형태는 완전히 동일합니다.
- **리액트의 성능개선 방법에 대해서 설명해주세요**

  - hook 함수를 사용 (useMemo, useCallback)하거나 코드 스플리팅 (react.lazy(), Next.js 프레임워크 사용 등)을 하는 방법이 있습니다.
  - Next.js는 코드 스플리팅(Code splitting)을 내장 지원한다. pages/ 경로에 있는 각 파일은 빌드 단계에서 자동으로 각각의 JavaScript 번들로 코드 스플릿된다.
  - React.lazy
    - React.lazy는 코드분할을 하게 해준다. 코드 분할은 앱을 "지연 로딩"하게 도와주고 사용자들에게 획기적인 성능 향상을 하게 해줍니다. 앱의 코드 양을 줄이지 않고도 사용자가 필요하지 않은 코드를 불러오지 않게 하며 앱의 초기화 로딩에 필요한 비용을 줄여준다. React.lazy는 아직 서버 사이드 렌더링을 하지 못 해서 서버사이드 렌더링을 위해서는 Loadable Components를 추천한다고 합니다.

- **컴포넌트에서 이벤트를 실행시키기 위해서는 어떻게 핸들링해야 하나요**

  - 이벤트로 설정할 함수를 호출하는 것이 아닌 직접 넣어 줄 때는 화살표 함수 문법을 사용하여 넣어 주어야 합니다.

    ```javascript
    case 1: 작동하지 않는 문법
    <button onClick={this.setState({ number: number + 1})}> (x)

    case 2: 작동하는 문법
    <button onClick={()=> this.setState({ number: number + 1}; )}> (o)

    or
    case 3: 아예 함수로 빼주고 해당 함수를 불러 사용한다.

    const plusNum = (number) => {
    setState(number : number + 1);
    }
    ...

    <button onClick={plusNum}>+ 1 </button>
    ```

- **SPA가 뭔가요**

  - SPA는 Single Page Application의 약어이며, 말 그대로 한 개의 페이지로 이루어진 애플리케이션이라는 의미입니다. 기존에는 사용자가 다른 페이지로 이동할 때마다 새로운 html을 받아오고, 페이지를 로딩할 때마다 서버에서 리소스를 전달받아 화면에 보여주었습니다. 요즘에는 이런 식으로 처리하게 되면 트래픽이 너무 많이 나오거나 서버에 높은 부하가 쉽게 걸릴 수 있습니다. 따라서 react와 같은 라이브러리 혹은 프레임워크를 사용하여 뷰(view) 렌더링을 사용자의 브라우저가 담당하도록 하고, 우선 애플리케이션을 브라우저에 불러와서 실행시킨 후에 사용자와의 인터랙션이 발생하면 필요한 부분만 자바스크립트를 사용하여 업데이트 해줍니다(JSON 형식으로 요청함).
  - **SPA의 단점**

    1. SPA의 단점은 앱의 규모가 커지면 자바스크립트 파일이 너무 커진다는 것입니다. 페이지 로딩시 사용자가 실제로 방문하지 않을 수도 있는 페이지의 스크립트도 불러오기 때문입니다. 따라서 코드 스플리팅을 사용하면 라우트별로 파일들을 나누어서 트래픽과 로딩 속도를 개선할 수 있습니다.
    2. react-router처럼 브라우저에서 자바스크립트를 사용하여 라우팅을 관리하는 것은 자바스크립트를 실행하지 않는 일반 크롤러에서는 페이지의 정보를 제대로 수집해 가지 못한다는 잠재적인 단점이 따릅니다.
    3. 자바스크립트가 실행될 때까지 페이지가 비어있기 때문에 자바스크립트 파일이 로딩되어 실행되는 짧은 시간 동안 흰 페이지가 나타날 수 있다는 단점도 있습니다. 이런 문제점은 서버 사이드 렌더링을 통해 해결할 수 있습니다.

  - **SPA vs MPA**
    ![](https://raw.githubusercontent.com/junh0328/TIL/master/React/images/SPAVSMPA.png)

- **SSR이 뭔가요**
  - 서버에서 사용자에게 보여줄 페이지를 모두 구성하여 사용자에게 페이지를 보여주는 방식입니다. 클라이언트가 요청을 하면 서버에서는 필요한 것들을 이용해 HTML 파일을 만들고, HTML 파일과 동적으로 제어할 수 있는 스크립트를 클라이언트에 보냅니다. 따라서 CSR을 사용할 때보다 페이지 로딩이 빠르기 때문에 사용자가 빠르게 화면을 볼 수 있는 장점이 있습니다. 또한 SEO에 효율적입니다. 하지만 페이지를 요청할때마다 필요한 부분만 바꿔서 보여주는 것이 아닌 새로운 페이지를 보여주기 때문에 화면이 깜빡이는 현상이 생길 수 있고, 서버에 계속 요청해야하기 때문에 서버 부하가 커진다는 단점이 있습니다.
- **SEO가 뭔가요**

  - 구글, 네이버와 같은 검색 엔진들이 서버에 등록된 웹사이트를 돌아다니면서 HTML 문서를 분석합니다. 이때 HTML에 사용된 태그를 바탕으로 사용자가 검색할 때 웹사이트를 빠르게 검색할 수 있게 도와줍니다.

- **TTV, TTI**

  - TTV는 보여지는 시점 (Time To View), TTI는 인터렉션 사용자와의 통신이 가능해지는 시점 (Time To Interact)입니다.

- **하이드레이션에 대해 알고 있나요**
  - 하이드레이션이란, 리액트에서 서버사이드 렌더링 혹은 SSG(스태틱 사이트 제네레이션)을 실행한 HTML 결과물을 받아온 뒤, 브라우저에서 이것을 다시 리액트 트리에 맞게 파싱하는 행위입니다.
- **Next의 렌더링 수행 방식**
  1. SSR을 기반으로 서버에 사전에 저장된 렌더트리(render tree)의 HTML을 로드
  2. ① 방식의 사전 렌더링(pre-render) 이후에는 CSR 사용
  3. 페이지가 그려진 이후에 페이지 내부에서 동적인 데이터를 패치(axios, fetch, XMLHttpRequest)하는 과정은 CSR 방식을 따른다.
  4. 만약 페이지가 로드될 때 함게 데이터가 패칭되어야 하는 상황이라면(pre-render)
  5. next.js의 데이터 패칭 방식 (① getInitialProps/ ② getStaticProps / ③ getStaticPath / ④ getServerSideProps) 을 이용해 첫 렌더링 시에 HTML 파일 뿐만 아니라 데이터가 패칭될 수 있도록 처리해야 합니다.
- **Next를 쓴 이유가 있나요**

  1. 사전 렌더링 및 서버 사이드 렌더링
     서버 사이드 렌더링 기능을 제공하여 클라이언트 사이드 렌더링 환경보다 빠른 렌더링을 불러올 수 있습니다.
  2. Hot Code Reloading을 지원
     Next 개발 환경에서는 코드 변경 사항이 저장되면 응용 프로그램을 자동으로 다시 로드합니다.
  3. 자동 코드 분할
     자동 코드 분할 기능 덕분에 코드의 모든 가져오기각 번들로 묶여 각 페이지와 함께 제공됩니다. 결과적으로, 불필요한 코드가 페이지에 로드되지 않게 됩니다.
  4. 설정이 필요없음
     Next.js는 기본적으로 webpack과 babel을 사용하고 있습니다. 이미 서버 사이드 렌더링 및 개발에 필요한 설정이 되어 있으므로 빠르게 개발을 시작할 수 있습니다. 사용하고 싶은 플러그인이 있다면 손쉽게 추가하여 사용할 수 있도록 지원을 하고 있습니다.
  5. 타입스크립트가 내장됨
  6. 파일기반 내비게이션 기능
     리액트에서는 라우트를 위해서 'react-router'라는 라이브러리를 사용하여 라우팅 설정을 해주어야 합니다. 그로 인해 페이지의 경로에 대하여 직접 설정을 해주어야 하였습니다. 하지만 넥스트는 파일 시스템 기반 라우팅을 사용합니다. 폴더의 경로에 따라 페이지의 경로가 설정되어 구축이 빠르고 관리가 편리하다는 장점이 있습니다.

- **Next를 구성하는 기본 설정 파일에 대해서 알고 있나요?**
  - pages 폴더 안에 중요한 기본 설정 파일이 있습니다.
    - 📙_app.jsx (tsx)
      - App 컴포넌트는 모든 페이지의 공통 페이지 역할을 합니다. 페이지들의 공통 레이아웃을 설정하거나 글로벌 CSS를 추가합니다.
    - 📙_document.jsx (tsx)
      - 사용자 정의 Document는 일반적으로 응용 프로그램 `<HTML>` 및 `<body>` 태그를 보강하는데 사용됩니다.
    - 📙_error.jsx (tsx)
      - Next.js에서는 빌드된 프로덕션 환경에서 에러가 발생한다면 에러 페이지로 넘어가게 됩니다. 에러 상황을 위한 페이지입니다. 예시) 404.jsx (tsx) / 500.jsx(tsx) ...
- **사전 렌더링을 위해 사용해 본 함수가 있나요**

  - `getStaticProps`와 `getServerSideProps`를 사용해본 적이 있습니다.
    - `getStaticProps`는 data를 빌드 시에 미리 땡겨와 정적으로 제공합니다. 매 유저의 요청마다 fetch할 필요가 없는 데이터를 가진 페이지를 렌더링할 때 유리하며, SEO 등의 이슈로 인해 빠르게 렌더링해야만 하는 페이지에 사용합니다.
    - `getServerSideProps`는 빌드와 상관없이, 매 페이지 요청마다 데이터를 서버로부터 가져옵니다.

- **Suspense**

- `suspense가 뭔가요?`
  - suspense는 '컴포넌트가 읽어들이고 있는 데이터가 아직 준비되지 않았다'고 React에 알려줄 수 있는, 데이터 불러오기 라이브러리에서 사용할 수 있는 메커니즘 입니다. 이후에 React는 데이터가 준비되기를 기다렸다가 UI를 갱신할 수 있습니다.
- `suspense로 가능한 것은 어떤 것들이 있나요?`
  1. 데이터 페칭 라이브러리(axios, SWR, react-query)와 React가 깊게 결합할 수 있도록 해줍니다.
  2. 의도적으로 설계된 로딩 상태를 조정할 수 있도록 해줍니다. suspense는 데이터가 어떻게 불러져야 하는지를 정하지 않고, 앱의 시각적인 로딩 단계를 밀접하게 통제할 수 있도록 해줍니다.
  3. 경쟁 상태(Race Condition)를 피할 수 있도록 돕습니다. await를 사용하더라도 비동기 코드는 종종 오류가 발생하기 쉽습니다. suspense를 사용하면 데이터를 동기적으로 읽어오는 것처럼 느껴지게 해줍니다.

## 나올 법한 질문

1. 리덕스에 대해 알고 계신거 설명해주세요.
   - Redux는 상태 관리 라이브러리 중 하나이며, 복잡한 상태 관리가 이루어지는 SPA에서 유용하게 사용됩니다. React의 데이터 흐름은 단방향이기 때문에 부모 컴포넌트만이 자식 컴포넌트에게 props를 전달할 수 있습니다. 따라서 depth가 깊어지기 쉽고, 쓸데없는 리렌더링이 발생하곤 합니다. 이러한 상황을 막기 위해 Redux를 사용하여 state를 컴포넌트 구조 바깥에 두고, store라는 중간자를 통해 상태를 업데이트하거나, 새로운 상태를 전달 받습니다.
   - action 타입을 정의하면, 액션 함수가 파라미터를 입력받아 객체 형태로 만듭니다. 상태가 변하면 dispatch가 액션을 발생시켜 store에게 알리고, store로 전달된 액션은 reducer 함수를 호출시켜 변화된 상태를 반환합니다. 반환된 상태는 store에 저장됩니다.
2. SPA가 뭔가요?
3. next의 렌더링 수행 방식에 대해 말해주세요.
4. 하이드레이션에 대해 알고 계신 거 있나요?
5. CSR과 SSR의 차이점에 대해 말해주세요.
