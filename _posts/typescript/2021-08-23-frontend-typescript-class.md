---
title: "[Typescript] Class"
excerpt: Typescript Class
categories:
- Typescript
tags:
- - Typescript
  - Programming
  - Web
  - NPM
toc: true
toc_sticky: true
popular: true
date: '2021-08-23T19:00:00'
last_modified_at: 2021-08-23T19:00:00
---

## 1. 클래스란?

- Object를 만드는 설계도
- 클래스 이전에 object를 만드는 기본적인 방법은 function
- Javascript에도 class는 ES6부터 사용 가능
- OOP을 위한 초석
- Typescript에서는 class도 사용자가 만드는 타입의 하나

```bash
# 프로젝트 생성

$ mkdir ts-class
$ cd ts-class
$ npm init -y
$ npm i typescript -D
$ npx tsc --init
```

<br>

```ts
// example.ts

// 간단한 Class 만들기 1
class Person { }

const p1 = new Person();
console.log(p1);  // Person {}
```

<br>

```bash
# 컴파일

$ npx tsc
$ node example.ts
```

<br>

```js
// example.js

// es5
"use strict";
var Person = /** @class */ (function () {
    function Person() {
    }
    return Person;
}());
var p1 = new Person();
console.log(p1);
```

<br>

```json
// tsconfig.json

// 컴파일 es6로 변경
"target": "es6"
```

<br>

```js
// example.js

// es6
"use strict";
class Person {
}
const p1 = new Person();
console.log(p1);
```

<br>

```ts
// example.ts

class Person {
  name;
  constructor(name: string) {
    this.name = name;
  }
}

const p2 = new Person("LWW");
console.log(p2);  // Person { name: 'LWW' }
```

<br>

- class 키워드를 이용하여 class를 만들 수 있음
- class 이름은 보통 대문자를 이용
- new를 이용하여 class를 통해 object를 만들 수 있음
- constructor를 이용하여 object를 생성하면서 값을 전달할 수 있음
- this를 이용해서 만들어진 object를 가리킬 수 있음
- Javascript로 컴파일되면 ES5의 경우 function으로 변경됨


<br>

## 2. Constructor & Initialize

- 생성자 함수가 없으면, 디폴트 생성자가 불림
- 개발자가 만든 생성자가 하나라도 있으면, 디폴트 생성자는 사라짐
- strict 모드에서 property를 선언하는 곳 또는 생성자에서 값을 할당해야 함
- peoperty를 선언하느 곳 또는 생성자에서 값을 할당하지 않는 경우에는 !를 붙여서 위험을 표현
- class의 property가 정의되어 있지만, 값을 대입하지 않으면 undefined
- 생성자에는 async를 설정할 수 없음

```ts
// example.ts

class Person {
  name: string = 'LWW';
  age!: number;

  constructor(age?: number) {
    if (age === undefined) {
      this.age = -1;
    } else {
      this.age = age;
    }
  }

  async init() {

  }
}

const p3: Person = new Person(29);
const p4: Person = new Person();

console.log(p3);  // Person { name: 'LWW', age: 29 }
console.log(p3.age);  // 29
console.log(p4);  // Person { name: 'LWW', age: -1 }
```


<br>

## 3. 접근 제어자

- 접근 제어자에는 public, private, protected가 있음
- 설정하지 않으면 public
- 클래스 내부의 모든 곳(생성자, 프로퍼티, 메서드)에 설정 가능
- private으로 설정하면 클래스 외부에서 접근할 수 없음
- Javascript에서는 private를 지원하지 않아 이름 앞에 _를 붙여서 표현했음


<br>

## 4. Initialization in Constructor Parameters

- 생성자의 Parameter를 받아 그 클래스에 Property로 초기화 하는 방법

```ts
// example.ts

class Person {
  public constructor(public name: string, private age: number) { }
}

const p5: Person = new Person("LWW", 29);
console.log(p5);  // Person { name: 'LWW', age: 29 }
```


<br>

## 4. Getters, Setters

```ts
// example.ts

class Person {
  public constructor(private _name: string, private age: number) { }

  get name() {
    console.log('get');
    return this._name + " 입니다.";
  }

  set name(n: string) {
    console.log('set');
    this._name = n;
  }
}

const p6: Person = new Person("LWW", 29);

// get을 하는 함수 getter
console.log(p6.name);  // get
                       // LWW 입니다.

// set을 하는 함수 setter
p6.name = 'Tom';  // set

console.log(p6.name);  // get
                       // Tom 입니다.
```


<br>

## 5. Readonly Property

- Set은 불가, Get만 가능
- Initialization 부분과 Constructor 안에서만 readonly property를 지정해 줄 수 있음
- 다른 메서드 등에서는 Set할 수 없음
- Property를 초기값으로 고정하고 다른 값으로 변경하고 싶지 않을 때, readonly를 붙여서 다른 개발자가 Set할 때 에러를 발생시킴

```ts
// example.ts

class Person {
  public readonly name: string = "LWW";
  private readonly country: string

  public constructor(private _name: string, private age: number) {
    this.country = "Korea";
  }

  hello() {
    this.country = "Japan";  // Error! 읽기 전용 속성이므로 ...
  }
}

const p6: Person = new Person("LWW", 29);

console.log(p7.name);
p7.name = 'Tom';  // Error! 읽기 전용 속성이므로 ...
console.log(p7.name);
```


<br>

## 6. Index Signatures in Class

- Class 안에서 Index Signatures를 선언하고 사용하는 방법
- Property가 고정된 형태가 아닐 때, 즉 동적으로 들어올 때 사용

```ts
// example.ts

class Students {
  // [index: string]: string;
  [index: string]: "male" | "female";
  LWW: "male" = "male"
}

const a = new Students();
a.LWW = "male";
a.Tom = "male";
console.log(a)  // Students { LWW: 'male', Tom: 'male' }

const b = new Students();
b.Amy = "female";
b.James = "male";
b.Anna = "female";
console.log(b)  // Students { Amy: 'female', James: 'male', Anna: 'female' }
```


<br>

## 7. Static Properties & Methods

```ts
// example.ts

class Person {
  private static CITY = "Seoul";

  public static sayHello() {
    console.log("안녕하세요.")
  }
  public hello() {
    console.log("Hi.", Person.CITY);
  }
  public change() {
    Person.CITY = 'Busan';
  }
}

const p8 = new Person();
Person.sayHello();  // 안녕하세요.
p8.sayHello();  // Error!
p8.hello();  // Hi. Seoul

const p9 = new Person();
p9.hello();  // Hi. Seoul
p8.change();
p9.hello();  // Hi. Busan
```


<br>

## 8. Singletons

```ts
// example.ts

class ClassName {
  private static instance: ClassName | null = null;

  public static getInstance(): ClassName {
    // ClassName으로부터 만든 object가 있으면 그걸 return
    // ClassName으로부터 만든 object가 없으면 만들어서 return
    if (ClassName.instance === null) {
      ClassName.instance = new ClassName();
    }
    return ClassName.instance;
  }

  private constructor() { }
}

const a = ClassName.getInstance();
const b = ClassName.getInstance();
const c = new ClassName();  // Error!

console.log(a === b);  // true
```


<br>

## 9. 상속

```ts
// example.ts

// Parent 클래스
class Parent {
  constructor(protected _name: string, private _age: number) { }

  public print(): void {
    console.log(`이름은 ${this._name} 이고, 나이는 ${this._age} 입니다.`);
  }

  protected printName(): void {
    console.log(this._name, this._age);
  }
}

const p = new Parent("LWW", 29);
p._age  // Error!
p._name  // Error!
p.print();  // 이름은 LWW 이고, 나이는 29 입니다.

// Child 클래스
class Child extends Parent {
  public gender = 'female';

  constructor(age: number) {
    super('LWW Jr.', age);
    this.printName();
  }
}

const c = new Child(5);  // LWW Jr. 5
c._age  // Error!
c._name  // Error!
c.gender
c.print();  // 이름은 LWW Jr. 이고, 나이는 5 입니다.
```


<br>

## 10. Abstract Classes

- 상속을 이용해 class를 구조적으로 작성하는데 도움을 줌

```ts
// example.ts

abstract class AbstractPerson {
  protected _name: string = 'LWW';

  abstract setName(name: string): void;
}

const p1 = new AbstractPerson()  // Error!

class Person extends AbstractPerson {
  setName(name: string): void {
    this._name = name;
  }
}

const p2 = new Person();
console.log(p2);  // Person { _name: 'LWW' }
p2.setName('Tom');
console.log(p2);  // Person { _name: 'Tom'}
```