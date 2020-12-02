# Package Manager


## NPM (Node Package Manager)

### 개요
- Node 설치 시 기본으로 같이 설치되는 패키지 매니저 (정확히는 npm CLI)
- 전 세계 JavaScript 개발자들이 패키지를 업로드하는 저장소(Registry)가 존재
- Package와 Module:
  - Package : ```package.json```으로 정의된 파일 또는 디렉토리
    - NPM Registry에 올릴 수 있는 조건이 ```package.json```의 존재임
  - Module : ```node_modules``` 폴더 안에 있어 Node.js가 ```require()```로 부를 수 있는 파일/디렉토리
    - Module은 단일 파일 또는 디렉토리(Package) 이다. 즉, 모든 모듈이 패키지인 건 아님.

### CLI 주요 기능
- 패키지 설치/제거
- Node.js 프로젝트 생성
- Node.js 프로젝트 관리 (패키지 버전, 호환성 관리 등)

### package.json
- Node 프로젝트의 정보를 정의하는 핵심 파일
- 프로젝트 이름, 저자 등의 기본 정보 기록
- Dependencies (프로젝트가 의존하는 모듈 및 버전) 기록
- 파일 예시 :
    ```javascript
    {
        "name": "my app",
        "version": "0.0.0",
        "dependencies": {
            "body-parser": "~1.13.2",
            "express", "~4.13.1"
        }
    }
    ```

### CLI 주요 명령
```sh
# 새 프로젝트 생성
npm init

# 패키지 설치 (dependency 추가)
npm install [package]
npm install [package]@[version]

npm install -g [package] # 전역 설치. 이 프로젝트 뿐만 아니라 PC에서 쓰고싶을 때

# 프로젝트가 의존하는 모든 모듈 설치 (프로젝트 폴더 내에서)
npm install

# package.json -> 'script' -> 'start' 명령 실행
npm start

# package.json -> 'script' -> 'test' 명령 실행
npm test

# package.json -> 'script' -> 'my-script-name' 명령 실행
npm run <my-script-name>
```


## Yarn

### 개요
- Facebook이 개발한 새로운 패키지 매니저
- NPM 대비 빠른 속도(지금은 동등)와 머신 간 패키지 일관성, 보안성 등에 우위
- 패키지 저장소(Registry)는 NPM과 동일한 곳을 사용함

### 설치
- [여기](https://classic.yarnpkg.com/en/docs/install#windows-stable)에서 인스톨러 다운받아 설치

### CLI 주요 명령
```sh
# 새 프로젝트 생성
yarn init

# 패키지 설치 (dependency 추가)
yarn add [package]
yarn add [package]@[version]
yarn add [package]@[tag]

# 프로젝트의 모든 dependency 설치
yarn
yarn install
```
