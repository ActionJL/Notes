### 5 配置项

#### vue初始化

```js
const app = new Vue({
  el: "#app", // element, vue作用的范围
  data: {
    isRed: true,
    birthday: 1529032123201,
  }
})
```

#### 5.5 v-if和v-show

v-if

示例：

```
v-if='布尔变量'
```

- v-for与v-if之间不能使用其他标签
- v-if 修改dom元素，用于一次操作

---

v-show：控制元素的显隐

#### 5.6 v-bind

- 用于给标签的属性绑定变量

- 插值表达式不能使用在标签属性上

#### 5.7 计算属性

```html
<h1>
  您的生日：{{birth}}
</h1>
```

```js
computed: {
  birth() {
    const day = new Date(this.birthday);
    return day.getFullYear() + "年" + day.getMonth() + "月" + day.getDay() + "日";
  }
}
```

- computed与methods区别
  - computed计算属性，只计算一次
  - methods定义方法，可以书写复杂逻辑

#### 5.8 watch

```js
watch: {
  num(arg1, arg2) {
    console.log(arg1, arg2);
    // arg1 为新值，arg2为未修改的值
  }
  // 对对象的监控，只监控地址值，如果需要深监控，需要
  person: {
    deep: true,
   	handler(val) {
      console.log(val.name + ":" + val.age);
    }
  }
}
```

### 6 组件化

#### 6.1 局部组件和全局组件

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>component</title>
  </head>
  <body>
    <div id="app">
      <counter></counter>
    </div>
    
    <button id="counter" @click='count++'>
      点击{{count}}次
    </button>
    
    <script src="vue.js"></script>
    <script>
    	//定义全局组件
      Vue.component("counter", {
        template: "#counter", 	// 只能有一个根标签
        data() {		// 定义成函数，为了其他地方使用组件时属性共享
          return {
          	count: 0,
          }
        }
      })
      
      // 局部组件
      const conter = {
        template: "#counter",
        data() {
          return {
            count: 0
          }
        }
      }
      
      const app = new Vue({
        el: "#app",
        data: {
          
        },
        // 注册局部组件
        components: {
          counter: counter
        }
      })
    </script>
  </body>
</html>
```

#### 6.2 组件通信

##### 6.2.1 父子组件通信

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <title></title>
  </head>
  <body>
    <div id="app">
      <introduce :title="msg"></introduce>
      <for-component :items='lessons'></for-component>
    </div>
    
    <script src="vue.js"></script>
    <script>
      // 局部组件
      const introduce = {
        template: "<h1>{{title}}</h1>",
        props:  ["title"]
        data() {
          return {
          }
        }
      }
      
      const forComponent = {
        template: "<ul><li v-for='item in items'>{{item}}</li></ul>",
        props: {
          items: {
            type: Array,
            default: ['java']
          }
        }
      }
      
      const app = new Vue({
        el: "#app",
        data: {
          msg: "大家好，我是渣渣辉！",
          lessons: ['java', 'php', 'python']
        },
        // 注册局部组件
        components: {
          introduce
        }
      })
    </script>
  </body>
</html>
```





