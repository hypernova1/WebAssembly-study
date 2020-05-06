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
* `wasm-game-of-life/Cargo.toml`
    * 러스트 패키지 매니저 및 빌드 툴
    * 의존성 관리 및 메타데이터 지정
    * `wasm-bindgen`으로 미리 구성되어 제공됨

* `wasm-game-of-life/src/lib.rs`
    * 웹어셈블리로 컴파일하는 크레이트의 루트
    * `wasm-bindgen`을 사용하여 자바스크립트와 연결
    * 이 프로젝트에서는 `window.alert`(js)함수를 가져오고 `greet`(rust)함수를 내보냄
    
* `wasm-game-of-life/src/util.rs`
    * 웹어셈블리로 컴파일된 러스트의 작업을 쉽게 하기 위한 공통 유틸리티 제공

### 프로젝트 빌드하기
~~~
$ wasm-pack build 
~~~
* Rust 1.30 이상 설치 확인 및 `rustup`을 통해 `wasm32-unknown-unknown`을 설치했는지 확인
* `cargo`를 통해 러스트 소스를 `.wasm` 파일로 컴파일
* `wasm-bindgen`을 사용하여 웹어셈블리에서 사용할 자바스크립트 API 
* 생성된 `pkg` 디렉토리 구조
~~~
  pkg/
  ├── package.json
  ├── README.md //메인 프로젝트에서 복사됨
  ├── wasm_game_of_life_bg.wasm
  ├── wasm_game_of_life.d.ts
  └── wasm_game_of_life.js
~~~
* `wasm-game-of-life/pkg/wasm_game_of_life_bg.wasm`