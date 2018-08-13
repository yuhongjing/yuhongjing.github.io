---
title: TP5源码分析之Db类实现
date: 2018-08-10 22:20:38
tags:  PHP
keywords: TP5源码分析
categories: "技术"
---
### 前言
从TP3.2到TP5，已经使用了TP框架快两年了。自认为使用TP处理一般的业务不成问题了。  
可是，却从来没有深究过TP是如何实现这些功能的，仅仅只是会调用API而已，也不敢动框架的代码。    
所以现在就整理一系列的文章来研究一下TP5的底层源码，设计模式，思想等。  
额！算是开始一个坑吧。从最经典的Db类开始吧！ gogogo！
<!--more-->
### 对Db类的初识
一直觉得TP5的Db类是很方便的，只需要更改一下database配置文件即可连接各种数据库。  
个人觉得还是挺强大的，他是如何通过配置文件更改一个值就能调用不同的数据库，这让我很是疑惑。    
所以来研究一下吧，不过我刚看了一本书《PHP的核心技术与最佳实践》，了解了通过工厂模式是可以完成这个要求的。  
不过还是看一下TP5是怎么实现的吧。
### Db类的相关文件分析
本系列的部分细节参考了此文档[戳我可见](https://www.kancloud.cn/zmwtp/tp5/155311)   
**文件thinkphp是TP5的核心库**  
而`thinkphp\think`目录下是我们各个类的入口   
```
    此目录下有一个Db.php是Db类的入口。
```
TP5的Db类文件夹目录为:thinkphp\think\db
```
    此文件夹为Db类的具体实现
    有如下文件
    db
        builder Db驱动类
            Mysql.php   Mysql数据库驱动
            Pgsql.php   Pgsql数据库驱动
            Sqlite.php  Sqlite数据库驱动
            Sqlsrv.php  Sqlsrv数据库驱动
        connector   Db连接器类
            Mysql.php   Mysql数据库连接
            Pgsql.php   Pgsql数据库连接
            pgsql.sql   Pgsql类型转换
            Sqlite.php  Sqlite数据库连接
            Sqlsrv.php  Sqlsrv数据库连接
        exception   Db错误类
            BindParamException.php  Pdo参数绑定异常
            DataNotFoundException.php   字段没有找到
            ModelNotFoundException.php  模型不存在
        Builder.php Db的抽象驱动类，通过此类构建对应的Db驱动类
        Connection.php Db的抽象连接器类，通过此类连接对应Db连接器类
        Query.php 将所有的Sql方法封装成一个类。
```
### Db入口类分析
一般我们调用Db类是需要`use thinkphp\Db`,这文件就是我们的入口文件，所以我们看看他的代码    
```
   namespace think; 
   
   use think\db\Connection; 
   use think\db\Query;
   class Db {
       // 数据库连接实例
       private static $instance = [];
       // 查询次数
       public static $queryTimes = 0;
       // 执行次数
       public static $executeTimes = 0;
       //   数据库初始化,并取得数据库类实例
       public static function connect($config = [], $name = false){
            .....先省略
       }
       // 清除所有的实例
       public static function clear() {
            self::$instance = null; // 很粗暴嘛
       }
       // 数据库连接参数解析
       private static function parseConfig($config){
            ....先省略
       }
       // DSN解析 把返回的参数解析一下 提取需要连接的关键字
       private static function parseDsn($dsnStr){
            ...先省略
       }
       // 调用驱动类的方法
       public static function __callStatic($method, $params){
             ...先省略
       }
   }
```
这就是Db入口类的基本目录结构。  
首先分析头部,命名空间为think,class为Db说明我们的入口没错。然后use两个类，一个连接器类，一个Query类。  
看一看此类的各个方法，发现主要是初始化+解析config的配置。  
#### 首先看看Db入口类是如何获取到database里面的参数的
```
    database的配置是通过parseConfig方法获取到的，代码如下
    private static function parseConfig($config)
        {
            if (empty($config)) {
                // 这里引入的database文件哟!!!
                $config = Config::get('database');
            } elseif (is_string($config) && false === strpos($config, '/')) {
                // 支持读取配置参数
                $config = Config::get($config);
            }
            if (is_string($config)) {
                return self::parseDsn($config);
            } else {
                return $config;
            }
        }
```
这里是通过了一个助手函数config把database里面的参数返回了，这样我们就得到了database的参数。  
#### 那我们看看database里面是什么样的呢?  
```
database在application目录下有，当然每一个模块下面也可以新建。
return [
    // 数据库类型
    'type'           => '',
    // 服务器地址
    'hostname'       => '',
    // 数据库名
    'database'       => '',
    // 用户名
    'username'       => '',
    // 密码
    'password'       => '',
    // 端口
    'hostport'       => '3306',
    // 连接dsn
    'dsn'            => '',
    // 数据库连接参数
    'params'         => [],
    // 数据库编码默认采用utf8
    'charset'        => 'utf8',
    // 数据库表前缀
    'prefix'         => 'qy_',
    // 数据库调试模式
    'debug'          => true,
    // 数据库部署方式:0 集中式(单一服务器),1 分布式(主从服务器)
    'deploy'         => 0,
    // 数据库读写是否分离 主从式有效
    'rw_separate'    => false,
    // 读写分离后 主服务器数量
    'master_num'     => 1,
    // 指定从服务器序号
    'slave_no'       => '',
    // 是否严格检查字段是否存在
    'fields_strict'  => true,
    // 数据集返回类型 array 数组 collection Collection对象
    'resultset_type' => '\think\Collection',
    // 是否自动写入时间戳字段
    'auto_timestamp' => true,
    // 是否需要进行SQL性能分析
    'sql_explain'    => false,
];
```
可以看见database文件把数据return了回来，所以可以获取到里面配置的所有内容，这样的解耦使我们的配置更加简便，不错！  
#### 然后看看最核心的连接类是如何执行的呢？
```
    如何通过配置文件即可连接相对于的数据库类呢？
    public static function connect($config = [], $name = false)
        {
            if (false === $name) {
                $name = md5(serialize($config));
            }
            if (true === $name || !isset(self::$instance[$name])) {
                // 解析连接参数 支持数组和字符串
                $options = self::parseConfig($config);
                if (empty($options['type'])) {
                    throw new \InvalidArgumentException('Undefined db type');
                }
                // 就是这句代码哦，实现的加载不同的连接器哟！！！
                $class = false !== strpos($options['type'], '\\') ? $options['type'] : '\\think\\db\\connector\\' . ucwords($options['type']);
                // 记录初始化信息
                if (App::$debug) {
                    Log::record('[ DB ] INIT ' . $options['type'], 'info');
                }
                if (true === $name) {
                    $name = md5(serialize($config));
                }
                self::$instance[$name] = new $class($options);
            }
            return self::$instance[$name];
        }
```
好吧，还是很经典的工厂模式。通过传入的配置参数，引入对应的文件。学习了，的确很方便！  
到目前为止已经能够获取database的参数了，也能初始化不同的连接器了，还差一个查询方法了。  
是的，还有一个`use think\db\Query`还没使用呢！对吧。
#### 驱动类的实现
```
    TP5把所有的SQL都通过PDO封装了，意思是无论你是什么数据库，查询的关键字都是这些！方便吧。
     // 调用驱动类的方法
     public static function __callStatic($method, $params)
     {
         // 自动初始化数据库
         return call_user_func_array([self::connect(), $method], $params);
     }
```
魔术方法，调用静态方法，每次调用前都会初始化数据库,并传入方法和参数。  
然后因为引入的连接器不同，所以会调用相对于的构建类他们都继承builder，而builder封装了所有的查询方法。  
这样就可以实现封装所有数据库的查询方法了！   
***接下来看看那两个use分别是什么吧***
### Connection连接类
```
    db文件下有connector文件夹，封装了每一种数据库的连接方式，他们都继承于connection
    他们绑定了相对于的构建器。例如： 
    connector下的Mysql.php
    protected $builder = '\\think\\db\\builder\\Mysql';
    所以只需要连接的时候判断类型，就会获得相对于的builder构建器
    然后主要看它们的父类Connection连接器
    代码很多，截取最主要的吧
    abstract class Connection
    {
        protected $config = [
             // 数据库类型
             'type'            => '',
             // 服务器地址
             'hostname'        => '',
             // 数据库名
             'database'        => '',
             // 用户名
             'username'        => '',
             // 密码
             'password'        => '',
             // 端口
             'hostport'        => '',
             // 连接dsn
             'dsn'             => '',
             // 数据库连接参数
             'params'          => [],
             // 数据库编码默认采用utf8
             'charset'         => 'utf8',
             // 数据库表前缀
             'prefix'          => '',
             // 数据库调试模式
             'debug'           => false,
             // 数据库部署方式:0 集中式(单一服务器),1 分布式(主从服务器)
             'deploy'          => 0,
             // 数据库读写是否分离 主从式有效
             'rw_separate'     => false,
             // 读写分离后 主服务器数量
             'master_num'      => 1,
             // 指定从服务器序号
             'slave_no'        => '',
             // 是否严格检查字段是否存在
             'fields_strict'   => true,
             // 数据返回类型
             'result_type'     => PDO::FETCH_ASSOC,
             // 数据集返回类型
             'resultset_type'  => 'array',
             // 自动写入时间戳字段
             'auto_timestamp'  => false,
             // 时间字段取出后的默认时间格式
             'datetime_format' => 'Y-m-d H:i:s',
             // 是否需要进行SQL性能分析
             'sql_explain'     => false,
             // Builder类
             'builder'         => '',
             // Query类
             'query'           => '\\think\\db\\Query',
             // 是否需要断线重连
             'break_reconnect' => false,
         ];
     
         // PDO连接参数
         protected $params = [
             PDO::ATTR_CASE              => PDO::CASE_NATURAL,
             PDO::ATTR_ERRMODE           => PDO::ERRMODE_EXCEPTION,
             PDO::ATTR_ORACLE_NULLS      => PDO::NULL_NATURAL,
             PDO::ATTR_STRINGIFY_FETCHES => false,
             PDO::ATTR_EMULATE_PREPARES  => false,
         ];
    }
```
有很多很多代码，上面主要是默认的config和PDO连接参数的初始化。 因为是抽象类所以实例化的是他们的各个子类。
#### builder的工厂模式
```
 public function getBuilder()
    {
        if (!empty($this->builder)) {
            return $this->builder;
        } else {
            return $this->getConfig('builder') ?: '\\think\\db\\builder\\' . ucfirst($this->getConfig('type'));
        }
    }
```
这里是通过子连接器的属性，用工厂模式引入的相对于的构建器和Db入口类的思想也是一样的。
**其余的都是各种的数据库基本操作了**
### Query类
Query类封装了各种Sql原生语句实现的方法，算是独立出来的，因为model也可以使用这个。
### Db类总结
TP5的Db类差不多就是如上，思想主要是通过工厂模式来通过同一入口，创建不同的实例，其中查询时封装了一层Pdo层，  
即方便了用户使用，也可以增强安全性。总之十分收益。不过我的描述不行，很多想写的不知道怎么写，再接再厉。  
TP5源码分析系列第一步OK。


  








