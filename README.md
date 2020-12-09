# 함수형 자바스크립트

## 함수형 프로그래밍이란 무엇일까?

* 순수함수로 프로그래밍을 하는 것
* 함수로 기능을 추상화해서 프로그래밍 하는 것
* 이미 입증된 함수로 새로운 함수로 만들어서 프로그래밍 하는 것
* 상태변이를 최소화하면서 프로그래밍하는 것

> FP와 OOP가 전혀 다른 패러다임이라는 사고방식은 객체를 정의하는 전통적인 방향 때문에 생긴 오해인듯 싶다며. 객체는 상태와 동작을 묶은 캡슐이라는 기존의 시각에선.. 함수도 객체라는 관점이 성립하기 어려워지니까. 그러나 실제로 함수는 객체와 전혀 다른 무엇이 아니라, “상태가 없는 객체”라는 관점으로 보는 것이 적절하다며. 따라서 객체 = 상태 + 동작이라는 시각이 수정된다면.. FP는 단지 동작만 갖고 있는 객체의 조합을 통해 코딩하는 방식으로 정의되어 OOP속으로 들어오게 된다고 말할 수 있게 된다며. 상태없이 동작만 있는 ADT만으로 객체 구성원들이 모두 표현이 된다면 ‘상태변이’라는 변수를 추적해야하는 기존 OOP가 갖고 있는 고질적인 문제에서 조금 더 예측하기 쉬운 코드로 표현되는 OOP로 개선될 수 있는데 이점을 그냥 FP라고 부를 뿐이람서. FP와 OOP는 패러다임이 다른 것이 아니라 모델이 다를 뿐이라며. - Facebook - Kim Lina님 피드에서

## 부수 효과가 없다는 것은 무엇인가?

* 효과가 아닌 것.
* 함수의 결과가 오직 파라미터에 의해서만 결정되는 것
* 외부 변수에 의존하지 않는다.
* 외부에 의해 영향을 받지 않는다.
* 외부에 영향을 주지 않는다.

## 효과란?

* 함수 반환값에 의해서만 변경이 일어나는 것

### 예시

```js
const sum = (a, b) => a + b;
```

```js
let other;

const sum = (a, b) => {
  other = a + b;
};
```

## 함수형 프로그래밍을 왜 해야할까?

* 복잡한 코드를 간결하게 분리할 수 있다.
* 선언적으로 할 수 있다.
* 테스트가 용이하다.
* 더 안전하게 프로그래밍할 수 있다.
* 순수한 순수하지 않은 부분을 명확하게 나눌 수 있다.

## 선언적인 프로그래밍이란?

* 결과만 기술할 뿐 어떻게는 기술하지 않는 프로그래밍 방법
* 의도에 집중한 프로그래밍 방법

### 함수란 무엇인가?

* 방정식 1 + 2 = 3이다. 같은 파라미터는 같은 결과가 나온다.
* 수학적 정의와 프로그래밍에서의 정의는 없다.
* 뭐 넣으면 뭐 나온다.

## 함수형 프로그래밍의 특징이란 무엇인가?

* 부수효과를 최소화한다.
* 선언적으로 한다.
* 결합도가 약해서 유연하다.
* 함수자체만으로 재사용할 수 있다.
* 기능을 함수로 분리한다.
* 불변 데이터를 사용한다.

```js
class Person {
  first = '';
  middleName = '';
  last = '';

  // 객체지향
  getFullName() {
    return this.first + this.last;
  }
}

// 함수형
const getName = (person: Person) => [person.firstName, person.lastName].join();
getName(person);
```

### Value Object 패턴이란 무엇일까?

* 오직 값에 좌우되는 객체
* 객체를 선언한 이후엔 그 상태가 절대 변하지 않는 것

### 참조 투명성이란? 무엇일까?

* 함수를 값으로 대체할 수 있는 것
* 순수성이랑 같은 의미다.

```js
const sum = (a, b) => {
  return a + b;
};

const value = sum(3, 4);
console.log('value: ', value); // value: 7
```

### 커링이란 무엇일까?

* 인자가 여러개를 받는 함수를 인자 하나씩만 받도록 만드는 것

### 커링을 왜 할까?

* 함수 합성을 쉽게하기 위해서 파라미터가 하나인 함수를 만들기 위해서
* 매개변수의 처리에 대한 책임을 나누기 위해서
* 중간과정에 개입할 수 있는 여지를 만들 수 있다.

```js
const arr = ['1', '2', '3'];

const curriedParseInt = (radix) => (value) => parseInt(value, radix);

const toDecimal = someFunction(curriedParseInt(10));
const toHex = curriedParseInt(16);

arr.map(toDecimal);
```

### 커링을 적용한 함수는?

* 커리된 함수라고 부른다.

### 단항함수

* 인자를 하나만 받는 함수

## 함수형/객체지향은 어떤 차이가 있는가?

차이가 없다.

객체지향은 데이터와 기능이 깊게 결합되어 있다.
상태를 가지고 프로그래밍한다.
객체들을 조합해서 프로그래밍하는 것. 기능이 객체단위로 있다.

함수는 데이터와 기능을 느슨하게 연결한다.
상태와 기능을 철저히 분리한 다음 이들을 다시 조합한 새로운 함수로 연산을 추가할 수 있다.
문제들을 작은 함수로 잘게 나눈다.
상태 없이 프로그래밍한다.
기능단위로 작게 나눠서 함수로 분리하고, 그 함수를 조합하여 프로그래밍하는 것이다. 이 함수들은 이미 입증이 되어있어서 쉽게 안전한 프로그램을 만들 수 있다.

## High order function이란 무엇일까?

## first class(일급 시민)이라는 것은 무엇일까?

## 클로저란 무엇일까?

## 3장 자료구조는 적게, 일은 더 많이

### 제어흐름이란 무엇인가?

프로그램이 정답에 이르기까지 거치는 경로

#### 명령형 프로그램과 함수형 프로그램이 어떻게 다른가?

명령형 프로그램은 무엇을 할지 세세하게 지정한다. 예르들어 분기를 한다면 각 조건에 따라 나눠주어야 한다.

함수형 프로그램은 어떻게 보다는 무엇을 할지에 대해서 나열하는 프로그램이다.
어떻게 서술하는지에 차이가 있다.

##### 예제 라면을 끓인다

```js
function 라면을 끓여라() {
  const 냄비 = 냄비를 가져온다.
  const 면, 스프, 건더기 = 봉지를 뜯는다.
  
  물을 넣는다.
  물을 끓인다.
  스프 뜯는다
  면 넣는다
}
```

```js
function 어디(공간) {
  return function 넣는다(재료) {
  }
}

function 함수형으로 라면을 끓여라() {
  flow(
    넣는다(냄비)
    넣는다(물)
    넣는다(스프)
    끓인다
    먹는다
  )
}
```

### 메서드란 무엇인가?

어떤 객체가 할 수 있는 행위를 메서드라고 부른다.

### 메서드 체이닝이란?

여러개의 메서드를 연달아 실행하는 것.

```js
'function'
  .subString(0, 10)
  .toLowerCase();
```

### 함수 체이닝이란?

작업을 수행하기 위해 무슨일을 해야 하는지 기술된 함수를 인수로 받는다.
함수형 프로그래밍은 자료구조를 새로 만들어 어떤 요건을 충족시키는 것이 아니라, 배열 등의 흔한 자료구조를 이용해 다수의 굵게 나뉜 고계연슨을 적용한다.

```js
['a', 'b', 'c', 'd', null]
  .filter((it) => it)
  .map((it) => it.toUpperCase());

// [A, B, C, D];
```

### 재귀적인 사고 방식이란?

반복적인 연산에서 자기 자신 또는 변형한 버전을 생각하는 것.
재귀는 주어진 문제를 자기 반복적인 문제들로 잘게 분해한 다음, 이들을 다시 조합해 원래 문제의 정답을 찾는 기법

예제

```js
const numbers = [1, 2, 3, 4, 5];

let sum = 0;

for (let i = 0; i < numbers.length;i++) {
  sum += numbers[i];
}

console.log(sum); // 15
```

```
1 + [2, 3, 4, 5];
1 + 2 + [3, 4, 5];
1 + 2 + 3 + [4, 5];
1 + 2 + 3 + 4 + [5];
1 + 2 + 3 + 4 + 5 + [];
15
```

```hs
sum :: [Int] -> Int
sum [] = 0
sum (x:xs) = x + sum xs
```

### 어떻게 반복적인 문제들로 잘게 분해할 수 있는가?

* base case
* recursive case

### 꼬리 호출 최적화

1 + sum[2, 3, 4, 5]
(1 + 2) + sum[3, 4, 5]
(1 + 2 + 3) + sum[4, 5]
(1 + 2 + 3 + 4) + sum[5]
(1 + 2 + 3 + 4 + 5) + sum[]

```js
// 재귀
const sum = (numbers) => {
  if (numbers.isEmpty()) {
    return 0;
  }

  // 1 + sum[2,3,4,5] => 스택에 넣어놓음 
  // 1 + 2 + sum[3,4,5] => 스택에 넣어놓음
  return first(numbers) + sum(drop(numbers));
}

// 꼬리 재귀 => 반복문으로 변경 가능 => 반복문으로
const sum = (numbers, sum = 0) => {
  if (numbers.isEmpty()) {
    return sum;
  }

  // sum([2,3,4,5], 0 + 1)
  // 스택이 2개 => 콜스택 터짐이 없다.
  return sum(drop(numbers), sum + first(numbers));
}
```

### 추상화 수준이 높다는 것은 무엇을 의미하는가?

```js
const isEmpty = (arr) => {
  if (arr === undefined) {
    return true;
  }

  if (arr === null) {
    return true;
  }

  arr.length === 0
}
```

```js
if (restaurants.length === 0) {
  return 비어있다;
}
```

### 수동 루프를 왜 없애야 하는가?

그게 뭐냐? 하스켈에 없어서 못썼습니다.
더 명시적이다. 의도가 더 잘 드러난다.

### reduce, map, filter란?

## 챕터 4 재사용 가능한 모듈적인 코드로

### 체이닝이란?

### 파이프라인이란? 무엇인가?

함수가 반환이 되면 리턴한 변수를 함수가 받아서 함수 체이닝의 또다른 방법이다.

### 함수 합성이란 무엇인가?

함수하나의 반환값을 다른 함수의 입력값으로 쓰는 것

### 커리된, 커리되지 않은 함수를 어떻게 구분할 수 있는가

커리된 함수는 모자란 매개변수가 비어있는 새로운 함수를 반환한다.
여러개의 매개변수를 받는 함수를, 매개변수를 하나만 받도록 쪼개는데, 각 매개변수를 넣으면 매개변수가 부분적용된 새로운 함수를 반환한다.

커리되지 않은 함수는 모자란 매개변수가 undefiend이다.

### 부분적용이란 무엇인가

오리처럼 행동하면 오리다.

### 덕 타이핑

### 함수의 인수를 적게 해야하는 이유

### 튜플이란 무엇인가? 함수간 데이터를 변환할 떄 튜플이 좋은 이유는?

만들어 놓으면 바꿀 수 없는 key value 자료형.

## 펑터란 무엇인가?

매핑이 가능한 자료형

## 모나드란 무엇인가?

Context가 있는 값에 일반 값을 받고 컨텍스트가 있는 값을 반환하는 함수를 매핑할 수 있는 자료형.

### Maybe 예제

```js
class Maybe {
  static just(a) {
    return new Just(a);
  }

  static nothing() {
    return new Nothing();
  }

  static fromNullable(a) {
    return (a !== null && a !== undefined) ? Maybe.just(a) : Maybe.nothing();
  }

  static of(a) {
    return Maybe.just(a);
  }

  get isNothing() {
    return false;
  }

  get isJust() {
    return false;
  }
}
class Just extends Maybe {
  constructor(value) {
    super();
    this._value = value;
  }

  get value() {
    return this._value;
  }

  map(f) {
    return Maybe.fromNullable(f(this._value));
  }

  chain(f) {
    return f(this._value);
  }

  getOrElse() {
    return this._value;
  }

  filter(f) {
    Maybe.fromNullable(f(this._value) ? this._value : null);
  }

  get isJust() {
    return true;
  }

  toString() {
    return `Maybe.Just(${this._value})`;
  }
}
class Nothing extends Maybe {
  map(f) {
    return this;
  }

  chain(f) {
    return this;
  }

  get value() {
    throw new TypeError('Nothing 값을 가져올 수 없습니다.');
  }

  getOrElse(other) {
    return other;
  }

  filter() {
    return this._value;
  }

  get isNothing() {
    return true;
  }

  toString() {
    return 'Maybe.Nothing';
  }
}

const benefits = {
  PERCENT: '%',
  PRICE: '원',
};

const getAmountText = ({ type, amount }) =>
  Maybe.just(type)
    .map(getPropertOf(benefits))
    .map((it) => `${amount} ${it}`)
    .getOrElse('');

test('maybe', () => {
  const amount = 10000;
  expect(getAmountText({ type: 'PRICE', amount }))
    .toBe(`${amount} 원`);

  expect(getAmountText({ type: 'PERCENT', amount }))
    .toBe(`${amount} %`);

  expect(getAmountText({ type: 'FREE', amount }))
    .toBe('');
});
```

### Either 예제

```js
class Either {
  constructor(value) {
    this._value = value;
  }

  get value() {
    return this._value;
  }

  static left(a) {
    return new Left(a);
  }

  static right(a) {
    return new Right(a);
  }

  static fromNullable(val) {
    return val !== null && val !== undefined ? Either.right(val) : Either.left(val);
  }

  static of(a) {
    return Either.right(a);
  }
}

class Left extends Either {
  map(_) {
    return this; // noop
  }

  get value() {
    throw new TypeError("Can't extract the value of a Left(a).");
  }

  getOrElse(other) {
    return other;
  }

  orElse(f) {
    return f(this._value);
  }

  chain(f) {
    return this;
  }

  getOrElseThrow(a) {
    throw new Error(a);
  }

  filter(f) {
    return this;
  }

  get isRight() {
    return false;
  }

  get isLeft() {
    return true;
  }

  toString() {
    return `Either.Left(${this._value})`;
  }

  tap(f) {
    return this;
  }
}

class Right extends Either {
  map(f) {
    return Either.of(f(this._value));
  }

  getOrElse(other) {
    return this._value;
  }

  orElse() {
    return this;
  }

  chain(f) {
    return f(this._value);
  }

  getOrElseThrow(_) {
    return this._value;
  }

  filter(f) {
    return Either.fromNullable(f(this._value) ? this._value : null);
  }

  get isRight() {
    return true;
  }

  get isLeft() {
    return false;
  }

  tap(f) {
    f();
    return this;
  }

  toString() {
    return `Either.Right(${this._value})`;
  }
}

const getStickers = (status) => new Promise((resolve, reject) => {
  if (status === true) {
    resolve(
      Either.right({
        stickers: ['할인', '증정'],
        total: 2
      })
    );
  } else {
    resolve(Either.left('getStickers error'));
  }
});

test('either', async () => {
  let error;
  const either = await getStickers(true);

  either
    .map((it) => it.stickers.filter((i) => i === '할인'))
    .tap(() => {
      console.log('성공!');
    })
    .orElse((err) => {
      error = err;
      console.log('실패!');
    });
});
```

## See also

* 함수형 프로그래밍이란 무엇인가? - https://medium.com/@jooyunghan/%ED%95%A8%EC%88%98%ED%98%95-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D%EC%9D%B4%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80-fab4e960d263
* 함수형 자바스크립트 - http://www.kyobobook.co.kr/product/detailViewKor.laf?barcode=9791162240427