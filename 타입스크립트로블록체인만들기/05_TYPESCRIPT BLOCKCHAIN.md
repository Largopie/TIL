# #5 TYPESCRIPT BLOCKCHAIN

### ❓블록체인의 PoC(Proof of Concept)[개념증명]를 객체 지향 프로그래밍을 활용하는 TypeScript로 만들 수 있다.

> ## 기본 세팅
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
>         "build": "tsc" // build
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

<br>

### target 옵션

- 자바스크립트 코드로 변환할 때 자바스크립트 버전 선택해주는 역할

`target` 을 `ES6`로 지정했을 때 (대부분 `ES6`선택 시 대부분 호환 됨)

```jsx
// build/index.js

const hello = () => "hi";
```

**[target 참고자료]** ( https://www.typescriptlang.org/tsconfig#target )

<br>

### lib 옵션

- 합쳐진 라이브러리의 **정의 파일[declaration files]** 을 특정해주는 역할
- 타입스크립트에게 코드가 어디서 동작할 것인지 알려줄 수 있는 옵션
- 사용할 API에 대한 자동완성 기능 제공
- 프로그램이 브라우저에서 실행되면 lib에 "DOM" 유형 정의를 할 수 있다.
ex) `"lib": ["ES6", "DOM"]`

❗️DOM(The Document Object Model): 문서 객체 모델은 HTML, XML 문서의 프로그래밍 interface이다. ex) `localStorage`, `window`, `document` 등

**[lib 참고자료]** ( https://www.typescriptlang.org/tsconfig#lib )

### strict 옵션

- `localStorage`같은 내장 객체를 `TypeScript`에서 사용할 수 있는 이유는 개발자들이 관련 type들을 미리 정의했기 때문이다. ex)`Math`, `localStorage`, `HTMLElement`, `window`등

myPackage.js

```jsx
export function init(config) {
  return true;
}

export function exit(code) {
  return code + 1;
}
```

<br>

index.ts

```tsx
import {init} from "myPackage"
// strict mode 비활성화 시 정상 작동하지만 .d.ts파일에 정의해줘야 함
// true 시 could not find a declaration file for module 에러 발생

init()
```

##

# 블록체인 제작 : 가상화폐의 기본적인 기능 몇 가지 구현

## 블록체인이란?

- 여러개의 블록이 사슬처럼 묶인 것
- 블록체인 내부에는 블록체인으로 보호하고 싶은 데이터가 존재
- 연결고리는 **해쉬값**

<br>

```json
//package.json
"scripts": {
    "build": "tsc",
		"dev": "nodemon --exec ts-node src/index.ts",
    "start": "node build/index.js"
}
```

💡기본적인 workflow : `npm run build && npm run start`

❗️`ts-node` : ts-node는 Node.js용 TypeScript 실행 엔진 및 REPL입니다. JIT는 TypeScript를 JavaScript로 변환하므로 사전 컴파일 없이 Node.js에서 TypeScript를 직접 실행할 수 있습니다.<br>
(`npm i -D ts-node`)<br>
**[관련자료]** https://www.npmjs.com/package/ts-node

<br>

❗️`nodemon` : 자동으로 커맨드 재실행<br>
(`npm i nodemon`)<br>
**[관련자료]** https://www.npmjs.com/package/nodemon

<br>

❗️`esModuleInterop` : CommonJS 모듈을 ES6 모듈 코드베이스로 가져오려고 할 때 발생하는 문제를 해결합니다. ES6 모듈 사양을 준수하여 CommonJS 모듈을 정상적으로 가져올 수 있게 해줍니다.<br>
**[관련자료]** https://www.typescriptlang.org/tsconfig/#esModuleInterop

##

💡**DefinitelyTyped** : TypeScript type 정의를 위한 리포지토리입니다.

**[해당 레포지토리]** https://github.com/DefinitelyTyped/DefinitelyTyped

<br>

## TypeScript 강의의 마무리
더 심도있게 타입스크립트를 배우려면 [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/intro.html)을 참고해서 읽기