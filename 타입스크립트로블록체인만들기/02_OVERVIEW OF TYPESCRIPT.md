# 노마드코더 - 타입스크립트로 블록체인만들기

## #2 OVERVIEW OF TYPESCRIPT

[**타입스크립트** **코드테스트]**
https://www.typescriptlang.org/play

### Type 시스템

명시적 정의 : 변수 선언 시 타입을 정의

```tsx
let a:boolean = "nico"; //boolean타입 변수에 string타입 할당이 불가능하므로 에러

let a:string = "nico";

let arr: number[] = [];
arr.push(1); // 가능
arr.push("1"); //불가능
```

변수만 생성 : 타입 추론

```tsx
let b = "hello"; //b변수가 string타입이라고 추론

b = 1; // string타입 변수에 number타입 할당이 불가능하므로 에러
```

❗️명시적으로 정의하는 방법보다 타입을 추론하는 방식이 코드 가독성 부분이나 시간소요 부분에서 적게 들기 때문에 타입 추론하는 방식을 권장

- 선택적 타입을 다루는 방법
- Alias 타입을 생성하는 방법
- argument의 타입을 지정하는 방법
- 함수 return값의 타입을 지정하는 방법

객체에 타입을 정의할 때

```tsx
const player1: {
	name:string,
	age?:number // age?:number는 age?: number | undefined 라는 뜻
} = {
	name="nico"
};

const player2: {
	name:string,
	age?:number // age?:number는 age?: number | undefined 라는 뜻
} = {
	name="jaeseok"
};
```

player 객체가 많이 필요하면 타입 정의가 어렵기 때문에 Alias(별칭)타입을 생성할 수 있음

```tsx
// type에 type도 정의 가능
type Age = number;

type Player = {
	name: string,
	age?: number // age?: Age
};

const nico: Player = {
	name="nico"
};

const jaeseok: Player = {
	name="jaeseok",
	age=25
};
```

💡 코드 재사용성 매우 용이

함수 return값의 타입을 지정하는 방법

```tsx
type Player = {
	name: string,
	age?: number
};

// 일반 함수 형태
function playerMaker(name: string): Player{ // 인수 지정 방법
	return { name }
};

// 화살표 함수 형태
const playeMaker = (name: string): Player => ({name});

const nico = playerMaker("nico");
nico.age = 12
```

readonly 사용하기

```tsx
type Player = {
	readonly name: string,
	age?: number
};

const playeMaker = (name: string): Player => ({name});

const nico = playerMaker("nico");
nico.age = 12
nico.name = "las" // 불가능. readonly가 있으면 최초 선언 후 수정 불가

// number타입 배열 선언 시
const numbers: readonly number[] = [1,2,3,4];
numbers.push(1) // 불가능.
```

Tuple

→ 정해진 개수와 순서에 따라서 배열 선언

```tsx
const player: [string, number, boolean] = ["nico", 1, true];

//readonly도 사용 가능
const player: readonly [string, number, boolean] = ["nico", 1, true];
```

사용 예) API가 여러 타입의 형태로 올 때가 있는데 그 상황에 사용할  수 있음

null, undefined, any

```tsx
let a: undefined = undefined;
let b: null = null;

// 어떤 타입이 들어와도 상관 없을 때, TypeScript로부터 빠져나오고 싶을 때 사용하는 타입
// any : TypeScript의 보호장치를 비활성화 시키는 역할
let c: any = "nico";
c = 12;
```

unknown, void, never

```tsx
// void
function noop() {
	return;
}

// unknown
function hello(a: any) {
	a.b(); // OK
}

function hello2(a: unknown) {
	a.b(); // 에러: Object is of type 'unknown'.
}

// never
function fail(msg: string): never {
	throw new Error(msg);
}

function hello(name: string|number){
	if(typeof name === "string"){
		name // type = string
	} else if(typeof name === "number"){
		name // type = number
	} else{
		name // type = never
	}
}
```

❗️void : 값을 반환하지 않는 함수의 반환 값을 나타낸다. 함수에 return문이 없거나 해당 return문에서 명시적 값을 반환하지 않을 때 항상 유추되는 타입이다.

❗️unknown: 모든 값을 나타낸다. any타입과 비슷하지만 any보다 unknown이 더 안전하다. 

❗️never: 일부 함수는 값을 반환하지 않는다. 함수가 예외를 throw하거나 프로그램 실행 종료를 의미