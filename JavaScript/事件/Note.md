## 事件
事件是电脑输入设备与页面进行交互的响应。我们称之为事件。  
### 常用的事件
* onload 加载完成事件 —— 页面加载完成之后，常用于做页面 js 代码初始化操作
* onclick 单击事件 —— 常用于按钮的点击响应操作。
* onblur 失去焦点事件 —— 常用用于输入框失去焦点后验证其输入内容是否合法。
* onchange 内容发生改变事件 —— 常用于下拉列表和输入框内容发生改变后操作
* onsubmit 表单提交事件 —— 常用于表单提交前，验证所有表单项是否合法。
### 事件注册
什么是事件的注册（绑定）？——  其实就是告诉浏览器，当事件响应后要执行哪些操作代码，叫事件注册或事件绑定。
* 静态注册事件 ：通过 html 标签的事件属性直接赋于事件响应后的代码，这种方式我们叫静态注册。  
* 动态注册事件 ：是指先通过 js 代码得到标签的 dom 对象，然后再通过 dom 对象.事件名 = function(){} 这种形式赋于事件响应后的代码，叫动态注册。
  * 动态注册基本步骤：
    1. 获取标签对象
    2. 标签对象.事件名 = fucntion(){}


## DOM模型
DOM 全称是 Document Object Model 文档对象模型——就是把文档中的标签，属性，文本，转换成为对象来管理。  
### Document对象
1. Document 它管理了所有的 HTML 文档内容。
2. document 它是一种树结构的文档。有层级关系。
3. 它让我们把所有的标签都对象化
4. 我们可以通过 document 访问所有的标签对象。

###  方法介绍
document.getElementById(elementId) ：通过标签的 id 属性查找标签 dom 对象，elementId 是标签的 id 属性值  

document.getElementsByName(elementName)：通过标签的name属性查找标签dom对象，elementName标签的name属性值  

document.getElementsByTagName(tagname)：通过标签名查找标签 dom 对象。tagname 是标签名  —— e.g < input >

document.createElement( tagName) ：通过给定的标签名，创建一个标签对象。tagName 是要创建的标签名  

注：  
* document对象的三个查询方法，如果有id属性，优先使用getElementById方法来进行查询
* 如果没有 id 属性，则优先使用 getElementsByName 方法来进行查询
* 如果 id 属性和 name 属性都没有最后再按标签名查getElementsByTagName
  * 以上三个方法，一定要在页面加载完成之后执行，才能查询到标签对象。


#### 节点的常用属性和方法
* 属性
  * childNodes：获取当前节点的所有子节点
  * firstChild：获取当前节点的第一个子节点
  * lastChild：获取当前节点的最后一个子节点
  * parentNode：获取当前节点的父节点
  * nextSibling：获取当前节点的下一个节点
  * previousSibling：获取当前节点的上一个节点
  * className：用于获取或设置标签的 class 属性值
  * innerHTML：表示获取/设置起始标签和结束标签中的内容
  * innerText：表示获取/设置起始标签和结束标签中的文本
* 方法
  * getElementsByTagName()：获取当前节点的指定标签名孩子节点
  * appendChild(oChildNode)：可以添加一个子节点，oChildNode 是要添加的孩子节点
    * 可以先创建好子节点所需要的东西，然后在依附到父节点上。
    * 添加子节点主要步骤
      1. 创建节点：var newNode = document.createElement("div")
      2. 添加内容：var content = document.createTextNode("HelloWorld");
      3. 添加子元素：newNode.appendChild(content); ——子节点创建完成
      4. 显示到页面中：document.body.appendChild(newNode);

**出现#text问题**


#### 查询方法练习


### 正则

表示要求字符串中，是否包含字母e

var patt = new RegExp("e");

var patt = /e/; ——也是正则表达式对象

表示要求字符串中，是否包含字母a或b或c：var patt = /[abc]/;

表示要求字符串，是否包含小写字母：var patt = /[a-z]/;

表示要求字符串，是否包含任意大写字母：var patt = /[A-Z]/;

表示要求字符串，是否包含任意数字：var patt = /[0-9]/;

表示要求字符串，是否包含字母，数字，下划线：var patt = /\w/;

表示要求字符串中是否包含至少一个a：var patt = /a+/;

表示要求字符串中是否 *包含* 零个 或 多个a：var patt = /a*/;

表示要求字符串是否包含一个或零个a：var patt = /a?/;

表示要求字符串是否包含连续三个a：var patt = /a{3}/;

表示要求字符串是否包至少3个连续的a，最多5个连续的a：var patt = /a{3,5}/;

表示要求字符串是否包至少3个连续的a：var patt = /a{3,}/;

表示要求字符串必须以a结尾：var patt = /a$/;

表示要求字符串必须以a打头：  var patt = /^a/;