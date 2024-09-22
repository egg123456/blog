---
title: react-router
date: 2022/5/10
categories:
- jsLibrary
---

> history.js 二次封装了浏览器history api
react-touter 底层使用了 history.js

### history
```js
  var history = {
    // 当前出发action类型 POP、PUSH、REPLACE
    get action() {
      return action;
    },
    // url 信息对象
    get location() {
      return location;
    },
    // 同过 location 获取url
    createHref: createHref,
    // 调用浏览器history.pushState(historyState, '', url); 然后出发监听
    push: push,
    // 调用浏览器history.replaceState(historyState, '', url); 然后出发监听
    replace: replace,
    // 调用浏览器 History.go(delta)
    go: go,
    // 调用浏览器 History.go(-1)
    back: function back() {
      go(-1);
    },
    // 调用浏览器 History.go(1)
    forward: function forward() {
      go(1);
    },
    // 注册监听器，监听url变化
    listen: function listen(listener) {
      return listeners.push(listener);
    },
    // 注册拦截，监听url变化
    block: function block(blocker) {
      var unblock = blockers.push(blocker);

      if (blockers.length === 1) {
        window.addEventListener(BeforeUnloadEventType, promptBeforeUnload);
      }

      return function () {
        unblock(); // Remove the beforeunload listener so the document may
        // still be salvageable in the pagehide event.
        // See https://html.spec.whatwg.org/#unloading-documents

        if (!blockers.length) {
          window.removeEventListener(BeforeUnloadEventType, promptBeforeUnload);
        }
      };
    }
  };
```
