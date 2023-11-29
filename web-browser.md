# web-browser

##  TOC

- [SOP와 CORS](#SOP와-CORS)
- [Critical Rendering Path](#Critical-Rendering-Path)
- [기타](#기타)
- [이미지 파일 포맷](#이미지-파일-포맷)

## SOP와 CORS

> 참고
>
> - https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy
> - https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS

### SOP 정책에 대해 설명해주세요?

> Origin은 scheme, domain name, port로 구성된다. 두 리소스의 Origin이 같다면 same-origin이라고 하고, 그렇지 않다면 cross-origin이라고 한다.

SOP(Same-Origin Policy)는 도큐먼트나 스크립트가 cross-origin 컨텐츠와 상호작용하지 못하도록 제한하는 보안 정책이다. 브라우저에는 사용자의 민감한 정보가 저장될 수 있고, 또 네트워크를 통해 이 데이터를 주고받을 수 있으므로 cross-origin 접근을 기본적으로 제한하는 것이다.

### CORS 정책에 대해 설명해주세요?

CORS(Cross-Origin Resource Sharing)은 HTTP 헤더를 사용하여 cross-origin 접근을 허용하거나 제한하는 메커니즘이다. CORS는 cross origin으로 보내는 요청 중 조건을 만족하는 일부 요청을 제외하면 `OPTIONS` 메서드로 preflight 요청을 보내어 CORS를 지원하는지 확인한다.

### cross-origin 요청의 종류에 대해 설명해주세요?

첫번째, preflight request 두번째, preflight request를 trigger하지 않는 request 세번째, preflight request를 trigger하는 request가 있다.  

preflight request는 실제 요청에 앞서 안전한지 확인하기 위한 요청이다. `OPTIONS` 메서드를 사용하고 `Access-Control-Reqeust-Method`(실제 요청의 메서드), `Access-Control-Request-Headers`(실제 요청의 추가 헤더) 헤더를 포함한다. 서버는 `Access-Control-Allow-Origin`(해당 자원에 대해 접근을 허용하고 있는 origin), `Access-Control-Allow-Methods`(해당 자원에 대해 지원 중인 메서드, `*` 불가), `Access-Control-Allow-Headers`(해당 자원에 대해 지원 중인 헤더, `*` 불가), `Access-Control-Max-Age`(이 응답을 캐시할 수 있는 시간, `*` 불가) 헤더를 포함하여 응답한다.

preflight request를 trigger하지 않는 요청은 다음 조건을 모두 만족한다. 첫번째, `GET`, `HEAD`, `POST` 중 하나의 메서드를 사용한다. 두번째, 브라우저가 설정한 헤더와 Fetch API 명세에서 CORS-safelisted request header로 정의한 헤더(`Accept`, `Accept-Language`, `Content-Language`, `Content-Type: 'application/x-www-form-urlencoded' | 'multipart/form-data' | 'text/plain'`)만 사용한다. 세번째, 요청에서 사용하는 `XMLHttpRequestUpload` 객체에 이벤트 리스너가 등록되어 있지 않다. 네번째, 요청에 `RedableStream` 객체를 사용하지 않는다.

preflight request를 trigger하는 요청은 위 조건들을 만족하지 않는 요청인데, 한편 credential(`Cookie`와 `Authorization` 헤더)를 붙여보내려면 다음 조건을 만족해야한다. `XHMLHttpRequest`를 사용하는 경우는 `withCredentials` 플래그를 설정하고 `fetch`를 사용하는 경우 `credentials: 'include'` 옵션을 전달해야한다. 서버는 `Access-Control-Allow-Credentials: true`와 `Access-Control-Allow-Origin`(`*` 불가) 헤더를 포함하여 응답해야하며 그러지 않으면 브라우저는 응답을 무시한다.

### 클라이언트와 서버는 CORS 정책 위반을 어떻게 해결할 수 있는가?

클라이언트는 개발 환경이라면 개발 서버에 proxy를 설정해서 회피하고, 요청 헤더에 반드시 `Origin`과 credential를 포함하도록 플래그를 설정해야한다. 서버는 CORS 관련 헤더, `Access-Control-Allow-Origin`을 적절하게 설정해야한다.

## Critical Rendering Path

> 참고
>
> - [Kruno: How browsers work | JSUnconf 2017](https://youtu.be/0IsQqJ7pwhw)
> - https://github.com/alex/what-happens-when
> - [web.dev - How browsers work](How browsers work)
> - [web.dev - Critical Rendering Path](https://web.dev/critical-rendering-path/)
> - [Naver D2 - 브라우저는 어떻게 동작하는가](https://d2.naver.com/helloworld/59361)
> - [HTML 명세 - HTML 문서 파싱하기](https://html.spec.whatwg.org/multipage/parsing.html#parsing)
> - [Critical rendering path - Crash course on web performance (Fluent 2013)](https://youtu.be/PkOBnYxqj3k)
> - [브라우저는 웹페이지를 어떻게 그리나요? - Critical Rendering Path](https://m.post.naver.com/viewer/postView.nhn?volumeNo=8431285&memberNo=34176766)
> - [프론트엔드 개발자라면 알고 있어야 할 브라우저의 동작 과정](https://wormwlrm.github.io/2021/03/27/How-browsers-work.html)
> - 모던 자바스크립트 Deep Dive 38장 브라우저의 렌더링 과정
> - [v8.dev 자바스크립트 모듈](https://v8.dev/features/modules#defer)
> - [2018 Deview 웹 성능 최적화에 필요한 브라우저의 모든 것](https://tv.naver.com/v/4578425)
> - [브라우저 동작 원리와 VSync](https://coffeeandcakeandnewjeong.tistory.com/55)
> - [NHN [2018] 프런트엔드 성능 최적화](https://youtu.be/G1IWq2blu8c?feature=shared)
> - [프론트앤드 웹 성능 최적화 가이드 - 성능 지표, 데이터 로드 최적화](https://www.stevy.dev/frontend-web-performance-guide-1/)
> - [MDN - Animation performance and frame rate](https://developer.mozilla.org/en-US/docs/Web/Performance/Animation_performance_and_frame_rate)
> - [MDN - Critial rendering path](https://developer.mozilla.org/en-US/docs/Web/Performance/Critical_rendering_path)
> - [Populating the page: how browsers work](https://developer.mozilla.org/en-US/docs/Web/Performance/How_browsers_work)
> - [렌더링 성능 개선(1) — 렌더링 과정 이해하기](https://so-so.dev/web/browser-rendering-process/)

### 브라우저 구성 요소에 대해 설명해주세요?

![main components of browser](https://camo.githubusercontent.com/c118e30ed4182487e4e2a67d9209c57cda6224ad012ec226c6b579515569b99f/68747470733a2f2f7765622d6465762e696d6769782e6e65742f696d6167652f54344679564b707a7534574b46316b424e76586570626930387435322f50675058365a4d794b537746366b42387a4968422e706e673f6175746f3d666f726d6174)

`User Interface`(페이지를 그린 창을 제외한 모든 것, 주소창과 북마크 메뉴 등이다), `Browser Engine`(사용자 인터페이스와 렌더링 엔진 사이의 동작을 제어한다), `Rendering Engine`(리소스를 화면에 표시한다), `Networking`(네트워크 통신에 사용한다), `UI backend`(combo box나 window와 같은 기본적인 위젯을 그릴 때 사용한다),` JavaScript Interpreter`(자바스크립트 엔진), `Data Storage`(브라우저에서 제공하는 스토리지, Indexed DB나 모던 스토리지 등이 있다)가 있다.

### 브라우저 렌더링 과정에 대해 설명해주세요?

`Byte Stream Decoding`(브라우저가 바이트 데이터를 `Content-Type` 헤더에 지정된 문자 인코딩 방식으로 해석한다), `HTML Parsing`(HTML 파서가 문자열을 HTML 토큰으로 분해하고 DOM 노드로 변환한다. 트리 생성자가 DOM 노드로 DOM 트리를 구축한다)과 `CSS Parsing`(HTML Parsing과 같은 프로세스로 CSSOM 트리를 구축한다) 병렬 실행, `Recalculate Style`(DOM 트리와 CSSOM 트리를 사용하여 실제로 화면에 렌더링되는 요소만을 포함한 렌더 트리를 구축한다), `Layout`(렌더 트리를 순회하며 DOM 노드의 크기와 위치를 계산한다), `Painting`(레이어별로 DOM 노드를 실제 픽셀로 변환한다), `Compositing`(레이어를 합성하여 실제 화면에 타일로 나눠서 그린다).

> DOM 요소는 1000개, Compositing은 레이어가 30개 정도까지는 효율적이라고 한다.

> 렌더링 엔진은 HTML 파싱을 하면서 `<script>` 태그를 만나면 HTML 파싱을 중단하고 자바스크립트를 다운로드, 파싱, 실행한다. 그러나 다음 태그들에 대해서는 에셋의 다운로드가 HTML 파싱을 중단하지 않으며 또한 다운로드는 병렬로 이루어진다.
>
> - async `<script>`, defer `<script>`
> - `<link>`, `<style>`
> - `<img>`, `<audio>`, `<video>`

### 웹 브라우저의 레이어는 어떤 종류가 있나요?

Background Layer(배경 이미지, 색상과 같은 백그라운드 컨텐츠를 렌더링한다), Text Layer(텍스트 컨텐츠를 렌더링한다), Shadow Layer(하드웨어 가속을 사용하여 비디오 컨텐츠를 렌더링한다) 등이 있다.

### 리플로우는 언제 발생하나요?

자바스크립트로 노드를 추가하거나 삭제하는 경우, 브라우저 창을 리사이징하여 viewport 크기가 변경되는 경우, HTML 요소의 레이아웃 변경을 발생시키는 스타일을 변경하는 경우 발생한다.

### 리플로우를 발생시키는 스타일에는 무엇이 있나요?

1. 요소의 크기를 변경시키는 속성: `width`, `height`, `padding`, `margin`
2. 요소의 위치를 변경시키는 속성: `position`, `top`, `left`, `right`, `bottom`
3. 폰트 스타일 변경: `font-size`, `font-family`, `line-height`
4. 테이블 레이아웃 변경

### 리플로우를 최소화하는 방법에 대해 알려주세요?

첫번째, 리플로우를 발생시키는 CSS 속성을 최소화하고, GPU 가속을 사용하는 CSS 속성을 사용해 성능을 최적화한다. 예를 들어, `top`, `left`와 같은 속성 대신 `transform: translate()`를 사용하여 요소의 위치를 변경한다. 두번째, 스타일을 변경할 때 가능한 한 한 번에 여러 개의 속성을 변경하거나 CSS 클래스를 사용해 한 번에 여러 요소에 스타일을 적용한다.

> GPU 가속을 사용하는 CSS 속성은 다음과 같다.
> CSS Transition, CSS Transform, CSS Animation, CSS Grid, CSS Flexbox, CSS Filter, `opacity` 등

### Painting 과정을 개선해볼 수 있을까요?

GPU Rasterization(3D 모델을 2D 이미지로 변환하는 과정) 기법을 사용해볼 수 있다. 첫번째, GPU 가속을 사용하는 CSS 속성을 사용한다. 두번째, 이미지나 비디오는 최적화된 형식을 사용한다. 세번째, `<meta name="viewport" content="width=device-width">`를 사용하면 웨일, 크롬, 오페라와 같은 최신 브라우저에는 GPU를 사용해서 렌더링한다고 한다.

### HTML 렌더링 중 자바스크립트가 실행되면 렌더링이 멈추는데 그 이유가 무엇인가요?

자바스크립트가 DOM 트리에 접근하여 DOM 트리를 수정할 수 있기 때문에, HTML과 자바스크립트는 병렬로 처리하지 않는다.

### `www.naver.com`에 접속하면 어떤 과정을 거쳐 웹 페이지가 화면에 그려지는지 설명해주세요?

`URL Parsing`(사용자가 입력한 URL을 프로토콜과 도메인으로 파싱한다. 이들이 유효하지 않다면 이 텍스트를 브라우저의 기본 웹 검색 엔진에 전달한다), `DNS Lookup`, `Socket System Call`, `TCP 3-way handshake`, `TLS handshake`, `HTTP Request`(TLS 세션으로 HTML 문서 요청), `Browser Rendering`

### progressive-rendering이란?

progressive-rendering은 컨텐츠를 가능한 한 빠르게 표시하기 위해 성능을 향상시키기 위해 사용되는 기술을 총칭한다. 모든 이미지를 가져오지 않고 스크롤할 때마다 이미지를 로드하는 등 이미지를 지연 로딩하는 것이 그 예시이다.

### CSS 스프라이트에 대해 설명해주세요? 페이지를 어떻게 향상시키나요?

CSS 스프라이트는 이미지나 아이콘을 하나의 이미지로 병합하는 것이다. 요청의 개수를 줄일 수 있어 초기 로딩 시간을 단축할 수 있다.

### FOUC에 대해 설명해주세요?

FOUC(Flash of Unstyled Content)는 웹 페이지 초기 로딩 단계에서 발생하며, 일시적으로 스타일이 적용되기 전의 컨텐츠가 표시되는 현상을 가리킨다. 스타일시트의 로딩이 완료되기 전 HTML 문서의 렌더링이 완료되는 경우, 혹은 동적으로 스타일을 변경하는 경우 발생할 수 있다.

### FOUC는 어떻게 해결할 수 있나요?

첫번째, 웹 페이지 초기 로딩에 필요한 최소한의 스타일(critical CSS)을 `<head>` 내에 인라인 스타일로 포함한다. 두번째, CSS 파일을 최적화하여 다운로드 시간을 단축한다. 세번째, 미디어 쿼리를 사용하여 viewport 크기 별로 필요한 스타일을 로딩한다. 네번째, 리소스를 병렬로 다운로드할 수 없는 `@import`의 사용을 피한다.

### 정적 에셋을 최적화하는 방법에 대해 알려주세요?

첫번째, (이미지의 경우) 이미지 스프라이트를 사용하여 요청의 개수를 줄이거나 `WebP` 같은 이미지 포맷을 사용해 이미지 파일을 최적화하여 이미지 파일의 크기를 줄인다. 두번째, (JavaScript의 경우) 번들링를 사용하여 요청의 개수를 줄이거나 경량화, 압축 등을 통해 자바스크립트 파일을 최적화하여 자바스크립트 파일의 크기를 줄인다. 세번째, (web font의 경우) `woff` 같은 폰트 포맷을 사용해 web font를 최적화하여 폰트 파일의 크기를 줄인다. 네번째, CDN을 사용하여 정적 에셋의 로딩 시간을 개선한다.

### 이미지 렌더링이 느리다면 어떻게 할 수 있을까요?

첫번째, 이미지 파일을 최적화해서 이미지 파일의 크기를 줄이겠다. `WebP`와 같은 이미지 포맷을 사용해서 품질은 유지하고 파일 크기를 줄이겠다. 두번째, `img` 태그의 `srcset` 속성을 사용해서 디바이스 해상도에 따라 적절한 크기의 이미지를 사용하겠다. 세번째, CDN을 사용하여 다운로드 시간을 개선하겠다. 다섯번째, 서버사이드에서 이미지를 렌더링해서 제공하겠다.

> `WebP`는 웹 이미지를 효율적으로 압축하여 제공하기 위한 이미지 포맷이다. 로딩 시간을 개선하고 대역폭을 절약할 수 있다.

### 이미지를 지연 로딩하는 방법에 대해 설명해주세요?

첫번째, `<img>` 태그의 `loading` 속성을 사용한다. 두번째, IntersectionObserver API를 사용한다.

### 자바스크립트는 어떻게 최적화할 수 있나요?

첫번째, 트리 쉐이킹으로 중복되는 코드를 제거한다. 두번째, 코드 스플리팅으로 초기 로딩에 필요한 스크립트가 아니면 지연 로딩한다. 세번째, 주석이나 공백과 같은 문자를 제거하거나 변수 이름을 축약한다(경량화). 네번째, `.gzip`과 같은 확장자를 사용하여 압축한다.

### web font는 어떻게 최적화하나요?

첫번째, 압축률이 좋은 폰트 포맷으로 제공하겠다. 두번째, `local` 문법을 사용하여 로컬에 설치되어있다면 다운로드하지 않도록 한다. 세번째, 서브셋 폰트(많이 사용하지 않은  문자는 제거한 버전)를 사용한다. 네번째, 필요한 굵기와 스타일의 폰트만 다운로드하겠다. 다섯번째, `<link>` 태그의 `rel="preload"`를 적용하여 다른 자원보다 우선순위를 높인다.

> 참고
>
> - https://whales.tistory.com/66

### Web Font를 제공할 때 어떤 포맷으로 제공할 것인가요?

`woff2`, `woff`, `ttf`, `eot`로 지원하겠다. IE8 이하를 지원해야한다면 `eot`를 먼저 선언을 하고, 압축률이 좋은 `woff2`, `woff`를 선언한 후 마지막으로 `ttf`를 선언하겠다.

> woff는 Web Open Font Format의 약어이다.

### 페이지 로드 시간을 줄이는 방법에 대해 아는 대로 설명해주세요?

> 정적 에셋을 최적화(요청의 개수와 리소스의 크기를 줄이고)하고 CPR을 최적화한다.

첫번째, 불필요한 리소스는 제거한다. 두번째, 정적 에셋은 CDN을 사용하여 로딩 시간을 개선한다. 세번째, 이미지 최적화, 이미지 스프라이트를 사용하여 로딩 시간을 개선한다. 네번째, 자바스크립트 최적화, 번들링을 사용하여 로딩 시간을 개선한다. 다섯번째, 이미지와 비디오와 같은 무거운 리소스나 초기 로딩에 필요하지 않은 리소스는 지연 로딩한다. 여섯번째, CSS `<link>` 태그는 `<head>` 태그 안에 위치시킨다. 일곱번째, `<script>` 태그는 `defer`로 지정하거나 `<body>` 종료 태그 바로 앞에 삽입한다.

### 만드신 서비스가 느리다는 피드백을 받았다면 어떤 것이 원인이었을까요?

어떤 점에서 느리다는 평가를 받았을까요? 초기 렌더링이 느렸을까요 아니면 사용자와의 상호작용 같은 곳에서 버벅거림이나 지연이 발생했을까요? (전자면 로딩 최적화, 후자면 렌더링 최적화에 대한 것임)

> 로딩 최적화와 렌더링 최적화 참고
>
> - https://ui.toast.com/fe-guide/ko_PERFORMANCE

### 간단한 슬라이드쇼 페이지를 만드는 방법에 대해 얘기해보세요?

컨테이너 요소 안에 이미지들을 나열해놓고 `setInterval`로 일정 시간마다 인덱스를 옮기며 `opacity`를 조절해볼 수 있겠다.

- [ ] 렌더링이 느리다는 평가를 받았다면 어떤 것이 원인이었을까요?
- [ ] AMP에 대해 설명해주세요?

## 기타

### SPA과 CSR의 차이점은 무엇인가요?

SPA(Single Page Application)는 페이지를 처음 한 번 로드한 후에는 페이지를 다시 로드하지 않고 애플리케이션 내에서 동적으로 페이지를 업데이트하는 방식이다. CSR(Client-Side Rendering)은 전체 웹 페이지의 렌더링을 클라이언트가 처리하는 방식으로, 초기 HTML에 자바스크립트를 실행하여 컨텐츠를 동적으로 생성하고 페이지에 추가한다. 비교 대상이 아니다.

### SSR과 CSR의 차이에 대해 알려주세요?

SSR(Server-Side Rendering)는 서버가 동적인 컨텐츠를 포함해서 완전한 웹 페이지의 HTML을 생성하고 이를 클라이언트에게 전달한다. 초기 로딩 시간이 빠르고, SEO에 유리하다. CSR(Client-Side Rendering)은 클라이언트에서 서버로부터 받은 초기 HTML에 JavaScript를 실행하여 동적으로 컨텐츠를 생성하고 페이지에 렌더링하는 것이다. 초기 로딩 시간이 비교적 느리지만 동적인 기능을 제공하기에 좋다.

### 크로스 브라우징에 대해 설명해주세요? 

크로스 브라우징(cross browsing)은 웹 표준을 적용하여 서로 다른 운영체제와 플랫폼에 대응하는 것이다.

### SEO가 무엇인가요?

SEO(Search Engine Optimization)은 검색 엔진이 페이지에서 데이터를 잘 수집하여 검색 결과에서 상위에 나타날 수 있도록 페이지를 구성하는 작업이다. SPA는 동적으로 컨텐츠를 생성하므로 SEO에 취약하므로, 첫 페이지만 SSR을 사용하면 이 문제를 해결할 수 있다.

### PWA에 대해 설명해주세요?

PWA(Progressive Web App)은 네이티브 앱에 가까운 사용자 경험을 제공하는 웹 애플리케이션이다. 서비스 워커(Service Worker)를 사용하여 오프라인 액세스나 푸쉬 알림을 제공하고 홈 화면 아이콘이나 네비게이션 같은 모바일 특화 기능을 제공한다.

## 이미지 파일 포맷

### 래스터 파일 포맷과 벡터 파일 포맷에 대해 설명해주세요?

래스터와 벡터는 모두 디지털 이미지 파일 포맷이다. 래스터(Raster) 파일의 이미지는 일정한 수의 픽셀로 구성된다. 때문에 크기를 조정하면 이미지가 왜곡되거나 흐려질 수 있다. 파일에 포함된 픽셀 수가 많을수록 품질이 높아지지만 파일 크기가 커지고 로딩 속도가 느려질 수 있다. 대표적인 파일 확장자로 JPEG, PNG, GIF, WebP가 있다. 벡터(Vector) 파일의 이미지는 수학적 공식에 기반하여 그리드에 고정된 점을 사용한 직선과 곡선으로 구성된다. 때문에 크기를 조정해도 해상도가 손실되지 않는다. 대표적인 파일 확장자로 PDF, SVG가 있다.

> 참고
>
> - [Adobe 래스터 파일](https://www.adobe.com/kr/creativecloud/file-types/image/raster.html)
> - [Adobe 벡터 파일](https://www.adobe.com/kr/creativecloud/file-types/image/vector.html)

### JPEG, PNG에 대해 설명해주세요?

JPEG과 PNG는 모두 래스터 이미지 파일이다. JPEG(Joint Photographic Experts Group)는 손실 압축을 사용하므로 파일 크기가 작아 웹 상에서 공유하기 적절하나 원본의 품질이 훼손될 수 있다. EXIF 데이터를 지원하지만 투명 배경은 지원하지 않는다. 일반적으로 디지털 이미지를 저장하기에 적합하다. 파일 확장자로 `.jpg`, `.jpeg`, `jpe` 등이 있다. PNG(Portable Network Graphic)는 무손실 압축을 사용하여 원본 데이터를 유지할 수 있으나 JPEG보다 파일 크기가 훨씬 크다. 투명 배경을 지원하지만 EXIF 데이터는 지원하지 않는다. 웹 사이트에서 디테일한 그래픽과 차트를 표시하는 등 웹 그래픽용으로 사용하기 적합하다. 파일 확장자는 `.png`이다.

> EXIF(Exchangeable image file format) 데이터는 이미지가 생성된 날짜와 시간, 사진이 촬영된 위치 정보, 제조사, 모델, 조리개, ISO 속도 등의 카메라 설정 등의 메타 데이터를 말한다.

> 참고
>
> - [Adobe JPEG 파일](https://www.adobe.com/kr/creativecloud/file-types/image/raster/jpeg-file.html)
> - [Adobe PNG 파일](https://www.adobe.com/kr/creativecloud/file-types/image/raster/png-file.html)
> - [Adobe JEPG vs. PNG](https://www.adobe.com/kr/creativecloud/file-types/image/comparison/jpeg-vs-png.html)

### SVG에 대해 설명해주세요?

SVG는 무손실 압축을 사용하는 벡터 이미지 파일로, 품질을 유지하면서 크기를 조정할 수 있어 로고와 같은 웹 그래픽에 적합하며 래스터 이미지보다 크기가 작다. 또한 SVG는 XML로 작성되어 검색 엔진이 읽을 수 있어 SEO에 유리하다. 그러나 픽셀이 부족하므로 고품질 디지털 사진을 표현하는데는 적합하지 않으며 레거시 브라우저에서는 호환되지 않는다. 파일 확장자는 `.svg`이다.

> 참고
>
> - [Adobe SVG 파일](https://www.adobe.com/kr/creativecloud/file-types/image/vector/svg-file.html)
> - [Adobe PNG vs. SVG](https://www.adobe.com/kr/creativecloud/file-types/image/comparison/png-vs-svg.html)
