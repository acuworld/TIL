# 회사에서 패키지 설치하기

## 문제 배경
- 회사 PC는 자체 SSL 인증서를 사용하기 때문에 항상 man-in-the-middle attack을 하고 있다.
- NPM은 이에 대해 SSL Certificate 경고를 띄우며 설치 에러를 발생시킨다.
  - ```Unable to verify the first certificate```
  - ```UNABLE_TO_VERIFY_LEAF_SIGNATURE```

## 해결법 1
- cmd.exe에서 SET 명령으로 환경 변수에 SSL 우회 옵션을 추가하는 방법
- 단점: cmd.exe 창을 닫으면 설정이 날아가므로 일회성 조치임
```
SET npm_config_strict_ssl=false
```

## 해결법 2
- npm config에 SSL 우회 옵션을 기록하는 방법
- 설정이 ```~/.npmrc``` 파일에 기록됨
```
npm config set strict-ssl false
npm config set registry="http://registry.npmjs.org/"
```

## 해결이 까다로운 케이스
- npm은 SSL 우회 옵션을 제공하지만, 문제는 node가 옵션 제공을 안한다.
- 예: https request가 들어있는 스크립트를 ```node install.js``` 로 실행하는 경우
  - node 명령은 SSL 인증을 무시하는 글로벌 옵션이 없다.
  - 스크립트 안에 직접 SSL 인증을 우회하는 코드를 삽입해야 함
- 해결법: ```.js``` 파일 상단에 아래와 같은 코드를 삽입하여 SSL 체킹을 우회 가능
```
process.env.NODE_TLS_REJECT_UNAUTHORIZED = '0';
```

- 이 문제는 electron 설치할 때 발생하여 골머리 앓았음
  - ```npm install electron``` 하면 '설치 스크립트만' 다운로드 받음
    - 즉, NPM이 다 설치하는 게 아니라 자체적인 설치 스크립트로 설치한다 (post-install)
  - 문제는 ```node install.js``` 를 실행하여 자기 스스로 설치를 진행할 때 SSL 문제가 터짐
    - **NPM 다운로드 > (코드 삽입) > install.js 실행**
    - 이처럼 짧은 찰나의 순간에 우회 코드를 삽입해야 함 -_-
  - **꿀팁:**
    - electron만 단독 설치하면 다운로드가 너무 빨리 끝나서 도저히 삽입각이 안나옴
    - 프로젝트 하나 생성하고 dependency 잔뜩 넣은 다음에 install 때리면 NPM 다운로드 시간이 길어지기 때문에 코드 삽입할 시간을 벌 수 있음 (ㅋㅋ)
