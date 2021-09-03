---
title: "[React] Testing"
excerpt: Jest, Testing-Library/react 활용
categories:
  - React
tags:
  - - React
    - Web
    - Node.js
    - Jest
toc: true
toc_sticky: true
popular: true
date: "2021-09-03T17:00:00"
last_modified_at: 2021-09-03T17:00:00
---

## 1. Jest

- Easy Setup
- Instant Feedback
- Snapshot Testing

```bash
# terminal

$ mkdir jest-example
$ cd jest-example
$ npm init -y
$ npm i jest -D
$ code .
```

<br>

```json
// package.json

"scripts": {
  "test": "jest"
}
```

<br>

```js
// example.test.js

describe("expect test", () => {
  it("37 to equal 37", () => {
    expect(37).toBe(37); // PASS
  });
  it("{age: 39} to equal {age: 39}", () => {
    expect({ age: 39 }).toEqual({ age: 39 }); // PASS
  });
  it(".toHaveLength", () => {
    expect("hello").toHaveLength(5); // PASS
  });
  it(".not.toHaveLength", () => {
    expect("hello").toHaveLength(7); // PASS
  });
  it(".toHaveProperty", () => {
    expect({ name: "LWW" }).toHaveProperty("name"); // PASS
    expect({ name: "LWW" }).toHaveProperty("name", "LWW"); // PASS
  });
  it(".toBeDefined", () => {
    expect({ name: "LWW" }.name).toBeDefined(); // PASS
    expect({ name: "LWW" }.age).toBeDefined(); // FAIL
  });
  it(".toBeFalsy", () => {
    expect(false).toBeFalsy(); // PASS
    expect(0).toBeFalsy(); // PASS
    expect("").toBeFalsy(); // PASS
    expect(null).toBeFalsy(); // PASS
    expect(undefined).toBeFalsy(); // PASS
    expect(NaN).toBeFalsy(); // PASS
  });
  it(".toBeGreaterThan", () => {
    expect(10).toBeGreaterThan(7); // PASS
  });
  it(".toBeGreaterThanOrEqual", () => {
    expect(10).toBeGreaterThanOrEqual(10); // PASS
  });
  it(".toBeInstanceOf", () => {
    class Foo {}
    expect(new Foo()).toBeInstanceOf(Foo); // PASS
  });
  it("async-await, catch", async () => {
    function p() {
      return new Promise((resolve, reject) => {
        setTimeout(() => {
          reject(new Error("error"));
        }, 1000);
      });
    }
    try {
      await p();
    } catch (error) {
      expect(error).toBeInstanceOf(Error);
    }
  });
});
```

<br>

```bash
# terminal

$ npm test
```

<br>

```bash
# terminal

# 테스트 자동화
$ npx jest --watchAll
```

<br>

## 2. Testing-Library/react

- Button Component
  - Component가 정상적으로 생성됨
  - "button"이라고 쓰여있는 엘리먼트는 HTMLButtonElement임
  - 버튼을 클릭하면, p 태그 안에 "버튼이 방금 눌렸다."라고 쓰여짐
  - 버튼을 클릭하기 전에는, p 태그 안에 "버튼이 눌리지 않았다."라고 쓰여짐
  - 버튼을 클릭하고 5초 뒤에는, p 태그 안에 "버튼이 눌리지 않았다."라고 쓰여짐
  - 버튼을 클릭하면, 5초 동안 버튼이 비활성화 됨

```bash
# terminal

$ npx create-react-app react-component-test
$ cd react-component-test
$ code .
$ npm test
(a)
```

<br>

```js
// src/components/Button.test.js

import { fireEvent, render } from "@testing-library/react";
import Button from "./Button";

describe("Button Component (@testing-library/react", () => {
  it("Component가 정상적으로 생성", () => {
    const button = render(<Button />);
    expect(button).not.toBe(null);
  });
  it('"button"이라고 쓰여있는 엘리먼트는 HTMLButtonElement임"', () => {
    const { getByText } = render(<Button />);
    const buttonElement = getByText("button");
    expect(buttonElement).toBeInstanceOf(HTMLButtonElement);
  });
  it('버튼을 클릭하면, p 태그 안에 "버튼이 방금 눌렸다."라고 쓰여짐', () => {
    const { getByText } = render(<Button />);
    const buttonElement = getByText("button");
    fireEvent.click(buttonElement);
    const p = getByText("버튼이 방금 눌렸다.");
    expect(p).not.toBeNull();
    expect(p).toBeInstanceOf(HTMLParagraphElement);
  });
  it('버튼을 클릭하기 전에는, p 태그 안에 "버튼이 눌리지 않았다."라고 쓰여짐', () => {
    const { getByText } = render(<Button />);
    const p = getByText("버튼이 눌리지 않았다.");
    expect(p).not.toBeNull();
    expect(p).toBeInstanceOf(HTMLParagraphElement);
  });
  it('버튼을 클릭하고 5초 뒤에는, p 태그 안에 "버튼이 눌리지 않았다."라고 쓰여짐', () => {
    jest.useFakeTimers();
    const { getByText } = render(<Button />);
    const buttonElement = getByText("button");
    fireEvent.click(buttonElement);
    // 5초 흐름
    act(() => {
      jest.advanceTimerByTime(5000);
    });

    const p = getByText("버튼이 눌리지 않았다.");
    expect(p).not.toBeNull();
    expect(p).toBeInstanceOf(HTMLParagraphElement);
  });
  it("버튼을 클릭하면, 5초 동안 버튼이 비활성화 됨", () => {
    jest.useFakeTimers();
    const { getByText } = render(<Button />);
    const buttonElement = getByText("button");
    fireEvent.click(buttonElement);

    // 비활성화
    expect(buttonElement).toBeDisabled();

    // 5초 흐름
    act(() => {
      jest.advanceTimerByTime(5000);
    });

    // 활성화
    expect(buttonElement).not.toBeDisabled();
  });
});
```

<br>

```jsx
// src/components/Button.jsx

import { useState } from "react";

const BUTTON_TEXT = {
  NORMAL: "버튼이 눌리지 않았다.",
  CLICKED: "버튼이 방금 눌렸다.",
};

export default function Button() {
  const [message, setMessage] = useState(BUTTON_TEXT.NORMAL);
  const timer = useRef();

  useEffect(() => {
    return () => {
      if (timer.current) {
        clearTimeout(timer.current);
      }
    };
  }, []);

  return (
    <div>
      <button onClick={click} disabled={message === BUTTON_TEXT.CLICKED}>
        button
      </button>
      <p>{message}</p>
    </div>
  );

  function click() {
    setMessage(BUTTON_TEXT.CLICKED);
    timer.current = setTimeout(() => {
      setMessage(BUTTON_TEXT.NORMAL);
    }, 5000);
  }
}
```

<br>

![react-testing](https://user-images.githubusercontent.com/62803763/131980667-db077a8d-fb70-4d28-a92d-650d114ad9b1.PNG){: .align-center .open-new}
