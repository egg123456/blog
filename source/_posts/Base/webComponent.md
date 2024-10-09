---
title: Web Component
date: 2018/5/2
categories: 
- base
---
> Web Component 是一套不同的技术，允许你创建可重用的定制元素（它们的功能封装在你的代码之外）并且在你的 web 应用中使用它们。

## core
custom element: 自定义元素，如自定义一个叫 egg 的元素
Shadow DOM: 影子 DOM（Shadow DOM）允许你将一个 DOM 树附加到一个元素上，并且使该树的内部对于在页面中运行的 JavaScript 和 CSS 是隐藏的。
template and slot: 模版 和 插槽


### custom element
```js
// 为这个元素创建类
class MyCustomElement extends HTMLElement {
  static observedAttributes = ["color", "size"];

  constructor() {
    // 必须首先调用 super 方法
    super();
  }

  connectedCallback() {
    console.log("自定义元素添加至页面。");
  }

  disconnectedCallback() {
    console.log("自定义元素从页面中移除。");
  }

  adoptedCallback() {
    console.log("自定义元素移动至新页面。");
  }

  attributeChangedCallback(name, oldValue, newValue) {
    console.log(`属性 ${name} 已变更。`);
  }
}

// 注册自定义元素，my-custom-element是它的名称，使用时 <my-custom-element />
customElements.define("my-custom-element", MyCustomElement);
```


### shadow dom
```js
// 获取页面元素
const host = document.querySelector("#host");
// 拿到元素的shadow
const shadow = host.attachShadow({ mode: "open" });
// 创建span元素
const span = document.createElement("span");
span.textContent = "I'm in the shadow DOM";
// 将span 加入到 shadow 中
shadow.appendChild(span);
```


### template + customElement + shadowDom
```js
<body>
  <user-card
    image="https://semantic-ui.com/images/avatar2/large/kristy.png"
    name="User Name"
    email="yourmail@some-email.com"
  >
    <span slot="slotA">I am slotA</span>
  </user-card>
  <template id="userCardTemplate">
    <style>
      /* <template>样式里面的:host伪类，指代自定义元素本身。 */
      :host { 
        display: flex;
        align-items: center;
        width: 450px;
        height: 180px;
        background-color: #d4d4d4;
        border: 1px solid #d5d5d5;
        box-shadow: 1px 1px 5px rgba(0, 0, 0, 0.1);
        border-radius: 3px;
        overflow: hidden;
        padding: 10px;
        box-sizing: border-box;
        font-family: 'Poppins', sans-serif;
      }
      .image {
        flex: 0 0 auto;
        width: 160px;
        height: 160px;
        vertical-align: middle;
        border-radius: 5px;
      }
      .container {
        box-sizing: border-box;
        padding: 20px;
        height: 160px;
      }
      .container > .name {
        font-size: 20px;
        font-weight: 600;
        line-height: 1;
        margin: 0;
        margin-bottom: 5px;
      }
      .container > .email {
        font-size: 12px;
        opacity: 0.75;
        line-height: 1;
        margin: 0;
        margin-bottom: 15px;
      }
      .container > .button {
        padding: 10px 25px;
        font-size: 12px;
        border-radius: 5px;
        text-transform: uppercase;
      }
    </style>

    <img class="image">
    <div class="container">
      <p class="name"></p>
      <p class="email"></p>
      <button class="button">Follow John</button>
      <slot name="slotA">defaultA</slot>
      <slot name="slotB">defaultB</slot>
    </div>
  </template>
  
  <script>
    class UserCard extends HTMLElement {
      constructor() {
        super();
        var shadow = this.attachShadow( { mode: 'closed' } );

        var templateElem = document.getElementById('userCardTemplate');
        // clone 模版
        var content = templateElem.content.cloneNode(true);
        // 对模版内的元素赋值
        content.querySelector('img').setAttribute('src', this.getAttribute('image'));
        content.querySelector('.container>.name').innerText = this.getAttribute('name');
        content.querySelector('.container>.email').innerText = this.getAttribute('email');

        shadow.appendChild(content); // 组件内部元素不可被外部访问
        // this.appendChild(content); // 组件内部元素可被外部访问

        // 给组件内的元素添加事件处理
        this.$button = shadow.querySelector('button');
        this.$button.addEventListener('click', (e) => {
          // console.log(t, e, 'hello')
          alert('i am a inner button');
          e.stopPropagation();
        });

        // 给组件本身添加事件处理
        this.addEventListener('click', () => {
          alert('I am a web component')
        })
      }
    }
    // 将 user-card 元素与 UserCard 绑定
    window.customElements.define('user-card', UserCard);
  </script>
</body>
```


