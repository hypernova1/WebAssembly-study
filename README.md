# Web Assembly (wasm-game-of-life)

## 1. 프로젝트 시작하기
### 프로젝트 템플릿 Clone
~~~
$ cargo generate --git https://github.com/rustwasm/wasm-pack-template
~~~
* 프로젝트명: `wasm-game-of-life`

### 프로젝트 구조
~~~
wasm-game-of-life/
├── Cargo.toml
├── LICENSE_APACHE
├── LICENSE_MIT
├── README.md
└── src
    ├── lib.rs
    └── utils.rs
~~~
#### `Cargo.toml`
* 러스트 패키지 매니저 및 빌드 툴
* 의존성 관리 및 메타데이터 지정
* `wasm-bindgen`으로 미리 구성되어 제공됨

#### `src/lib.rs`
* 웹어셈블리로 컴파일하는 크레이트의 루트
* `wasm-bindgen`을 사용하여 자바스크립트와 연결
* 이 프로젝트에서는 `window.alert`(js)함수를 가져오고 `greet`(rust)함수를 내보냄
    
#### `src/util.rs`
* 웹어셈블리로 컴파일된 러스트의 작업을 쉽게 하기 위한 공통 유틸리티 제공

### 프로젝트 빌드하기
~~~
$ wasm-pack build 
~~~
* Rust 1.30 이상 설치 확인 및 `rustup`을 통해 `wasm32-unknown-unknown`을 설치했는지 확인
* `cargo`를 통해 러스트 소스를 `.wasm` 파일로 컴파일
* `wasm-bindgen`을 사용하여 웹어셈블리에서 사용할 자바스크립트 API
 
### `pkg` 디렉토리 구조
~~~
  pkg/
  ├── package.json
  ├── README.md //메인 프로젝트에서 복사됨
  ├── wasm_game_of_life_bg.wasm
  ├── wasm_game_of_life.d.ts
  └── wasm_game_of_life.js
~~~
#### `wasm_game_of_life_bg.wasm`
* `.wasm`
    * 러스트로 컴파일된 웹어셈블리 바이너리 파일
* 러스트 함수 및 컴파일된 wasm 버전 포함
    
#### `wasm_game_of_life.js`
* `wasm-bindgen`으로 생성됨
* DOM 및 자바스크립트 함수를 러스트로 가져오고 웹어셈블리 함수에 대한 API를 자바스크립트와 연결

#### `wasm_game_of_life.d.ts`
* `wasm_game_of_life.js`의 타입스크립트 버전
    
#### `package.json`
* 자바스크립트 및 웹어셈블리 패키지에 대한 메타데이터 포함
    
## 2. 웹 페이지에 적용하기
~~~
$ npm init wasm-app www
~~~

### `www` 디렉토리 구조
~~~
wasm-game-of-life/www/
├── bootstrap.js
├── index.html
├── index.js
├── LICENSE-APACHE
├── LICENSE-MIT
├── package.json
├── README.md
└── webpack.config.js
~~~

#### `package.json`
* `webpack` 및 `webpack-dev-server`, `hello-wasm-pack`이 의존성으로 제공됨
    *  `hello-wasm-pack`: 초기 `wasm-pack-template` 패키지의 버전
    
#### `wasm-game-of-life/www/webpack.config.js`
* 웹팩 및 로컬 개발 서버 구성 파일

#### `index.js`
* 자바스크립트의 기본 진입점
* `wasm-pack-template`의 컴파일 된 웹어셈블리 및 자바스크립트 글루가 포함된 `hello-wasm-pack` npm 패키지를 가져온 다음 `hello-wasm-pack`의 `greet` 함수 호출

### 의존성 설치하기
~~~
$ cd www
$ npm install
~~~

### `www`에서 로컬 `wasm-game-of-life` 패키지 사용
* `hello-wasm-pack` 패키지를 사용하는 대신 `wasm-game-of-life` 사용
1. `www/package.json` 수정
    ~~~
    {
      // ...
      "dependencies": {                     // Add this three lines block!
        "wasm-game-of-life": "file:../pkg"
      },
      "devDependencies": {
        //...
      }
    }
    ~~~
2. `www/index.js` 수정
    ~~~javascripts
    import * as wasm from "wasm-game-of-life";
      
    wasm.greet();
    ~~~

3. 설치
    ~~~
    $ npm install
    ~~~
 
4. 로컬에 배포
    ~~~
    $ npm start
    ~~~