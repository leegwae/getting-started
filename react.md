# react

> 질문과 답변은 [이 레포지토리](https://github.com/leegwae/study-react)에 정리된 텍스트에 기반합니다. 자세한 내용은 해당 레포지토리를 참고하세요.
>
> **대부분 [React 공식 문서](https://react.dev/)에 기반하여 정리되어있습니다. 해당 텍스트를 참고하세요.**

> **참고**
>
> - **[React 공식문서 스터디 그룹의 비공식 한글 번역 사이트](https://react-ko.dev/)**
> - [React 예상 면접 질문 리스트](https://velog.io/@ye-ji/React-예상-면접-질문-리스트)
> - [[React\] 리액트 면접 질문 (기초 개념)](https://ahnanne.tistory.com/60)
> - [React 인터뷰 대비 질문과 답변 15](https://velog.io/@dojunggeun/React-interview-questions-15)
> - [[프론트엔드\] FE 기술면접(React) 복기 모음](https://torimaru.tistory.com/35)
> - [실제로 받은 프론트엔드 개발자 면접 질문 모음](https://xiubindev.tistory.com/119)
> - [React 면접 질문과 답변 (난이도 상)](https://careerly.co.kr/comments/73555)
> - [Top 40 ReactJS Interview Questions and Answers for 2023](https://www.simplilearn.com/tutorials/reactjs-tutorial/reactjs-interview-questions)
> - https://github.com/sudheerj/reactjs-interview-questions

### React란 무엇인가

React는 웹이나 네이티브 앱에서 사용자 인터페이스를 작성하기 위해 사용하는 라이브러리이다. 컴포넌트를 기반으로 하여 독립적인 컴포넌트를 조립해 UI를 구축한다.

### React의 특징은 무엇인가

첫번째, UI를 만드는 컴포넌트를 정의하고 재사용할 수 있다. 두번째, 렌더링 과정에서 Virtual DOM을 사용한다. 세번째, 컴포넌트 간 단방향식 데이터 플로우를 사용한다.

### React의 장점은 무엇인가

첫번째, 컴포넌트를 재사용할 수 있어 유지보수가 편리하다. 두번째, Virtual DOM을 사용하여 변화를 적용하는 비용이 적다. 세번째, 단방향 데이터 흐름을 사용하므로 상태를 추적하기 쉽다. 네번째, 클라이언트 사이드 렌더링과 서버사이드 렌더링을 모두 지원할 수 있다. 다섯번째, 라이브러리이므로 애플리케이션에서 일부만 담당하고 다른 프레임워크와 함께 사용할 수 있다. 

### React의 단점은 무엇인가

첫번째, 단방향 데이터 흐름을 사용하므로 양방향 데이터 흐름보다는 더 많은 타이핑이 필요하다. 두번째, 규모가 큰 애플리케이션이면 Virtual DOM 사용에 성능 문제가 발생할 수 있다.

### JSX란 무엇인가

JSX는 JavaScript XML의 약자로 JavaScript를 확장한 문법이다. React에서 컴포넌트를 만들 때 JavaScript 내에서 HTML과 유사한 마크업으로 작성할 수 있게 해준다. JSX는 브라우저에 마크업을 렌더링하는 자바스크립트 함수로 컴파일되고 이것이 곧 컴포넌트이다.

### React에서 컴포넌트란 무엇인가

React 컴포넌트는 브라우저에 마크업을 렌더링하는 JavaScript 함수이다. 각각의 컴포넌트는 독립적이며 재사용할 수 있다. React에서는 이 컴포넌트를 조립하여 애플리케이션을 구성한다.

### Virtual DOM이란 무엇인가

Virtual DOM은 Real DOM의 복사본이다. 메모리 상에서 JavaScript 객체로 존재하며 렌더링을 목적하지 않으므로 DOM에 접근할 수 있는 API를 제공하지 않는다. 이러한 Virtual DOM의 특징 때문에 Virtual DOM은 Real DOM보다 DOM 연산 비용이 싸다. React는 Virtual DOM을 사용하여 리렌더링 연산의 크기는 키우고 횟수는 줄인다.

#### Real DOM만 사용해서 리렌더링 횟수를 줄일 수는 없을까?

Real DOM에서 DOM API를 한 번 호출할 때마다 잠재적으로 리렌더링이 한 번 발생할 수 있다. 그렇다면 최대한 DOM API를 호출하지 않고 한 번 호출할 때마다 많은 변경 사항을 DOM에 적용하면 된다. 경량 Document인 `DocumentFragment`에 변경 사항을 적용하고 DOM에 넣는 방법이다. 이렇게 하면 리렌더링 연산 하나의 크기 자체는 커지지만 리렌더링 횟수를 줄일 수 있다.

#### 그렇다면 Virtual DOM은 왜 쓰는가?

Real DOM만 쓴다면 리렌더링 횟수를 줄이기 위해 `DocumentFragment`를 직접 관리해야한다. 즉, 상태 중 하나가 변하면 그 상태를 참조하고 있는 모든 요소를 찾아내고 `DocumentFragment`에 반영해주어야한다. 그러나 Virtual DOM을 사용하면 그 작업을 자동화할 수 있다.

#### Real DOM과 Virtual DOM의 차이점은 무엇인가

첫번째, Real DOM은 실제로 화면에 렌더링되지만 Virtual DOM은 그렇지 않다. 두번째, Real DOM은 DOM을 갱신할 수 있는 API를 제공하지만 Virtual DOM은 그렇지 않다. 세번째, 이러한 차이로 Virtual DOM은 Real DOM보다 연산 비용이 싸다.

### React에서 Virtual DOM이 작동하는 방식을 설명하라

React는 상태의 변경으로 리렌더링을 하기 위해 먼저 메모리에 새로운 Virtual DOM을 만든다. 새로운 Virtual DOM을 기존의 DOM과 비교한다(Diffing). 이때 변경 사항이 있는 요소들을 한 번에 Real DOM에 반영한다(Reconciliation).

### React에서 state란 무엇인가

state는 컴포넌트 내부의 데이터로 인스턴스 간에 공유되지 않는다. state는 컴포넌트 내부에서 변경 가능한 값으로, 컴포넌트는 자신의 state를 변경할 수 있다. 이때 state의 변화는 컴포넌트의 재렌더링을 촉발하며 이 변경 사항은 재렌더링 후에도 유지된다.

> 컴포넌트 내부의 지역 변수는 변경되어도 재렌더링을 촉발하지 않고 이 변경 사항은 state의 변경으로 인한 재렌더링 후에도 유지되지 않는다.

### React에서 props란 무엇인가

props는 부모 컴포넌트에서 자식 컴포넌트에게 전달하는 데이터이다. props를 통한 데이터의 흐름은 단방향으로, 자식 컴포넌트에서는 부모 컴포넌트가 전달한 props를 바꿀 수 없다. 즉, props는 변경 불가능한 값이다.

### React에서 state와 props의 차이는 무엇인가

state는 컴포넌트 내부의 데이터로 변경이 가능하다. props는 자식 컴포넌트가 부모 컴포넌트로부터 전달받은 데이터로 변경이 불가능하다.

### React에서 prop drilling이란 무엇이고 어떻게 피할 수 있는가

상태가 여러 컴포넌트 간 공유되어야 할 경우, 가장 가까운 공통 조상 컴포넌트로 state를 끌어올려 props로 전달해줄 수 있다. 이때 prop drilling 문제는 props를 제공하는 컴포넌트와 사용하는 컴포넌트가 너무 멀리 떨어져있어 전달이 어렵고 컴포넌트를 변경하는 게 어려운 상황을 뜻한다.

prop drilling 문제는 컴포넌트를 하위 컴포넌트로 쪼개지 않거나, 상태를 전역으로 올려 prop를 거치지 않고 상태를 사용할 수 있게 만들어 해결할 수 있다. 후자는 React의 Context API나, 외부 전역 상태 관리 라이브러리를 사용하면 된다.

### 컴포넌트에서 key는 어떻게 사용되는가

컴포넌트에 고유성을 부여할 때 사용할 수 있다. JSX는 어떤 상태를 보유하는 인스턴스나 DOM 노드가 아니다. 그래서 React에서는 동일한 위치에 있는 동일한 컴포넌트는 state를 유지한다. 예를 들어 `<Profile>` 이라는 컴포넌트가 `name`이라는 props가 변경될 때마다 모든 state가 초기화되길 원할 수 있지만 그렇지 않다. 이런 경우 `key` props를 전달하여 해결할 수 있다.

### React는 상태 변화를 어떻게 감지하는가?

`useState` 훅을 사용하여 상태의 변화를 감지한다. `set` 함수가 호출되면 컴포넌트의 재렌더링을 촉발한다.

#### state를 직접 변경하지 않고 `set` 함수를 사용하는 이유는?

state를 직접 변경하면 React는 그걸 알 방법이 없다. `set` 함수를 호출하고 이때 새로운 객체를 전달하면 React는 `Object.is`로 이전 상태 값과 비교하여 상태의 변경을 감지할 수 있다.

### React에서 렌더링 과정을 설명하라

React는 화면에 무언가를 표시하기까지 세 단계를 거친다. (1) 렌더링이 촉발된다. 첫 렌더링의 경우 `createRoot`로 만든 루트의 `render` 메서드를 호출하여 촉발된다. 리렌더링의 경우 `set` 함수를 호출하여 촉발된다. (2) 컴포넌트가 재귀적으로 렌더링된다. 첫 렌더링의 경우 루트 컴포넌트를 호출하여 DOM 노드를 생성한다. 리렌더링의 경우 렌더링이 촉발된 컴포넌트를 호출하여 이전 렌더링과 비교해 변경된 속성을 계산한다. (3) DOM에 변경 사항을 커밋한다. 첫 렌더링의 경우 이전 단계에서 생성한 DOM 노드를 `appendChild` DOM API를 사용해 화면에 표시한다. 리렌더링의 경우 차이가 있는 계산 결과만 DOM 노드에 반영한다.

> 참고
>
> - https://react-ko.dev/learn/render-and-commit

### React 컴포넌트의 라이프사이클을 설명하라

`mount`(컴포넌트가 처음으로 렌더링되어 화면에 나타난다), `update`(`set` 함수의 호출이나 상위 컴포넌트의 리렌더링으로 컴포넌트의 리렌더링이 촉발되며, 이때 props나 state의 변경이 생길 수 있다). `unmount`(최종적으로 컴포넌트가 화면에서 지워진다).

### React Hooks란 무엇인가

React Hooks는 컴포넌트의 최상위 레벨에서만 사용할 수 있는 함수로 컴포넌트 렌더링 중에 호출된다.

### 제어 컴포넌트와 비제어 컴포넌트의 차이는 무엇인가?

컴포넌트의 중요한 정보가 props로 제어된다면 제어 컴포넌트, 그렇지 않다면 비제어 컴포넌트이다. 예를 들어 `<input>` 태그의 `value` prop에 값을 전달하면 그 `<input>`은 제어 컴포넌트가 된다. 대개는 state를 전달하여 `<input>`을 제어한다.  렌더링 중에 `<input>`의 `value` 값이 필요하다면 제어 컴포넌트를, 그렇지 않다면 `<input>`의 `ref` prop에 Ref를 전달하고 이 Ref를 통해 필요할 때마다 `ref.current.value`로 값에 접근하면 된다.

> 참고
>
> - https://react-ko.dev/learn/sharing-state-between-components#controlled-and-uncontrolled-components

### 클라이언트 사이드 라우팅에 대해 설명하라

전통적으로 사용자가 링크를 클릭하면, 브라우저는 해당 도메인으로 HTML, JS, CSS 등 자원을 요청하고 새로운 페이지를 렌더링한다. 클라이언트 사이드 라우팅(client side routing)은 애플리케이션이 서버에 요청하지 않고 URL을 업데이트하고 새로운 UI를 렌더링하는 것이다. SPA에서 일반적으로 사용된다. React 애플리케이션에서 클라이언트 사이드 라우팅을 제공하는 라이브러리는 React Router가 있다.

### React에서 presentational component와 container component의 차이는 무엇인가?

프레젠테이션 컴포넌트는 UI를 처리하는 데 중점이 있고 컨테이너 컴포넌트는 비지니스 로직을 처리하는 데 중점이 있다. 예를 들어 컨테이너 컴포넌트는 데이터를 fetching하고 해당 데이터를 프레젠테이션 컴포넌트에 props로 내려주며, 프레젠테이션 컴포넌트는 전달받은 props를 적절히 표시하는 JSX를 반환한다.

### React에서 최적화를 어떻게 하는가?

첫번째, `useCallback`, `useMemo` 훅을 통해 값을 캐싱한다. `memo`를 통해 컴포넌트 리렌더링을 건너뛴다. 두번째, Webpack과 같은 번들러를 사용하여 번들하고 번들 파일에 대해 최적화(경량화, 트리 쉐이킹, 코드 스플리팅 등)을 수행하여 초기 로딩 시간을 개선한다. 세번째, `React.lazy`나 React Router v6 lazy 등을 통해 지연 로딩하여 초기 로딩 시간을 개선한다. 네번째, 불필요한 래퍼를 삭제하거나 `React.Fragment`를 사용하여 컴포넌트 트리를 단순하게 만든다.

### useMemo와 useCallback에 대해 설명하라

`useMemo`은 값을 캐싱하는 훅이고 `useCallback`은 함수 객체를 캐싱하는 훅이다. 렌더링 중 훅이 호출되면 의존성 배열을 `Object.is`로 이전 렌더링과 비교하여 달라진 경우 새로운 값을 계산하여 반환하고 그렇지 않다면 이전에 캐싱한 값을 반환한다.

### useEffect와 useLayoutEffect에 대해 설명하라

`useEffect`는 렌더링으로 발생하는 사이드 이펙트를 실행한다. 기본적으로는 컴포넌트가 렌더링될 때마다, 브라우저가 컴포넌트를 화면에 리페인트한 후 실행된다. 클린업 함수는 컴포넌트가 언마운트될 때, 그리고 Effect가 다시 실행되기 전마다 실행된다. `useLayoutEffect`는 브라우저가 화면을 리페인트하기 전에 실행되는 버전의 `useEffect`이다. 화면에 나타나기 전 레이아웃 정보를 사용해서 리렌더링을 촉발하기 위해 사용할 수 있다.

### useEffect에서는 왜 `await` 키워드를 사용할 수 없을까?

`useEffect`에 전달하는 함수는 클린업 함수를 반환하거나 아무것도 반환하지 않아야한다. 한편으로 본문에서 `await`를 사용하는 함수는 `async` 함수가 되어 언제나 프로미스를 반환한다. 즉 `useEffect`에 전달하는 함수 내부에서 `await` 키워드를 사용하면 함수를 반환할 수 없다.

### React Context API에 대해 설명하라. 또 어떻게 사용되는가?

`React.createContext`로 생성한 Context의 Provider로 컴포넌트 트리를 감싸면, 트리에 속한 모든 컴포넌트는 `React.useContext` 훅을 사용하여 Provider가 제공하는 Context의 값을 읽을 수 있다. 컨텍스트의 Context의 값이 변경되면 Provider부터 값을 읽는 모든 자식 컴포넌트까지 리렌더링된다. `theme`과 값은 값을 저장하는데 적절하다.

### React는 useState가 어떤 state를 반환할 지 어떻게 알 수 있을까?

컴포넌트 내에서 훅은 항상 동일한 순서로 호출되기 때문이다. React는 내부적으로 컴포넌트마다 state와 `set` 함수 쌍의 배열을 유지하여 `useState`를 호출할 때마다 state 쌍을 반환하고 인덱스를 증가시킨다. 

> 참고
>
> - https://react-ko.dev/learn/state-a-components-memory#how-does-react-know-which-state-to-return
> - https://medium.com/@ryardley/react-hooks-not-magic-just-arrays-cd4f1857236e

### 클래스 컴포넌트와 함수형 컴포넌트의 차이를 설명하라

클래스 컴포넌트는 자바스크립트 상속에 기반하고 있어 복잡하고 디버깅이 어렵다. 함수형 컴포넌트는 순수 함수에 기반하므로 디버깅이 용이하다.

### 클래스와 함수형 중 무엇을 선택할 것이고 그 이유가 무엇인지 설명하라

순수 함수는 동일한 입력에 대해 항상 동일한 출력을 반환한다. 이런 특징에 따라 디버깅이 쉽다. 입력이 변경되지 않는다면 렌더링을 건너뛰어 성능을 향상시킬 수 있다. 언제든지 계산을 중단해도 안전하다. 가령 렌더링 중 사용자의 입력으로 데이터가 변하면 기존 트리를 버리고 새로운 렌더링을 다시 할 수 있다. 훅을 사용하면 클래스 컴포넌트의 라이프사이클도 흉내낼 수 있다.