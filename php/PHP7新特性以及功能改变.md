PHP7 新特性以及功能修改
=======
[从PHP 7.0.x 移植到 PHP 7.1.x](http://php.net/manual/zh/migration71.php)     
[从PHP 5.6.x 移植到 PHP 7.0.x](http://php.net/manual/zh/migration70.php)         
[PHP 7 的五大新特性](http://developer.51cto.com/art/201510/494674.htm)      
[PHP7新特性](http://www.cnblogs.com/cjblogs/p/6980499.html)      
[让PHP7达到最高性能的几个Tips](http://www.laruence.com/2015/12/04/3086.html)     

### 运算符（NULL 合并运算符）

新增的 ?? 运算符简化判断
```
<?php
$a = $_GET['a'] ?? 1;  // 新增运算符
$a = isset($_GET['a']) ? $_GET['a'] : 1;
$a = $a ?: 1
$a && $a = 1;
```
### 函数返回值类型声明

```
<php 
function arraysSum(array ...$arrays): array 
{ 
    return array_map(function(array $array): int { 
        return array_sum($array); 
    }, $arrays); 
} 
 
print_r(arraysSum([1,2,3], [4,5,6], [7,8,9])); 
```
> 注意 … 的边长参数语法在 PHP 5.6 以上的版本中才有
> **fun() : array ** 声明返回值为数组
> **fun() : int ** 声明返回值为整形
> **fun() : string ** 声明返回值为字符串

### 返回值类型声明-强制模式

```
<php 
function foo($a) : int 
{ 
    return $a; 
} 
foo(1.0); 
```
以上代码可以正常执行，foo 函数返回 int 1，没有任何错误。

### 返回值类型声明-严格模式

```
<php 
declare(strict_types=1); 
 
function foo($a) : int 
{ 
    return $a; 
} 
 
foo(1.0); 
# PHP Fatal error:  Uncaught TypeError: Return value of foo() must be of the type integer, float returned in test.php:6 
```

在声明之后，就会触发致命错误。类似 js 的 strict mode


### 标量类型声明
PHP 7 中的函数的形参类型声明可以是标量了。在 PHP 5 中只能是类名、接口、array 或者 callable (PHP 5.4，即可以是函数，包括匿名函数)，现在也可以使用 string、int、float和 bool 了。

```
<php 
// Coercive mode  
function sumOfInts(int ...$ints) 
{ 
    return array_sum($ints); 
} 
var_dump(sumOfInts(2, '3', 4.1)); 
```

需要注意的是上文提到的严格模式的问题在这里同样适用：强制模式（默认，既强制类型转换）下还是会对不符合预期的参数进行强制类型转换，严格模式下则触发 TypeError 的致命错误。

### use 批量声明

PHP 7 中 use 可以在一句话中声明多个类或函数或 const 了：
```
<php 
use some/namespace/{ClassA, ClassB, ClassC as C};   // 非混合模式
use function some/namespace/{fn_a, fn_b, fn_c}; 
use const some/namespace/{ConstA, ConstB, ConstC}; 
use Publishers\Packt\{   // 混合模式
    Book,
    Ebook,
    Video,
    function getBook,
    function saveBook,
    const COUNT,
    const KEY
};
use Publishers\Packt\{  // 复合模式
    Paper\Book,
    Electronic\Ebook,
    Media\Video
};
```
需要留意的问题是：如果你使用的是基于 composer 和 PSR-4 的框架，这种写法是否能成功的加载类文件？其实是可以的，composer 注册的自动加载方法是在类被调用的时候根据类的命名空间去查找位置，这种写法对其没有影响。


### 扩展

1. 匿名类
2. define 可以定义常量数组
3. 闭包（ Closure）增加了一个 call 方法
4. 生成器（或者叫迭代器更合适）可以有一个最终返回值（return），也可以通过 yield from 的新语法进入一个另外一个生成器中（生成器委托）,生成器的两个新特性（return 和 yield from）可以组合。

### 新特性

ZEND引擎升级到Zend Engine 3，也就是所谓的PHP NG
增加抽象语法树，使编译更加科学
64位的INT支持
统一的变量语法
原声的TLS - 对扩展开发有意义
一致性foreach循环的改进
新增 <=>、\**、?? 、\u{xxxx}操作符
增加了返回类型的声明
增加了标量类型的声明
核心错误可以通过异常捕获了
增加了上下文敏感的词法分析


### 移除的特性

.移除一些旧的扩展，被移迁移到了PECL（例如：mysql）
2.移除SAPIs的支持
3.<?和<? language=“php”这样的标签被移除了
4.16进制的字符串转换被废除了
```
//PHP5
"0x10" == "16"
 
//PHP7
"0x10" != "16"
```
5.HTTP_RAW_POST_DATA移除了（可以使用php://input替代）
6.静态函数里面不再支持通过一个不兼容的$this调用一个非静态的函数了
$o = & new className{}，不再支持这样的写法
7.php.ini文件移除了#作为注释，统一用;去注释


### 64位的INT支持

支持存储大于2GB的字符串
支持上传大小大于2GB的文件
保证字符串在所有平台上【64位】都是64bit
统一的语法变量
```
$$foo['bar']['baz']
 
//PHP5
($$foo)[‘bar']['baz']
 
//PHP7: 遵循从左到右的原则
${$foo[‘bar']['baz']}
```

### foreach循环的改进

```
//PHP5
$a = array(1, 2, 3);foreach ($a as $v){var_dump(current($a));}
int(2)
int(2)
int(2)
 
$a = array(1, 2, 3);$b=&$a;foreach ($a as $v){var_dump(current($a));}
int(2)
int(3)
bool(false)
 
$a = array(1, 2, 3);$b=$a;foreach ($a as $v){var_dump(current($a));}
int(1)
int(1)
int(1)
 
//PHP7：不再操作数据的内部指针了
$a = array(1, 2, 3);foreach ($a as $v){var_dump(current($a))}
int(1)
int(1)
int(1)
 
$a = array(1, 2, 3);$b=&$a;foreach ($a as $v){var_dump(current($a))
int(1)
int(1)
int(1)
 
$a = array(1, 2, 3);$b=$a;foreach ($a as $v){var_dump(current($a))}
int(1)
int(1)
int(1)
```

### 新增的几个操作符

```
//<=> - 比较两个数的大小【-1：前者小于后者，0：前者等于后者，1：前者大于后者】
echo 1 <=> 2;//-1
echo 1 <=> 1;//0
echo 1 <=> 0;//1
 
// ** - 【a的b次方】
echo 2 ** 3;//8
 
//?? - 三元运算符的改进
//php5
$_GET['name'] ? $_GET['name'] : '';//Notice: Undefined index: …
//php7
$_GET['name'] ?? '' -> '';
 
//\u{xxxx} - Unicode字符的解析
echo "\u{4f60}";//你
echo "\u{65b0}";//新
```

### 返回类型的声明

```
function getInt() : int {
  return “test”;
};
 
getInt();
 
//PHP5
#PHP Parse error: parse error, expecting '{'...
 
//PHP7
#Fatal error:Uncaught TypeError: Return value of getInt() must be of the type integer, string returned 

```


### 标量类型的声明

```
function getInt(int $num) : int {
  return $num;
};
 
getInt(“test”);
 
//PHP5
#PHP Catchable fatal error: Argument 1 passed to getInt() must be an instance of int, string given…
 
//PHP7
#Fatal error: Uncaught TypeError: Argument 1 passed to getInt() must be of the type integer, string given…
```

### 核心错误异常捕获

```
try {
  non_exists_func();
} catch(EngineException $e) {
  echo “Exception: {$e->getMessage();}\n”;
}
//这里用php7试了一下还是没法捕获，但是看鸟哥介绍说是可行的。。。
#Exception: Call to undefined function non_exists_func()

```

### 敏感的词法分析

```
//PHP5
class Collection {public function foreach($arr) {}}
#Parse error: parse error, expecting `"identifier (T_STRING)”'...
 
//PHP7
class Collection {
  public function foreach($arr) {}
  public function in($arr){}
  public function where($condition){}
  public function order($condition){}
}
$collection = new Collection();
$collection->where()->in()->foreach()->order();

```


### 匿名类

匿名类的声明与使用时同时进行的，具备其他类所具备的所以功能，区别在于匿名类没有类名。

```
new class(argument) { definition };
```
匿名类是没有类名的，但在PHP内部，会在内存的引用地址表中为其分配一个全局唯一的名称。

```
$name = new class('You') {
    public function __construct($name)
    {
        echo $name;
    }
};
```

匿名类可以继承父类及父类的方法。
```
class Packt
{
    protected $number;

    public function __construct()
    {
        echo 'parent construct';
    }

    public function getNumber() : float
    {
        return $this->number;
    }
}

$number = new class(5) extends Packt
{
    public function __construct(float $number)
    {
        parent::__construct();
        $this->number = $number;
    }
};

echo $number->getNumber();
```

匿名类可以继承接口。
```
interface Publishers
{
    public function __construct(string name, string address);
    public function getName();
    public function getAddress();
}

class packt
{
    protected $number;
    protected $name;
    protected $address;
    public function ...
}

$info = new class('name', 'address') extends Packt implement Publishers
{
    public function __construct(string $name, string $address)
    {
        $this->name = $name;
        $this->address = $address;
    }

    public function getName() : string
    {
        return $this->name;
    }

    public function getAddress() : string
    {
        return $this->address;
    }
}

echo $info->getName() . ' ' . $info->getAddress();
```

匿名类可以嵌套在一个类中使用。

```
class Math
{
    public $first_number = 10;
    public $second_number = 10;
    public function add() : float
    {
        return $this->first_number + $this->second_number;
    }

    public function mutiply_sum()
    {
        return new class() extends Math
        {
            public function mutiply(float $third_number) : float
            {
                return $this->add() * $third_number;
            }
        };
    }
}

$math = new Math();
echo $math->mutiply_sum()->mutiply(2);
```

### 摒弃老式构造函数

从PHP4开始，构造函数可以通过命名与类名一致的方式来声明自己是构造函数，在PHP7中这种方式声明构造函数依然可以使用，但不推荐使用，会输出不推荐的信息, PHP7中推荐使用 `__construct()`


### throwable接口

从PHP7开始，程序中的fatal错误都可以被截获，PHP7提供了throwable接口，异常与错误都继承于这个接口。

### Error

现在大多数的fatal错误情况会抛出一个error实例，类似于截获异常，error实例可以被try/catch截获。

```
try {
    ...
} catch(Error $e) {
    echo $e->getMessage();
}
```
一些错误情况只有error的子实例会被抛出，例如 TypeError、DivisionByZeroError、ParseError等。

### <=>操作符
`<=>`操作符将`==`、`<` 、`>` 三个比较操作符打包在了一起，具体使用规则如下。

```
操作符两边相等时返回 0
操作符左边小于右边时返回 -1
操作符左边大于右边时返回 1
```

### null合并运算符
`??`合并运算符，在第一操作数存在时可被直接返回，否则返回第二操作数。
```
$title = $post['title'] ?? NULL;

$title = $post['title'] ?? $get['title'] ?? 'No title';
```

### uniform变量语法
```
$first = ['name' => 'second'];
$second = 'two';
echo $$first['name'];
echo ${Sfirst['name']}; // PHP7

...
echo $object->$methods['title'];
echo $object->{$methods['title']}; // PHP7
```
主要是因为PHP7与之前版本PHP的解析方式不一样，在PHP7中加上花括号就可以啦，就像上边代码这样，否则会报错。


### 常量数组
从PHP5.6开始常量数组可以用`const`关键字来声明，在PHP7中常量数组可以通过`define`函数来初始化。

```
const STORES = ['en', 'fr', 'ar']; // php5.6
define('STORES', ['en', 'fr', 'ar']); // php7
```

### switch中的default默认值
在PHP7之前，switch语句中允许多个default默认值，从PHP7开始，只能有一个default默认值，否则会产生fatal级别错误。
```
// php7之前
switch (true) {
    case 'value':
        # code...
        break;
    default:
        # code...
        break;
    default:
        # code...
        break;
}

// php7
switch (true) {
    case 'value':
        # code...
        break;
    default:
        # code...
        break;
}
```
### session_start函数中的选项数组
在PHP7之前，使用session的时候都必须先调用session_start()函数，且这个函数并没有参数需要传递，所有session相关的配置都在php.ini文件中，从PHP7开始，可以在调用这个函数时传递参数选项数组，这些设置信息将覆盖php.ini中的session配置。

```
session_start([
    'cookie_lifetime' => 3600,
    'read_and_close' => true
]);
```

### unserialize函数引入过滤器
unserialize()可以反序列化任何类型的对象，没有任何过滤项，不安全，PHP7在unserialize()中引入了过滤器，且默认允许反序列化所有类型的对象。
```
$result = unserialize($object, ['allowed_classes' => ['Book', 'Ebook']]);
```


### 

