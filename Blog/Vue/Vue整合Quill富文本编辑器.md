# Vue整合Quill富文本编辑器

## Quill介绍

Quill是一款开源的富文本编辑器，基于可扩展的架构设计，提供丰富的 API 进行定制。截止2021年1月，在github上面已有28.8k的star。

Quill项目地址：https://github.com/quilljs/quill/

Quill官网：https://quilljs.com/

<br>

## 简单使用

### 创建项目

创建一个vue的项目，名为**demo-quill-vue**，不需要vuex、router和css预处理器。

<br>

### 安装Quill

`npm install vue-quill-editor --save`

如果安装过程很慢的话，也可以使用下面的cnpm

```shell
npm install cnpm -g --registry=https://registry.npm.taobao.org
cnpm install vue-quill-editor --save
```

<br>

### 引入Quill

在main.js中导入

```js
import Vue from 'vue'
import VueQuillEditor from 'vue-quill-editor'

import 'quill/dist/quill.core.css'
import 'quill/dist/quill.snow.css'
import 'quill/dist/quill.bubble.css'

Vue.use(VueQuillEditor)
```

<br>

### 在页面中使用

在页面级的组件里，直接使用。

在App.vue里，写入如下代码：

```js
<template>
  <div id="app">
    <quill-editor
      id="quill-editor"
      v-model="content"
      :options="editorOption"
      @change="onEditorChange($event)"
    >
    </quill-editor>
  </div>
</template>

<script>
import QuillEditor from 'vue-quill-editor'

export default {
  name: 'App',
  data: function () {
    return {
      content: '',
      editorOption: {}
    }
  },
  methods: {
    onEditorChange() {
      console.log(this.content);
    }
  }
}
</script>

<style>
#app {
  width: 800px;
  height: 500px;
}

#quill-editor {
  width: 100%;
  height: 100%;
}
</style>
```

## demo地址

https://github.com/tanyiqu/demo-quill-vue