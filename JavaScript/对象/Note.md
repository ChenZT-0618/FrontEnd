 ## Object类型
 
 对象属于一种复合的数据类型，在对象中可以保存多个不同数据类型的属性。
 
 ### 对象的分类：
1. 内建对象
- 由ES标准中定义的对象，在任何的ES的实现中都可以使用
- 比如：Math String Number Boolean Function Object....
2. 宿主对象
- 由JS的运行环境提供的对象，目前来讲主要指由浏览器提供的对象
- 比如 BOM DOM
3. 自定义对象
- 由开发人员自己创建的对象  

### 对象创建
1. 三种创建方式

```javascript
var a = new Object();
// 对象字面量语法
var a = {
    name: "张三",
    gender: "male",
    age: 14,
    isStu: true
}
```

2. 属性添加/属性的表达方式
   
```javascript
var a = new Object();
// 添加属性:两种方式
a.name = "张三";
a.gender = "male";

a['id'] = 10086; 
```
两种方式的区别

3. 属性删除  
 
```javascript
delete a.age;  
delete a['gender'];
```
4. 属性检查

```javascript
a.hasOwnProperty('xxx');
'xxx' in a;
```
5. 遍历对象


## Array类型

特点：   
* 数组的每一项都可以保存任何类型的数据
* 数组的大小是可以动态调整的
* 数组长度 最大值：4,294,967,295

### 创建数组(两种方式)
一、使用Array构造函数：Array()
```javascript
var colors = new Array();
var colors = new Array(20); // length为20的数组
```
二、使用**数组字面量表示法**
```javascript
var colors = ["red","blued","green"]; // 长度为3的数组
var colors = []; // 空数组
```
* 数组的**length属性有一个特点**：可以通过设置这个属性，从数组的末尾移除或添加数组元素。
```javascript
var colors = ["red","blued","green"]; // length=3
colors.length = 2;
colors[2] => undefined // 将长度修改为2时，末尾的元素被移除
```
* 利用这一特性，可以方便地在数组末尾添加新元素
```javascript
var colors = ["red","blued","green"]; // 长度为3的数组
colors[colors.length] = "black";
colors[colors.length] = "brown";
```
### 数组方法介绍
#### 转字符串
1. toLocaleString()
2. join(arg) : 可以使用其他符号来作为字符串的分隔符，默认值是逗号
3. toString()
4. valueOf()
示例：
```javascript
var colors = ["red", "blued", "green"];
var test3 = colors.toString();          // red,blued,green   string
var test = colors.toLocaleString();     // red,blued,green  string
var test2 = colors.join(";");           // red;blued;green    string
var test4 = colors.valueOf();           // (3) ["red", "blued", "green"]  object
```

#### 排序方法
1. reverse() 
2. sort() ： 根据字符串Unicode码来比较，所以比较数字时会出错，需要定义一个比较函数
```javascript
var values = [1, 5, 10, 15];
console.log(values.sort());                 // (4) [1, 10, 15, 5]
console.log(values.sort(function (a, b) {
    return a - b;
}))                                         // (4) [1, 5, 10, 15]
```
#### 操作方法
1. concat() ：数组拼接，可传0个或多个参数，返回拼接后的数组
   * 0个参数：数组复制
   * 多个参数：数组拼接
    ```javascript
    var color2 = colors.concat();
    var color3 = colors.concat("yellow", "black");
    console.log(color2); // (3) ["red", "blued", "green"]
    console.log(color3); // (5) ["red", "blued", "green", "yellow", "black"]
    ```

2. slice()：返回指定位置的数组，可传一个或两个参数。
    * 一个参数(a)：从a开始带数组末尾
    * 两个参数(a,b)：从a开始到b-1处的数组，左闭右开区间
    * 如果参数时负数的话，从末尾开始。等同于加上数组长度得到的正数
    ```javascript
                    0       1        2        3         4
    var color3 = ["red", "blued", "green", "yellow", "black"];
    console.log(color3.slice(2));       // (3) ["green", "yellow", "black"]
    console.log(color3.slice(1, 4));    // (3) ["blued", "green", "yellow"]
    console.log(color3.slice(-3, -1));  // (2) ["green", "yellow"]
    console.log(color3.slice(2, 4));    // (2) ["green", "yellow"]
    ```
3. splice()：数组的删除，插入，替换功能，返回删除的数组
   * 删除：需要2个参数，第一个为“起始位”，第二个删除元素个数
    ```javascript
                    0       1        2        3         4
    var color3 = ["red", "blued", "green", "yellow", "black"];
    console.log(color3.splice(0, 2)); // (2) ["red", "blued"]
    console.log(color3);              // (3) ["green", "yellow", "black"]
    ```
   * 插入： 需要3个参数，第一个为“起始位”，第二个为要删除元素个数（插入的话填0），第三个往后后为要插入的项
    ```javascript
                    0       1        2        3         4
    var color3 = ["red", "blued", "green", "yellow", "black"];
    console.log(color3.splice(2, 0, "orange")); // []
    console.log(color3); // (6) ["red", "blued", "orange", "green", "yellow", "black"]
    ```
   * 替换：其实替换和第二个方式一样，其实就是插入几个就删除几个，就达到效果了
    ```javascript
                    0       1        2        3         4
    var color3 = ["red", "blued", "green", "yellow", "black"];
    console.log(color3.splice(2, 2, "orange", "pink")); // (2) ["green", "yellow"]
    console.log(color3); // (5) ["red", "blued", "orange", "pink", "black"]
    ```

#### 迭代方法
对数组中的每一项运行给定函数
1. every():     &emsp;&emsp;如果该函数对每一项都返回true，则返回true。
2. some():      &emsp;&emsp;如果该函数对任一项返回true，则返回true。
3. filter():    &emsp;&emsp;&emsp;返回改函数会返回true的项组成的数组。
```javascript
var numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9];
var Result = numbers.filter(function (item) {
    return item % 2 == 0;
})
console.log(Result); //[2, 4, 6, 8]
```   
4. map():       &emsp;&emsp;&emsp;返回每次函数调用的结果组成的数组。
```javascript
var numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9];
var Result = numbers.map(function (item) {
    var a = item + 1;
    return a;
})
console.log(Result); //[2, 3, 4, 5, 6, 7, 8, 9, 10]
```
5. forEach():   &emsp;该方法没有返回值，本质上与使用for循环遍历数组一样。