# Emoji picker for Vue 3
<a href="https://www.npmjs.com/package/vue-emoticon-picker"><img src="https://img.shields.io/npm/dt/vue-emoticon-picker.svg" alt="Downloads"></a>
<a href="https://www.npmjs.com/package/vue-emoticon-picker"><img src="https://img.shields.io/npm/v/vue-emoticon-picker.svg" alt="Version"></a>
<a href="https://spdx.org/licenses/MIT.html"><img src="https://img.shields.io/npm/l/vue-emoticon-picker.svg" alt="License"></a>

## Table of contents
- [Demo](#demo)
- [Installation](#installation)
  - [With npm](#with-npm)
  - [With a CDN](#with-a-cdn)
- [Import](#import)
  - [With an ES6 bundler (via npm)](#with-an-es6-bundler-via-npm)
    - [Use per component](#use-per-component)
    - [Use via `<script setup>`](#use-globally)
- [Usage](#usage)
  - [Very simple usage, without any CSS defined](#very-simple-usage-without-any-css-defined)
- [License](#license)


## Demo
The live demos are available here:
- [Simple](https://codepen.io/DCzajkowski/pen/JLypqP),

## Installation
### With npm
```bash
npm i vue-emoticon-picker --save
```

## Import
### With an ES6 bundler (via npm)
#### Use per component
```js
import Emoticon from 'vue-emoticon-picker'

export default {
  // ..
  emits: ['clickEmoticon'],
  components: {
    Emoticon,
  },
  // ...
}
```
#### Use via `<script setup>`
```js
import { ref, defineEmits } from 'vue'
const emit = defineEmits(['clickEmoticon'])

// ...
const input = ref('')
const emoticonRef = ref(null);

const handleClickEmoji = (emoji) => {
  input.value += emoji;
}
```

### Very simple usage, without any CSS defined
You will need two things. A textarea (or an input), where emojis will be injected, and a component declaration. A simple example is provided below.
```html
<template>
  <textarea v-model="input"></textarea>
  <button type="button" @click="emoticonRef.toggleShow()">:)</button>
  <!-- // .... // -->
  <Emoticon ref="emoticonRef" @click-emoticon="handleClickEmoji" />

  <!-- // .... // -->
</template>
```

```js
{
  setup() {
    const emoticonRef = ref(null)

    return {
      emoticonRef
    }
  },
  data() {
    return {
      input: '',
    }
  },
  methods: {
    handleClickEmoji(emoji) {
      this.input += emoji
    },
  },
}
```

## License
This work is an open-sourced software licensed under the [MIT license](https://opensource.org/licenses/MIT).
