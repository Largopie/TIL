# 김민태의 프론트엔드 아카데미

# JavaScript & TypeScript Essential

## Chapter2. JavaScript 그리고 TypeScript

### JavaScript 변천사

1995년에 처음 등장했다. 기존 이름은 `LiveScript`였으며 `HTML`을 간단하게 조작하기 위한 목적으로 만들어진 프로그래밍 언어였다. `Ecma`라는 이름으로 표준을 개발하는 방식으로 진행됐다. 현재 `JavaScript` 공식 명칭은 `EcmaScript`이다. 2009년까지 `EcmaScript 5.0`이 발표되었다.

`ECMA2015` 이후부터 모던 자바스크립트 라는 이름으로 불렸다.
중요한 버전은 `ECMA 5.0` 이유는 현역에 실행되는 `JavaScript` 버전이기 때문. 모던 `JavaScript`는 `ES2015` 이후부터 중요하다. 이 두가지 버전이 어떤 의미에서 중요성을 가지는지 알아야 한다.

### 웹앱의 구성요소

웹 앱의 필수 구성요소 → `HTML`, `CSS`, `JavaScript`

앱 : 상태라는 것을 가지고 있고, 사용자와 상호적으로 주고받을 수 있는 다양한 기능을 제공해주는 것

웹 앱을 실행시키는 요소가 `브라우저` 이다.

브라우저 :  런타임 환경을 제공하는 환경

서버 사이드 렌더링 : 웹  서버에서 주도적으로 만들고 브라우저로 전송하는 방법

클라이언트 사이드 렌더링 : 브라우저에서 실행되는 `JavaScript`의 결과로 `HTML`을 주도적으로 만들어서 UI를 표현하는 방법

캔버스 태그는 일종의 그래픽 시스템을 표현하기 위한 도화지(2D나 3D그래픽을 표현하기 위한 영역만을 제공)

태그 안의 내용은 자바스크립트로 이루어져있음

### 모던 JavaScript와 개발 환경

**프론트엔드 개발환경의 핵심적인 변화**

- `ES2015`부터 등장한 ‘`모듈`’이라는 스펙

❗️**모듈** : 파일과 파일 간에 특정 파일의 기능을 사용하기 위해서 불러들여서 쓸 수 있는 기능(`import`, `export`)

**프론트엔드 개발환경이 복잡하게된 핵심적인 이유**

- 웹 앱의 규모가 굉장히 커지고 복잡해졌다

`npm`을 통해 손쉬운 툴들을 다른 개발자들에게 알리고 배포하기가 훨씬 쉬워졌다.

이 환경이 만들어진 상황에서 ‘`번들러`’라는 소프트웨어가 등장했다.

번들러가 하는 가장 중요한 일 중 하나가 ‘`트랜스파일러`’가 중간에 끼어있는 것이다.

❗️**번들러** : 브라우저에서 로딩하기 전에 많은 파일을 하나로 묶어주는 소프트웨어

❗️**트랜스파일러** : 같은 언어이지만 문법적으로 변환해주는 도구 (ex. 높은 버전의 `JavaScript`문법을 브라우저가 호환할 수 있도록 낮은 버전의 `JavaScript`문법으로 변환해주는 방식)

실무적으로 가장 많이 쓰는 번들러 : `webpack`

`TypeScript`도 원하는 `JavaScript` 버전으로 바꿀 수 있는 `트랜스파일링` 동작이 일어나기 때문에 `트랜스파일러`의 한 종류라고 할 수 있다.

### TypeScript vs JavaScript

**TypeScript**

- `TypeScript`는 `JavaScript`의 슈퍼셋이다. 100% 호환이되는건 물론이고 그 외에도 추가적인 기능들을 제공한다.
- Type + Script ⇒ (타입을 제공한다) 명시적인 유형 설명. 기존 `JavaScript`는 Type이 없었지만 `TypeScript`는 자료 유형을 명시해준다. (자바스크립트의 문법보다 코드를 나타내는 표현력이 명확하고 풍성해진다)

```tsx
// JavaScript의 방식
let age = 10;

// TypeScript의 방식
type Centimeter = number;
type RainbowColor = 'red' | 'orange' | 'yellow' | 'green' | 'blue' | 'indigo' | 'violet';

let weight:number = 80;
let height:Centimeter = 176;
let color:RainbowColor = 'orange';

// 오류가 뜸. 이유는 RainbowColor의 type에 존재하는 값들만 넣을 수 있음.
color = 'black';
```

`JavaScript`는 콘셉트 상 구조적으로 데이터 유형을 설명하기 어려운 언어이다 보니 `트랜스파일링`이라는 과정 속에서 데이터 유형을 설명할 수 있는 `TypeScript`라는 언어가 각광받고 있다.