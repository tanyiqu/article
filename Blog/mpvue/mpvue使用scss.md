## 安装scss

安装命令如下，不带版本号可能会导致报错

```
npm i sass-loader@7.3.1 -D
npm i node-sass@4.14.1 -D
```

然后修改 `build` 文件夹下的 `webpack.base.conf.js`

在rules下添加

```js
{
   test: /\.scss$/, 
   loaders: ['style', 'css', 'sass']
}
```

<br>

## 使用

在使用前可以先重启一下项目 `npm run dev`

```html
<style lang="scss" scoped>
.container {
  background: greenyellow;

  p {
    color: salmon;
  }
}
</style>
```

