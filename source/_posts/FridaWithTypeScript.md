---
title: Frida：自动补全功能和TypeScript模块化脚本
date: 2020-03-07 16:42:41
categories:
- [Frida, Skill]

tags:
- Frida

---

## 简介

配合使用集成开发环境编辑器（例如：JetBrains IDEA或Visual Code）编写[TypeScript](https://www.typescriptlang.org/)脚本来规范化、模块化并提供自动补全你的代码，让你的开发效率大大提升。



## 部署

- 项目地址：[frida-agent-example](https://github.com/oleavr/frida-agent-example)

```shell
$ git clone git://github.com/oleavr/frida-agent-example.git
$ cd frida-agent-example/
$ npm install
$ npm run watch
```



- 集成开发环境打开`frida-agent-example`目录

编辑`frida-agent-example/index.ts`文件并保存

`npm run watch`会监控[index.ts](https://github.com/oleavr/frida-agent-example/blob/master/agent/index.ts)文件并在项目根目录下生成`_agent.js`目标脚本。



- `Frida`注入

```shell
$ frida -U -f com.example.android --runtime=v8 --no-pause -l _agent.js
```



## 好用的TypeScript脚本

