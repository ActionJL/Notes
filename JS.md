##### ajax

```js
$.ajax({
  url: "",		// 必填项，访问网址需加http://, string
  data: "",   // 请求携带参数，将自动转换为字符串，string
  async: true, // 异步请求，默认为true， boolean
  success: function(data) {
    console.log(data);  // 请求成功回调
  },
  error: function() {
    // 请求失败回调函数
  }
})
```

##### ES6

```js
// 函数声明
function fname() {
}
// 函数表达式
let fname = function() {
}
// lamda
(a, b) => a + b;
// Object中函数写法
{
  fname() {
  }
}
```









