---
title: webpack plugin
date: 2018/5/7
categories:
- ProjectTools
---
> webpack规定插件必须是一个javascript对象，且对象上必须有一个apply方法，这个apply方法会在webpack进行编译的时候进行调用.

[toc]

## getting start
```js
class RemoveCommentsPlugin {
  apply(compiler) {
    console.log('RemoveCommentsPlugin start');
    
    // emit钩子：输出 asset 到 output 目录之前执行
    compiler.hooks.emit.tap('RemoveCommentsPlugin', compilation => {
      console.log('emit event touch')
      // compilation 可以理解为本次打包的上下文
      for (const name in compilation.assets) {
        if (name.endsWith('.js')) {
          const fileContent = compilation.assets[name].source();
          const reg = /console.log(.*)/g;
          // const reg = /\/\/[^\\r\\n]*/;
          const noComments = fileContent.replace(reg, '');
          compilation.assets[name] = {
            source: () => noComments,
            size: () => noComments.length,
          }
        }
      }
    })

  }
}

module.exports = RemoveCommentsPlugin;

```

## webpack 的整体编译流程
webpack 的编译流程可以分为以下几个主要阶段：
+ initialize‌：初始化阶段，创建 Compiler 实例。
+ run‌：运行阶段，调用 Compiler 的 run 方法。
+ compiler‌：编译器阶段，处理配置和插件。
+ compilation‌：编译阶段，创建 Compilation 实例，处理入口文件。
+ ‌make‌：构建阶段，创建 NormalModuleFactory 和 ContextModuleFactory，处理模块构建。
+ ‌emit‌：发射阶段，生成资源文件。
+ ‌done‌：完成阶段，完成编译过程‌。


## webpack 5 类 hook
1. compiler类hook
2. compilation类hook
3. ContextModuleFactory类hook
4. NormalModuleFactory类hook
5. JavascriptParser类hook
[more hook detail](https://www.webpackjs.com/api/compiler-hooks/)


## Hook List
```js
class RemoveCommentsPlugin {
  apply(compiler) {
    console.log('RemoveCommentsPlugin start');

    compiler.hooks.environment.tap('environmentHook', () => {
      console.log('environmentHook');
    });
    compiler.hooks.afterEnvironment.tap('afterEnvironmentHook', () => {
      console.log('afterEnvironmentHook');
    });
    compiler.hooks.entryOption.tap('entryOptionHook', (context, entry) => {
      console.log('entryOptionHook', context, entry);
    });
    compiler.hooks.afterPlugins.tap('afterPluginsHook', (compiler) => {
      console.log('afterPluginsHook');
    });
    compiler.hooks.afterResolvers.tap('afterResolversHook', (compiler) => {
      console.log('afterResolversHook');
    });
    compiler.hooks.initialize.tap('initializeHook', () => {
      console.log('initializeHook');
    });
    compiler.hooks.normalModuleFactory.tap('normalModuleFactoryHook', (normalModuleFactory) => {
      console.log('normalModuleFactoryHook', Object.keys(normalModuleFactory.hooks));
      normalModuleFactory.hooks.parser
        .for('javascript/auto')
        .tap('parserHook', (parser, options) => {
          console.log('parserHook', Object.keys(parser.hooks), options)
          // parser.hooks.someHook.tap(/* ... */);
        });
    });
    compiler.hooks.contextModuleFactory.tap('contextModuleFactoryHook', (contextModuleFactory) => {
      console.log('contextModuleFactoryHook', Object.keys(contextModuleFactory.hooks));
    });
    compiler.hooks.beforeCompile.tap('beforeCompileHook', (compilationParams) => {
      console.log('beforeCompileHook', Object.keys(compilationParams));
    });
    compiler.hooks.compile.tap('compileHook', (compilationParams) => {
      console.log('compileHook', Object.keys(compilationParams));
    });
    compiler.hooks.thisCompilation.tap('thisCompilationHook', (compilation, compilationParams) => {
      console.log('thisCompilationHook', Object.keys(compilationParams));
    });
    compiler.hooks.compilation.tap('compilationHook', (compilation, compilationParams) => {
      console.log('compilationHook', Object.keys(compilationParams));
    });

    compiler.hooks.make.tap('makeHook', (compilation) => {
      console.log('makeHook');
    });
    compiler.hooks.afterCompile.tap('afterCompileHook', (compilation) => {
      console.log('afterCompileHook', Object.keys(compilation.hooks).join());
    });
    compiler.hooks.shouldEmit.tap('shouldEmitHook', (compilation) => {
      console.log('shouldEmitHook');
      // 返回 true 以输出 output 结果，否则返回 false
      return true;
    });
    
    // change output content
    compiler.hooks.emit.tap('RemoveCommentsPlugin', compilation => {
      console.log('emit event touch')
      // compilation 可以理解为本次打包的上下文
      for (const name in compilation.assets) {
        if (name.endsWith('.js')) {
          const fileContent = compilation.assets[name].source();
          const reg = /console.log(.*)/g;
          // const reg = /\/\/[^\\r\\n]*/;
          const noComments = fileContent.replace(reg, '');
          compilation.assets[name] = {
            source: () => noComments,
            size: () => noComments.length,
          }
        }
      }
    })

    compiler.hooks.afterEmit.tap('afterEmitHook', (compilation) => {
      console.log('afterEmitHook');
    });
    compiler.hooks.assetEmitted.tap('assetEmittedHook', (file, info) => {
        const { content, source, outputPath, compilation, targetPath } = info;
        console.log('assetEmittedHook', content); // <Buffer 66 6f 6f 62 61 72>
      }
    );
    compiler.hooks.done.tap('doneHook', (stats) => {
        console.log('doneHook');
      }
    );

    compiler.hooks.additionalPass.tapAsync('additionalPassHook', () => {
        console.log('additionalPassHook');
      }
    );
  }
}

module.exports = RemoveCommentsPlugin;

```
