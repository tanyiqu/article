# mpvue下拉刷新

## 1 开启下拉刷新

在想要下拉刷新的页面的 `main.json` 里，添加：

```json
{
    "navigationBarTitleText": "页面标题",
    "enablePullDownRefresh": true 
}
```

<br>

## 2 实现下拉刷新函数

在 `index.vue` 文件里，实现如下方法

```js
export default {
  
  onPullDownRefresh() {
    console.log("下拉刷新");

    // ... 操作

    // 用于停止刷新
    wx.stopPullDownRefresh();
  },
  
}
```

