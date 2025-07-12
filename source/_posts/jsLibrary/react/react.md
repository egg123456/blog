---
title: react
date: 2022/5/10
categories:
- jsLibrary
---

### react组件扽渲染流程
1. 执行组件的render方法
2. 执行render方法里的React.createElement方法创建虚拟DOM，从而得到虚拟DOM树
3. 根据虚拟DOM树在界面上生成真实DOM

### react组件的更新流程
1. 组件的props/state发生改变
2. render方法重新执行
3. 利用React.createElement方法重新生成新虚拟DOM树
4. 新旧虚拟DOM树通过“diff 算法”进行比较
5. 每发现一个不同就生成一个mutation去记录这个不同
6. 根据mutation更新真实DOM

### DIFF 算法
+ 只会同层比较
+ 默认在同层比较时，只会进行同位置比较
  + 在比较的是相同类型元素时，就只记录变化
  + 在比较的是不同类型元素时，就直接使用新的元素即新元素的子孙元素（即直接从这个元素开始的分支）

## setState
setState 是异步的，不会立即更新状态。React 会在合适的时机将多次setState调用组合成一次更新，及以**浅合并**的方式合并出最终的state后触发一次组件更新，从而提高性能。
```js
  // 下面逻辑执行后，只触发一次更新，state结果为多次set合并后的值 
  // { num：3， name：2, obj: { id: 1 }, arr: ['egg'] }
  handleClick = () => {
    this.setState({ num: 2 }, () => {
      console.log('one', this.state);
    })
    this.setState({ num: 3, name: 1 }, () => {
      console.log('two', this.state);
    })
    this.setState({ name: 2, obj: { name: 'egg' }, arr: [1,2,3] }, () => {
      console.log('three', this.state);
    })
    this.setState({ obj: { id: 1 }, arr: ['egg'] }, () => {
      console.log('four', this.state);
    })
  }
```
setState 回调函数是更新完成后在依次执行，即状态更新并渲染完成之后。及当使用多setState并都传入回调函数时，在状态更新并渲染完成后，依次调用回调函数


## hooks
1. useRef和useState的区别
+ useState‌：用于在组件中存储状态，当状态更新时，组件会重新渲染。它接受一个参数作为初始状态，返回当前状态和一个更新状态的函数。
+ ‌useRef‌：用于在组件的整个生命周期内存储一个可变的引用，这个引用不会触发组件的重新渲染。它返回一个可变的 ref 对象，其 .current 属性可以被自由地修改，但这种修改不会导致组件重新渲染。
tips：主要区别在于useRef的改变不会导致组件重新渲染

2. useState and useReducer
+ 适用场景
  - useState‌：适用于管理简单的、独立的状态。当你的状态管理逻辑较为简单，或者只需要管理单个状态时，useState是一个不错的选择。例如，管理一个计数器的值‌12。
  - useReducer‌：适用于管理复杂的状态逻辑，特别是当状态更新涉及多个相关状态或复杂的逻辑时。useReducer通过一个reducer函数来管理状态的更新，这个函数接收当前状态和动作(action)，并返回新的状态‌12。

+ 底层实现
  - useState‌：在底层实现上，useState可以视为使用了一个简单的reducer函数（称为basicStateReducer）来管理状态。在mount阶段和update阶段，useState内部调用了这个reducer函数‌4。
  - useReducer‌：useReducer直接使用提供的reducer函数来管理状态。这使得它更适合处理复杂的逻辑和多个相关的状态更新‌4。

tips1: 当set函数传入的更新值==原值时，不触发组件更新
tips2: 直接修改state值不会触发组件更新，但state值是修改成功的


## React中super()和super(props)的区别
不传props时，组件props不会被挂在 this 上，但react内部
```js
// react 内部
const instance = new YourComponent(props);
instance.props = props;
```
所以实际的区别只有在构造函数执行期间使用 this.props 为 undefined
```js
class YourComponent extends React.Component {
  construct(props) {
    super(); // 不传props
    console.log(props); // {...}
    console.log(this.props); // undefined
  }
}
```

```js
mountDom = {
  __reactContainer: root.current,
  _reactListening: true, // 已添加事件监听标记
}

// ReactDOMRoot
const root = {
  // FiberRootNode
  internalRoot: {
    containerInfo: mountDom,
    // rootFiber
    current: {
      memoizedState: {
        element: initialChildren,
        isDehydrated: hydrate,
        cache: null,
        // not enabled yet
        transitions: null,
        pendingSuspenseBoundaries: null
      },
      updateQueue: {
        baseState: fiber.memoizedState,
        firstBaseUpdate: null,
        lastBaseUpdate: null,
        shared: {
          pending: null,
          interleaved: null,
          lanes: NoLanes
        },
        effects: null
      },
    }
  }
}
```

### ReactElement
```json
{
  "$$typeof": "Symbol(react.element)",
  "key": "99",
  "ref": null,
  "props": {
    "id": 1,
    "children": "ReactElement"
  },
  "_owner": null,
  "_store": { "validated": false }
}

```

### update
{
    eventTime: eventTime,
    lane: lane,
    tag: UpdateState,
    payload: <App />,
    callback: null,
    next: null
}

### callstack
```js
ReactDomRoot.proprotype.render = function render(children) {
  updateContainer(children, fiberRoot, null, null) {
    scheduleUpdateOnFiber(fiberRoot, rootFiber, lane, eventTime) {
      ensureRootIsScheduled(fiberRoot, eventTime) {
         root.callbackNode = scheduleCallback$1(schedulerPriorityLevel, performConcurrentWorkOnRoot.bind(null, fiberRoot))
      }
    }
  }
}

function performConcurrentWorkOnRoot(fiberRoot, didTimeout) {
  renderRootSync(root, lanes) {
    workLoopSync() {
      while (workInProgress !== null) {
        performUnitOfWork(workInProgress) {
          next = beginWork$1(current, unitOfWork, subtreeRenderLanes);
          if (next === null) {
            // If this doesn't spawn new work, complete the current work.
            completeUnitOfWork(unitOfWork);
          } else {
            workInProgress = next;
          }
        }
      }
    }
  }
  finishConcurrentRender(fiberRoot, exitStatus = 5, lanes = 4) {
    commitRoot(fiberRoot, null, null) {
      commitRootImpl(fiberRoot, null, null, 0)
    }
  }
}
```

众所周知，React为了保证一帧内有足够的时间渲染ui，使用了requestIdleCallback这个API。但实际上，由于requestIdleCallback工作帧率低，只有20FPS，还有兼容问题，React并没有使用它，而是用requestAnimationFrame和MessageChannel进行polyfill。


