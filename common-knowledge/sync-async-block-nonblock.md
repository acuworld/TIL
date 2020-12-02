# Synchronous/Asynchronous와 Blocking/Non-blocking

## Blocking vs Non-blocking
함수를 호출했을 때 제어권이 바로 돌아오느냐?
- Blocking : 처리가 끝날 때까지 제어권을 뺏겨 아무것도 못함.
- Non-blocking: 제어권이 즉시 반환되어 다음 작업을 진행할 수 있음. 단, 결과 처리는 따로 해야함. (콜백함수로)

## Synchronous/Asynchronous
함수를 호출했을 때 그 결과를 누가 신경쓰느냐?
  - Synchronous : 내가 호출한 함수가 끝났는지를 계속 확인하며 신경써야 함.
  - Asynchronous : 함수 한 번 호출하면 내 관심은 거기서 끝. 이후로 뭔 일이 생기던 신경 안씀.
  
## 헷갈리는 부분
- 사실 Blocking/Synchronous와 Non-blocking/Asynchronous 조합은 흔히 찾을 수 있음.
- Non-blocking/Synchronous:
  - CPU 멈춤 없이 다양한 작업을 할 수 있으나, 아까 호출했던 함수의 결과를 계속 신경써야 함.
  - 예시:
    - 나는 역에서 출발을 기다리는 지하철이고, 다음 역에 다른 열차가 멈춰서 있다.
    - 앞 열차에게 출발하라는 메시지를 보냈다. 즉시 알았다는 답이 왔다. (Non-blocking)
    - 현재 나는 안내 방송, 문 열고 닫기 등등 다양한 일을 할 수 있다. (Non-blocking)
    - 근데 출발은 못한다. 계속 1초마다 앞 열차가 출발했는지 확인한다. (Synchronous)
    - 앞 열차가 출발하면 그제서야 나도 출발할 수 있는 상태가 된다. (Synchronous)
- Blocking/Asynchronous:
  - 이게 제일 문제. Blocking이라서 어차피 아무것도 못하는데 Async인게 의미가 있나?
  - 이 방식을 일부러 사용하는 사람은 없는데, 어쩌다가 강제로 쓰게 되는 경우가 있다.
  - Node.js와 MySQL :
    - Node.js는 Non-blocking Asynchronous 방식이나, 문제는 MySQL driver가 Blocking 이다.
    - 따라서 쿼리를 날리면 어쩔 수 없이 Blocking 된다ㅠ
  - 즉, Non-blocking Asynchronous 과정 중에 하나라도 Blocking이 껴 있으면 강제로 사용...

## References
- [Blocking-NonBlocking-Synchronous-Asynchronous](http://homoefficio.github.io/2017/02/19/Blocking-NonBlocking-Synchronous-Asynchronous/)
- [동기와 비동기, 그리고 블럭과 넌블럭](https://musma.github.io/2019/04/17/blocking-and-synchronous.html)
