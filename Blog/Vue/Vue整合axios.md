# Vue整合axios

## 1 创建一个vue的项目

使用命令 `vue create axios-vue` 创建，可以什么都不用勾选

<br>

## 2 安装axios

`npm install axios --save`

如果安装过程很慢的话，也可以使用下面的cnpm

```shell
npm install cnpm -g --registry=https://registry.npm.taobao.org
cnpm install axios --save
```

<br>

## 3 创建封装请求的文件夹

用vue插件的方式封装，而不是使用工具类进行封装。

这样方便使用，只需要在 `main.js` 引入一次就可以在所有vue组件中使用。

在 `src` 下面创建 `plugin` 文件夹，并在里面创建 `http.js`

http.js内容如下：

```js
/**
 * axios vue插件
 */

import axios from 'axios';

const MyAxiosHttp = {};

const axios_instance = axios.create({
    baseURL: 'http://127.0.0.1:8866/',
    timeout: 5000
});


MyAxiosHttp.install = (Vue) => {

    /**
     * 添加get方法 这个方法我写的比较简单，可以按照你们的需求完善
     * 返回一个Promise
     * 并将错误信息全部转换成字符串
     * @param {*} path 
     * @param {*} params 
     */
    Vue.prototype.$get = (path, params) => {
        return new Promise((resolve, reject) => {
            axios_instance.get(path, {
                params: params
            }).then(res => {
                resolve(res.data);
            }).catch(err => {
                reject('服务器异常');
            });
        });
    }
};

export default MyAxiosHttp;
```

<br>

## 4 如何使用

在 `main.js` 中引入

```js
import Vue from 'vue'
import App from './App.vue'

// 下面这两行
import MyAxiosHttp from '@/plugin/http.js';
Vue.use(MyAxiosHttp);

Vue.config.productionTip = false

new Vue({
  render: h => h(App),
}).$mount('#app')
```

在vue组件中使用

```js
export default {
  name: 'App',
  components: {
  },
  beforeMount() {
    this.$get('user/findById', {
      id: 1
    }).then(res => {
      console.log(res);
    });
  },
}
```

