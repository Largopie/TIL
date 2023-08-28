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

HashMap 예제
```tsx
type Words = {
    [key:string]: string
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
        public def: string
    ){}
}

const kimchi = new Word("kimchi", "한국의 음식")
const kimbob = new Word("kimbob", "한국의 간식")

const dict = new Dict()

dict.add(kimchi);
dict.add(kimbob)
dict.def("kimchi");
console.log(dict)
dict.del("kimbob")
console.log(dict)

dict.update("kimchi", "한국 토종 음식")
console.log(dict)

// Dict클래스에서 단어를 삭제, 업데이트 하는 메소드 만들기
// Word클래스에서 단어의 정의를 추가, 수정하는 메소드, 단어를 출력하는 메소드 만들기
```