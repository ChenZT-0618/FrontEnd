 ### Object类型
 
 对象属于一种复合的数据类型，在对象中可以保存多个不同数据类型的属性。
 
 #### 对象的分类：
1. 内建对象
- 由ES标准中定义的对象，在任何的ES的实现中都可以使用
- 比如：Math String Number Boolean Function Object....
2. 宿主对象
- 由JS的运行环境提供的对象，目前来讲主要指由浏览器提供的对象
- 比如 BOM DOM
3. 自定义对象
- 由开发人员自己创建的对象  

#### 对象创建
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


### Array类型

特点：   
* 数组的每一项都可以保存任何类型的数据
* 数组的大小是可以动态调整的
* 数组长度 最大值：4,294,967,295

#### 创建数组
