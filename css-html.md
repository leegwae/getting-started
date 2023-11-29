# CSS/HTML

> 질문 출처
>
> - https://h5bp.org/Front-end-Developer-Interview-Questions/questions/css-questions/
> - https://www.frontendinterviewhandbook.com/css-questions/
> - https://www.frontendinterviewhandbook.com/html-questions/

## TOC

- [CSS](#CSS)
- [HTML](#HTML)

## CSS

### CSS가 무엇이고 여기서 Cascading에 대해 설명해주세요?

CSS는 Cascading Style Sheets의 줄임말로 Cascading을 따르는 스타일시트란 뜻이다. Cascading는 여러 CSS 규칙의 우선순위나 상속을 정의한 알고리즘이다. 첫번째, 더 중요한 규칙이 높은 우선순위를 가진다(Importance). `!important` 키워드를 속성값 뒤에 명시하면 우선순위를 높일 수 있다. 두번째, User Agent Stylesheet, Local User Stylesheet, Author Stylesheet, `!important` Author Stylesheet, `!important` Local User Stylesheet, `!important` User Agent Stylesheet 순으로 (뒤에 올수록) 높은 우선순위를 가진다(Origin). 세번째, 더 구체적인 규칙이 높은 우선순위를 가진다(Specificity). 태그, class, id, 인라인 순으로 구체적이다. 네번째, 더 나중에 위치한 규칙이 높은 우선순위를 가진다(Order of appearance).

> User Agent Stylesheet는 브라우저에서 제공하는 스타일시트, Local User Stylesheet는 운영체제나 브라우저 익스텐션에서 제공하는 스타일시트, Author Stylesheet는 개발자가 작성한 스타일시트를 가리킨다.

> 참고
>
> - https://web.dev/learn/css/the-cascade?hl=ko
> - https://developer.mozilla.org/en-US/docs/Web/CSS

### 1px은 몇 바이트로 표현되고 왜 그러한가?

3바이트로 표현된다. R(Red), G(Green), B(Blue) 값이 각각 1바이트로 표현되기 때문이다.

### px, rem, em의 차이에 대해 말씀해주세요?

`px`은 화면의 픽셀을 나타내는 단위로 고정된 크기이다. `em`은 상속된 사이즈에 대해 상대적인 크기를 나타낸다. 예를 들어 부모 요소의 `font-size`가 `16px`이고 자식의 `font-size`가 `1.5em`이면, 자식의 `font-size`는 24px(16px*1.5)이 된다. `rem`은 루트 요소인 `<html>`에 대해 상대적인 크기를 나타낸다.

### CSS 선택자란 무엇인가?

CSS 선택자는 스타일을 적용할 HTML 요소를 선택하기 위해 사용한다. 요소 선택자, 클래스 선택자, ID 선택자 등이 있다.

### class와 id의 차이에 대해 설명해주세요?

첫번째, class는 하나 이상의 요소에 적용할 수 있지만 id는 문서 내에서 유일한 요소에 적용할 수 있다. 두번째, id가 class보다 우선순위가 높다.

### 박스 모델에 대해 설명해주세요?

CSS에서 표시하는 것은 모두 box이다. 하나의 box는 margin box->border box->padding box->content box로 이루어져있다.

> 참고
>
> - https://web.dev/learn/css/box-model?hl=ko

### padding과 margin의 차이에 대해 설명해주세요?

padding은 border와 content 사이의 간격이고 margin은 외부 요소와의 간격이다.

### `box-sizing: content-box | border-box`의 차이는?

`content-box`은 기본값으로 width나 height로 지정한 크기가 content box에 적용된다. `border-box`로 지정하면 width나 height로 지정한 크기가 border box로 지정된다.

### `* { box-sizing: border-box; }`은 어떤 기능을 하고 사용했을 때 어떤 이점이 있나요?

모든 box의 크기가 padding과 border의 크기를 포함하여 직관적이다.

### `display` 속성은 어떤 역할을 하는가?

box가 inline인지 block인지 결정하고, box의 자식들이 어떻게 동작해야하는지 결정한다.

### `display: inline | inline-block | block`의 차이는?

- `inline`이면 문장 안의 단어처럼 배치되며 크기는 컨텐츠에 의존한다. 따라서 width나 height를 지정해도 무시하며 margin과 padding은 좌우만 반영한다. 예를 들어 `<span>`이 있다.
- `block`이면 새로운 라인에 배치되며 너비가 부모와 같다. width, height, margin, padding 모두 반영한다. 예를 들어 `<div>`가 있다.
- `inline-block`는 기본적으로 `inline`처럼 배치되나 `block`처럼 width. height, margin, padding을 반영한다. 예를 들어 `<button>`, `<input>`, `<select>`가 있다.

> 참고
>
> - https://developer.mozilla.org/en-US/docs/Web/CSS/display

### `display: flex | grid | table`의 차이는?

기본적으로 box는 블록 레벨 box가 된다. `flex`이면 자식들이 flex-item이, `grid`이면 grid-item이, `table`이면 table-item이 된다.

### `position` 속성은 어떤 역할을 하는가?

box의 위치를 결정하는 방식을 명시한다. top, left, right, bottom 속성은 `position` 기준에 맞춰 동작한다.

- `static`은 모든 요소의 기본값이다. (`<body>` 태그는 예외적으로 `relative`이다.) top, left, right, bottom이 영향을 주지않는다.
- `relative`는 `static`일 때의 위치를 기준으로 위치가 결정된다.
- `absolute`는 `static`이 아닌 가장 가까운 부모를 기준으로 위치가 결정된다. normal flow에서 제거되며 공간이 만들어지지 않는다.
- `fixed`는 viewport를 기준으로 위치가 결정된다. normal flow에서 제거되며 공간이 만들어지지 않는다.
- `sticky`는 스크롤 동작이 붙은 가장 가까운 조상을 기준으로 동작한다.

> 참고
>
> - https://developer.mozilla.org/en-US/docs/Web/CSS/position

### `float` 속성은 어떻게 작동하는가?

자신을 포함하는 블록 내에서의 위치를 결정한다. `left`는 요소를 블록의 왼쪽에 띄우고 다른 요소가 이 요소 주위로 흐른다. `right`는 요소를 블록의 오른쪽에 띄우고 다른 요소가 이 요소 주위로 흐른다.

### `float`을 해제하는 방법은 무엇인가요? (클리어링에는 어떤 것들이 있고 각각 언제 사용하나요?

`clear` 속성을 사용한다. `float`된 요소의 부모에 다음과 같이 pseudo-elements를 만든다.

```css
 .clearfix::after { content: ''; display: table; clear: both; }
```

### `z-index`에 대해 설명해주세요?

요소의 Z축 방향의 깊이를 결정한다. 동일한 `z-index` 값을 가지면 가장 나중에 나온 요소가 앞으로, 다른 `z-index` 값을 가지면 더 높은 값을 가진 요소가 앞으로 온다. `position: static;`인 요소의 `z-index`는 `auto` 즉 `0`으로 고정되어있으므로 `z-index`의 값은 `position: static;`이 아닌 요소에만 영향을 준다.

### pseudo-elements가 무엇인가?

CSS 선택자에 추가되는 키워드로, 선택된 요소의 특정 부분에 스타일링을 적용할 수 있다. 예를 들어 `:before`나 `:after`를 사용하면 HTML을 수정하지 않고도 해당 요소 옆에 임의의 텍스트 데코레이션을 사용할 수 있다.

### SVG는 어떻게 스타일링할 수 있는가?

속성을 지정하거나, inline CSS를 사용할 수 있다. SVG를 채색하려면 `fill`로 안쪽 색을, `stroke`로 주위의 선 색을 설정한다.

### Flexbox를 사용하는 이유에 대해 설명해주세요?

Flexbox를 사용하면 요소들을 행이나 열 형태로 정렬하고 배치하기 쉽다. 기존의 CSS `float`과 `position`만으로 어려운 레이아웃을 구현하기 좋다.

### 반응형 디자인과 적응형 디자인의 차이는 무엇인가요?

반응형 디자인은 하나의 웹 사이트가 여러 화면 크기와 장치에 대응하도록 하는 것이다. 미디어 쿼리를 사용하여 break point를 기준으로 스타일을 조절한다.적응형 디자인은 화면 크기와 장치에 기반해 미리 정의된 레이아웃을 사용한다.

### reset과 normalize의 차이는?

reset은 기본 브라우저 스타일을 제거한다. normalize는 기본 스타일을 보존하고 일부만 제거한다.

### 인라인 스타일과 CSS-in-JS의 차이에 대해 설명해주세요?

인라인 스타일은 HTML 요소의 `style` 어트리뷰트를 사용하는 방식이고, CSS-in-JS는 자바스크립트 객체나 함수로 스타일을 정의하는 방식이다. CSS-in-JS의 경우 컴포넌트 레벨로 추상화가 되어 유지보수가 더 편리하다. 그러나 런타임에 동적으로 스타일을 생성하므로 초기 로딩 속도는 느릴 수 있다.

### CSS 전처리기를 사용해보셨나요? 장점과 단점에 대해 설명해주세요?

SCSS를 사용해보았다. SCSS의 장점 첫번째, 태그의 중첩 구조처럼 선택자를 중첩할 수 있어 직관적이고 두번째, `@mixin`을 사용하여 반복되는 스타일을 재사용할 수 있다. 단점은 브라우저는 CSS만 처리할 수 있으므로 CSS로 컴파일하는 별도의 빌드 단계가 필요하다.

### SASS와 SCSS의 차이에 대해 설명해주세요?

SASS(Syntatically Awesome Style Sheets)는 CSS 전처리기 중 하나이고, SCSS(Sassy SASS)는 SASS에 더해 추가적인 기능과 구문을 CSS 프리미티브에 더 가까운 문법으로 제공하는 버전이다.

### 사용해 본 CSS 프레임워크가 있다면 무엇이고 어떤 이점이 있었는지 설명해주세요?

Tailwind CSS를 사용해보았다. 첫번째, 미리 정의된 유틸리티 클래스가 제공되고 사용자가 직접 유틸리티를 조정하고 추가할 수도 있다. 두번째, 중단점을 모바일 퍼스트로 제공해서 반응형 디자인을 적용하기에도 간편하다. (예를 들어 `md:bg-blue`는 중단점이 `md`인 곳 이상부터 적용된다). 세번째, 클래스 이름을 고민하는 비용이 없다. 예를 들어 중첩된 플렉스 컨테이너 이름을 고민하지 않아도 된다. 네번째, 별도의 스타일 시트와 스크립트를 왔다갔다 하는 문맥 교환 비용이 없다. 다섯번째, 번들링 과정에서 CSS로 컴파일되기 때문에 동적으로 스타일을 생성하는 CSS-in-JS보다 빠르다.

### CSS-in-JS와 비교했을 때 장점은 어떤가요?

Styled-Component로 개발했을 때는 작은 변경 사항이 생기면 그걸 반영하기 위해 Wrapper 컴포넌트를 뜯어보고 고쳐야하고 무엇을 하는지 알기 어려운 컴포넌트를 만들어서 끼워넣어야하는 경우가 많았다. 즉, 변화에 유연하게 대응하기가 생각보다 어려웠다. `<Container>`나 `<Wrapper>` 등 사람마다 다양한 네이밍을 하나로 통일하는 것도 어려웠다.

### GPU를 활용하여 하드웨어 가속(GPU; Graphics Processing Unit)을 사용하는 CSS 속성에 대해 알려주세요?

CSS Transition, CSS Transform, CSS Animation, CSS Grid, CSS Flexbox, CSS Filter, `opacity` 등

> 참고
>
> - https://d2.naver.com/helloworld/2061385
> - https://iropke.com/archive/animation-gpu.html

### `position: absolute` + width/height/top/bottom/left/right 대신 `transform: translate()`를 사용하는 이유는 무엇인가?

전자는 리플로우가 발생할 수 있기 때문이다. `transform`을 사용하면 요소 자체의 레이아웃을 수정하지 않으므로 합성만 실행된다.

### `visibility: hidden`과 `display: none`의 차이는 무엇인가요?

전자는 공간을 차지하지만 후자는 공간을 차지하지 않는다. 따라서 DOM을 조작하거나 스타일을 변경한다면 둘 다 리페인트는 발생하지 않지만 전자는 리플로우가 발생할 수도 있다.

### 스크린 리더에서만 가시화하려면 어떻게 해야할까요?

```css
position: absolute;
width: 1px;
height: 1px;
padding: 0;
margin: -1px;
overflow: hidden;
clip: rect(0, 0, 0, 0);
white-space: nowrap;
border-width: 0;
```

클래스 선택자에 `sr-only`를 적용하거나 화면 밖으로 나가도록 스타일링한다.

- [ ] BFC(Block Formatting Context)에 대해 설명해주세요?
- [ ] CSS 애니메이션과 JavaScript 애니메이션에 대해 설명해주세요?

## HTML

### XML과 XHTML의 차이점은 무엇인가요?

첫번째, XML은 데이터를 표현하기 위해 사용하는 마크업 언어이고, XHTML은 XML에 기반하여 웹 페이지를 표현하기 위해 사용하는 마크업 언어이다. 두번째, XHTML은 브라우저에 의해 웹 페이지로 해석되어 렌더링될 수 있지만 XML은 그렇지 않다.

### XHTML을 이용한 웹페이지의 한계는 무엇인가요? (`Content-Type: 'application/xhtml+xml'`로 지정한 페이지에는 어떤 문제가 있나요?)

첫번째, 엄격한 규칙을 따르는 XML에 기반하고 있어 HTML보다 유연성이 떨어진다. 두번째, 레거시 브라우저에서는 호환성 문제가 발생할 수 있다.

### HTML5 문서에 대해 설명해주세요? 

HTML5 문서는 `<!DOCTYPE html>`, `<html>`, `<head>`, `<body>` 태그를 필수적으로 포함한다. `<!DOCTYPE html>`은 문서의 타입을 선언한 것으로 브라우저에게 문서를 HTML5로 해석해야한다는 것을 알려준다. `<html>`은 HTML 문서의 루트를 나타낸다. `<head>`는 `<title>`, `<script>`, `<link>`, `<meta>` 등의 태그를 포함한다. `<meta>` 태그는 브라우저에게 제공할 메타데이터를 명시한다. 예를 들어 `<meta charset="utf-8">`은 브라우저에게 문서를 utf-8 문자 인코딩을 사용하여 해석하라고 알려주는 것이다. `<meta name="description" content="페이지 설명">`으로 페이지에 대한 설명을 제공할 수도 있다. `<body>`는 사용자가 실제로 보게 되는 문서의 주요 컨텐츠를 나타낸다.

### `<!DOCTYPE>`은 어떤 역할을 하나요?

DOCTYPE은 document type의 약자로 문서의 타입과 문서가 어떤 버전으로 작성되었는지 명시한다. HTML5는 일반적으로 `<!DOCTYPE html>`로 명시한다.

### HTML5 시맨틱 태그에 대해 설명해주세요?

HTML5 시맨틱 태그는 브라우저와 개발자가 컨텐츠를 더 잘 이해할 수 있도록 사용하는 태그이다. 예를 들어 `<span>`과 `<div>`는 non-semantic이고 `<header>`나 `<table>`, `<form>`은 semantic이다.

### `data-` 속성은 언제 사용하는가?

DOM 자체에 추가적인 데이터를 저장하기 위해 사용한다. 예를 들어 리스트 아이템이 표시하는 데이터의 id 값을 `data-id`로 담아놓는다. 하지만 클라이언트에서 조작 가능하기 때문에 데이터를 신뢰할 수 없다.

### `<meta name="viewport" content="width=device-width, initial-scale=1.0" />`은 어떤 일을 하는가?

올바른 반응형 웹 디자인을 적용하기 위해 필요하다. `width=device-width`는 viewport의 너비를 디바이스의 너비와 동일하게 설정하라는 의미이다. `initial-scale:1.0`은 페이지가 처음 로드될 때 줌 레벨을 1.0으로 설정하라는 의미이다.

### 왜 CSS `<link> `태그를 `<head>` 태그 안에 넣는 것이 좋을까?

CSS `<link>` 태그를 상단에 배치하면 CSS 파일을 먼저 다운로드하고 파싱하므로 초기 로딩 속도를 개선해 스타일이 적용된 페이지 레이아웃을 빠르게 보여줄 수 있다.

### 왜 JavaScript `<script>` 태그를 `<body>` 종료 태그 앞에 넣는 것이 좋을까?

브라우저는 `<script>` 태그를 만나면 파싱을 멈추고 스크립트를 다운로드, 파싱, 실행한다. 즉, HTML 파싱을 블로킹한다. 따라서 HTML 파싱을 먼저 완료하여 사용자에게 초기 컨텐츠를 보여줄 수 있어야한다.

### 클래식 스크립트, `async` 스크립트, `defer` 스크립트의 차이는?

기본적으로 스크립트는 HTML 파싱을 블로킹한다. 파싱 완료 후 스크립트를 실행한 후에야 HTML 파싱을 재개한다. async 스크립트는 스크립트 파싱이 HTML 파싱을 블로킹하지 않는다. 스크립트 파싱이 완료된 직후 스크립트를 실행한다. defer는 스크립트 파싱이 HTML 파싱을 블로킹하지 않는다. HTML 파싱이 완료된 직후 스크립트를 실행한다(`DOMContentLoaded` 이벤트 발생 전에 실행된다).

### `DOMContentLoaded` 이벤트와 `load` 이벤트의 차이점은?

`DOMContentLoaded` 이벤트는 HTML 문서가 파싱된 후 실행되고 `load` 이벤트는 모든 리소스가 로드된 후 발생한다.

### `load` 이벤트는 언제 사용하나요? 단점이 있다면 설명해주세요?

`load` 이벤트는 모든 컨텐츠가 로드된 후 페이지를 초기화할 때 사용할 수 있다. 그러나 모든 자원의 로딩을 기다려야하므로 사용자 경험 측면에서 좋지 않고, 당장 웹 페이지를 렌더링 하기 위해 필요하지 않은 자원의 로딩도 기다려야한다.

### `document.write`는 언제 사용하나요?

HTML 파싱 도중에 동적으로 컨텐츠를 추가할 때 사용한다.

### `img` 태그에 `srcset` 속성을 사용하는 이유는 무엇인가요?

디스플레이의 크기와 해상도에 따라 서로 다른 이미지를 제공할 수 있다. (브라우저는 디스플레이의 픽셀 밀도를 고려하여 적합한 이미지를 선택해서 다운로드하고 표시한다.)

```html
<img src="image.jpg" srcset="image-1x.jpg 1x, image-2x.jpg 2x, image-3x.jpg 3x" alt="이미지 설명">
```

> 참고
>
> - https://heropy.blog/2019/06/16/html-img-srcset-and-sizes/

### clientHeight, offsetHeight, scrollHeight의 차이에 대해 알려주세요?

`clientHeight`는 padding box까지의 높이를 말하며 화면에 표시된 영역만 포함한다. `offsetHeight`는 border box의 높이를 말하며 화면에 표시된 영역만 포함한다 `scrollHeight`는 border box까지의 높이를 말하며 화면에 표시되지 않은 영역도 포함한다. 따라서 스크롤이 붙지 않은 box는 `scrollHeight`와 `offsetHeight`가 동일하다.

### clientTop, offsetTop, scrollTop의 차이에 대해 알려주세요?

`clientTop`은 요소의 상단 가장자리부터 border box의 상단 가장자리까지의 거리를 나타낸다. `offsetTop`은 부모의 상단 가장자리부터 요소의 상단 가장자리까지의 거리를 나타낸다. `scrollTop`은 요소의 상단 가장자리부터 스크롤의 상단 가장자리까지의 위치를 나타낸다.

### 다국어 페이지를 제공하는 방법에 대해 설명해주세요?

`www.test.com/kr`이나 `www.test.com/en`처럼 지원하는 언어별로 URL을 제공하거나, 클라이언트 쪽에서 별도의 데이터 파일을 받아 뿌려주면 되겠다.

### 쿠키와 HTML5 모던 스토리지(세션 스토리지, 로컬 스토리지)에 대해 설명해주세요?

쿠키는 최대 4바이트까지 저장되는 키-값 형식의 문자열 데이터이다. 서버는 HTTP 응답의 `Set-Cookie` 헤더로 쿠키를 설정할 수 있으며 클라이언트는 HTTP 요청의 `Cookie` 헤더로 쿠키를 전송할 수 있다. CSRF 공격에 취약하다. HTML5 모던 스토리지는 5MB~10MB까지 저장되며 자바스크립트 객체 형식의 데이터이다. 키와 값은 모두 문자열로 저장된다. 세션 스토리지는 브라우저 세션 간에 공유되지 않지만 로컬 스토리지는 공유된다. 세션 스토리지는 브라우저 세션이 종료되기 전까지 데이터를 유지하지만 로컬 스토리지는 유효 기간 없이 데이터를 저장한다. 자바스크립트로 접근할 수 있으므로 XSS 공격에 의해 탈취당할 수 있다.

### ARIA와 스크린 리더기에 대하여 설명해주세요? 또한 접근성을 지원하는 웹 사이트를 어떻게 만드는지 설명해주세요?

ARIA(Accessible Rich Internet Applications)는 웹 컨텐츠와 웹 애플케이션을 장애인들이 보다 쉽게 접근할 수 있도록 하는 방법을 정의한 것이다. 스크린 리더기(screen reader)는 시각 장애인을 위한 보조 기술 중 하나로, 웹 컨텐츠와 웹 애플리케이션을 음성이나 점자로 변환한다. 접근성을 지원하려면 첫번째, semantic HTML을 사용한다. 두번째 적절한 ARIA role, property, state를 제공한다. 세번째, 폼 요소에 레이블을 제공한다. 네번째, 키보드를 사용하여 웹 페이지를 탐색할 수 있게 한다. 다섯번째, 적절한 색상 대비를 사용하거나 글자 크기를 조절할 수 있게 하여 가독성을 개선한다.
