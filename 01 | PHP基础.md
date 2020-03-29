# 理论很重要
## Touch一下子

 - php是啥子哦？ [看这里](https://www.baidu.com/s?ie=UTF-8&wd=php%E8%83%BD%E5%81%9A%E4%BB%80%E4%B9%88)
 - php去哪里找工作？ [来这里](https://www.baidu.com/s?ie=UTF-8&wd=php%E6%8B%9B%E8%81%98)
 - 哪里可以学到最正宗的php? [php官方手册](https://www.php.net/manual/zh/) [英文版](https://www.php.net/manual/en/)
 
 
## php基础

### 基本数据类型
9种数据类型，php属弱类型语言，无需定义直接使用，可覆盖其值的类型（但不推荐随意覆盖类型）
 - Int 整形
 - Bool 布尔
 - Float 浮点
 - String 字符串
 - Array 数组
 - Object 对象
 - Callback 可回调
 - Resource 资源
 - NULL

### 流程控制
 - if elseif else
    - 条件分支简洁是推荐使用
 - switch case
    - 条件分支较多（一般大于3个）推荐使用
 - for
    - 一般常用与已知次数循环操作
 - while
    - 常用于守护进程以及重试任务，特别注意死循环问题
 - foreach （拿本记上这是重点）
    - 遍历数组常用，关联数组以及索引数组都不在话下，在项目中上镜率较高

### 函数
 - 系统内置函数 
    - sort 、 array 、 echo 、 die 等
 - 自定义函数 function 
    - function xxx () {}

### 面向对象 class
 - 封装 
    - public private protected final static 
 - 抽象
    - 把想实现的功能抽象成最小执行体，通过组合的方式完成一个整体需求
 - 继承 extends
    - 父子关系，优良传统需要代代相传
 - 抽象类 abstract 
    - is-a
    - 代码复用
 - 接口 interface 
    - has-a 
    - 抽象

### 数组
    
#### 定义数组
数组 ： 根据排名、映射构成的一组数据，由键值对(key=>value)组成
`eg:[0 => 'maying', 'name' => 'xxx']`

 - 索引数组
    - 键由从0开始的连续数字构成，eg:["a","b","c"] 
 - 关联数组
    - 键由非从0开始的连续数字构成,eg:["name"=>"ming", "age"=>18, "sex"=>1]

#### 常用内置函数
 - sort
 - array
 - count
 - implode


### 字符串
#### 定义字符串
字符串：由一系列字符组成，常用与单引号或双引号表达
`eg: 'abc' 、 '1a2b3c' 、 '你好' `

#### 常用内置函数
 - trim
 - strlen
 - strstr
 - strpos
 - explode

### CURD必杀技
#### PDO
php提供的扩展，用于与据库交互, 使用PDO MySQL驱动操作mysql数据库。


# 我们来上手实操一下

## 数据类型、流程控制

```php
<?php
//变量以及数据类型
$name = 'phper'; //字符串类型变量
$age = 18; //int型变量
$sex = '1'; //字符串类型 值为1
$language = ['English', 'Chinese'];

//流程控制
if ($age > 18) {
    echo "hi";
} else {
    echo "hello";
}

foreach ($language as $k=>$v) {
    echo $v;
}

//自定义函数
function say ($inputParam) {
    $result = '';
    $result = 'hi '. $inputParam;
    return $result;
}
$str = say('xiaoming');
echo $str; // hi xiaoming

```

## 面向对象
```php
<?php

//抽象类，包含say、run两个方法，子类必须自己实现run方法
abstract class People
{
    //普通方法可
    public function say($input)
    {
        return 'hi ' . $input;
    }

    abstract public function run();
}

//work接口，约束必须实现 do1 do2两个方法
interface work
{
    public function do1();

    public function do2();
}

//study接口，约束必须实现study1 study2两个方法
interface study
{
    public function study1();

    public function study2();
}

//工人类 继承People 实现接口work
class Workman extends People implements work
{
    public function run()
    {
        echo 'car';
    }

    public function do1()
    {
        echo 'do sth 1';
    }

    public function do2()
    {
        echo 'do sth 2';
    }
}

class Student extends People implements study
{
    public function run()
    {
        echo 'bicycle';
    }

    public function study1()
    {
        echo 'study sth 2';
    }

    public function study2()
    {
        echo 'study sth 2';
    }
}

$obj1 = new Workman();
$obj1->run();

$obj2 = new Student();
$obj2->run();

# 解释一下：
# 抽象类表示is-a  工人和学生都是国民，都可以说话和走路，所以继承自 People
# 接口表示 has-a  工人的重点是工作所以实现了work接口， 学生的重点是学习所以上线了study接口


```

## 数据库
```php
<?php

try {
    //连接
    //host
    $dbh = new PDO('mysql:host=localhost;dbname=test', 'user', '123456');

    //执行增删改查
    foreach ($dbh->query('select id,username,sex from user where id < 10') as $row) {
        print_r($row);
    }

    //关闭连接
    $dbh = null;
} catch (PDOException $e) {
    //异常处理
    print "Error!: " . $e->getMessage() . "<br/>";
    die();
}

```

