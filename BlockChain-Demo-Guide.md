---
title: BlockChain-Demo 使用手册
tags: 区块链,手册,矩阵元
---

## 矩阵元区块链平台

### 准备工作

 * Ubuntu16.04  
 * [NodeJS 5.0+ recommended.](#nodejs)
 * [npm 安装](#npm)
 * [truffle2.1.1安装](#truffle)
 * 矩阵元联盟链

 操作前请确保您已成功安装部署**矩阵元联盟链**，如果还未安装，请参考部署手册[矩阵元区块链云平台部署手册](#)

#### <span id="nodejs">Nodejs安装</span>
```shell
$ sudo apt-get install nodejs
```

#### <span id="npm">npm安装</span>
```shell
$ sudo apt-get install npm
# 配置国内镜像源，提高下载速度
$ sudo npm config set registry https://registry.npm.taobao.org
$ sudo npm config list
```

#### <span id="truffle">truffle安装</span>
```shell
# -g 为全局安装
$ npm install -g truffle@2.1.1
```

### 合约介绍

  * 实现了一个基本的股权交易合约
  * 基于该合约能够实现基本的股权登记与非交易过户等功能特性
  * 采用零知识证明与同态加密算法实现用户股权账户的隐私保护
  * 初步呈现了矩阵元联盟链在交易执行、业务查询、隐私保护等方面的功能

### 合约发布

目录介绍
```none
app/						- truffle 测试WEB程序
contracts/					- 合约目录
- interfaces/					  - 合约接口定义（抽象合约）
  - IJuzixTokenManager.sol			  - 接口:股权交易
  - IRegisterManager.sol			  - 接口：注册中心
  - IRoleFilterManager.sol			  - 接口：角色过滤器
library/					- Libray库目录
- LibTokenPailler.sol				  - Lib:合约信息Struct
- LibTokenRecord.sol				  - Lib:交易记录Struct
nizk/						- 同态加密Lib库
- LibNIZK.sol
- LibNizkParam.sol				
sysbase/					- 系统合约目录
- BaseModule.sol				  - 基础模块合约，所有模块需要继承该合约
- OwnerNamed.sol				  - 所有业务合约都需继承该合约
token/						- ERC2.0接口标准
- BasicToken.sol
- ERC20.sol
- ERC20Basic.sol
- StandardToken.sol
utillib/					- 系统工具合约
- LibDB.sol
- LibDecode.sol
...
JuzixTokenManager.so				- 股权交易主合约
TokenModuleManager.sol 				- 股权DAPP对应模块
truffle.js					- truffle 配置文件
package.json					- npm包配置文件
install.js					- 合约发布程序
```

安装nodejs包依赖    
```shell
$ npm install 
```

编译合约
```none
$ truffle compile
```
```none
 如出现无法编译情况，请尝试使用此设置运行: node --max_old_space_size=2000000 /usr/local/bin/truffle
```

发布合约
```none
$ node install.js --passwd 11111111 --url http://127.0.0.1:6789 --address 0xa5efb0582443bc5b77f707cea850ef099e3068cc
```
* --passwd 为新建的钱包口令
* --url 矩阵元联盟链的JSON-RPC访问地址
* --address 钱包地址（特指您本地可使用的钱包地址）

说明：    
1、address 参数务必仔细填写，在合约发布完成后会自动重置合约的归属者，此地址会被设置会合约的owner地址；         
 
2、发布合约前请务必先编译合约；








