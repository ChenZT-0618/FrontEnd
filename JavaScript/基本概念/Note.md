JavaScript是一种弱类型语言

### 变量：
	var
	let

### 标识符：
可以自主命名的都是标识符，不能关键字和保留字相同，严格区别大小写，(课件第7页)  
规则：  
1.  只可含有：字母、数字、 下划线、$
2. 不能以数字开头
3. 一般采用驼峰命名法

### 基本数据类型：  
**查看类型：typeof xxx**
 
1.**String**:  
使用双引号、单引号括起来的字符串  
&emsp;&emsp;var str = "hello";  
&emsp;&emsp;var str = "我说：'今天天气不错。'" -> 可以在字符串中显示引号  
&emsp;&emsp;var str = "我说：/"今天天气不错。/"" -> 同理  
2.**Number**:所有数值类型 包括整数和小数  
* Number.MAX_VALUE  
* Number.MIN_VALUE -- 最小的正数
* Number.POSITIVE_INFINITY  -- 正无穷
* Number.NEGATIVE_INFINITY  -- 负无穷  

十六进制表示：0x... 八进制表示：0..  二进制：0b...  
JavaScript的浮点运算结果不太精确，eg：0.1 + 0.2

3.**Boolean** ：逻辑判断 &emsp;ture|false  
4.**Null** ： 表示一个空值的对象，**当typeof null时，结果为object**  
5.**Undefined**  : 声明变量不赋值  
6.类型转换：  
* 其他类型转strning   
  * 调用xxx.toString()方法，但是null和undefined类型的对象没有该方法  
  * 调用String(xxx)方法，null和undefined类型的对象可用
  * xxx + "" : 任何的值和字符串做加法运算，都会先转换为字符串，然后再和字符串做拼串的操作
* 其他类型转Number  
  * 调用Number(xxx)函数
      - 字符串 --> 数字  
      如果是纯数字的字符串，则直接将其转换为数字  
      如果字符串中有非数字的内容，则转换为NaN  
        如果字符串是一个空串或者是一个全是空格的字符串，则转换为0  
      - 布尔 --> 数字   true 转成 1  false 转成 0  
      - null -->  0  
      - undefined --> NaN  
  * 调用：parseInt()，parseFloat() 函数 ：把一个字符串中有效的数字转为整数or浮点数
  * **任何值做 - * / % 运算时都会自动转换为Number** 
  * **使用一元的+来进行类型转换** ->  
  
    ```JavaScript
        var a = "123";					
        a = +a;
    ```
* 其他类型转Boolean
  * 使用Boolean()函数
    * 数字 ---> 布尔： 除了0和NaN，其余的都是true			  
	* 字符串 ---> 布尔 ：除了空串，其余的都是true
	* null和undefined都会转换为false
	* 对象也会转换为true
  * **进行两次取反**  -> 如果对非布尔值进行元素，则会将其转换为布尔值

### 运算符
* 算数运算符 : + - * / %  
* 一元运算符 ： ++ , --    
* 逻辑运算符: ! , && , ||   
   