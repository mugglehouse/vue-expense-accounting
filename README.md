# vue-expense-accounting

This template should help get you started developing with Vue 3 in Vite.

## Recommended IDE Setup

[VSCode](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (and disable Vetur).

## Customize configuration

See [Vite Configuration Reference](https://vite.dev/config/).

## Project Setup

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Compile and Minify for Production

```sh
npm run build
```

### Lint with [ESLint](https://eslint.org/)

```sh
npm run lint
```


## 一些小错误

```
Eslint针对template多根节点的错误，原因是vscode打开的是你工程文件的子目录，将你工程文件变为根目录即可
```

## 安装最新node版本

```
下载地址：https://nodejs.org/en/download/prebuilt-installer
更改npm镜像：npm config set registry=https://registry.npmmirror.com
检查镜像地址：npm config get registry
```

## 创建vue应用

```
npm create vue@latest
npm install
npm run dev
```

## 配置代码片段

```
vue.json中配置
{
"vue setup": {
"prefix": "<script setup>",
"body": [
"<script setup>",
"",
"</script>",
"",
"<template>",
"    ",
"</template>",
"",
"<style>",
"",
"</style>",
],
"description": "vue setup template"
}
}
```

## 使用TailwindCSS

```
1. 安装--创建tailwindcss.js
npm install -D tailwindcss
npx tailwindcss init

2. 配置tailwindcss.js
/** @type {import('tailwindcss').Config} */
export default {
  content: [
    './index.html',
    './src/**/*.{vue,js,ts,jsx,tsx}',
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}

3. css中引入Taiwind基本指令
@tailwind base;
@tailwind components;
@tailwind utilities;
会显示unknow，解决：
vscode打开设置，搜索 "未知"
CSS > Lint: Unknown At Rules:ignore

3. main.js引入css
import './assets/style.css'
```

## vue-expense-accounting

```
技术栈：Vue3+Vite

Demo描述：
1. 单页面记账应用，用户可以记录收入和支出，查看交易列表，计算总余额。
2. 使用 Vue 3 的组合式 API 进行组件化开发，提升代码可读性和可维护性。
3. 实现了数据持久化功能，使用 localStorage 存储交易记录，确保页面刷新后数据不丢失。
4. 通过props和自定义事件实现子组件与父组件之间的通信，用户可以添加和删除交易记录。

基本结构：单页面+1个父组件APP和5个子组件
Header -- 标题
Balance -- 总结余
IncomeExpenses -- 收入支出
TransactionList -- 消费列表
AddTransaction -- 增加消费

tree /F 命令生成文件结构树

1. AddTransaction
父组件监听提交事件，并触发回调函数将新的交易记录添加到交易列表，回调函数接收来自子组件emit回来的一条交易记录

2. TransactionList
父组件绑定prop传递给子组件交易列表，并监听删除事件，触发删除回调函数。子组件通过defineProps接收来自父组件的交易列表数据

3. IncomeExpenses
计算属性通过计算交易表中的收入和支出总合，通过props传递给子组件

4. Balance
计算属性通过计算交易表中的收入和支出的平衡，通过props传递给子组件

```
