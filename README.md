## debug-tsc

VSCode 用于调试 tsc 的配置。  
下文 `{TypeScript_Root}` 为本地 TypeScript 源码根目录。

### 1. 前置条件
#### （1）克隆 TypeScript
```
$ git clone https://github.com/microsoft/TypeScript.git {TypeScript_Root}
$ cd {TypeScript_Root}
$ git checkout v3.7.3
```

#### （2）构建
```
$ npm i
$ node node_modules/.bin/gulp LKG
```
关于 `gulp LKG`，可参考 [TypeScript/lib/README.md](https://github.com/microsoft/TypeScript/blob/v3.7.3/lib/README.md)

#### （3）修改 package.json
添加 `debug` scripts，
```
{
  ...
  "scripts": {
    "debug": "node --inspect-brk=9001 bin/tsc debug/index.ts",
    ...
  },
  ...
}
```
`--inspect-brk=9001` 端口号 `9001` 要与本仓库 `.vscode/launch.json` 中的 `"port": 9001` 保持一致。

#### （4）修改 bin/tsc
```
#!/usr/bin/env node
require('../built/local/tsc.js');
```

#### （5）新建 debug/index.ts
```
const i: number = 1;
```

#### （6）拷贝调试配置
将本仓库的 `.vscode/launch.json` 拷贝到 `{TypeScript_Root}`。

### 2. 使用方式

用 VSCode 打开 `{TypeScript_Root}`，按 `F5` 启动调试。

- - -

### 参考

[淡如止水 TypeScript（一）](https://www.yuque.com/thzt/typescript/ailg7r)
