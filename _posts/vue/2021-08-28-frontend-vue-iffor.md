---
title: "[Vue.js] 조건문, 반복문"
excerpt: Vue.js의 조건문과 반복문
categories:
- Vue
tags:
- - Vue
  - Web
  - Node.js
toc: true
toc_sticky: true
popular: true
date: '2021-08-28T06:10:00'
last_modified_at: 2021-08-28T06:10:00
---

## 1. 프로젝트 시작

```bash
# terminal

$ npx degit LeeWonWoo1/vue3-webpack-template vue3-test
$ cd vue3-webpack-template vue3-test
$ code . -r
$ npm i
```

## 2. 조건문

```vue
// src/App.vue


<template>
  <h1 @click="increase">
    {{ count }}
  </h1>
  <div v-if="count > 4">  // 조건문 작성
    4보다 큽니다!
  </div>
</template>

<script>
  data() {
    return {
      count: 0,
    }
  },
  methods: {
    increase() {
      this.count += 1
    }
  }
}
</script>

<style lang="scss">
  h1 {
    font-size: 50px;
    color: royalblue;
  }
  ul {
    li {
      font-size: 40px;
    }
  }
</style>>
```

<br>

![vue5](https://user-images.githubusercontent.com/62803763/131190862-960b8008-f9de-4a92-abfc-176b159585b1.PNG){: .align-center .open-new}


<br>

## 3. 반복문

```vue
// src/App.vue

<template>
  <h1 @click="increase">
    {{ count }}
  </h1>
  <div v-if="count > 4">
    4보다 큽니다!
  </div>
  <ul>  // 반복문
    <Fruit 
      v-for="fruit in fruits"
      :key="fruit"
      :name="fruit">
      {{ fruit }}
    </Fruit>
  </ul>
</template>

<script>
import Fruit from '~/components/Fruit'

export default {
  components: {
    Fruit
  },
  data() {
    return {
      count: 0,
      fruits: ['Apple', 'Banana', 'Cherry']
    }
  },
  methods: {
    increase() {
      this.count += 1
    }
  }
}
</script>

<style lang="scss">
  h1 {
    font-size: 50px;
    color: royalblue;
  }
  ul {
    li {
      font-size: 40px;
    }
  }
</style>>
```

<br>

```vue
// src/components/Fruit.vue

<template>
  <li>{{ name }}?!</li>
</template>

<script>
export default {
  props: {
    name: {
      type: String,
      default: ''
    }
  }
}
</script>

<style scoped lang="scss">
  h1 {
    color: red !important;
  }
</style>
```

<br>

![vue6](https://user-images.githubusercontent.com/62803763/131190883-816a2a4b-01e7-44bc-b322-b32b281ad493.PNG){: .align-center .open-new}
