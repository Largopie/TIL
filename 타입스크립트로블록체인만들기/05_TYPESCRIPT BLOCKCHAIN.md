# #5 TYPESCRIPT BLOCKCHAIN

### ❓블록체인의 PoC(Proof of Concept)[개념증명]를 객체 지향 프로그래밍을 활용하는 TypeScript로 만들 수 있다.

> ## **기본 세팅**
> 
> 1. typechain 폴더 생성
> 2. `npm init -y` 명령어로 `package.json` 파일 생성
> 3. `package.json` 파일에서 “test”라인을 지운 후 `npm -i -D typescript` 명령어를 통해 타입스크립트 설치 ( -D를 입력함으로써, 타입스크립트가 devDependencies에 설치된다. )
> 4. `src`폴더 생성 후 폴더 안에 `index.ts`파일 생성
>     
>     ```tsx
>     // src/index.ts
>     
>     const hello = () => "hi";
>     ```
>     
> 5. js파일로 컴파일이 잘 되는지  확인을 위해 `tsconfig.json`파일 생성
>     
>     ```json
>     // tsconfig.json
>     
>     {
>       "include": ["src"], // 컴파일할 폴더 지정
>       "compilerOptions": {
>         "outDir": "build" // 컴파일해서 js파일을 저장해줄 공간
>       }
>     }
>     ```
>     
> 6. `package.json`에 ‘build’ 스크립트 생성
>     
>     ```json
>     {
>       "name": "typechain",
>       "version": "1.0.0",
>       "description": "",
>       "main": "index.js",
>       "scripts": {
>         **"build": "tsc"**
>       },
>       "keywords": [],
>       "author": "",
>       "license": "ISC",
>       "devDependencies": {
>         "typescript": "^5.2.2"
>       }
>     }
>     ```
>     
> 7. `npm run build`를 입력하면 `build` 폴더 내에 `index.js` 파일이 컴파일되어 생성됨
>     
>     ```jsx
>     // build/index.js
>     var hello = function () { return "hi"; };
>     ```
>     
>     - TypeScript의 화살표 함수 → 일반 함수로 변경
>     - const 대신 var 사용
>     
>     **타입스크립트가  이 코드를 컴파일 해 낮은 버전의 자바 스크립트코드로 변환해줌**
>     
>     `tsconfig.json`의 `compilerOptions`에서 `target`을 통해 버전 설정 가능
>     
> 8. `target` 을 `ES6`로 지정했을 때 (대부분 `ES6`선택 시 대부분 호환 됨)
>     
>     ```jsx
>     // build/index.js
>     
>     const hello = () => "hi";
>     ```
>