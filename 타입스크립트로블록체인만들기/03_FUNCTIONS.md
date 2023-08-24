# 노마드코더 - 타입스크립트로 블록체인만들기

## #03 FUNCTIONS

### Call signature

함수 이름 위에 커서를 올렸을 때 나타나는 파라미터 타입 정보와 리턴 타입 정보

**나만의 call signature 선언 방법**

```tsx
type Add = (number, number) => number;
```

<br>

### Function Overloading

- 동일한 이름에 **매개 변수만 다른** 여러 버전의 함수를 만드는 것

```tsx
type Add = {
	(a:number, b:number) => number;
	(a:number, b:string) => number;
};

// b의 type이 number | string으로 나오기 때문에 예외처리가 필요함
const add:Add = (a, b) => {
	if(typeof b === "string") return a;
	return a + b
}
```

<br>

Next.js문법에서의 타입 오버로딩 예시

```tsx
// object, string 타입 둘 다 보낼 수 있음

Router.push({
	path: "/home",
	state: 1
})

Router.push("/home")

// 이 때 TypeScript에서는 overloading으로 타입을 지정해줄 수 있음
type Config = {
	path:string,
	state:object
}

type Push = {
	(path:string):void
	(config:Config):void
}

// config의 type은 Push에 존재하는 type인 string | Config 두 가지를 받을 수 있다.
const push:Push = (config) => {
	if(typeof config === "string") {console.log(config)} // type = string
	else{
		console.log(config.path) // type = object
	}
}
```

<br>

### Polymorphism(다형성)

❓poly(접두사) : 많은

❓morphos: 형태, 구조

**poly + morphos = 많은 형태(구조)[다형성]**

**concrete type ⇒** 우리가 전부터 봐왔던 타입(number, boolean, string…)

```tsx
type SuperPrint = {
	(arr:number[]):void,
	(arr:boolean[]):void
}

const superPrint: SuperPrint = (arr) => {
	arr.forEach(i => console.log(i))
}

superPrint([1,2,3,4]) // 정상 동작
superPrint([true, false, true, true]) // 정상 동작
superPrint(["1", "2", "3"]) // 오류
```

다양한 형태의 값이 들어와야 할 때 마다 type에 추가를 해주는 작업을 해야하는가? ❌ → generic기법 사용

<br>

**genereic type ⇒** 타입의 placeholder와 비슷한 개념, 타입스크립트가 타입을 유추

```tsx
// 화살표 함수 이용
type SuperPrint = <T>(a: T[]) => T
const superPrint: SuperPrint = (arr) => arr[0]

// 일반 함수 이용
function SuperPrint<T>(a:T[]){
	return a[0]
}

// 모두 정상 동작
superPrint([1,2,3,4])
superPrint([true, false, true, true])
superPrint(["1", "2", "3"])
superPrint([1, 2, false, true, "hello"])
```

💡**any와의 차이점** : any는 해당 타입의 정보가 any라고만 명시되어 있지만 generic은 해당 타입의 정보를 알 수 있다.

<br>

- 제네릭은 선언 시점이 아니라 생성 시점에 타입을 명시하여 하나의 타입만이 아닌 다양한 타입을 사용할 수 있도록 하는 기법
- 다양한 타입에서 작동할 수 있는 컴포넌트 생성 가능
- 구체적인 타입을 지정하지 않고 다양한 인수와 리턴 값에 대한 타입 처리 가능
- `TypeScript`에서 제네릭을 통한 인터페이스, 함수 등의 재사용성을 높일 수 있음