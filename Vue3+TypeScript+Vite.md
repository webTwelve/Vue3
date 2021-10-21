[toc]



# 01.Vue3 CDN引入创建

```javascript
<body>
  <div id="app"></div>
</body>
<script src="https://unpkg.com/vue@next"></script>
<script>
  const container={
    template:'<h1>Hello Word</h1>'
  }
  const app =Vue.createApp(container)
  app.mount('#app')
</script>
```

# 02.计算案例

```JS
<body>
  <div id="app"></div>
</body>
<script src="https://unpkg.com/vue@next"></script>
<script>
  const container={
    template:`
    <div>
      <h1>{{count}}</h1>
      <button @click='count++'>+</button>
      <button @click='count--'>-</button>
    </div>
    `,
    data(){
      return {
        count:0
      }
    }
  }
  Vue.createApp(container).mount('#app')
</script>
```

# 03.template模板

```JS
<body>
  <div id="app"></div>
  <template id="container">
    <h1>Hello Word</h1>
  </template>
</body>
<script src="https://unpkg.com/vue@next"></script>
<script>
  Vue.createApp({
    template:'#container'
  }).mount('#app')
</script>
```

# 04.Vue methods this指向问题

```
事实上Vue的源码当中就是对methods中的所有函数进行了遍历，并且通过bind绑定了this
```

![](D:\vue3\img\methods原理.png)

# 05.绑定属性

```JS
<body>
    <div id="app">
      
    </div>
    <template id="aaa">
          <div v-bind='info'>哈哈哈</div>
    </template>
</body>
<script src="https://unpkg.com/vue@next"></script>
<script>
  const container ={
    template:'#aaa',
    data(){
      return {
        info:{
          height:'199px',
          name:'呀呀呀'
        }
      }
    }
  }
  const app =Vue.createApp(container)
  app.mount('#app')
```

# 06.key的diff算法作用

```JS
key属性主要用在Vue的虚拟DOM算法，在新旧nodes对比时辨识VNodes；
如果不使用key，Vue会使用一种最大限度减少动态元素并且尽可能的尝试就地修改/复用相同类型元素的算法；
而使用key时，它会基于key的变化重新排列元素顺序，并且会移除/销毁key不存在的元素；
```

```JS
使用while循环先从前往后进行新旧DOM比较然后发现不同的元素时break跳出，再从后向前进行比较，比较到不同的时break跳出，判断length进行增加还是删除DOM
```

# 07.babel作用

```JS
1.对js代码ES5到ES6做转化
```

# 08.proxy配置代理

```JS
devServer：{
   proxy：{
       "/api":{
           target:''  //跨域的域名
       }，
       pathRewrite：{
           "^/api":"" //将域名 的/api重写为''要不404
       }，
       secure：false //默认为false  如果为ture的话则不支持https代理
   }
}
```

# 09.非props的attribute

```JS
组件传入props没有的属性叫做非props的attribute
这种属性会继承到组件的根节点上，如不想继承
```

# 10.attrs

```JS
$attrs可以访问所有非props的attribute
```

# 11.provide与inject传递数据

```JS
/父组件
<script>
import Home from './01_provide和inject传递数据/home.vue'
export default {
  components: {
    Home
  },
  provide: {
    name: '哈哈',
    age: '18'
  }
}
</script>
```

```js
/子组件
<script>
export default {
  inject:['name','age']
}
</script>
```

# 12.provide如何获取data中的数据

```JS
因为provide中this指向undefined所以需要将provide写成函数并return出去
  provide () {
    return {
      name: '哈哈',
      age: '18'
    }
  }
```

