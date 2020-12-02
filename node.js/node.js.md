# Node.js


## 개요
- JavaScript 런타임이다.
- Chrome의 V8 JavaScript engine을 이용해 JavaScript 코드를 실행한다.
- (1) Non-blocking I/O (2) Event-driven (3) Single thread


## 인기 이유
- (1) JavaScript를 사용할 수 있어서 (제일 큰 이유)
  - 프론트엔드와 언어를 통일함으로써, 사람도 공유하고 개발 환경도 공유
  - 특히 혼자서 FE/BE를 다 하는 풀스택 개발자에게 더할 나위 없는 축복이다.
  - 언어 측면에서도 Java(Spring) 대비 JavaScript가 생산성이 더 좋다.
- (2) 개발이 단순해서
  - 단일 쓰레드이므로, 멀티 쓰레딩에 수반되는 Sync, Lock 같은 골치 아픈 문제가 없다.
  - Apache, Tomcat 같은 별도의 서버 없이 자체적으로 웹서버가 동작한다. (Express)
  - 비동기 프로그램을 동기 프로그래밍 하듯이 편하게 할 수 있다.
    - ```Promise``` 또는 ```async/await``` 문법
- (3) 풍부한 생태계
  - 공개된 다양한 module이 존재하며 NPM으로 갖다 쓰기 편하다.
  - ```package.json``` 기반의 의존성 관리가 편리하다.
- 결론:
  - 위 장점들에 일맥상통하는 부분이 있다. **높은 생산성.**


## 성능과 안정성
- 네이버에서 초당 5,000건 질의를 24-core 서버 4대로 처리했다는 정보가 있다. ([Naver D2 포스트](https://d2.naver.com/helloworld/4994500))
- Node.js 프로세스가 켜지는 속도도 1~2초 미만으로 매우 짧다.


## 설치
- [여기](https://nodejs.org/en/download/)에서 인스톨러를 다운로드 받아 설치.
- 짝수 버전을 LTS로 지정하여 3년간 유지보수를 지원하므로, 짝수 버전 사용 추천.


## 실행
- ```hello.js``` 파일 작성:
```javascript
console.log('hello, world!')
```
- terminal 에서 실행:
```
node hello.js
```
- Output:
```
hello, world!
```


## 기본 개념

### Non-blocking I/O
- 일반적으로 I/O가 발생하면 거기서 코드가 멈추는 Blocking 동작을 한다.
- Node에서는 Non-blocking 구현을 위해 Callback 함수를 사용한다.
  - 콜백함수 : 어떠한 동작이 끝났을 때 실행되는 함수
  - Non-Blocking 구현을 하면 CPU의 멈춤 없이 다른 작업을 계속 수행할 수 있다.
- Blocking I/O 예제:
    ```javascript
    const fs = require('fs');
    const data = fs.readFileSync('/file.md'); // blocking
    console.log('read done!') // 위 I/O가 끝나야 출력된다
    ```
- Non-blocking I/O 예제:
    ```javascript
    const fs = require('fs');
    fs.readFile('/file.md', (err, data) => {
        console.log('read done!')
    });
    console.log('another jobs...')

    // readFile() 두 번째 인자로 콜백함수를 전달했다. I/O가 끝나면 호출된다.

    // readFile()이 Non-blocking 동작을 하므로 다음 줄 코드가 즉시 실행된다.
    // 따라서 'another jobs...' 가 즉시 출력되고, I/O 종료 후 'read done!' 이 출력된다.
    ```

### Event-driven
- 흔히 알려진 Event-Driven Programming 패턴을 사용하겠다는 것.
- 두 가지 요소를 사용 : (1) Event 발생 (2) Event Handler 실행
- Node가 싱글 쓰레드기 때문에 단일 큐에 모든 이벤트가 대기하며 순차 처리됨.

### Single-thread
- Node는 싱글 쓰레드 기반으로 동작한다.
- 여러 일을 동시에 못하냐? 못한다. 대신 순차 처리를 한다.
  - 이벤트 루프에 등록된 이벤트들을 옵저버가 순차 처리한다.
- 순차 처리이기 때문에 개별 이벤트가 오래 걸리면 전체 퍼포먼스에 영향을 준다.
  - 따라서 각 이벤트의 처리 시간이 짧도록 신경 써서 구현해야 한다.
  - 대부분 I/O에서 시간이 소요되므로 Non-blocking I/O만 잘하면 충분히 빠르다는 게 중론...


## References
- [Node.js & event driven programming?](https://lygggg.github.io/blog/nodejs/)
- [Node.js - Event Loop](https://www.tutorialspoint.com/nodejs/nodejs_event_loop.htm)
