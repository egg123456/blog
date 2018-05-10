---
title: vue
---
# Vue 原理
> 当把一个普通的 JavaScript 对象传给 Vue 实例的 data 选项时，Vue 将遍历此对象所有的属性，并使用 Object.defineProperty 把这些属性全部转为访问器属性（getter/setter）。Object.defineProperty 是 ES5 中一个无法 shim 的特性，这也就是为什么 Vue 不支持 IE8 以及更低版本浏览器的原因。
```js
//Object.defineProperty()接收三个参数：属性所在对象、属性的名字和一个（描述符对象）
var obj = {},
    value=5;
    bind=[];
Object.defineProperty(obj,s,{
    set:function(val){
        bing['s']=val;
    },
    get:function(){
        return bind['s'];
    }
});
obj['s']=value;//触发set方法，间接修改了bind
```

# 基本
```html
<body>
    <div id="app">
    <!-- Mustache语法 (双大括号) -->
        {{ message + seen+1 }}<br>
        <!--v-model双向数据绑定  -->
        <input v-model="message">
        <!--v-bind绑定元素特性  -->
        <span v-bind:title="message">鼠标悬停几秒钟查看此处动态绑定的提示信息！</span>
        <!--v-if条件渲染  -->
        <p v-if="seen">现在你看到我了</p>
        <ol>
        <!--v-for李彪渲染（重复元素不重复内容渲染）  -->
            <li v-for="todo in todos">
                {{ todo.text }}
            </li>
        </ol>
        <!--v-on事件绑定  -->
        <button v-on:click="reverseMessage">逆转消息</button><br>
        <!--双大括号显示的是普通文本内容，v-html显示html代码  -->
        <p>Using mustaches: {{ rawHtml }}</p>
        <p>Using v-html directive: <span v-html="rawHtml"></span></p>
    </div>
</body>
```
```js
var app = new Vue({ 
        el: '#app',
        data: {
            message: 'Hello Vue!',
            seen:true,
            todos: [
                    { text: '学习 JavaScript' },
                    { text: '学习 Vue' },
                    { text: '整个牛项目' }
                ],
                rawHtml:'<span style="color:red;">this should be red</sapn>',
            
        },
        methods: {
                reverseMessage: function () {
                    this.message = this.message.split('').reverse().join('')
                }
            }
    });
```

+ 双大括号会将数据解释为普通文本，而非 HTML 代码。为了输出真正的 HTML，你需要使用 v-html 指令：

+ 双大括号里的表达式会在所属 Vue 实例的数据作用域下作为 JavaScript 被解析，不解析语句

# 计算属性与侦听器
```html
<body>
    <div id="demo">
        <p>侦听器</p>
        <input type="text" v-model="firstName">
        <input type="text" v-model="lastName">
        <input type="text" v-model="fullName">
    </div>
    <div id="demo1">
        <p>计算属性</p>
        <input type="text" v-model="firstName">
        <input type="text" v-model="lastName">
        <input type="text" v-model="fullName">
    </div>
</body>
```
```js
<script>
    var vm = new Vue({
        el: '#demo',
        data: {
            firstName: 'Foo',
            lastName: 'Bar',
            fullName: 'Foo Bar'
        },
        watch: {
            firstName: function (val) {
                this.fullName = val + ' ' + this.lastName
            },
            lastName: function (val) {
                this.fullName = this.firstName + ' ' + val
            }
        }
    });
    var vm1 = new Vue({
            el: '#demo1',
            data: {
                firstName: 'Foo',
                lastName: 'Bar'
            },
            computed: {
                fullName: {
                    // getter
                    get: function () {
                        return this.firstName + ' ' + this.lastName
                    },
                    // setter
                    set: function (newValue) {
                        var names = newValue.split(' ')
                        this.firstName = names[0]
                        this.lastName = names[names.length - 1]
                    }
                }
            }
        })
</script>
```
+ 计算属性：可以向绑定data选项中的属性一样绑定到页面。
    + 计算属性只有在它的相关依赖发生改变时才会重新求值。有缓存

+ 侦听器：侦听数据变化做出响应

+ 计算属性与侦听器可以完成许多相似的功能，
    + 但计算属性的 getter 函数是没有副作用 (side effect) 的，这使它更易于测试和理解。
    + 但使用 watch 选项允许我们执行异步操作 (访问一个 API)，限制我们执行该操作的频率，并在我们得到最终结果前，设置中间状态。这些都是计算属性无法做到的。


# class绑定
```html
<body>
    <div id="demo">
    <!--isActive,hasError的true or false决定active与text-denger类的有无  -->
        <my-component v-bind:class="{ active: isActive,'text-danger': hasError }"></my-component>
        <my-component v-bind:class="classobj"></my-component>
        <!--数组语法，可包含多个类对象  -->
        <my-component v-bind:class="[classobj]"></my-component>
    </div>
</body>
```
```js
    <script>
        Vue.component('my-component', {
            template: '<p class="foo bar">Hello World!</p>'
        })
         var vm = new Vue({
            el: '#demo',
            data: {
                isActive:true,
                hasError:false
            },
            computed:{
                classobj:{
                    get:function(){
                        return {
                             active: !this.isActive,
                            'text-danger': !this.hasError
                        }
                    }
                }
            }
        });
        
</script>
```

# style绑定
```html
<body>
    <div id="demo">
        <!--对象语法  -->
        <!--样式名采用驼峰命名法 例font-size==>fontSize  -->
        <my-component v-bind:style="{color: setcolor, fontSize: setfontSize + 'px' }"></my-component>
        <my-component v-bind:style="classobj"></my-component>
        <!--数组语法  -->
        <my-component v-bind:style="[classobj]"></my-component>
    </div>
</body>
```
```js
<script>
    Vue.component('my-component', {
        template: '<p class="foo bar">Hello World!</p>'
    })
        var vm = new Vue({
        el: '#demo',
        data: {
            setcolor:'greenyellow',
            setfontSize:100,
        },
        computed:{
            classobj:{
                get:function(){
                    return {
                        fontSize: this.setfontSize+'px',
                        color: this.setcolor,
                        
                    }
                }
            }
        }
    })
</script>
```

# component
## global-component
```html
<body>
    <div id="demo">
        <!--动态组件 绑定post  监听自定义事件 组件附加内容egg -->
        <blog-post v-bind：is=" currentcomponent"  v-on:enlarge-text="postFontSize += 0.1" v-for="post in posts" v-bind:key="post.id" v-bind:post="post">yeg</blog-post>
    </div>
</body>
```
```js

    Vue.component('blog-post', {
            props: ['post'],    //通过 Prop 向子组件传递数据
            template: `
                <div class="blog-post">
                <h3>{{ post.title }}</h3>
                <button v-on:click="$emit('enlarge-text')">
                    Enlarge text
                </button>
                <div v-html="post.content"></div>
                <slot></slot>
                </div>
            `
        })
    var vm = new Vue({
            el: '#demo',
            data: {
                posts: [
                    { id: 1, title: 'My journey with Vue',content:'egg' },
                    { id: 2, title: 'Blogging with Vue',content:'egg' },
                    { id: 3, title: 'Why Vue is so fun',content:'egg' },
                ]
            }
        });
```
+ 全局注册的组件可以用在其被注册之后的任何 (通过 new Vue) 新创建的 Vue 根实例，也包括其组件树中的所有子组件的模板中。

+ Vue 实例提供了一个自定义事件的系统来解决这个问题。我们可以调用内建的 $emit 方法并传入事件的名字，来向父级组件触发一个事件：

+ slot插槽：组件中加内容的地方

+ is特性：值为要显示的组件名，实现类选项卡

## 局部注册组件
```js
var ComponentA = {template:"<h1>我是局部组件A</h1>"};
var ComponentB = {template:"<h1>我是局部组件B</h1>"};
new Vue({
  el: '#app'
  components: {
    'component-a': ComponentA,
    'component-b': ComponentB，
    'component-c':{//C可用组件A方式
        components: {
            'component-a': ComponentA
        },
    }
})
```
+ 对于 components 选项中的每个属性来说，其属性名就是自定义元素的名字，其属性值就是这个组件的选项对象

+ 局部注册的组件在其子组件中不可用（A不能用B）


# 过渡
过渡的类名
在进入/离开的过渡中，会有 6 个 class 切换。

v-enter：定义进入过渡的开始状态。在元素被插入之前生效，在元素被插入之后的下一帧移除。

v-enter-active：定义进入过渡生效时的状态。在整个进入过渡的阶段中应用，在元素被插入之前生效，在过渡/动画完成之后移除。这个类可以被用来定义进入过渡的过程时间，延迟和曲线函数。

v-enter-to: 2.1.8版及以上 定义进入过渡的结束状态。在元素被插入之后下一帧生效 (与此同时 v-enter 被移除)，在过渡/动画完成之后移除。

v-leave: 定义离开过渡的开始状态。在离开过渡被触发时立刻生效，下一帧被移除。

v-leave-active：定义离开过渡生效时的状态。在整个离开过渡的阶段中应用，在离开过渡被触发时立刻生效，在过渡/动画完成之后移除。这个类可以被用来定义离开过渡的过程时间，延迟和曲线函数。

v-leave-to: 2.1.8版及以上 定义离开过渡的结束状态。在离开过渡被触发之后下一帧生效 (与此同时 v-leave 被删除)，在过渡/动画完成之后移除。