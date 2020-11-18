---
title: webpack plugins
tags: [webpack,plugins]
renderNumberedHeading: true
grammar_cjkRuby: true
date: 2020-11-17
Author: Dean
comments: true
---

# plugin：插件
- plugin是一个类，里面包含一个apply函数，接收一个参数：compiler
- plugin在某个时刻帮助我们处理一些事情的地址

```
class CopyrightWebpackPlugin {
  // 获取外部参数的参数配置
  constructor(options) {
    console.log(options, "Hello plugins");
  }

  apply(compiler) {
    // 同步
    compiler.hooks.emit.tap("CopyrightWebpackPlugin", (compilation) => {
      console.log("同步hooks执行");
    });
    // emit生成资源到output目录之前
    // 异步
    compiler.hooks.emit.tapAsync(
      "CopyrightWebpackPlugin",
      (compilation, cb) => {
        compilation.assets["copyright.txt"] = {
          source: function () {
            // 定义文档的内容
            return "hello my plugin";
          },
          size: function () {
            return 30;
          },
        };
        cb();
      }
    );
  }
}

module.exports = CopyrightWebpackPlugin;

```
  - 详情参考https://webpack.js.org/concepts/plugins/#anatomy