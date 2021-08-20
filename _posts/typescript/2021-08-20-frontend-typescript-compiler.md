---
title: "[Typescript] 컴파일러"
excerpt: Typescript Compiler
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
date: '2021-08-20T20:00:00'
last_modified_at: 2021-08-20T20:00:00
---

## 1. Compilation Context

[https://radlohead.gitbook.io/typescript-deep-dive/](https://radlohead.gitbook.io/typescript-deep-dive/){:target="_blank"} 
{: .notice--info}

- Typescript를 Javascript로 변환하는데 사용하는 Typescript Compiler가 어떤 파일과 어떤 방식으로 컴파일 할 것인지를 규명한 것이 Compilation Context
- tsconfig.json 파일에 선언되어 있음


<br>

## 2. tsconfig schema

[http://json.schemastore.org/tsconfig](http://json.schemastore.org/tsconfig){:target="_blank"} 
{: .notice--info}

- 최상위 프로퍼티
    - compileOnSave
    - extends
    - conpileOptions
    - files
    - include
    - exclude
    - references

```bash
# 새 프로젝트 생성

$ mkdir compilation-context

$ cd compilation-context

$ npm init -y

$ npm i typescript -D

$ npx tsc --init

$ cat tsconfig.json
```


<br>

## 3. compileOnSave

- Save 하면 컴파일
- true / false (default false)
- Visual Studio 2015 with Typescript 1.8.4 이상
- atom-typescript 플러그인

```json
// 형태

{
  ...,
  "compileOnSaveDefinition": {
    "properties": {
      "compileOnSave": {
        "description": "Enable Compile-on-Save for this project.",
        "type": "boolean"
      }
    }
  },
  ...,
}
```

<br>

```json
// tsconfig.json

{
  "compileOnSave": true,
  "compilerOptions": {
    ...
  }
}
```


<br>

## 4. extends

- 파일 (상대) 경로명: string
- Typescript 2.1 New Spec

```json
// 형태

{
  ...,
  "extendsDefinition": {
    "properties": {
      "extends": {
        "description": "Path to base configuration file to inherit from. Requires TypeScript version 2.1 or later.",
        "type": "string"
      }
    }
  },
  ...,
}
```

<br>

```json
// tsconfig.json

{
  "extends": "./base.json",
  "compilerOptions": {
    ...
  // "strict": true 옵션 주석처리
  }
}


// base.json
{
  "compilerOptions": {
    "strict": true
  }
}
```

<br>

```ts
// test.ts

const a: number = undefined;  // Error
```

<br>

```bash
# 설정 다운로드
$ npm install --save-dev @tsconfig/deno
```

<br>

```json
// 설정 적용
{
  "extends": "@tsconfig/deno/tsconfig.json",
  ...
}
```


<br>

## 5. files, include, exclude

- 셋다 설정이 없으면, 전부다 컴파일 하려고 함
- files
    - 상대 혹은 절대 경로의 리스트 배열
    - exclude 보다 강함
- include
    - glob 패턴 (마치 .gitignore)
    - exclude 보다 약함
    - *같은 것을 사용하면, .ts / .tsx / .d.ts 만 include(allowJS)
- exclude
    - glob 패턴 (마치 .gitignore)
    - 설정 안하면 4가지(node_modules, bower_components, jspm_packages, &#60;outDir&#62;)를 default로 제외함
    - &#60;outDir&#62;은 include에 있어도 항상 제외

```json
{
  ...
  // files 형태
  "filesDefinition": {
    "properties": {
      "files": {
        "description": "If no 'files' or 'include' property is present in a tsconfig.json, the compiler defaults to including all files in the containing directory and subdirectories except those specified by 'exclude'. When a 'files' property is specified, only those files and those specified by 'include' are included.",
        "type": "array",
        "uniqueItems": true,
        "items": {
          "type": "string"
        }
      }
    }
  },
  // exclude 형태
  "excludeDefinition": {
    "properties": {
      "exclude": {
        "description": "Specifies a list of files to be excluded from compilation. The 'exclude' property only affects the files included via the 'include' property and not the 'files' property. Glob patterns require TypeScript version 2.0 or later.",
        "type": "array",
        "uniqueItems": true,
        "items": {
          "type": "string"
        }
      }
    }
  },
  // include 형태
  "includeDefinition": {
    "properties": {
      "include": {
        "description": "Specifies a list of glob patterns that match files to be included in compilation. If no 'files' or 'include' property is present in a tsconfig.json, the compiler defaults to including all files in the containing directory and subdirectories except those specified by 'exclude'. Requires TypeScript version 2.0 or later.",
        "type": "array",
        "uniqueItems" : true,
        "items": {
          "type": "string"
        }
      }
    }
  },
  ...,
}
```


<br>

## 6. compileOptions - typeRoots, types

- @types는 Typescript 2.0부터 사용 가능한 내장 type definition 시스템
- 아무 설정도 하지 않으면, node_modules/@types라는 모든 경로를 찾아서 사용
- typeRoots를 사용하면, 배열 안에 들어있는 경로들 아래서만 가져옴
- types를 사용하면, 배열 안의 모듈 혹은 ./node_modules/@types/ 안의 모듈 이름에서 찾아옴, [] 빈 배열을 넣으면 이 시스템을 이용하지 않겠다는 뜻
- typeRoots와 types를 같이 사용하지 않음

```json
{
  ...,
  // typeRoots 형태
  "typeRoots": {
    "description": "Specify multiple folders that act like `./node_modules/@types`.",
    "type": "array",
    "uniqueItems": true,
    "items": {
      "type": "string"
    },
    "markdownDescription": "Specify multiple folders th ... "
  },
  // types 형태
  "types": {
    "description": "Specify type package names to be included without being referenced in a source file.",
    "type": "array",
    "uniqueItems": true,
    "items": {
      "type": "string"
    },
    "markdownDescription": "Specify type package names to be ... "
  },
  ...,
}
```

<br>

```bash
# terminal

$ npm i react
```

<br>

```ts
// test.ts

import React from "react";  // Error
```

<br>

```bash
# terminal

$ npm i --save-dev @types/react
```

<br>

```ts
// test.ts

import React from "react";
```


<br>

## 7. compileOptions - target, lib

- target
    - 빌드의 결과물을 어떤 버전으로 할 것인지 결정
    - 지정을 하지 않으면 es3
- lib
    - 기본 type definition 라이브러리를 어떤 것을 사용할 것인지 결정
    - lib를 지정하지 않을 때,
        - target이 'es3'이고, 디폴트로 lib.d.ts를 사용
        - target이 'es5'이면, 디폴트로 dom, es5, scripthost를 사용
        - target이 'es6'이면, 디폴트로 dom, es6, dom.iterable, scripthost를 사용
    - lib를 지정하면 그 lib 배열로만 라이브러리를 사용
        - 빈 [] : Error. 'no definition found ... '

```json
// target 형태

{
  "target": {
    "description": "Set the JavaScript language version for emitted Javascript and include compatible library declarations.",
    "type", "string",
    "default": "ES3",
    "anyOf": [
      {
        "enum": [
          "ES3",
          "ES5",
          "ES6",
          "ES2015",
          ...
          "ES2020",
          "ESNext"
        ]
      },
      {
        "pattern": "^([Ee][Ss]([356]|(20(1[56789]|20))|[Nn][Ee][Xx][Tt]))$"
      }
    ],
    "markdownDescription": "Set the JavaScript language version ..."
  },
  ...,
}
```

<br>

```json
// tsconfig.json
// target은 es5

"target": "es5"
```

<br>

```ts
// test.ts

const hello = () => {};
```

<br>

```bash
# terminal

npx tsc
```

<br>

```js
// test.js
// es5 에서는 arrow function이 변경되서 컴파일 됨

"use strict";
var hello = function () { };
```

<br>
<br>

```json
// tsconfig.json
// target을 es6로 변경

"target": "es6"
```

<br>

```ts
// test.ts

const hello = () => {};
```

<br>

```bash
# terminal

npx tsc
```

<br>

```js
// test.js
// es6 에서는 arrow function이 그대로 컴파일 됨

"use strict";
const hello = () => { };
```

<br>

```json
// lib 형태

{
  "lib": {
    "description": "Specify a set of bundled library declaration files that describe the target runtime environment.",
    "type": "array",
    "uniqueItems": true,
    "items": {
      "type": "string",
      "anyOf" : [
        {
          "enum": [
            "ES5", "ES6", ...
          ]
        },
        {
          "pattern": "^[Ee][Ss]5|[Ee][Ss]6|[Ee][Ss]7$"
        }
      ]
    }
  }
}
```


<br>

## 8. compileOptions - outDir, outFile, rootDir

```json
{
  // outFile 형태
  "outFile": {
    "description": "Specify a file that bundles all outputs into one JavaScript file. If `declaration` is true, also designates a file that bundles all .d.ts output.",
    "type": "string",
    "markdownDescription": "Specify a file that bundles all outputs ..."
  },
  // outDir 형태
  "outDir": {
    "description": "Specify an output folder for all emitted files.",
    "type": "string",
    "markdownDescription": "Specify an output folder for all emitted files. ..."
  },
  // rootDir 형태
  "rootDir": {
    "description": "Specify the root folder within your source files.",
    "type": "string",
    "markdownDescription": "Specify the root folder within your source files. ..."
  }
}
```

<br>

```json
// tsconfig.json

"outDir": "./dist"
"rootDir": "./src"
```

<br>

```ts
// src/test.ts

console.log("hello")
```

<br>

```bash
# terminal

$ npx tsc
```

<br>

```js
// dist/test.js
// dist 폴더가 생성되고 컴파일 됨

console.log("hello")
```


<br>

## 9. compileOptions - strict

```json
// strict 형태

{
  "strict": {
    "description": "Enable all strict type checking options.",
    "type": "boolean",
    "default": false,
    "markdownDescription": "Enable all strict type checking options. ..."
  }
}
```

<br>

* --noImplicitAny
    - 명시적이지 않게 any 타입을 사용, 표현식과 선언제 사용하면 에러 발생
    - Typescript가 추론을 실패한 경우, any가 맞으면 any라고 지정
    - 아무것도 쓰지 않으면, 에러 발생
    - 이 오류를 해결하면, any라고 지정되어 있지 않은 경우는 any가 아닌 것
    - suppressImplicitAnyIndexErrors
        - 인덱스 객체에 인덱스 signature가 없는 경우 오류 발생. 이를 예외처리

```ts
//noImplicitAny
function noImplicitAnyTestFunc(arg) {
  console.log(arg);  // Error! Parameter 'arg' implicitly has an 'any' type.
}


// suppressImplicitAnyIndexErrors
var obj = {
  bar: 10
};

// obj['foo']로 사용할 때, 인덱스 객체라 판단하여, 타입에 인덱스 시그니처가 없는 경우, 에러 발생
obj['foo'] = 10; // Error: Index signature of object type implicitly has an 'any' type
obj['bar'] = 10;  // Okay
obj.baz = 10;

// 이때 suppressImplicitAnyIndexErrors 옵션을 사용하면 예외로 간주하여 에러발생 x
```

<br>

* --noImplicitThis
    - 명시적이지 않게 any 타입을 사용하여, this 표현식에 사용하면 에러 발생

```ts
// noImplicitThis
function noImplicitThisTestFunc(name: string, age: number) {
  this.name = name;
  this.age = age;
  return this;  // Error! 'this' implicitly has type 'any' ...
}


// 첫 번째 매개변수 자리에 this를 놓고, this 타입을 표현하지 않으면 에러
// Javascript에서는 매개변수에 this를 넣으면, 예약어라 SyntaxError 발생
// call / apply / bind와 같이 this를 대체하여 함수 콜을 하는 용도로도 쓰임
// this를 any로 명시적으로 지정하는 것은 합리적
// 물론 구체적인 사용처가 있는 경우 타입을 표현하기도 함
function noImplicitThisTestFunc(this, name: string, age: number) {
  this.name = name;
  this.age = age;
  return this;  // Error! Parameter 'this' implicitly has an 'any' type
}


// Class에서는 this를 사용하면서, noImplicitThis와 관련한 에러가 나지 않음
// CLass에서 constructor를 제외한 멤버 함수의 첫 번째 매개변수도 일반 함수와 마찬가지로 this를 사용할 수 있음
// noImplicitTHis 2
class NoImplicitThisTestClass {
  private _name: string;
  private _age: number;

  constructor(name: string, age: number) {
    this._name = name;
    this._age = age;
  }

  public print(this: NoImplicitThisTestClass) {
    console.log(this._name, this._age)
  }
}

new NoImplicitThisTestClass('LWW', 29).print();
```

<br>

* --strictNullChecks
    - null및 undefined 값이 모든 유형의 도메인에 속하지 않으며, 그 자신을 타입으로 가지거나, any일 경우에만 할당이 가능
    - 한 가지 예외는 undefined에 void 할당 가능
    - strictNullChecks 옵션을 적용하지 않으면
        - 모든 타입은 null, undefined 값을 가질 수 있음
        - string으로 타입을 지정해도, null 혹은 undefined 값을 할당할 수 있음
    - strictNullChecks를 적용하면
        - 모든 타입은 null, undefined 값을 가질 수 있음
        - null, undefined 값을 가지려면 union type을 이용하여 직접 명시해야 함
        - any 타입은 null과 undefined를 가짐
        - 예외적으로 void 타입은 undefined를 가짐
    - strictNullChecks를 적용하지 않고 사용하면, 정확히 어떤 타입이 오는지 개발자 스스로 간과할 수 있음
    - 정말로 null과 undefined를 가질 수 있는 경우, 해당 값을 조건부로 제외하고 사용하는 것이 좋음
    - strictNullChecks를 적용하는 경우, 사용하려는 함수를 선언할 때부터 매개변수와 리턴 값에 정확한 타입을 지정하려는 노력을 기울여야 함

```ts
// strictNullChecks
const a: number = null;
const b: string = undefined;
const c: number | null = null;
const d: any = null;
const e: any = undefined;
const f: void = undefined;
```

<br>

* --strictFunctionTypes
    - 함수 타입에 대한 bivariant 매개변수 검사를 비활성화 함
    - 반환 타입은 공변적, 인자 타입은 반공변적
    - Typescript에서 인자 타입은 공변적이면서, 반공변적임
    - 이 문제를 해결하는 옵션이 strictFunctionTypes
    - 옵션을 켜면 에러가 나지 않던 것을 에러가 발생하게 함

```ts
// strictFunctionTypes
const button = document.querySelector('#id') as HTMLButtonElement;

buttom.addEventListener('keydown', (e: MouseEvent) => {});

// 이전에는 위와 같은 코드도 에러를 발생시키지 않았지만, 이제는 에러 발생
```

<br>

* --strictPropertyInitialization
    - 정의되지 않은 클래스의 속성이 생성자에서 초기화되었는지 확인
    - 이 옵션을 사용하려면 --strictNullChecks를 사용하도록 설정해야 함

```ts
// strictPropertyInitialization
class Person {
  private _name: string;
  private _age: number;  // Error! Property '_age' has no initializer and is ..
  
  constructor() {}

  public print() {
    console.log(this._name, this._age)
  }
}



// constructor에서 초기 값을 할당한 경우는 정상 동작
class Person {
  private _name: string;
  private _age: number;

  constructor(name: string, age: number) {
    this._name = name;
    this._age = age;
  }

  public print() {
    console.log(this._name, this._age)
  }
}


// constructor에서 안하는 경우
// - 보통 다른 함수로 이니셜라이즈 하는 경우 (async 함수)
// - constructor에는 async를 사용할 수 없음
class Person {
  private _name!: string;
  private _age!: number;

  public async initialize(name: string, age: number) {
    this._name = name;
    this._age = age;
  }

  public print() {
    console.log(this._name, this._age)
  }
}
```

<br>

* --strictBindCallApply
    - Function의 내장 함수인 bind, call, apply에 대한 더 엄격한 체크 수행
    - bind는 해당 함수 안에서 사용할 this와 인자를 설정해주는 역할
    - call과 apply는 this와 인자를 설정한 후, 실행까지 함
    - call과 apply는 인자를 설정하는 방식에서 차이점이 있음
        - call은 함수의 인자를 여러 인자의 나열로 넣어서 사용
        - apply는 모든 인자를 배열 하나로 넣어서 사용

<br>

* --alwaysStrict
    - 각 소스 파일에 대해 Javascript의 strict mode로 코드를 분석
    - "엄격하게 사용"을 해제

```ts
// alwaysStrict
var e1 = 015;
var e2 = { p: 1, p: 2 };  // Error! An object literal cannot have multiple ...
var e3;
delete e3;

// syntex 에러가 ts error로 나옴
// 컴파일된 Javascript 파일에 "use strict"가 추가 됨
```