---
title: Foundry基础教程
published: 2026-01-31
description: Foundry的基础安装和使用
tags: [Web3, Foundry, Toturial]
category: Web3
draft: false
---

## 安装
### 下载安装脚本
``` bash
curl -L https://foundry.paradigm.xyz | bash
```
安装后记得更新环境变量
### 运行Foundryup
运行`foundryup`或者 `foundryup -i nightly`
这会安装forge, cast, anvil, chisel
## 各部分作用
- forge: 构建、测试、调试、部署和验证智能合约
- anvil: 本地的开发节点
- cast: 用命令行与链上应用交互
- chisel: idk?
## 基本项目结构
使用 `forge init dapp_name` 创建dapp项目目录
- `src/` 智能合约
- `test/` 测试文件
- `script/` 部署脚本
## 基本使用流程
### 壹
运行`anvil`来启动本地节点，找到 `Private Keys` 下面的第一行（`0xac09...` 开头那一长串），复制它！ 这是系统的“上帝账号”，里面有无限的钱？
### 贰
部署合约
``` bash
forge create src/Counter.sol:Counter \
  --rpc-url <http://127.0.0.1:8545> \
  --private-key <你的私钥> \
  --broadcast
```
`你的私钥`即`壹`中的`0xac09`
成功部署后会得到合约地址`Deployed to: 0x...`
### 叁
使用`cast`进行交互合约
1. 无gas消耗操作<br>使用`cast call <合约地址> "函数名()" --rpc-url http://127.0.0.1:8545` 示例中number()函数输出为16进制，加上`| cast --to-dec`人类可读
2. 修改链上数据（有gas消耗）<br> `cast send <合约地址> "setNumber(uint256)" 666 --rpc-url <http://127.0.0.1:8545> --private-key <你的私钥>`
