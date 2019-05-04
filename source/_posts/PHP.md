---
title: php
date: 2018/5/13
categories:
- PHP
---

http://www.itcast.cn:80/index.html
protocol hostname  port  sourcename

# PHP(person home page)个人主页

>helloworld
```php
<?php
    echo 'helloworld!';
?>
```

LAMP(WEB应用程序平台)由Linux Apache MySQL PHP组成与Javaee和.net形成三足鼎立之势

## 关闭占用端口的程序
+ 查询对应端口号的占用情况： $ netstat -ano"80"
+ ctrl + c 结束当前操作
+ 输入tasklist命令会显示所有的进程和对应对的PID
+ 在任务管理器中找到这个程序，关闭掉或者taskkill /F /PID 4896 

## Apache是一款web服务器软件，几乎可以运行在所有的计算机平台上
+ Apache服务设置：使用windows服务来管理，
    - 右击我的电脑--管理--服务和应用程序--服务 找到Apache服务

## content
+ PHP中的标识符是区分大小写的，但函数名例外

+ 定义常量  define("name","value",true); true表示不区分大小false则区分

+ datatype: String（字符串）, Integer（整型）, Float（浮点型）, Boolean（布尔型）, Array（数组）, Object（对象）, NULL（空值）。

+ PHP也是一中弱语言
  - 定义变量
    - 定义整形  $a=123 $b=0123(8进制) $c=0x123c(16进制)
    - 定义float  $a = 3.1415 
    - 定义string   $a = 'abc$c' (单引号模式不解析)     $b = "abc$c" (双引号莫斯，$c会看成其变量值与其他字符相加，且双引号中的{$a},${a}形式也会被解析，多一个空格将看成字符串)
    - 变量一般为传值赋值，但将 & 符号加到要赋值的变量钱就可变为引用传值（共同指向同一值）   
    ```php
        $text = 'hello';
        $new = &$text;
    ```

+ 变量检测  is_*(var) 返回true or false   eg：is_bool(true) true

+ php中并没有字符串连接符“+”，但有点运算符将数值拼接成字符串

## function
> function内部不以变量名的形式直接访问外部变量，需如下使用global $var 或直接使用全局变量组中的$GLOBALS["var"]

+ 内置函数
    + 字符串相关函数
        - 字符串分割函数array explode(",",$str)    以逗号分割字符串并以数组形式返回
        - 数组转字符串函数 string implode("&",$arr)
        - 字符串比较函数 int strcmp($str1,$str2)
        - 字符串替换 mixed str_replace($search,$replace,$str,$count可选)
        - 字符串截取 string substr($source,开始下标,长度)
        - 字符长度 int strlen($str) 注：一个中文字符长度为3
        - string trim(%str) 去除两端空白符
    + 时间
        - int time(void) 获得70年到现在的毫秒数
        - 格式化时间 string date(Y年m月d日H时i分s秒,time())
        - 字符串转换时间戳 int strtotime("2014-5-14 17:20:55")
        - 自定义时间戳 int mktime($hour,$minute,$second,$month,$day,$year,1/0);参数可省略，从左至右，省略的部分由，系统时间的对应项补充，也就是说不传参数时，即是系统时间

> tips：[手册](http:www.php.net/manual/zh/index.php)

## 数组
+ 数组
    - 索引数组：下标为整数的数组
    - 关系数组：键值为字符串
    - 数组定义 
        + $arr[0]=123;$arr['id']=15;  
        + $arr = array(key1=>value,key2=>value)
        + 注意当没有键值时，使用默认键，即“键”从零开始，依次递增
    - 输出数组：print_r($arr);/var_dump($arr);两者的区别在于var_dump连带数组元素中的值得类型打印出来
    - PHP是弱类型语言，所以PHP数组具备动态增长的特性$arr[num]=val;
    - 删除
        + unset($arr[1]);删除$arr[1]
        + unset($arr);删除数组$arr;
        + 注意：PHP中的删除数组某一个元素时，其他元素下标不会自动改变
    - 数组操作符
        + 操作符 + == === != !===  <>
        + $c = $arr1+$arr2; 数组1 2 中有相同下标的元素，以1位准合并为一个数组给$c
    - 数组指针操作函数
        + mixed current($arr)获取数组当前下标的值
        + mixed key($arr)获取当前元素的key值
        + mixed next($arr)将数组的内部指针向前移动一位（当前下标值移动）
        + mixed pre($arr)将数组的内部指针向后移动一位
        + mixed end($arr)将数组的内部指针指向最后一个元素
        + mixed reset($arr)重置指针，即数组的指针指向第一个元素
    - 数组遍历
        + foreach($arr as $value){$value……}值遍历
        + foreach($arr as $key=>$value){$key……;$value……}键值对一起遍历
    - 数组常用函数
        + bool is_arr($arr)判别数组
        + int count($arr)数组长度，当统计二维数组时，要加上一维数组名的个数
        + array array_unique($arr)去重，保留前面的
        + array array_keys($arr,"11",true);查询字符串11，的键值
        + array array_keys($arr,"11",false);查询11，的键值
        + bool sort($arr,SORT_NUMERIC);按数字排序
        + array array_merge($arr1,$arr2);数组合并
        + array array_chunk($arr,length);分为length长度的数组，不足length的也是一个数组
        + array array_rand($arr,num);随机去除num个数组元素
        + array array_reverse($arr,true);返回保留原始键名的颠倒数组

## 面向对象
> 特征：封装性、继承性、多态性
+ 类是对某一类事物的抽象描述，描述一组对象的共同特征，而对象用于表示现实中该事物的个体
+ 修饰符
    - public    外部可以访问
    - protect   外部不可以访问，子类可以访问
    - private   外部和子类都不可以访问
+ $this 在对象内部指向当前对象 $this.name
+ 访问： 
    - 对象-属性访问： obj->property
    - 类-属性访问： ClassName::property
+ 魔术方法：无需手动调用的对象方法  eg： __get() __set()  __costruct()
+ 类常量：const PI=3.1415926
    - 访问类常量
    - 类内部： ClassName::PI/self::PI
    - 外部： ClassName::PI
+ 类静态成员
    - 静态属性： public static $schoolname="name"
    - 静态方法： public static function show(){}
    - 访问方法与类常量一致
    - 一个类的所有实例，共用类中的静态属性，即在内存中即使有多个实例，静态的属性也只有一份。
+ 类继承
    - class dog extends animal {  }
    - 重写父类方法： 同名、同参、更大访问权限（public……）就可覆盖父类方法
    - 在重写情况下调用父类方法： parent::function()
+ final:确定类或类方法的最终形式，即使用final修饰的类将不可被继承、使用final修饰的类方法将不可重写
+ 抽象类：通过abstract修饰的类，且其类方法有被abstract修饰的只有方法名而无具体内容
+ 接口： 如果一个抽象类中的所有方法都是抽象的，则可以将这个类用接口表示
    - 接口：interface animal { }其内部都是抽象方法，无需使用abstract特地声明


# 魔术常量
> PHP 向它运行的任何脚本提供了大量的预定义常量。不过很多常量都是由不同的扩展库定义的，只有在加载了这些扩展库时才会出现，或者动态加载后，或者在编译时已经包括进去了。

有八个魔术常量它们的值随着它们在代码中的位置改变而改变。[魔术常量](http://php.net/manual/zh/language.constants.predefined.php)
<table class="doctable table">
    <caption><几个 PHP 的“魔术常量”</caption>
    <thead>
       <tr>
        <th>名称</th>
        <th>说明</th>
       </tr>
    </thead>

      <tbody class="tbody">
       <tr id="constant.line">
        <td><strong><code>__LINE__</code></strong></td>
        <td>
         文件中的当前行号。
        </td>
       </tr>

       <tr id="constant.file">
        <td><strong><code>__FILE__</code></strong></td>
        <td>
         文件的完整路径和文件名。如果用在被包含文件中，则返回被包含的文件名。自
         PHP 4.0.2 起，<strong><code>__FILE__</code></strong>
         总是包含一个绝对路径（如果是符号连接，则是解析后的绝对路径），而在此之前的版本有时会包含一个相对路径。
        </td>
       </tr>

       <tr id="constant.dir">
        <td><strong><code>__DIR__</code></strong></td>
        <td>
         文件所在的目录。如果用在被包括文件中，则返回被包括的文件所在的目录。它等价于
         <em>dirname(__FILE__)</em>。除非是根目录，否则目录中名不包括末尾的斜杠。（PHP 5.3.0中新增）
       </td>
       </tr>
       
       <tr id="constant.function">
        <td><strong><code>__FUNCTION__</code></strong></td>
        <td>
         函数名称（PHP 4.3.0 新加）。自 PHP 5
         起本常量返回该函数被定义时的名字（区分大小写）。在
         PHP 4 中该值总是小写字母的。
        </td>
       </tr>

       <tr id="constant.class">
        <td><strong><code>__CLASS__</code></strong></td>
        <td>
         类的名称（PHP 4.3.0 新加）。自 PHP 5
         起本常量返回该类被定义时的名字（区分大小写）。在
         PHP 4 中该值总是小写字母的。类名包括其被声明的作用区域（例如
         <em>Foo\Bar</em>）。注意自 PHP 5.4 起 __CLASS__
         对 trait 也起作用。当用在 trait 方法中时，__CLASS__
         是调用 trait 方法的类的名字。
        </td>
       </tr>

       <tr id="constant.trait">
        <td><strong><code>__TRAIT__</code></strong></td>
        <td>
         Trait 的名字（PHP 5.4.0 新加）。自 PHP 5.4 起此常量返回 trait
         被定义时的名字（区分大小写）。Trait 名包括其被声明的作用区域（例如
         <em>Foo\Bar</em>）。
        </td>
       </tr>

       <tr id="constant.method">
        <td><strong><code>__METHOD__</code></strong></td>
        <td>
         类的方法名（PHP 5.0.0 新加）。返回该方法被定义时的名字（区分大小写）。
        </td>
       </tr>

       <tr id="constant.namespace">
        <td><strong><code>__NAMESPACE__</code></strong></td>
        <td>
         当前命名空间的名称（区分大小写）。此常量是在编译时定义的（PHP 5.3.0 新增）。
        </td>
       </tr>

      </tbody>
     
</table>

# 超全局变量
> 超级全局变量在PHP 4.1.0之后被启用, 是PHP系统中自带的变量，在一个脚本的全部作用域中都可用。

Super global variable|content
----|----
$GLOBALS |是一个包含了全部变量的全局组合数组。变量的名字就是数组的键。
$_SERVER |是一个包含了诸如头信息(header)、路径(path)、以及脚本位置(script locations)等等信息的数组。
$_REQUEST |用于收集HTML表单提交的数据。
$_POST |被广泛应用于收集表单数据，在HTML form标签的指定该属性："method="post"。
$_GET |同样被广泛应用于收集表单数据，在HTML form标签的指定该属性："method="get"
$_FILES |包含上传文件信息的数组
$_ENV |
$_COOKIE |用于取回 cookie 的值。[cookie](http://www.runoob.com/php/php-cookies.html)
$_SESSION |用于存储关于用户会话（session）的信息


# 命名空间
>PHP 命名空间(namespace)是在PHP 5.3中加入的，如果你学过C#和Java，那命名空间就不算什么新事物。 不过在PHP当中还是有着相当重要的意义。

+ PHP 命名空间可以解决以下两类问题：
    + 用户编写的代码与PHP内部的类/函数/常量或第三方类/函数/常量之间的名字冲突。
    + 为很长的标识符名称(通常是为了缓解第一类问题而定义的)创建一个别名（或简短）的名称，提高源代码的可读性。

## 全局空间
如果没有定义任何命名空间，所有的类与函数的定义都是在全局空间，与 PHP 引入命名空间概念前一样。在名称前加上前缀 \ 表示该名称是全局空间中的名称，即使该名称位于其它的命名空间中时也是如此。

## [乱码问题](http://www.php.cn/php-weizijiaocheng-361604.html)


### session
// 初始化session
session_start();
$sid=session_id();


### cookie
setcookie()    — 发送 Cookie
参数
+ name          Cookie 名称。

+ value         Cookie 值。 这个值储存于用户的电脑里，请勿储存敏感信息。 比如 name 是 'cookiename'， 可通过 $_COOKIE['cookiename'] 获取它的值。

+ expire        Cookie 的过期时间。 这是个 Unix 时间戳，即 Unix 纪元以来（格林威治时间 1970 年 1 月 1 日 00:00:00）的秒数。 也就是说，基本可以用 time() 函数的结果加上希望过期的秒数。 或者也可以用 mktime()。 time()+60*60*24*30 就是设置 Cookie 30 天后过期。 如果设置成零，或者忽略参数， Cookie 会在会话结束时过期（也就是关掉浏览器时）。

+ path          Cookie 有效的服务器路径。 设置成 '/' 时，Cookie 对整个域名 domain 有效。 如果设置成 '/foo/'， Cookie 仅仅对 domain 中 /foo/ 目录及其子目录有效（比如 /foo/bar/）。 默认值是设置 Cookie 时的当前目录。

+ domain        Cookie 的有效域名/子域名。 设置成子域名（例如 'www.example.com'），会使 Cookie 对这个子域名和它的三级域名有效（例如 w2.www.example.com）。 要让 Cookie 对整个域名有效（包括它的全部子域名），只要设置成域名就可以了（这个例子里是 'example.com'）。

旧版浏览器仍然在使用废弃的 » RFC 2109， 需要一个前置的点 . 来匹配所有子域名。

+ secure        设置这个 Cookie 是否仅仅通过安全的 HTTPS 连接传给客户端。 设置成 TRUE 时，只有安全连接存在时才会设置 Cookie。 如果是在服务器端处理这个需求，程序员需要仅仅在安全连接上发送此类 Cookie （通过 $_SERVER["HTTPS"] 判断）。

+ httponly      设置成 TRUE，Cookie 仅可通过 HTTP 协议访问。 这意思就是 Cookie 无法通过类似 JavaScript 这样的脚本语言访问。 要有效减少 XSS 攻击时的身份窃取行为，可建议用此设置（虽然不是所有浏览器都支持），不过这个说法经常有争议。 PHP 5.2.0 中添加。 TRUE 或 FALSE

+ 返回值         如果在调用本函数以前就产生了输出，setcookie() 会调用失败并返回 FALSE。 如果 setcookie() 成功运行，返回 TRUE。当然，它的意思并非用户是否已接受 Cookie。