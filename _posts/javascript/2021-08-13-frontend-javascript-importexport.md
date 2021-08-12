---
title: "[Javascript] 가져오기, 내보내기"
excerpt: import, export
categories:
- Javascript
tags:
- - Javascript
  - Programming
  - Web
toc: true
toc_sticky: true
popular: true
date: '2021-08-13T02:00:00'
last_modified_at: 2021-08-13T02:00:00
---

## import, export

- 외부에 있는 다른 javascript 파일을 가지고 올 수 있는 하나의 통로를 가짐
- 특정 내용을 밖으로 내보낼 수 있는 2가지 통로를 가짐(Default export, Named export)

```javascript
// getType.js  (default)
export default function (data) {  // default는 함수의 이름을 지정하지 않아도 됨
  return Object.prototype.toString.call(data).slice(8, 11)
}

// default는 하나의 파일에서 하나의 데이터만 내보낼 수 있음
export default 123  // Only one default export allowed per module.
```

<br>

```javascript
// getRandom.js  (이름 지정)
export function random() {
  return Math.floor(Math.random() * 10)
}

// 이름만 지정되어 있으면 여러개의 데이터를 내보낼 수 있음
export const user = {
  name: 'LWW',
  age: 45
}

// Named export와 Default export 같이 사용 가능
export default 123  
```

<br>

```javascript
// main.js
import _ from 'lodash'  // From `node_modules`
import checkType from './getType'  // getType.js
// 이름이 지정된 통로로 나오는 데이터는 데이터를 {}로 묶어서 사용!
import { random, user as lww} from './getRandom'  // getRandom.js

console.log(_.camelCase('the hello world'))  // theHelloWorld
console.log(checkType([1, 2, 3]))  // Array
console.log(random(), random())  // 0~9 랜덤값 0~9 랜덤값
console.log(lww)  // {name: "LWW", age: 45}


// 한번에 가져오기 (와일드카드 * 사용)
import * as R from './getRandom'

console.log(R)  // {user: {...}, default: 123, __esModule: true, random: f}
```
