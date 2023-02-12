# 📣 실시간 모니터링 시스템을 만들며 정복하는 MEVN
## Node.js의 기본
### 비동기적 이벤트 주도 방식
- nodejs에서는 이벤트를 이벤트 큐에서 처리. 즉 A(10ms),B(3ms),C(8ms)의 요청이 있다면, nodejs는 이 세가지 요청을 하나의 스레드, 즉 싱글 스레드로 모두 이벤트 큐에 넣고 먼저 완료되는 
요청을 우선적으로 끄집어 내어 결과적으로 B,C,A의 순으로 결과가 나온다. 이처럼 큐에 넣고 이벤트를 처리하면서 완료되는 순서대로 요청을 처리하는 것이 비동기적 이벤트 주도 방식이다.<br>
### 논블로킹 I/O 모델
- 위의 비동기적 이벤트는 I/O모델에서 작동한다. 이는 I/O bound를 처리하는 모델로 fs, network, DB 작업을 일컫는다. 이에 해당하는 요청을 실행하는 동안 블로킹, 즉 중단되는 행위가
벌어지지 않는다. 예를 들어 사용자가 페이지에서 버튼을 클릭해서 파일을 다운로드 할때, 버튼을 클릭하고 파일을 다운로드하는 동안 페이지에 랙이 걸리는 등의 행위가 발생되는 않는다. 반대로
블로킹 I/O모델은 요청을 처리하는 동안 스레드를 점유하기 때문에 동시요청을 처리하기 위해 응답시간이 느려지거나 서버가 중단될 수 도 있다.
### 구글 V8 Engine
- 일처리하는 엔진. 크롬 등 많이 사용중임. JIT(just in time) 즉 프로그램을 실행하는 시점에서 기계어로 번역하는 컴파일 기법이란 특징이 있다.
### 자바스크립트 런타임
- 런타임이란 프로그램이 실행될때 프로그램이 머무는 공간을 의미. 브라우저가 자바스크립트의 런타임이기도 함. 브라우저 공간안에서 js 프로그램을 실행 가능하기 때문이다. 즉 자바스크립트로 
만든 게임, 알고리즘, 서버 등 많은 것을 실행할 수 있다. 

## Express로 서버구축 및 로거
### express?
- node.js에서 동작하는 웹 프레임워크 중 가장 많이 사용되며 유연하고 http유틸 함수를 이용해 api를 쉽고 빠르게 만들 수 있다.
- 미들웨어란 ? 톨게이트와 같다. 차선이 확장되기전 톨게이트를 거치는 것처럼 하나의 로직을 거침으로써 일일이 무언가를 설정하지 않아도 된다.
- 미들웨어는 어떤 로직 계층을 중간에 넣는 것으로 ,  3000번 서버로 요청했을 때 이하 로직이 실행되게 만든 것을 의미.

## Vue.js
### SPA(single page application)
- 최초의 정적 리소스를 다운로드를 한번에 하고 새로운 페이지 요청 시 페이지 갱신에 필요한 데이터만을 전달받아 페이지를 갱신함.
- 즉 트레픽을 줄이고, 전체를 렌더링할 필요가 없으므로 UX가 향상되어 사용자 경험의 질이 높아짐.
- 단점으로는 모든 리소스를 최초에 다 다운로드하기 때문에 느릴 수 밖에 없음. 서버 사이드 렌더링이 아니므로 SEO에 불리하다.
- MVVM 디자인 패턴 : model, view, viewmodel로 이루어진 패턴
- 사용자가 보는 페이지, 데이터처리, 이들을 중간에서 제어하는 뷰모델

### virtual DOM, 데이터 중심 그리고 컴포넌트 기반
- vue.js에서는 뷰인스턴스로 관리하는 DOM에 대해 가상돔이라는 가상 객체를 만들어 기존의 DOM과 업데이트된 DOM을 매우 빠르게 비교해서 바꾸는 작업을 쉽게 한다.
- 양방향 바인딩을 적용하여 데이터 중심으로만 생각가능하다. 즉 데이터가 갱신되었을때 DOM이 알아서 갱신되거나, 입력폼등 DOM의 데이터가 갱신되어도 실제 데이터가 변경된다. <br>
💡 데이터 바인딩이란?  화면상에 보여지는 데이터(View)와 브라우저 메모리에 있는 데이터(Model)를 묶어서(Binding) 서로 간의 데이터를 동기화하는 것을 의미합니다. 예를 들어서 HTML에서 서버 혹은 스크립트상에서 받아온 데이터를 화면상에 그려주고 있다고 가정을 했을 때, 해당 값이 변경이 될 경우 다시 HTML 상에 데이터(값)를 변경된 값에 따라서 맞추어 주는 동작을 '데이터 바인딩'이라고 합니다.
- 뷰인스턴스 : vue가 DOM을 관리하도록 부리는 일꾼이다. vue 인스턴스로 관리할 특정 DOM을 설정할 수 있다.
- 컴포넌트 기반 : .vue 확장자로 이루어진 코드는 다음과 같다. template script style

### 라이프사이클과 composition API
- vue의 라이프 사이클은 다음과 같다. beforeCreate, created, beforeMount, mounted, beforeUpdated, beforeDestroy, destroyed
- created : 컴포넌트가 생성된 단계. DOM에 vue인스턴스가 붙지 않아서 주로 ajax요청으로 데티어를 fetch하는데 쓰인다.
- mounted : 컴포넌트 및 DOM에 인스턴스까지 붙은 상태. 부모 컨포넌트가 created된 후 자식 컴포넌트의 created, mounted 훅이 시작되고 이후 부모 컨포넌트의 mounted가 시작된다.
- composition API : vue.js 3.0 부터는 created, mounted 에서 setup, onMounted를 사용한다.