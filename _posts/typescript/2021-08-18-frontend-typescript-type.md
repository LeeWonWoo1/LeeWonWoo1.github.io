---
title: "[Typescript] Typescript Types"
excerpt: Typescript types
categories:
- Typescript
tags:
- - Typescript
  - Programming
  - Web
  - Node.js
toc: true
toc_sticky: true
popular: true
date: '2021-08-18T21:00:00'
last_modified_at: 2021-08-18T21:00:00
---

## 1. Type Annotation

```ts
// 타입 에러
let a = "Amy";
a = 39;  // Error

// a의 타입을 string로 지정
let a: string;

a = "Amy";
a = 39;  // Error

// a의 타입을 number로 지정
let a: number;

a = "Amy";  // Error
a = 39;

// 함수 내의 type annotation
function hello(b: number) {
  
}
hello(39);
hello('Amy');  // Error
```


<br>

## 2. Typescript Types vs Javascript Types

- Typescript : Static Types(개발 중간에 타입 체크)
- Javascript : Dynamic Types(runtime에 들어가야 체크)

```js
// Javascript

function add(n1, n2) {
  // runtime에서 에러 체크
  if (typeof n1 !== 'number' || typeof n2 !== 'number') {
    throw new Error('Incorrect input!');
  }
  return n1 + n2;
}

const result = add(10, 20);
```

<br>

```ts
// Typescript

// 개발중에 체크
function add(n1: number, n2: number) {
  return n1 + n2;
}

const result = add(10, 20);
```

<br>

- Typescript에서 제공하는 데이터 타입
- Javascript 기본 자료형 포함(superset)
    - ECMAScript 표준에 따른 기본 자료형(6가지)
    - Boolean
    - Number
    - String
    - Null
    - Undefined
    - Symbol(ECMAScript 6에 추가)
    - Array: object형
- 프로그래밍을 도울 몇가지 타입 추가 제공
    - Any, Void, Never, Unknown
    - Enum
    - Tuple: object형


<br>

## 3. Primitive Types

- 오브젝트와 레퍼런스 형태가 아닌 실제 값을 저장하는 자료형
- Primitive 형의 내장 함수를 사용 가능한 것은 Javascript 처리 방식 덕분
- Primitive types은 모두 **_소문자_**
- ES2015 기준 6가지
    - boolean
    - number
    - string
    - symbol
    - null
    - undefined
- literal 값으로 Primitive 타입의 서브 타입을 나타낼 수 있음
- wrapper 객체로 만들 수 있음

```ts
// 내장함수 사용 가능
let name = 'Amy';
name.toString();

// literal 값으로 Primitive 타입의 서브 타입 표시
true;
'hello';
3.14;
null;
undefined;

// wrapper 객체(Typescript에서는 권장하지 않음)
new Boolean(false);  // typeof new Boolean(false) : 'object'
new String('world');  // typeof new String('world') : 'object'
new Number(29);  // typeof new Number(29) : 'object'
```


<br>

## 4. boolean

```ts
// boolean.ts

let isDone: boolean = false;
isDone = true;
console.log(typeof isDone)  // boolean
console.log(isDone);  // true

let isOk: Boolean = true;
isOk = false;
console.log(typeof isOk);  // boolean
console.log(isOk);  // false

let isNotOk: boolean = new Boolean(true);  // Error
```

<br>

```bash
$ nxp tsc
$ node boolean.js  # boolean
```


<br>

## 5. number

- Javascript와 같이 Typescript의 모든 숫자는 부동 소수점 값
- 10진수 및 16진수 외에도, ECMAScript 2015에 도입된 2진수 및 8진수 지원
- NaN
- 1_000_000과 같은 표기 가능

```ts
// number.ts

// 10진수 리터럴
let decimal: number = 7;

// 16진수 리터럴
let hex: number = 0xf00e;

// 2진수 리터럴
let binary: number = 0b1100;

// 8진수 리터럴
let octal: number = 0o732;

// NaN
let notANumber: number = NaN;

// 밑줄 표기
let underscoreNum: number = 1_000_000;
```


<br>

## 6. string

- 텍스트 형식을 참조하기 위해 `string` 형식을 사용
- 문자열 데이터를 둘러싸기 위해 큰 따옴표나 작은 따옴표를 사용

```ts
// string.ts

let myName: string = 'Lee';
myName = "LWW";
```

<br>

### - Template String

- 행에 걸쳐 있거나, 표현식을 넣을 수 있는 문자열
- 이 문자열은 backtick 기호에 둘러쌓여 있음
- 포함된 표현식은 &#96;${expr}&#96; 와 같은 형태로 사용

```ts
// template string 사용
let fullName: string = 'WW Lee';
let age: number = 29;
let sentence: string = `Hello, My name is ${fullName}.

I'll be ${age + 1} years old next month.`;

console.log(sentence);  // Hello, My name is WW Lee.

                        // I'll be 30 years old next month.

// template string을 사용하지 않을 경우
let sentence: string = "Hello, My name is " + fullName + ".\n\n" +
  "I'll be " + (age + 1) + " years old next month.";
```

<br>

```bash
$ nxp tsc
$ node string.js
```


<br>

## 7. Symbol

- ECMAScript 2015에 추가
- new Symbol로 사용할 수 없음
- Symbol을 함수로 사용해서 symbol 타입을 만들 수 있음
- Primitive type의 값을 담아서 사용
- 고유하고 수정 불가능한 값으로 만들어 줌
- 주로 접근을 제어하는데 쓰는 경우가 많음

```json
// tsconfig.json

"lib": [
  "ES2015",
  "DOM"
]
```

<br>

```ts
// symbol.ts

console.log(Symbol('foo') === Symbol('foo'))  // false

const sym = Symbol();
const obj = {
  [sym]: "value",
};

obj["sym"];  // 접근 불가
obj[sym];
```

<br>

```bash
$ nxp tsc
$ node symbol.js
```


<br>

## 8. null & undefined

- Typescript에서 null과 undefined는 실제로 각각 null과 undefined 타입을 가짐
- void와 마찬가지로, 그 자체로는 그다지 유용하지 않음
- 둘 다 소문자만 존재
- 다른 모든 타입의 서브타입으로 존재
- 컴파일 옵션에서 &#96;--strictNullChecks&#96; 사용하면, void나 자기 자신에만 할당 가능
    - 이 경우, null과 undefined를 할당할 수 있게 하려면, union type을 이용해야 함

```ts
// null.ts

let MyName: string = null;  // Error
let u: undefined = null;  // Error

let v: void = undefined;
let union: string | null = null;
union = "LWW";
```

<br>

### - null in Javascript

- null이라는 값으로 할당된 것
- 무언가 있는데, 사용할 준비가 덜 된 상태
- null 타입은 null 값만 가질 수 있음
- 런타임에서 typeof 연산자를 이용해 알아내면, object

### - undefined in Javascript

- 값을 할당하지 않은 변수는 undefined 값을 가짐
- 무언가가 아예 준비가 안된 상태
- object의 property가 없을 때도 undefined
- 런타임에서 typeof 연산자를 이용해 알아내면, undefined


<br>

## 9. object

- Primitive type이 아닌 것을 나타내고 싶을 때 사용하는 타입
- Primitive type이 아닌것
    - number, string, boolean, bigint, symbol, null, undefined가 아닌 것

```ts
// object.ts

// person1은 object 타입이 아님
// person1은 {name: string, age: number} 타입
const person1 = {
  name: 'LWW',
  age: 29
};

// object 타입
const person2 = Object.create({
  name: 'LWW',
  age: 29
});

let obj: object = {};
obj = {name: 'LWW'};
obj = [{name: 'LWW'}];
obj = 29;  // Error
obj = 'LWW';  // Error
obj = true;  // Error
obj = 100n;  // Error
obj = Symbol();  // Error
obj = null;  // Error
obj = undefined  // Error

declare function create(o: object | null): void;
create({prop: 0});
create(null);
create(42);  // Error
create("string");  // Error
create(false);  // Error
create(undefined);  // Error

Object.create(0);  // Error
```


<br>

## 10. Array

- 원래 Javascript에서 array는 객체
- 사용방법
    - Array<타입>
    - 타입[]

```ts
// array.ts

// 방법 1(선호)
let list1: number[] = [1, 2, 3];

// 방법 2
let list2: Array<number> = [4, 5, 6];

// 여러 타입
let list3: (number | string)[] = [7, 8, 9, "0"];
```


<br>

## 11. Tuple

```ts
// tuple.ts

let x: [string, number];

x = ['hello', 29];
x = [10, 'world']  // Error
x[3] = 'item';  // Error

const person: [string, number] = ["LWW", 29];

// const first: string, const second: number
const [first, second] = person;
```


<br>

## 12. any

- 어떤 타입이어도 상관없는 타입
- any를 써야하는데 쓰지 않으면 오류를 뱉는 컴파일 옵션 nolmplicitAny가 있음
- any는 계속해서 개체를 통해 전파됨
- 모든 편의는 타입 안전성을 잃는 대가로 오는 것
- 타입 안전성은 Typescript를 사용하는 주요 동기
- 최대한 쓰지 않는 것을 권장
- 컴파일 타임에 타입 체크가 정상적으로 이루어지지 않을 수 있음

```ts
// any.ts

function returnAny(message: any): any {
  console.log(message);
}

const any1 = returnAny('리턴은 아무거나');
any1.toString();

// 전파를 통해 안전성을 잃음
let losselyTyped: any = {};
const d = losselyTyped.a.b.c.d;

// any 누수 막는 법
function leakingAny(obj: any) {
  // 타입을 지정
  const a: number = obj.num;  // const a: number
  const b = a + 1;  // const b: number
  return b;
}

const c = leakingAny({ num: 0 });  // const c: number
c.indexOf("0");
```


<br>

## 13. unknown

- 응용 프로그램을 작성할 때 모르는 변수의 타입을 묘사해야 할 수 있음
- 이러한 값은 동적 콘텐츠의 모든 값을 의도적으로 수락하기를 원할 수 있음
- 컴파일러와 사람에게 이 변수가 무엇이든 될 수 있음을 알려주는 unknwon 타입을 제공
- any와 짝으로 any보다 Type-safe한 타입
    - any와 같이 아무거나 할당 가능
    - 컴파일러가 타입을 추론할 수 있게끔 타입의 유형을 좁힘
    - 타입을 확정해주지 않으면 다른 곳에 할당할 수 없고, 사용 불가
- unknown 타입을 사용하면, runtime error를 줄일 수 있음
- 사용 전에 데이터의 일부 유형의 검사를 수행하야 함을 알리는 API에 사용 가능

```ts
// unknown.ts

declare const maybe: unknown;
const aNumber: number = maybe;  // Error

if (maybe === true) {
  const aBoolean: boolean = maybe;  // const maybe: true
  const aString: string = maybe;  // Error
}

if (typeof maybe === 'string') {
  const aString: string = maybe;  // const maybe: string
  const aBoolean: boolean = maybe;  // Error
}
```


<br>

## 14. never

- never 타입은 모든 타입의 서브타입이며, 모든 타입에 할당 할 수 있음
- never에는 어떤 것도 할당할 수 없음
- any조차도 never에 할당할 수 없음
- 잘못된 타입을 넣는 실수를 막고자 할 때 사용

```ts
// never.ts

function error(message: string): never {
  throw new Error(message);
}

function fail() {
  return error('failed');
}

function infiniteLoop(): never {
  while (true) { }
}

let a: string = 'hello';
if (typeof a !== 'string') {
  a;  // let a: never
}

declare const b: string | number;
if (typeof b !== "string") {
  b;  // const b: number
}

type Indexable<T> = T extends string ? T & { [index: string]: any } : never;
type ObjectIndexable = Indexable<{}>;

const b: Indexable<{}> = '';  // Error
```


<br>

## 15. void

- 리턴값으로 무엇도 하지 않음을 명시적으로 표현

```ts
function returnVoid(message: string): void {
  console.log(message);
  return undefined;
}

const r = returnVoid('리턴이 없음.');  // const r: void
```