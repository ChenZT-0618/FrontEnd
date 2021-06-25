### Vue的options选项

- el：决定Vue示例会绑定那个HTML元素
- data：Vue示例对于的数据对象
  - 组件(component)中的data选项必须是个函数
- methods：Vue示例的一些方法

### Vue的生命周期

生命周期：事物从诞生到消亡的整个过程。

生命周期函数（勾子函数 -- Hook）：当Vue对象到某个阶段后，如初始化Events & Lifecycle，就会调用一个勾子函数，该函数是在new Vue() 语句中设置的。可以通过勾子函数在Vue对象的生命周期中执行一些操作。

<img src="./image/lifecycle.png" style="zoom:33%;" />

## 基本语法

### 数据插入指令

#### 把数据插入到文本中

- Mustache语法：渲染数据最常用语法
- v-text：与Mustache语法相似，也是将数据进行展示，会覆盖标签之间的内容。但不够Mustache语法灵活
- v-once：表示该HTML元素只会渲染一次。不会选择变量的改变而改变。在某些特殊情况下使用
- v-html：将字符串解析成HTML格式
- v-pre：用于跳过该元素和它子元素的编译过程，用于显示原本的字符串。去掉了渲染过程

```vue
<body>
    <div id="app">
        <h2>v-text指令</h2>
        <!-- 等同于Mustache语法，但是会覆盖标签之间的内容 -->
        <h4 v-text="message"></h4>
        <h2>v-once指令</h2>
        <h4 v-once>表示该元素只渲染一次：{{message}}</h4>
        <h2>v-html指令</h2>
        <h4>没使用v-html指令：{{url}}</h4>
        <h4 v-html="url"></h4>
        <h2>v-pre指令</h2>
        <h4>没使用v-pre指令：{{message}}</h4>
        <h4 v-pre>使用v-pre指令：{{message}}</h4>
    </div>
</body>
<script src="../js/vue.js"></script>
<script>
    const app = new Vue({
        el: "#app",
        data: {
            message: "HelloWorld",
            url: "<a href='https://www.baidu.com'>百度一下</a>"
        }
    })
</script>
```

#### 把数据插入到属性中

例如将数据（字符串）等 动态绑定到 \<img>元素中的src属性，或者\<a>元素的href属性中。

这时，可以使用 v-bind 指令：

##### 绑定标签属性

```vue
<body>
  <div id="app">
    <h2>{{message}}</h2>
    <!-- img标签同理，只要在属于动态绑定数据的属性前面加上 v-bind: 或者 : 即可  -->
    <a v-bind:href="aHref">基本用法</a><br>
    <a :href="aHref">简写</a>
  </div>
</body>
<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el: "#app",
    data: {
      message: "v-bind指令基本使用方法",
      aHref: "https://www.baidu.com"
    }
  })
</script>
```

在实际开发中，链接或者图片都是用服务器以json格式传过来的，这里只是简单的示范如何动态绑定属性数据。

##### Class绑定：对象语法

> class属性规定元素的类的名称。如需为一个元素规定多个类，用空格分隔类名。

假设我定义了两个样式。

```html
<style>
  .style1 {
    color: red;
  }

  .style2 {
    color: blueviolet;
  }
</style>
```

然后在实践中，我希望能够动态的将这两个class绑定到一个HTML元素中，例如通过一个按钮改变一个元素的样式。可以使用 v-bind 指令动态绑定class。

在使用 v-bind 指令对class属性进行绑定时，可以传一个对象，该对象可以用键值对表示，如下：{class-1:boolean, class-2: boolean,...,}。

该语句的作用如下：如果 class-i 的值 为true时，该类class-i 会被绑定到HTML元素中，false则不绑定。**注意：类名不能有横杆，如red-color**

```vue
<style>
  .style1 {
    color: red;
  }

  .style2 {
    color: blueviolet;
  }
</style>

<body>
  <div id="app">
    <h2>{{message}}</h2>
    <h3 v-bind:class="{style1:isStyle1,style2:isStyle2}">样式显示</h3>
    <button @click="btnClick">样式切换</button>
  </div>
</body>
<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el: "#app",
    data: {
      message: "v-bind动态绑定class -- 对象语句",
      isStyle1: true,
      isStyle2: false
    },
    methods: {
      btnClick: function () {
        this.isStyle1 = !this.isStyle1;
        this.isStyle2 = !this.isStyle2;
      }
    }
  })
</script>
```

此外，v-bind:class 指令也可以与普通的 class 共存。

```vue
<style>
  .static {
    font-style: italic;
  }
</style>
<body>
  <div id="app">
    <h3 class="static" v-bind:class="{style1:isStyle1,style2:isStyle2}">样式显示</h3>
  </div>
</body>

页面渲染结果：
<h3 class="static style1">样式显示</h3>
```

##### Class绑定：数组语法

我们可以把一个数组传给 v-bind:class，以应用一个 class 列表：

```vue
<div id="app">
    <h2>{{message2}}</h2>
    <h3 :class="[StyleClass1]">样式显示</h3>
</div>
<script>
  const app = new Vue({
    el: "#app",
    data: {
      StyleClass1: 'style1'
    }
  })
</script>
```

解释：StyleClass1 表示一个变量，VUE会在data中找对于的键值对中的值绑定到class中

##### style绑定：对象语法

v-bind:style 的对象语法十分直观——看着非常像 CSS：v-bind:style="{属性名：属性值，属性名：属性值}"。

CSS property 名可以用驼峰式 (camelCase) 或短横线分隔 (kebab-case，记得用引号括起来) 来命名。

```vue
<body>
  <!-- 点击列表中的某一项，该项的文本变成红色 -->
  <div id="app">
    <h2 :style="{color:'red',fontSize:'50px'}">{{message}}</h2>
  </div>
</body>
<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el: "#app",
    data: {
      message: "v-bind绑定sytle",
    }
  })
</script>
```

或者直接绑定到一个对象上：

```vue
<body>
  <!-- 点击列表中的某一项，该项的文本变成红色 -->
  <div id="app">
    <h4 :style=styleObject>调用对象来绑定style</h4>
  </div>
</body>
<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el: "#app",
    data: {
      styleObject: {
        color: "blue",
        fontSize: '30px'
      }
    }
  })
</script>
```

##### style绑定：数组语法

v-bind:style  的数组语法可以将多个样式对象应用到同一个元素上：

```vue
<body>
    <!-- 点击列表中的某一项，该项的文本变成红色 -->
    <div id="app">
        <h4 :style=[styleObject,fontStyle]>使用数组语法来绑定style</h4>
    </div>
</body>
<script src="../js/vue.js"></script>
<script>
    const app = new Vue({
        el: "#app",
        data: {
            styleObject: {
                color: "blue",
                fontSize: '30px'
            },
            fontStyle: {
                fontStyle: 'italic'
            }
        }
    })
</script>
```



### 组件系统

