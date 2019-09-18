---
title: echarts
date: 2018/5/10
categories:
- js library
---
> 组件化，认清组件，找所配

# 常用配置
```js
// 标题
title{
    show:true,  
    text:"{title|行业总览 | }{b|用户多头占比三天}",    //主标题文本
    textStyle:{
        color:'#333',
        fontSize:'18',
        rich: {
            title:{
                fontWeight: "bolder",
            },
            b:{
                // fontWeight: "lighter"
            }
        }
        
    },
    textAlign:'[auto,left,right,center]',
    textVerticalAlign:'[auto,top,middle,bottom]',
    subtext: '' ,   // 副标题文本 ，同样有很多同样设置
}
// 图例
legend{         
    type: '[plain,scroll]',     
    show: true,
    left: 'num',       // 图例组件离容器左侧的距离
    orient: '[horizontal,vertical]',  //各图例水平与垂直排列
    itemGap: 'num',     // 图例每项之间的间隔
    selected: {
        系列1：true     // 默认为true都选择显示
    },
    data: [{
        name: '系列1',
        // 强制设置图形为圆。
        icon: 'circle',    //'emptyCircle', 'circle', 'rect', 'roundRect', 'triangle', 'diamond', 'pin', 'arrow', 'none'
        // 设置文本为红色
        textStyle: {
            color: 'red'
        }
    }{
        name: '系列2',
        // 强制设置图形为圆。
        icon: 'circle',
        // 设置文本为红色
        textStyle: {
            color: 'red'
        }
    }],  //系列1,2就是图裂的文字内容
}
//网格
grid: [{
    left: '51px',
    right: '84px',
    top: '30px',
    bottom: '30px',
    height: '64px'
}],
// x 轴
xAxis{          
    show: true,
    gridIndex: 0,   //选择第几个网格
    type: '[
        value,   //数值轴，适用于连续数据
        category, // 类目轴，适用于离散的类目数据，为该类型时必须通过 data 设置类目数据
        time,  // 时间轴，适用于连续的时序数据，与数值轴相比时间轴带有时间的格式化，在刻度计算上也有所不同，例如会根据跨度的范围来决定使用月，星期，日还是小时范围的刻度。
        log  //对数轴。适用于对数数据。
        ]',
    name: 'name', //坐标轴名
    nameLocation: '[end,middle,start]',
    nameTextStyle: {
        color: red,
        ....
    },
    nameGap: 15,  //坐标轴名称与轴线之间的距离
    nameRotate: 'num',  //坐标轴名字旋转，角度值
    data: [{    //类目数据，在类目轴（type: 'category'）中有效。
        value: '周一',     //单个类目名称。
        // 突出周一
        textStyle: {        //类目标签的文字样式...
            fontSize: 20,
            color: 'red'
        }
    }, '周二', '周三', '周四', '周五', '周六', '周日'],
    axisLine: {             //坐标轴轴线相关设置。
        lineStyle: {
            color: "#cecece",
            width: 1,
            type: 'solid|dashed|dotted'
            opacity: 0.6
        }
    },
    axisLabel: {
        color: "#a5a5a5",
        formatter: function (value, index) {return '...';}      //参数分别为刻度数值（类目），刻度的索引
        align: 'left|center|right',     //文字水平对齐方式
        verticalAlign: 'top|middle|bottom'      //文字垂直对齐方式
    }
}
//原生图形元素组件
graphic:[{      
    type: circle,   //image, text, circle, sector, ring, polygon, polyline, rect, line, bezierCurve, arc, group,
    left: 10,
    shape: {
        cy: y,
        r: a
    },
    style: {
        fill: "#c5c5c5",        //填充色
        stroke: "#5c5c5c",      //笔画色 
        lineWidth: 1            //笔画宽度
    }
},{
    type: "text",
    style: {
        text: "文本内容",
        x: a + c / 2 - 10,
        y: y,
        fill: "#ffffff",
        stroke: "#898989"
    }
}],
series: [
    {
        silent: false;             //是否响应和触发鼠标事件
        type: '[line,bar....]',    //图表类型
        name: 'name',               //系列名称
        barWidth: 12                //柱子的宽度
        itemStyle: {                // 系列显示颜色。。。
            normal: {               // 一般
                color: "red"        // 系列显示颜色
                },
            emphasis: {          // 鼠标放上时   
                borderColor: "#919191"  
            }
        },
        data: [                 //需要显示的数据 （可由dataset 设置）
            // 维度X   维度Y   其他维度 ...
            [  3.4,    4.5,   15,   43],
            [  4.2,    2.3,   20,   91],
            [  10.8,   9.5,   30,   18],
            [  7.2,    8.8,   18,   57]
        ],
        animationType: 'expansion',         // 默认研圆弧展开的效果
        animation: true,                    // 默认开启动画
        animationDuration: 1000,            // 初始动画时长
        animationEasing: 'cubicOut',        // 初始动画的缓动效果
        animationDelay: 0,                  // 初始动画的延迟
        animationDurationUpdate: 300,       // 数据更新动画时长
        animationEasingUpdate: 'cubicOut',  // 数据跟新缓动效果
        animationDelayUpdate: 0,            // 数据更新动画延迟  
    }
]
//数据集
dataset:{
    dimensions：,      //使用 dimensions 定义 series.data 或者 dataset.source 的每个维度的信息。
    source：[
        ['product', '2015', '2016', '2017'],
        ['Matcha Latte', 43.3, 85.8, 93.7],
        ['Milk Tea', 83.1, 73.4, 55.1],
        ['Cheese Cocoa', 86.4, 65.2, 82.5],
        ['Walnut Brownie', 72.4, 53.9, 39.1]
    ]
    // 注意：如果使用了 dataset，那么可以在 dataset.source 的第一行/列中给出 dimension 名称。于是就不用在这里指定 dimension。但是，如果在这里指定了 dimensions，那么 ECharts 不再会自动从 dataset.source 的第一行/列中获取维度信息。
}
// 提示框
toolTip:{     
    show: true
    trigger: '[         // 触发类型
        item,           // 数据项图形触发，主要在散点图，饼图等无类目轴的图表中使用
        axis,           // 坐标轴触发，主要在柱状图，折线图等会使用类目轴的图表中使用
        none            // 什么都不触发
        ]',
    axisPointer: {            // 坐标轴指示器，坐标轴触发有效
        type : 'shadow'        // 默认为直线，可选为：'line' | 'shadow'
    },
    formatter: function(params){return ''} //提示框的内容
}
```



# 提示框 params
```js
params={
    componentType: 'series',
    // 系列类型
    seriesType: string,
    // 系列在传入的 option.series 中的 index
    seriesIndex: number,
    // 系列名称
    seriesName: string,
    // 数据名，类目名
    name: string,
    // 数据在传入的 data 数组中的 index
    dataIndex: number,
    // 传入的原始数据项
    data: Object,
    // 传入的数据值
    value: number|Array,
    // 数据图形的颜色
    color: string,

    // 饼图的百分比
    percent: number,
}
// 在多系列图表中 params 为多个上诉 params 组成的数组

// value和data 中拥有所有（选中）系列 x轴值 和 所有系列的 y轴值 (实例推测)
data = {
    '0' : ’3-24‘， // x轴值
    '1' : 35,      // 系列1 的值
    '2' : 60       // 系列2 的值
}
value = ['3-24',35,60]

```

# 调色盘颜色列表
['#c23531','#2f4554', '#61a0a8', '#d48265', '#91c7ae','#749f83',  '#ca8622', '#bda29a','#6e7074', '#546570', '#c4ccd3']
调色盘颜色列表。如果系列没有设置颜色，则会依次循环从该列表中取颜色作为系列颜色。


[echarts渐变色实现方法](https://www.cnblogs.com/liuwei54/p/9962182.html)
[GEOJSON标准格式](https://www.jianshu.com/p/852d7ad081b3)
[世界国家及中国各省市级地图ArcGIS MXD/SHP/QGIS/JSON/SQL数据文件](https://blog.csdn.net/taiyang1987912/article/details/82796693)