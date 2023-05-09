---
layout: archive
title: "Vue.js keyup issue"
---

# Vue.js keyup.enter 중복 이슈

## @keyup
키보드를 누를 시에 대한 이벤트를 주는 경우가 있을겁니다.

간단한 input으로 예를 들어볼게요.

```vue
<template>
  <input v-model="text" type="text" @keyup.enter="handleKeyupEnter"/>
</template>
<script>
export default {
  name: 'Input',
  data: () => ({
    text: ''
  }),
  methods: {
    handleKeyupEnter() {
      console.log('enter')
    }
  }
}
</script>
```

v-model에 text를 바인딩 하고 엔터를 누를시 handleKeyupEnter를 호출하는 input 컴포넌트입니다.

영문 입력시 다음과 같이 이상이 없습니다.

![eng](/assets/images/2023-05-10/1.png)

keyup 이벤트는 영문일때는 상관이 없지만 한글입력후 엔터를 누를 시 이벤트가 두번호출 되는 것을 확인할 수 있습니다.

![kor](/assets/images/2023-05-10/2.png)


해당 이슈에 관한 정보는 [여기로](https://github.com/vuejs/vue/issues/10277)

해당 이벤트 핸들러를 ~~keyup~~ -> keypress로 변경해주면 엔터의 감지를 할수 있습니다.

```vue
<input v-model="text" type="text" @keypress.enter="handleKeypressEnter"/>
```
