# Vue路由跳转时修改页面标题

## 1 在main.js中添加如下代码

```javascript
import Vue from 'vue'
import App from './App.vue'
import router from './router'

// 路由发生变化修改页面title
router.beforeEach((to, from, next) => {
  if (to.meta.title) {
    document.title = to.meta.title;
  }
  next();
})

Vue.config.productionTip = false

new Vue({
  router,
  render: h => h(App)
}).$mount('#app')
```

<br>

## 2 在路由index.js中添加如下代码

```js
const routes = [{
  path: '/login',
  name: 'Login',
  component: Login,
  meta: {
    title: '登录'
  }
}]
```

之后再切换路由时会自动修改title。