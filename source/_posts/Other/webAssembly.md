---
title: webAssembly
date: 2018/5/3
categories:
- Other
---

> WebAssembly是一种可以在现代Web浏览器中运行的新型代码类型 - 它是一种具有紧凑型二进制格式的低级汇编语言，具有近乎本地性能，并提供C/C ++，C＃和Rust等语言使用汇编目标，以便它们可以在网络上运行。它还旨在与JavaScript一起运行，使两者都可以一起工作。

### install Sdk
```bash
# Get the emsdk repo
git clone https://github.com/emscripten-core/emsdk.git

# Enter that directory
cd emsdk

# Download and install the latest SDK tools.
./emsdk install latest

# Make the "latest" SDK "active" for the current user. (writes .emscripten file)
./emsdk activate latest

# Activate PATH and other environment variables in the current terminal
source ./emsdk_env.sh

# check install
emcc -v

```
tips: 错误解决 https://www.jianshu.com/p/d6b268634e46
