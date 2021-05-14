---
title: dva
date: 2018/5/10
categories:
- jsLibrary
---

> dva 首先是一个基于 redux 和 redux-saga 的数据流方案，然后为了简化开发体验，dva 还额外内置了 react-router 和 fetch，所以也可以理解为一个轻量级的应用框架。[Official documents](https://dvajs.com/)

### use

#### model
```js
import {eggApply} from '../services';

export default {
  namespace: 'apply',

  state: {
    count: 1,
    list: [],
  },

  effects: {
    * submit({payload}, effects) {    //effects: {call, put, select}
      // const count = yield select((state)=>state.apply ) // 测试输出state
      console.log(payload, effects);
      let abc = yield effects.call(eggApply);
      console.log(333, abc);
      yield effects.put({
        type: 'list',
        payload: abc,
      });
    },
  },

  reducers: {
    addApply(state, action) {   // 此state 指当前model的state 即全局state.apply
      return {
        count: state.count + action.payload,
      };
    },
    list(state, action) {
      return {
        ...state,
        list: action.payload.list,
      };
    },
  },

  //subscriptions 监听路由变化，鼠标，键盘变化，服务器连接变化，状态变化等，这样在其中就可以根据不同的变化做出相应的处理
  subscriptions: {
    setup({ dispatch, history }) {  
      // 这里的方法名可以随便命名，当监听有变化的时候就会依次执行这的变化,这里的dispatch和history和之前说的是一样的
      window.onresize = () => {   
        //这里表示的当浏览器的页面的大小变化时就会触发里面的dispatch方法，这里的save就是reducers中的方法名
        dispatch (type:"save")  
      }
    },
};

```

#### view
```js
import React, { Component } from 'react';
import { Table, Input } from 'doraemon';
import { connect } from 'dva';

const dataSource = [{
  key: '1',
  name: '胡彦斌',
  age: 32,
  address: '西湖区湖底公园1号',
}, {
  key: '2',
  name: '胡彦祖',
  age: 42,
  address: '西湖区湖底公园1号',
}];

const columns = [{
  title: '姓名',
  dataIndex: 'name',
  key: 'name',
}, {
  title: '年龄',
  dataIndex: 'age',
  key: 'age',
}, {
  title: '住址',
  dataIndex: 'address',
  key: 'address',
}];

@connect(({ apply }) => ({
  apply,
}))
export default class extends Component {
  click = (e) => {
    console.log(this.props);
    this.props.dispatch({
      type: 'apply/addApply',
      payload: 90,
    });
    this.props.dispatch({
      type: 'apply/submit',
      payload: 123,
    });
  }
  render() {
    return (
      <div>
        <Table rowKey={item => item.id} dataSource={this.props.apply.list} columns={columns} />
        <Input onChange={this.click} value={this.props.apply.count} />
      </div>
    );
  }
}
```

### 