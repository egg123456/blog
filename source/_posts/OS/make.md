---
title: make
date: 2018/5/4
categories:
- OS
---

> 代码变成可执行文件，叫做编译（compile）；先编译这个，还是先编译那个（即编译的安排），叫做构建（build）。
Make是最常用的构建工具，诞生于1977年，主要用于C语言的项目。但是实际上 ，任何只要某个文件有变化，就要重新构建的项目，都可以用Make构建。
总之，make只是一个根据指定的Shell命令进行构建的工具。

### MAKE 规则
+ target 构建的目标
+ prerequisites 前置条件
+ [tab]  <commands> 以 tab 键起首的命令
```makefile
target: prerequisites.txt prerequisites1.txt
  @ echo my name is egg
  @ echo what's yuur name
```

### 内置变量（Implicit Variables）
```makefile
ImplicitVar:
  $(CC) -o output input.c
  # $(CC) 指向当前使用的编译器(用于编译C程序的程序；默认“cc”)
  @ echo $(CC)
  # $(CC) 指向当前使用的编译器(用于编译C++程序的程序；默认“g++”)
  @ echo $(CXX)
  # $(MAKE) 指向当前使用的Make工具
  @ echo $(MAKE)
```

### 自动变量（Automatic Variables）
```makefile
AutomaticVar%: source.txt source1.txt
  @ echo my name is egg
  # $@指代当前目标，就是Make命令当前构建的那个目标。比如，make foo的 $@ 就指代foo。
  @ echo $@
  # $< 指代第一个前置条件。比如，规则为 t: p1 p2，那么$< 就指代p1。
  @ echo $<
  # $? 指代比目标更新的所有前置条件，之间以空格分隔。比如，规则为 t: p1 p2，其中 p2 的时间戳比 t 新，$?就指代p2
  @ echo $?
  # $^ 指代所有前置条件，之间以空格分隔。比如，规则为 t: p1 p2，那么 $^ 就指代 p1 p2 。
  @ echo $^
  # $* 指代匹配符 % 匹配的部分， 比如% 匹配 f1.txt 中的f1 ，$* 就表示 f1。
  @ echo $*
  # $(@D) 和 $(@F) 分别指向 $@ 的目录名和文件名。比如，$@是 src/input.c，那么$(@D) 的值为 src ，$(@F) 的值为 input.c。
  @ echo $(@D) $(@F)
  # $(<D) 和 $(<F) 分别指向 $< 的目录名和文件名。
  @ echo $(<D) $(<F)
```

### 条件判断
```makefile
txt = Hello World
list = one two three
test%:
  @# if else
ifeq ($(txt),Hello World) 
  @ echo $* one
else
  @ echo egg $* egg
endif
  @ echo $(list)
  for i in $(list); do \
    echo $$i 23; \
  done
```

### make 示例
```makefile
# 为了防止目标名与现有文件冲突，显式声明目标为伪文件。
.PHONY: lint
js_files = $(shell find ../ -name 'thi*.js')
lint: $(js_files)
	@ echo $(js_files)
  # js文件语法检查
	jshint $?
  # 编译C文件输入可执行文件output
  $(CC) -o output input.c
```