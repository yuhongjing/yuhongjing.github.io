---
title: Php魔术方法
date: 2017-12-04 22:05:57
tags: PHP魔法变量
keywords: PHP，PHP魔法变量，PHP魔法方法
categories: "研究"
---
PHP在设计的时候，预先定义了9个超级全局变量、8个魔术变量和13个魔法方法，这些变量和函数可以在脚本任何地方不用声明就可以使用。  
在PHP开发会频繁的使用这些变量和方法。会很方便的帮我们解决很多事情。  
<!--more-->
## PHP超级全局变量（9个）
```
    $GLOBALS        存储全局作用域中的变量
    $_SERVER        获取服务器相关信息
    $_REQUEST       获取POST和GET请求的参数
    $_POST          获取表单的POST请求参数
    $_GET           获取表单的GET请求参数
    $_FILES         获取上传文件的变量
    $_ENV           获取服务器端环境变量的数组
    $_COOKIE        浏览器cookie的操作
        设置cookie    setcookie(name,value,expire,path,domain);
        获取cookie    $_COOKIE["name"];
        删除cookie    setcookie("user","",time()-3600);//设置过期时间
    $_SESSION       服务器session的操作
        启动session   session_start();
        存储session   $_SESSION["name"]="Li hua";
        销毁session   unset($_SESSION["name"]);
        seesion_destroy()和unset($_SESSION);//销毁所有的session
```
## PHP魔术变量（8个）
```
    __LINE__　　        文件中的当前行号。
　　__FILE__　　        文件的完整路径和文件名。如果用在被包含文件中，则返回被包含的文件名。
　　__DIR__　　         文件所在的目录。如果用在被包括文件中，则返回被包括的文件所在的目录。
　　__FUNCTION__　　    常量返回该函数被定义时的名字
　　__CLASS__　　       常量返回该类被定义时的名字（区分大小写）。
　　__METHOD__　　      类的方法名（PHP 5.0.0 新加）。返回该方法被定义时的名字（区分大小写）。
　　__NAMESPACE__　　   当前命名空间的名称（区分大小写）。此常量是在编译时定义的（PHP 5.3.0 新增）。
```
## PHP魔术方法（13个）
```
　  __construct()　　      实例化对象时被调用，当__construct和以类名为函数名的函数同时存在时，__construct将被调用，另一个不被调用
　　__destruct()　　       当删除一个对象或对象操作终止时被调用。
　　__call()　　　　　     对象调用某个方法，若方法存在，则直接调用；若不存在，则会去调用__call函数。
　　__get()　　　　        读取一个对象的属性时，若属性存在，则直接返回属性值；若不存在，则会调用__get函数。
　　__set()　　　　        设置一个对象的属性时，若属性存在，则直接赋值；若不存在，则会调用__set函数。
　　__toString()　　      打印一个对象的时被调用。如echo $obj;或print $obj;
　　__clone()　　　       克隆对象时被调用。如：$t=new Test();$t1=clone $t;
　　__sleep()　　　       serialize之前被调用。若对象比较大，想删减一点东东再序列化，可考虑一下此函数。
　　__wakeup()　　        unserialize时被调用，做些对象的初始化工作。
　　__isset()　　　       检测一个对象的属性是否存在时被调用。如：isset($c->name)。
　　__unset()　　　　     unset一个对象的属性时被调用。如：unset($c->name)。
　　__set_state()　　     调用var_export时，被调用。用__set_state的返回值做为var_export的返回值。
　　__autoload()　　      实例化一个对象时，如果对应的类不存在，则该方法被调用。
```

