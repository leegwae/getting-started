# etc

## TOC

- [프로젝트 기본 질문](#프로젝트-기본-질문)
- [프로젝트 기술 질문](#프로젝트-기술-질문)
- [개발 상식](#개발-상식)
- [컬쳐핏 및 역량](#컬쳐핏-및-역량)

## 프로젝트 기본 질문

- [ ] 프로젝트에서 함께 한 사람은 누구이고, 어떤 서비스인지 설명해주세요?
- [ ] 프로젝트에서 사용한 라이브러리의 버전은 몇인가요?
- [ ] 다른 라이브러리도 있는데 왜 그 라이브러리를 선택했나요?
- [ ] 다른 프로젝트할 때도 그 라이브러리를 선택하실건가요?
- [ ] 프로젝트를 하면서 어떤 것을 배웠나요?
- [ ] 지금 프로젝트에 어떤 문제가 있나요?
- [ ] 프로젝트를 진행하면서 가장 어려웠던 경험에 대해 소개해주세요?
- [ ] 배포 아키텍처에 대해 설명해주세요?
- [ ] 성능 최적화한 경험이 있다면 설명해주세요?
- [ ] CI/CD 파이프라인을 구축한 경험이 있나요?
- [ ] 자신 있는 프론트엔드 기술이 있나요? 어느 정도로 사용할 수 있나요?
- [ ] TDD 적용하게 된 계기가 있을까요?
- [ ] TDD 적용해보니까 어떠셨나요? 느꼈던 장점과 단점에 대해 말씀해주세요
- [ ] 테스트 코드 작성하면서 어떤 점이 어려웠나요?
- [ ] 테스트 코드를 작성할 때 보통 어떤 기준을 가지고 작성하시나요?
- [ ] 이력서에 적힌 모든 문장에 대하여 질문과 답변 만들어보기

## 프로젝트 기술 질문

### 왜 패키지 매니저로 Yarn을 선택했나요?

첫번째, npm은 패키지를 순차적으로 설치하지만 yarn은 패키지 설치를 병렬로 진행하므로 훨씬 빠르다. 두번째, 모노 레포를 구성하려했는데 당시에는 npm workspace보다 yarn workspace 레퍼런스가 더 많았다.

### Zustand는 어떻게 동작하는가?

내부적으로로는 publish/subscribe 패턴의 스토어를 사용하고, 훅들이 클로저로서 이 스토어를 참조하고 있다.

> 참고
>
> - [React 상태 관리 라이브러리 Zustand의 코드를 파헤쳐보자](https://ui.toast.com/posts/ko_20210812)

### AWS에서 EC2와 S3, CloudFront는 무엇인가요?

EC2는 가상 서버(실제 하드웨어와 유사한 동작을 하는 소프트웨어 기반의 가상 환경에서 실행되는 가상 컴퓨터)를 제공하는 서비스이고 S3는 클라우드 기반의 스토리지 서비스이다. CloudFront는 정적 에셋을 빠르게 서빙하기 위한 CDN 서비스이다. EC2에서는 다양한 OS나 애플리케이션을 실행할 수 있고 S3는 정적 에셋을 서빙하는데 사용할 수 있다. S3와 CloudFront를 연동하면 S3에 직접적으로 접근하는 것보다 빠르다.

### Socket.io와 WebSocket의 차이가 무엇인가요?

Socket.io는 서버와 클라이언트 간의 양방향 통신을 제공하는 라이브러리이고 HTML5 WebSocket은 HTTP를 기반으로 서버와 클라이언트 간의 양방향 통신을 제공하는 애플리케이션 계층의 데이터 전송 프로토콜이다. Socket.io는 내부적으로 WebSocket을 사용하고 fallback으로 HTTP 기반 long polling을 사용한다.

### Webpack은 어떻게 동작하는가?

Webpack은 내부적으로 플러그인을 기반으로 한 컴파일러로 파일을 번들링하기 위해 라이프사이클을 가진다. 첫번째, 컴파일러가 설정 파일의 진입점으로부터 컴파일을 시작한다. 두번째, Resolver가 상대 경로를 절대 경로로 변환한다. 모듈 팩토리가 파일의 크기, 종류, 경로 등을 담은 모듈 객체를 만든다. 트랜스파일러가 파일의 종류에 따라 파일을 브라우저가 읽을 수 있는 형태로 트랜스파일한다. 세번째, 파서가 파일을 파싱하여 `require`나 `import`문을 찾아 모듈 객체의 의존성 정보를 갱신해 의존성 그래프를 만든다. 네번째, 의존성 그래프를 위상 정렬하여 청크로 변환하고 청크를 병합해 번들 파일을 만든다. 다섯번째, 번들 파일에 경량화나 트리 쉐이킹 등 후처리를 수행한다.

> 참고
>
> - [How Webpack works](https://github.com/leegwae/til/blob/main/How%20Webpack%20works.md)

### Webpack의 장점과 단점이 무엇인가요?

Webpack의 장점 첫번째, 자바스크립트 아닌 다른 의존성을 번들할 수 있다. 두번째, 개발 서버, HMR, 최적화(트리 쉐이킹, 지연 로딩, 코드 스플리팅, 경량화) 지원, 생태계 안정적이다. Webpack의 단점 첫번째, 설정이 번거롭고 ESM 출력을 지원하지 않는다. 두번째, 자바스크립트로 작성된 컴파일러이므로 느리다.

### React Query가 무엇인가요?

비동기 상태를 관리할 수 있는 전역 상태 라이브러리이다. stale-while-revalidate 웹 캐싱 전략의 구현체이다.

### Stale-While-Revalidate 전략이란 무엇인가요?

만료된 후에도 캐싱된 리소스를 보여준 후 백그라운드에서는 서버에 재검증 요청을 보내어 리소스의 유효성을 확인하는 것이다. HTTP 응답 헤더의 `Cache-Control`을 통해 설정할 수 있다. 

### 왜 React Query를 선택했나요?

 React의 `useEffect`만으로도 네트워크 요청을 처리할 수 있지만 적절하지는 않다. 그 이유는 첫번째, 경쟁 상태가 나타날 수 있다. 두번째, 캐싱이나 중복 요청 등을 직접 구현해야한다. 세번째, 전역 상태로 관리할 경우 클라이언트 로컬 상태와 구분되지 않고 전역 상태 코드에도 비동기 로직이 많아진다. React Query는 `useQuery`를 통해서 서버 상태를 손쉽게 관리하고 쿼리 클라이언트를 통해 전역 상태로 사용할 수 있다.

## 개발 상식

### 컴파일러와 트랜스파일러의 개념에 대해 설명해주세요?

컴파일러는 언어를 다른 추상화 수준의 언어로 바꾸는 것이다. 예를 들어 C 언어에서 컴파일러는 코드를 어셈블리어로 변환한다. 트랜스파일러는 언어를 비슷한 수준의 언어로 바꾸는 것이다. 예를 들어 TypeScript를 JavaScript로 변환한다.

### 객체 지향의 특징에 대해 설명해주세요?

객체 지향의 특징에는 상속, 캡슐화, 다형성, 추상화가 있다. 상속은 자식 클래스가 부모 클래스의 속성과 기능을 사용할 수 있는 것이다. 이를 통해 코드의 중복을 줄이고 재사용성을 높인다. 예를 들어, "동물" 클래스에서 "강아지" 및 "고양이" 클래스를 생성하고, 공통된 특성과 동작을 상속받을 수 있다. 캡슐화는 데이터와 데이터에 접근하는 메서드를 그룹화하고 그 세부 구현 내용은 은닉하는 것이다. 예를 들어, 클래스 내부에 비공개(private) 변수를 선언하고, getter와 setter 메서드를 사용하여 데이터에 접근 및 수정을 허용할 수 있다. 다형성은 오버라이딩이나 오버로딩으로 메서드를 확장하거나 다른 형태로 정의할 수 있는 것이다. 예를 들어, 여러 도형 객체를 동일한 `calculateArea` 메서드를 사용하여 다룰 수 있다. 추상화는 객체의 공통적인 속성과 기능을 데이터와 메서드로 추출하는 것이다. 예를 들어, "자동차" 클래스는 실제 자동차의 핵심 기능과 특성을 추상화하여 표현한다.

### 오버로딩과 오버라이딩의 차이에 대해 설명해주세요?

오버로딩(overloading)은 이름이 같은 메서드를 다양한 시그니처(매개변수, 반환값)로 정의하는 것이다. 오버라이딩(overriding)은 자식 클래스가 상속받은 메서드를 재정의하거나 확장하는 것이다.

### SOLID 원칙에 대해서 설명해주세요?

SOLID 원칙은 객체 지향 설계를 바람직하게 만들기 위한 설계 원칙이다. 단일 책임 원칙은 클래스는 하나의 책임만 가져야한다는 원칙이다. 개방/폐쇄 원칙은 새로운 기능을 추가할 때 기존  코드를 수정하지 않고 확장할 수 있어야한다는 원칙이다. 리스코프 치환 원칙은 파생 클래스가 상위 클래스를 대체할 수 있어야한다는 원칙이다. 인터페이스 분리 원칙은 클래스는 자신이 사용하지 않는 인터페이스는 구현하지 않는다는 원칙이다. 이를 위해 인터페이스는 작고 단일한 책임을 가진다. 의존성 역전의 원칙은 모듈 간의 의존성을 느슨하게 작성해야한다는 원칙이다.

### 문자 인코딩이란 무엇이고 어떤 종류가 있는가?

문자 인코딩(Character Encoding)은 문자나 기호를 컴퓨터가 처리할 수 있는 비트로 나타내는 과정이다. 문자 인코딩에는 ASCII, UTF-8 등이 있다.

### ASCII란 무엇인가?

ASCII는 7비트의 문자를 사용하여 128개의 문자를 인코당하는 문자 인코딩 방식이다. 그러나 1바이트로는 세계의 모든 기호나 문자를 사용할 수 없기 때문에 2바이트 이상을 사용하는 한글과 같은 경우 글자가 깨지는 문제가 발생한다.

### 유니코드란 무엇인가?

유니코드는 전 세계의 모든 문자와 기호를 2바이트에 매핑한 것이다. 유니코드 문자를 인코딩하는 방식에 UTF-8과 UTF-16이 있다.

### 가변 길이 유니코드 방식과 UTF-8과 UTF-16에 대해 설명해주세요?

가변 길이 유니코드 방식은 고정 길이를 사용하지 않은 유니코드 인코딩 방식으로 UTF-8과 UTF-16이 있다. UTF-8은 1바이트부터 4바이트로 한 개의 문자를 나타낸다. 예를 들어 영문자는 1바이트, 한글은 3바이트로 나타낸다. UTF-16은 2바이트에서 4바이트로 나타낸다. 예를 들어 한글과 영문자 모두 2바이트로 처리할 수 있다.

### 블로킹과 논블로킹에 대해 알려주세요?

블로킹은 작업을 실행하기 위해 다른 작업의 실행을 차단하는 것이다. 예를 들어 입출력이 있다. 논블로킹은 작업을 실행하기 위해 다른 작업의 실행을 차단하지 않아도 되는 것이다. 예를 들어 브라우저가 Ajax 통신하는 동안 사용자는 애플리케이션 계속 사용할 수 있다.

### 동기 함수와 비동기 함수의 차이에 대해 설명해주세요?

동기 함수는 호출한 함수가 종료된 후 다음 함수를 호출한다. 프로그램이 일반적으로 순차적으로 실행되는 것과 같다. 비동기 함수는 호출한 함수가 종료되지 않아도 다음 함수를 호출할 수 있는 것이다. 브라우저에서는 네트워크 요청을 하고 있는 동안에도 사용자의 이벤트를 처리할 수 있다.

### 프레임워크와 라이브러리의 차이에 대해 설명해주세요?

프레임워크는 프로젝트의 구조를 강제하지만 라이브러리는 그렇지 않다. 예를 들어 React는 라이브러리로 다른 라이브러리와 함께 사용할 수 있다. Next.js는 프레임워크는 디렉토리 구조를 강제한다.

### MVC 디자인 패턴과 MVP 디자인 패턴, MVVM 디자인 패턴에 대해 설명해주세요?

MVC(Model-View-Controller)는 애플리케이션을 관심사에 따라 Model, View, Controller로 나누는 디자인 패턴이다. View는 사용자 인터페이스를 담당하며 Model은 데이터와 비지니스 로직을 처리한다. Controller는 사용자의 입력을 받아 Model을 조작하며, 이 변경은 View에 갱신된다. Model과 View가 강결합되어있다는 문제가 있다.

MVP(Model-View-Presenter)는 애플리케이션을 Model, View, Presenter로 나누는 디자인 패턴이다. Model은 MVC와 같으며, View는 사용자 인터페이스를 담당하고 사용자의 입력을 처리해 이벤트를 발생시킨다. Presenter는 MVC의 Controller를 대체한 것으로, Model과 View 사이의 중재자 역할을 한다. View와 Model을 연결하며 View에서 이벤트가 발생하면 이를 처리한다. View와 Presenter 사이의 의존성이 높다는 문제가 있다.

MVVM(Model-View-ViewModel)은 애플리케이션을 Model, View, ViewModel로 나누는 디자인 패턴이다. ViewModel는 Model과 View 사이의 중재자 역할을 한다. View에 표시할 데이터를 가지고 View의 상태와 동작을 제어한다. View와 ViewModel은 양방향 데이터 바인딩으로 연결되어있다.

> 참고
>
> - https://opentutorials.org/course/697/3828

### 옵저버 패턴에 대해 설명해주세요, 어떻게 구현할 수 있을까요?

옵저버(Observer) 패턴은 한 명의 게시자와 다수의 구독자로 이루어지며 게시자가 데이터에 변경이 있을 때마다 모든 구독자에게 그 사실을 공지하는 디자인 패턴이다.

```typescript
class Subject {
	observers = [];

	subscribe(observer) {
		this.observers.push(observer);
	}

	unsubscribe(observer) {
		this.observers = this.observers.filter(item => item !== observer);
	}

	notifyAll() {
		this.observers.forEach(observer => {
			observer.notify();
		});
	}
}

class Observer {
	constructor(id) {
		this.id = id;
	}
	
	notify() {
		console.log(`Observer ${this.id} has been notified!`);
	}
}

const subject = new Subject();
const observer1 = new Observer(1);
const observer2 = new Observer(2);

subject.subscribe(observer1);
subject.subscribe(observer2);

subject.notifyAll();
// Observer 1 has been notified!
// Observer 2 has been notified!
```

### 싱글톤 패턴에 대해 설명해주세요, 어떻게 구현할 수 있을까요?

싱글톤(singleton) 패턴은 특정 클래스의 인스턴스가 하나만 생성되도록 하는 디자인 패턴이다. 자바스크립트에서는 `static` 멤버를 사용하여 구현해볼 수 있다.

```typescript
class GameManager {
  static #instance = null;

  constructor() {
    if (GameManager.#instance === null) GameManager.#instance = this;
    return GameManager.#instance;
  }
}
```

### 매개변수와 인자의 차이에 대해 설명해주세요?

매개변수(parameter)는 함수 정의에서 선언된 변수이다. 인자(argument)는 함수를 호출할 때 함수 내부로 전달되는 실제 값이다.

### Call by Value, Call by Reference, Call by Sharing에 대해 설명해주세요?

Call by Value는 인자에 복사된 값을 전달하는 평가 전략이다. 함수 내부에서의 변경은 호출자에게 가시적이지 않다. Call by Reference는 인자에 참조값을 전달하는 평가 전략이다. 함수 내부에서의 변경은 호출자에게 가시적이다. Call by Sharing은 자바스크립트의 평가 전략을 설명하기 위해 사용하는 용어이다. 자바스크립트는 기본적으로 Call by Value를 사용하지만 전달된 객체의 프로퍼티를 수정했을 경우엔 그 변경이 호출자에게 가시적이다.

### 애자일 프로세스에 대해 설명해주세요?

애자일은 개발 과정을 짧은 주기의 사이클로 나누고 반복하는 소프트웨어 개발 방법론이다. 하나의 반복주기는 분석, 설계, 구현, 테스트로 이루어지고, 반복주기마다 완성된 기능을 산출한다.

### 스크럼 프로세스에 대해 설명해주세요?

스크럼 방법론은 애자일의 일종으로 대개 매일 어제 한 일, 오늘 할 일, 장애 현상 등을 공유하는 미팅을 가지는데 이를 스크럼이라고 하며 반복주기는 스프린트라고 한다. 스크럼 프로세스는 백로그를 작성하고 스프린트를 진행한 후, 스프린트를 리뷰하고 회고하는 과정으로 이루어진다.

### 함수형 프로그래밍에 대해 설명해주세요?

함수형 프로그래밍은 순수 함수와 부수 효과로 이루어진다. 외부 상태에 의존하거나 외부 상태를 변경하는 함수는 부수 효과(side effect)가 있다고 한다. 순수 함수는 부수 효과가 없는 함수이다. 어떤 외부 상태에도 의존하지 않고 전달된 인수에만 의존하여 계산하기 때문에 동일한 입력에 대해 항상 동일한 출력을 반환한다. 함수형 프로그래밍을 사용하면 예상치 못한 오류를 디버깅하기 용이하다.

> 출처
>
> - 모던 자바스크립트 Deep Dive 12.7.5 순수 함수와 비순수 함수

### CI/CD에 대해 설명해주세요?

CI/CD는 Continuous Integration(지속적 통합)과 Continuous Deployment(지속적 배포)의 약어로, 소프트웨어의 개발과 배포 프로세스를 자동화하고 향상시키는 소프트웨어 개발 방법론이다. CI는 공유 레포지토리에 지속적으로 코드를 통합하는 프로세스이다. CD는 소프트웨어를 자동으로 배포하는 프로세스이다. CI/CD의 장점은 첫번째, 프로세스를 자동화하기 때문에 휴먼 에러를 방지하고 일관성을 유지할 수 있다. 두번째, 지속적으로 코드의 변경 사항을 반영하고 테스트하므로 빠르게 오류를 포착할 수 있다. 세번째, 롤백 등을 통해 배포에서 발생한 문제를 빠르게 해결할 수 있다.

### TDD란 무엇인가요? TDD는 어떤 장점이 있나요?

TDD는 Test Driven Development의 약자로 테스트를 먼저 작성하는 개발 방법론이다. 우선 실패하는 테스트를 작성한 후 테스트가 통과하도록 코드를 최대한 빠르게 작성하고, 중복을 제거하는 등 리팩토링을 진행하는 과정을 반복한다. TDD의 장점은 첫번째, 코드를 유지보수와 확장에 용이하도록 작성할 수 있다. 두번째, 코드를 문서화하여 동료들이 코드를 이해하는데 도움을 줄 수 있다.

## 컬쳐핏 및 역량

> 🎀은 거의 모든 면접에서 출제되었음

- [ ] 🎀자기소개해주세요? / 간단하게 자기소개해주세요?
- [ ] 🎀(비전공자나 복수전공자의 경우) 철학과인데 왜 개발자를 진로로 선택하게 되셨나요? / 철학과인데 왜 컴퓨터과학부 복수전공하시나요?
- [ ] 지원자는 어떤 사람이신가요? / 성격이 어떠신가요?
  - [ ] 예시가 있을까요?
- [ ] 평소에 어떻게 시간 보내세요? / 여가시간에 뭐하세요?
- [ ] 스트레스는 어떻게 관리하고 있나요?
- [ ] 최근에 재밌게 읽었던 책이나 살면서 가장 재밌게 읽었던 책이 있나요?
- [ ] 본인이 프론트엔드 개발자로서 가진 강점을 무엇이라고 생각하나요?
- [ ] 백엔드에는 어느 정도의 역량이 있나요?
- [ ] 알고리즘에 어느 정도의 역량이 있나요?
- [ ] 🎀회사에 대해 알고 계신가요?
  - [ ] 회사가 제공하는 서비스에 대해 설명해주세요?
  - [ ] 회사가 제공하는 서비스를 사용해본 적이 있나요?
  - [ ] 최근에 봤던 회사 관련 뉴스 생각나는게 무엇인가요?
- [ ] 🎀회사의 가치관/인재상에 대해 알고 계신가요?
  - [ ] 인재상에서 본인과 가장 잘 어울리는 것을 뽑고 뒷받침할 수 있는 사례를 공유해주세요
- [ ] 회사의 장점과 단점에 대해 설명해주세요?
- [ ] 🎀왜 이 회사를 선택했나요?
- [ ] 🎀회사에 지원하게 된 계기가 있을까요?
- [ ] 🎀회사를 선택하는 기준이 있나요?
- [ ] 이 회사를 선택하지 않는다면 이유가 무엇인가요?
- [ ] 회사에서 써보고 싶은 기술이 있나요?
- [ ] 회사에서 맡아보고 싶은 업무가 있나요?
- [ ] 이 회사에 지원하여 어떤 성장을 하고 어떤 것을 얻을 수 있다고 생각했나요?
- [ ] 회사에서 더 이상 배울 게 없는 경우엔 어떻게 할 계획인가요?
- [ ] 좋은 개발 문화는 무엇이라고 생각하나요?
- [ ] 🎀좋은 코드란 무엇이라고 생각하나요?
- [ ] 🎀요즘 관심 있는 기술이 무엇인가요? / 요즘 공부하고 있는 게 있나요?
- [ ] 사용해본 적 없는 기술을 학습하고 적용하는 과정에 대해 말씀해주세요?
- [ ] Figma를 사용한다고 했을 때 디자이너에게 무엇을 요구할 것인가요?
- [ ] 개발 과정에서 우선순위를 어떻게 두고 있나요?
- [ ] 어떤 사람과 일할 때 잘 맞았나요?
- [ ] 어떤 사람과 일할 때 잘 맞지 않았나요?
- [ ] 동료에게 "지원자의 장점은 무엇이고 단점은 무엇인가요?" 라고 묻는다면, 어떻게 대답할 것 같나요? 
- [ ] 인생에서 가장 열심히 해본 일이 무엇인가요?
- [ ] 🎀목표하는 커리어가 있나요? / 5년, 10년 뒤 어떤 개발자가 되어있을 것 같나요?
- [ ] 인생에서 실패한 경험을 말씀해주세요
- [ ] 🎀회사에 궁금한 점이 있나요?
