---
layout: post
title:  "海鲜意面"
categories: 西餐
tags:  做法
author: Lissa
---

* content
{:toc}

“意面是西餐中比较容易制作，也是中国人在口感上最容易接受的品种。意面的口味有很多，更有些朋友喜欢在家中创造一些混搭风的意面，今天我发的是比较常见的红酱海鲜意面。海鲜只用了家里现有的虾和鱿鱼，本想再去买些蛤蜊，可是实在不喜欢用叉子吃蛤蜊的感觉，干脆也就不难为自己了。红酱是我自己做的，谈不上正宗，却是我很喜欢的味道。”

<div><img src="https://raw.githubusercontent.com/Lissa-321/Lissa-321.github.io/master/9.jpg"></div>




## 食材明细

### 主料
意面
100克
虾
适量
鱿鱼
适量
西兰花
适量
圣女果
250克
洋葱
四分之一个
### 辅料
盐
适量
罗勒
适量
黑胡椒
适量
橄榄油
适量
### 口味
酸甜
### 其他
工艺
### 耗时
三刻钟
### 难度
简单

## 海鲜意面的做法步骤
1西兰花洗净，撕成小朵后焯熟备用。
2虾去皮去虾线备用。
3鱿鱼切丝。
4将洋葱切几刀，同圣女果一同放入料理机打成泥。
5锅内烧水，加入半勺盐，放入意面煮至没有硬心后捞出控水。
6在意面中加入一勺橄榄油拌匀备用。
7锅内放入适量橄榄油，放入虾和鱿鱼翻炒熟后取出。
8不用洗锅，将打好的番茄泥倒入锅中，中小火熬煮。
9番茄汁熬至浓稠后放入适量的盐、罗勒、黑胡椒翻炒均匀。
10将意面和海鲜一同倒入锅中，均匀地裹上酱汁后装盘。

## 代码

获取剩余时间的代码如下：

```js
/**
 * 获取剩余时间
 * @param  {Number} endTime    截止时间
 * @param  {Number} deviceTime 设备时间
 * @param  {Number} serverTime 服务端时间
 * @return {Object}            剩余时间对象
 */
let getRemainTime = (endTime, deviceTime, serverTime) => {
    let t = endTime - Date.parse(new Date()) - serverTime + deviceTime
    let seconds = Math.floor((t / 1000) % 60)
    let minutes = Math.floor((t / 1000 / 60) % 60)
    let hours = Math.floor((t / (1000 * 60 * 60)) % 24)
    let days = Math.floor(t / (1000 * 60 * 60 * 24))
    return {
        'total': t,
        'days': days,
        'hours': hours,
        'minutes': minutes,
        'seconds': seconds
    }
}
```

<del>获取服务器时间可以使用 mtop 接口 `mtop.common.getTimestamp` </del>

然后可以通过下面的方式来使用：

```js
// 获取服务端时间（获取服务端时间代码略）
getServerTime((serverTime) => {

    //设置定时器
    let intervalTimer = setInterval(() => {

        // 得到剩余时间
        let remainTime = getRemainTime(endTime, deviceTime, serverTime)

        // 倒计时到两个小时内
        if (remainTime.total <= 7200000 && remainTime.total > 0) {
            // do something

        //倒计时结束
        } else if (remainTime.total <= 0) {
            clearInterval(intervalTimer);
            // do something
        }
    }, 1000)
})
```

这样的的写法也可以做到准确倒计时，同时也比较简洁。不需要隔段时间再去同步一次服务端时间。

## 补充

在写倒计时的时候遇到了一个坑这里记录一下。

**千万别在倒计时结束的时候请求接口**。会让服务端瞬间 QPS 峰值达到非常高。

![](https://img.alicdn.com/tfs/TB1LBzjOpXXXXcnXpXXXXXXXXXX-154-71.png)

如果在倒计时结束的时候要使用新的数据渲染页面，正确的做法是：

在倒计时结束前的一段时间里，先请求好数据，倒计时结束后，再渲染页面。

关于倒计时，如果你有什么更好的解决方案，欢迎评论交流。
