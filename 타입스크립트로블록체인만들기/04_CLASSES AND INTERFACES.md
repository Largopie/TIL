# 노마드코더 - 타입스크립트로 블록체인만들기

## #04 CLASSES AND INTERFACES

### Classes

❗️ 접근 가능 위치
구분　　　선언한 클래스 내　상속받은 클래스 내　인스턴스
private 　 　　　⭕　　　　　　　❌　　　　　❌
protected 　　　⭕　　　　　　　⭕　　　　　❌
public　　　　　⭕　　　　　　　⭕　　　　　⭕

|구분|선언한 클래스 내|상속받은 클래스 내|인스턴스
|----|----|----|----|
|private|⭕|❌|❌|
|protected|⭕|⭕|❌|
|public|⭕|⭕|⭕|

### 추상(Abstract) 클래스

다른 클래스가 상속받을 수 있는 클래스

직접 새로운 인스턴스를 만들 수는 없다.

```tsx
abstract class User{
	constructor(
		private firstname:string,
		private lastname:string,
		public nickname:string
	){
		abstract getNickname():void
	}
}

class Player extends User{
	// 추상 메서드는 추상 클래스를 상속받는 클래스들이 반드시 구현(implement)해야하는 메서드이다.
	getNickname(){
		console.log(this.nickname)
	}
}
```

<br>

해쉬맵 예제
```tsx
type Words = {
    [key:string]: string[]
}

class Dict {
    private words:Words
    constructor(){
        this.words = {}
    }
    // 클래스를 타입처럼 이용
    add(word:Word){
        if(this.words[word.term] === undefined){
            this.words[word.term] = word.def;
        }
    }
    def(term:string) {
        return this.words[term]
    }
    // 단어를 삭제하는 메소드
    del(word:string){
        if(Object.keys(this.words).includes(word)) delete this.words[word];
    }
    update(word:string, change_def:string){
        if(Object.keys(this.words).includes(word)) this.words[word] = change_def;
    }
    
}

class Word {
    constructor(
        public term: string,
        public def: string[]
    ){}
    print() {
        return 'word: '+ this.term + "\n" + 'def: ' + this.def;
    }
    add_def(def: string){
        this.def.push(def)
    }
    update_def(def: string, update: string){
        this.def[this.def.indexOf(def)] = update
    }
}

const kimchi = new Word("kimchi", ["한국의 음식"])
const kimbob = new Word("kimbob", ["한국의 간식"])

const dict = new Dict()

kimbob.add_def("분식")
kimbob.update_def("분식", "분식집")
console.log(kimbob.print())

// Dict클래스에서 단어를 삭제, 업데이트 하는 메소드 만들기
// Word클래스에서 단어의 정의를 추가, 수정하는 메소드, 단어를 출력하는 메소드 만들기
```

### Interfaces

- interface는 오로지 오브젝트의 모양을 타입스크립트에게 설명하기 위해서만 사용되는 키워드

<br>

Type을 특정 값으로 지정하는 방법

```tsx
type Team = "red" | "blue" | "yellow"
type Health = 1 | 5 | 10

type Player = {
	nickname: string,
	team: Team
	health: Health
}

// interface 표현 방식
interface Player {
	nickname: string,
	team: Team
	health: Health
}

const nico: Player = {
	nickname: "nico",
	team: "red", // 위에 정의한 Team type에 벗어난 문자열이면 에러가 남
	health: 10
}
```

<br>

추상클래스의 사용 방법

```tsx
abstract class User{
    constructor(
        protected firstName:string,
        protected lastName:string
    ){}

    abstract sayHi(name:string):string
    abstract fullName():string
}

class Player extends User{
    fullName(){
        return `${this.firstName} ${this.lastName}`
    }
    sayHi(name: string){
        return `Hello ${name}. My name is ${this.fullName()}`
    }
}
```

추상클래스는 자바스크립트로 컴파일되면 결국 일반적인 클래스 형태가 된다. 대신 인터페이스는 가볍기 때문에 컴파일하면 JS로 바뀌지 않고 사라진다.

<br>

interface와 implements를 이용하여 변형

```tsx
interface User{
    firstName: string
    lastName: string
    sayHi(name:string):string
    fullName():string
}

interface Human{
    health: number
}

// 한 클래스에서 여러 인터페이스도 상속 가능
class Player implements User, Human{
    constructor(
        // 상속했기 때문에 public으로만 선언해야 함
        public firstName: string,
        public lastName: string,
        public health: number
    ){}
    fullName(){
        return `${this.firstName} ${this.lastName}`
    }
    sayHi(name: string){
        return `Hello ${name}. My name is ${this.fullName()}`
    }
}
```