---
title: windows以太坊Dapp开发环境
date: 2019-02-19 17:16:35
tags:
---

### windows搭建以太坊的开发环境
#### 安装Node.js
[官网](https://nodejs.org/zh-cn/)下载并安装即可。  

打开cmd执行以下命令:
```cmd
C:\Users\Administrator> node -v
v10.14.2
```
出现版本号即表示安装成功。
<!--more-->

#### 安装节点仿真器
为了快速开发和测试以太坊DApp，我们通常使用以太坊节点仿真器来模拟区块链，最流行的节点仿真器就是Ganache，之前被称为TeseRPC。

安装Ganache的命令:
```cmd
C:\Users\Administrator> npm install -g ganache-cli
```

执行以下命令验证是否安装成功:
```cmd
C:\Users\Administrator> ganache-cli
Ganache CLI v7.0.0-beta.0 (ganache-core: 3.0.0-beta.0)
```
默认会开启节点,并打印出很多的信息即表示安装成功。

要了解ganache命令行的详细用法,可以查看[以太坊ganache CLI命令行参数详解](https://my.oschina.net/u/3794778/blog/1799768)

#### 安装solidity编译器
solidity是开发以太坊智能合约的编程语言,不熟悉的话可以查看[以太坊solidity开发语言简介](https://my.oschina.net/u/3794778/blog/1799912)。

安装solidity编译器命令:
```cmd
C:\Users\Administrator> npm install –g solc
```

执行以下命令验证是否安装成功:
```cmd
C:\Users\Administrator> solcjs --version
0.5.4+commit.9549d8ff.Emscripten.clang
```
出现信息即表示安装成功。

#### 安装web3

```cmd
C:\Users\Administrator> npm install –g web3
```

#### 安装truffle框架

```cmd
C:\Users\Administrator> npm install –g truffle
```

执行以下命令验证是否安装成功:
```cmd
C:\Users\Administrator> truffle.cmd version
Truffle v5.0.4 (core: 5.0.4)
Solidity v0.5.0 (solc-js)
Node v10.14.2
```
出现信息即表示安装成功。

#### 安装webpack

```cmd 
C:\Users\Administrator> npm install –g webpack
```

执行以下命令验证是否安装成功:
```cmd
C:\Users\Administrator> webpack –v
3.11.0
```
出现信息即表示安装成功。

### 构建示例项目
#### 新建DApp项目
通过webpack模板初始化项目骨架架构:
```cmd
d:\demo> truffle.cmd unbox webpack
Downloading…
Unpacking…
Setting up…
Unbox successful. Sweet!
```

#### 安装项目依赖的NPM包

```cmd 
d:\demo> npm install
```

#### 修改truffle配置
在truffle.js文件中,开启如下代码:
```js
module.exports = {
  networks:{
    development: {
      port: 8545
    }
  }
}
```

#### 启动节点仿真器
```cmd
C:\Users\Administrator> ganache-cli
```

#### 编译合约
```cmd
d:\demo> truffle.cmd compile
```

#### 部署合约
注意: 必须先开启节点,才能在节点上部署合约。
```cmd
d:\demo> truffle.cmd migrate
```

#### 启动DApp
```cmd
d:\demo> cd app
d:\demo\app> npm run dev
```
浏览器访问http://localhost:8080即可。

如果希望别人访问我们的DApp应用,需要修改package.json:
```json
{
  scripts:{
    "dev": "webpack-dev-server –-host 0.0.0.0"
  }
}
```
添加`--host 0.0.0.0`。