# Front-end 개발에 필요한 패키지

## 개요
- Front-end 개발은 '브라우저 위에서 돌아가는 프로그램' 을 개발하는 것 이라고 할 수 있다.
  - 따라서 코드가 구동되는 환경인 '브라우저' 의 영향을 많이 받게 된다.
- JavaScript 언어가 계속 버전업 되면서 신기능은 추가되는데, 브라우저는 그대로이다.
  - 오래된 브라우저를 쓰는 유저는 내 최신 코드를 실행하지 못하는 문제가 생길 수도 있다.
  - 결국 오래된 브라우저까지 지원하려면 오래된 JavaScript 버전을 사용해야 하는데?
- 위 모든 단점을 극복하는 방향으로 Front-end 개발은 발전해왔고, 발전하고 있다.
  - 프론트엔드 개발의 생산성이 향상되도록
  - 개발자가 모든 브라우저를 일일이 신경쓰지 않도록
  - 브라우저에서 코드가 빠르게 돌아갈 수 있도록

## Babel
- Babel is a JavaScript compiler (공식 사이트 문구)
  - 입력도 JavaScript 이고, 출력도 JavaScript 이다.
  - '언어 대 언어 변환기' 이므로 Transpiler 라고도 부를 수 있다.
- 사용 목적은 하위 호환성 보장(backwards compatible)이다.
  - Babel은 ES2015(ES6) 이상의 최신 코드를 ES5 로 변환한다.
  - 브라우저마다 [JavaScript 지원 버전](https://kangax.github.io/compat-table/es5/)이 다르고, 그 중 ES5 정도면 IE11 까지도 무리없이 지원한다.
  - 개발자는 최신 문법(ES6+)을 사용해 생산성 있는 개발을 하고, 최종적으로 Babel이 ES5로 변환한다.
  - 결론적으로 생산성과 하위호환성을 얻을 수 있고, 개발자가 모든 브라우저를 일일이 신경쓰지 않아도 된다.
- Babel은 다양한 플러그인과 프리셋으로 이뤄져 있다.
  - Babel core 그 자체로는 번역 기능을 가지고 있지 않다.
  - 각 언어(ES6, JSX, TypeScript, ...)별로 번역할 수 있는 플러그인을 같이 설치해서 사용한다.
  - 특히 언어 변환만으로는 채울 수 없는 기능(Function)에 대해서 Polyfill 플러그인을 사용한다.

## webpack
- webpack is a module bundler (공식 사이트 문구)
  - 의존 관계에 있는 모듈들을 1개의 JavaScript 파일로 합치는(bundling) 역할.
  - 사용 목적은 (1) 모듈 개수 최대한 줄이기 (2) 모듈 시스템을 사용하기 위해
- (1) 브라우저는 파일을 많이 로드할 수록 느려진다.
  - http 요청은 느리기 때문에 웹페이지의 리소스 파일(html, js, css, img)개수가 많을수록 페이지가 늦게 뜬다.
  - 따라서 웹사이트의 리소스 파일(assets) 개수를 줄이기 위한 노력이 있었고, 이를 webpack이 해준다.
- (2) JavaScript 프로젝트의 규모가 커지면 코드 관리에 한계가 온다.
  - 코드 양이 많아지면 유지보수를 위해 모듈로 나눠 관리하는 것이 좋은데, JavaScript는 언어 자체의 모듈 시스템이 없다.
    - 지금은 ES2015(ES6)부터 모듈 시스템을 지원하여 이를 사용하지만, webpack이 나왔던 시절에는 없었다.
  - 그래서 JavaScript에서도 모듈을 쓸 수 있도록 만들어진 모듈 시스템이 CommonJS 와 AMD 이다.
  - 이 두가지 모듈 시스템이 브라우저에서 잘 돌아갈 수 있도록 webpack이 도와준다.
- 결론적으로는 Babel과 같은 목적이다 : 개발 생산성 확보 + 브라우저 호환성 확보

## ESLint
- Linter란 무엇인가?
  - 코드 정적 분석 도구이며, 정적 분석이란 코드를 실행하지 않고 분석을 수행한다는 의미.
  - 문법 검사, 코딩 컨벤션 체크 등 코드의 품질 관리 역할을 수행한다.
  - 코드의 가독성을 높이고, 잠재적인 오류와 버그를 찾아내는 결과가 된다.
- JavaScript 특성상 문제를 디버깅 하기가 쉽지 않다.
  - 컴파일을 하지 않으므로 실제로 실행을 해봐야 런타임 오류가 발생한다.
  - 오류가 있어도 어떻게던 코드가 돌아는 가기 때문에... 비록 잘못된 방향이더라도 일단 실행은 된다.
- 따라서 요즘 JavaScript 개발자라면 필수적으로 정적 분석 도구를 사용한다고 볼 수 있다.
  - ESLint는 다양한 JavaScript Linter 중에서 가장 많이 쓰이는 린터임
  - VS Code의 확장 프로그램으로 설치하면, 코딩하는 실시간으로 체킹을 해 준다.

## References
- [프론트엔드 개발환경의 이해: 웹팩(기본)](https://jeonghwan-kim.github.io/series/2019/12/10/frontend-dev-env-webpack-basic.html)
- [Babel과 Webpack을 이용한 ES6 환경 구축 ②](https://poiemaweb.com/es6-babel-webpack-2)
- [웹팩의 기본 개념](https://jeonghwan-kim.github.io/js/2017/05/15/webpack.html)
- [Webpack과 Babel을 이용한 React 개발 환경 구성하기](https://medium.com/wasd/%EC%9B%B9%ED%8C%A9-webpack-%EA%B3%BC-%EB%B0%94%EB%B2%A8-babel-%EC%9D%84-%EC%9D%B4%EC%9A%A9%ED%95%9C-react-%EA%B0%9C%EB%B0%9C-%ED%99%98%EA%B2%BD-%EA%B5%AC%EC%84%B1%ED%95%98%EA%B8%B0-fb87d0027766)
- [ESLint 조금 더 잘 활용하기](https://tech.kakao.com/2019/12/05/make-better-use-of-eslint/)
