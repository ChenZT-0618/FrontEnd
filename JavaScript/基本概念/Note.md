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
**typeof操作符：**  typeof xxx ; 返回值： undefined、boolean、string、number、object、function
 
1.**String**:  
使用双引号、单引号括起来的字符序列  
&emsp;&emsp;var str = "hello";  
&emsp;&emsp;var str = "我说：'今天天气不错。'" -> 可以在字符串中显示引号  
&emsp;&emsp;var str = "我说：/"今天天气不错。/"" -> 同理  
> 特点：**字符串不可改变**，更改字符串的过程是：先创建一个新容量的字符串（数组），然后填充新值，最后销毁原来的字符串。  
2.**Number**:所有数值类型 包括整数和小数  
* Number.MAX_VALUE  
* Number.MIN_VALUE -- 最小的正数
* Number.POSITIVE_INFINITY  -- 正无穷 无法参与数值计算
* Number.NEGATIVE_INFINITY  -- 负无穷 无法参与数值计算  
> isFinite() ： 判断是否位于 MAX_VALUE  与 MIN_VALUE 之间   

十六进制表示：0x... 八进制表示：0..  二进制：0b...  
> 八进制第一位0后面的数如果>7的话，**会忽略第一位的0，把后面的数当作十进制数解析**  
> 十六进制和二进制的话会当作标识符处理，但是因为标识符不能以数字开头，**所以会报错。**


JavaScript的浮点运算结果不太精确，eg：0.1 + 0.2

3.**Boolean** ：逻辑判断 &emsp;ture|false  
4.**Null** ： 表示一个空对象指针，所以**当typeof null时，结果为object**  
5.**Undefined**  : 声明变量不赋值   
**实际上，undefined是派生自null的，所以 null == undefined的值为true**  
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
   可添加第二个参数表示要解析成几进制
  
  * **任何值做 - * / % 运算时都会自动转换为Number** 
  * **使用一元的+来进行类型转换** ->  
  
    ```JavaScript
        var a = "123";					
        a = +a;
    ```
* 其他类型转Boolean
  * 使用Boolean()函数
    | 数据类型   | 结果为：true | 结果为：false |
    | ---------- | ------------ | ------------- |
    | String     | 非空字符串   | 空字符串""    |
    | Number     | 非零数字值   | 0 和NaN       |
    | Object     | 任何对象     | null          |
    | Underfined | 无           | underfined    |
  * **进行两次取反**  -> 如果对非布尔值进行元素，则会将其转换为布尔值

### 运算符
* 一元运算符 ： ++ , --    
  * 除了Number之外，也可用于其他类型
    * String ： 只包含数字 —> 转为数字再加减1；包含其他 -> NaN
    * Boolean:  true -> 转为数字1再加减1；false -> 转为数字0再加减1；
    * Object ：看valueof的类型
* 位操作符：
  *  ~ ，& ，| ，^ : 按位非、与、或、异或  
  用在Number类型上的，其他类型会自动用Number()转换
  * 左移、右移：>> , << （有符号移位）
  > 右移会以符号位进行补充，正数补0，负数补1 
  * 左移、右移：>>> , <<<（无符号移位）
  >  右移时补0，正负数一样，**同时负数会变为正数**
* 算数运算符 : + - * / %  

* 逻辑运算符: ! , && , ||   
特殊规则：
  | 与：&&   | 第一个操作数类型 | 第二个操作数类型 | 返回结果     |
  | -------- | ---------------- | ---------------- | ------------ |
  |          | 对象             | 任意             | 第二个操作数 |
  |          | true             | 任意             | 第二个操作数 |
  |          | null             | 任意             | null         |
  |          | NaN              | 任意             | NaN          |
  |          | undefined        | 任意             | underfined   |
  | 或：\|\| | 第一个操作数类型 | 第二个操作数类型 | 返回结果     |
  |          | 对象             | 任意             | 第一个操作数 |
  |          | 结果为false      | 任意             | 第二个操作数 |
  |          | null             | null             | null         |
  |          | NaN              | NaN              | NaN          |
  |          | undefined        | undefined        | underfined   |
* 关系操作符：> ，< ， >= ， <=  一般用在数字比较  
  * 两个字符(串)：从第0位开始按照ASCII码转换进行比较  
  * 字符串跟数字比较：字符串能转为数字 ? 字符串转数字-> 比较 : false
  * 有布尔值：转数字再比较
  * 两个对象：调用valueOf()方法，根据结果比较
  * **任何操作数与NaN比较都是返回false**
* 相等操作符：  
  
  * 相等和不相等：先转换类型再比较  ==， !=  
    变换规则：  
    1. 布尔值比较前先转数值 :true为1 ，false为0  
    2. 字符串 跟 数值比-> 字符串转数值  
    3. 其中一个是对象 调用 valueOf() ，两个都是对象，比较是否是同一个对象  
    4. **null 和 undefined 是相等的**，null，undefined不能转为其他值   
   
    特殊比较结果  
    | 表达式            | 值    | 表达式       | 值    |
    | ----------------- | ----- | ------------ | ----- |
    | null == undefined | true  | NaN == NaN   | false |
    | null == 0         | false | NaN != NaN   | true  |
    | undefined == 0    | false | "NaN" == NaN | false |
  * 全等和不全等：仅比较而不转换 ===，!== 
* 条件操作符： a ? b : c
* 赋值操作符、 逗号操作符 （PDF 72页，书53页）