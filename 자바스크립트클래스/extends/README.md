# 실습을 통한 예제 이해

## 인스턴스 생성 오류

아래 코드에서 `Rabbit`은 `Animal`을 상속받습니다.

그런데 `Rabbit` 객체를 만들 수가 없습니다. 무엇이 잘못된 것일까요? 코드를 수정해보세요.

```js
class Animal {
  constructor(name) {
    this.name = name;
  }
}

class Rabbit extends Animal {
  constructor(name) {
    this.name = name;
    this.created = Date.now();
  }
}

let rabbit = new Rabbit('White Rabbit'); // Error: this is not defined
alert(rabbit.name);
```

### 정답

```js
class Animal {
  constructor(name) {
    this.name = name;
  }
}

class Rabbit extends Animal {
  constructor(name) {
    super(name);
    this.created = Date.now();
  }
}

let rabbit = new Rabbit('White Rabbit'); // Error: this is not defined
alert(rabbit.name);
```

## 시계 확장하기

```js
매 초마다 시간을 출력해주는 클래스 Clock이 있습니다.

class Clock {
  constructor({ template }) {
    this.template = template;
  }

  render() {
    let date = new Date();

    let hours = date.getHours();
    if (hours < 10) hours = '0' + hours;

    let mins = date.getMinutes();
    if (mins < 10) mins = '0' + mins;

    let secs = date.getSeconds();
    if (secs < 10) secs = '0' + secs;

    let output = this.template
      .replace('h', hours)
      .replace('m', mins)
      .replace('s', secs);

    console.log(output);
  }

  stop() {
    clearInterval(this.timer);
  }

  start() {
    this.render();
    this.timer = setInterval(() => this.render(), 1000);
  }
}
```
### `Clock`을 상속받는 `ExtendedClock`을 만들고, `precision`(정확도)이라는 매개변수도 추가해보세요. `precision`은 ‘초’ 사이의 간격을 의미하고, 기본값은 1000(1초)이 되어야 합니다.

- 새로운 파일(`extended-clock.js`)을 만들어 답을 작성해주세요.
- `clock.js`은 수정하면 안 됩니다. 상속을 사용하세요.
