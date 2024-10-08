---
title: vue3
date: 2022/5/10
categories:
- jsLibrary
---

### Options API 和 Composition API 之间的映射
Vue2 Options-based API | Vue Composition API
-----------------------|---------------------
beforeCreate | setup()
created | setup()
beforeMount | onBeforeMount
mounted | onMounted
beforeUpdate | onBeforeUpdate
updated | onUpdated
beforeDestroy | onBeforeUnmount
destroyed | onUnmounted
errorCaptured | onErrorCaptured

```html
<template>
    <div>
        <p>计数器实例: {{ count }}</p>
        <input @click="myFn" type="button" value="点我加 1">
        <p>count的平方: {{ count }}</p>
    </div>
</template>

<script>
import {ref, onMounted, watch, computed， provide，inject} from 'vue';

export default {
    /**
     * props - 包含父组件传过来的属性 
     * emit - 用于出发自定义事件（及触发父组件绑定在本组件的事件方法）
     */
    setup(props，{ emit, slots, attrs }){
        //定义初始值为0的变量，要使用ref方法赋值，直接赋值的话变量改变不会更新 UI
        let count = ref(0);

        // 定义点击事件 myFn
        function myFn(){
            console.log(count);
            count.value += 1;
        }
       
        // 组件被挂载时，我们用 onMounted 钩子记录一些消息
        onMounted(() => console.log('component mounted!'));

        // 监听
        watch(count, (newValue, oldValue) => {
            console.log('The new count value is: ' + newValue.value)
        })

        // 计算
        let count2 = computed(() => count.value ** 2)

        // 提供property
        // provide(key, value)
        provide('themeColor', '#f00')
        // 其他子孙组件中注入property 
        // inject(key, defaultValue)
        // const themeColor = inject('themeColor', '#fff')


        // 外部使用组合API中定义的变量或方法，在模板中可用。
        return {count,myFn} // 返回的函数与方法的行为相同
    }
}
</script>
```

## 响应式
reactive 响应式实现原理是proxy
ref 当属为基本类型时，使用getter、setter劫持。为引用类型时通过reactive创建响应式

### ref与reactive的不同
1. ref 主要用于包装基础数据类型（如字符串、数字、布尔），当数据是个数组或对象时，该数组将通过 reactive 转为具有深层次响应式。
2. ref 返回一个对象（RefImpl），该对象中 value 属性为数据的值，读取或修改该值时，必须通过该对象的 value 属性，但在模板中使用时，直接调用，不能加 value，vue3已经帮我们处理了
3. reactive 只能包装部分引用类型（如数组、对象），且具有深层次响应式。