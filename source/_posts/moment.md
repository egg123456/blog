---
title: moment
date: 2018/5/10
categories:
- js-library
---
> 一个非常实用的日期工具类moment.js

# get start
```js
import 'moment/locale/zh-cn'
moment.locale('zh-cn');   
```

# Alone-function
Alone-function|decription
--------|----------
moment()|当前日期和时间
moment().minute(10)|修改当前的分钟数为10
moment().weekday(0)|获取或设置星期一（参考区域设置）
moment().dayOfYear(32)|获取或设置一年中的第32天
moment().daysInMonth()|获取当月的天数（无参）
moment().weeksInYear()|获取当年的周数（无参）
moment().isoWeek(Number)|获取或设置当前是第几周

tips: 以上 function 不带参数均无需 format 输出，它们类似于moment().get('year')等与moment().set('year',2090)的结合体

# 追溯
moment().add(7, 'days')|七天后
moment().subtract(7, 'days')|七天前

# startOf and endOf
moment().startOf('year')|将年以下的设为初始时刻 即 1月1日00:00
moment().startOf('hour')|将小时以下的设为结束时刻 即 xx:59


# 时差
moment([2007, 0, 29]).fromNow()|2007年1月29日相对于当前时刻的时间差 ‘12年前’
end.from(start)|start 于 end 的时差

b.diff(a) | 毫秒级时差

# 检查
moment('2010-10-20').isBefore('2010-10-21'); // true
moment('2010-10-20').isSame('2010-10-20'); // true
moment('2010-10-20').isAfter('2010-10-19'); // true
moment('2010-10-20').isBetween('2010-10-19', '2010-10-25'); // true

moment([2000]).isLeapYear() // true
moment.isMoment(moment()) // true
moment.isDate(new Date()); // true

moment([2011, 2, 12]).isDST(); // false, March 12 2011 is not DST
moment([2011, 2, 14]).isDST(); // true, March 14 2011 is DST

# timestamp and date
moment().valueOf();     //1556333607736
moment(1556333607736).format('YYYY-MM-DD HH:mm:ss');  //"2019-04-27 10:53:27"
