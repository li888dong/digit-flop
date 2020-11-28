# upgrade

@tiamaes/digital-flop  数字翻牌器


# 安装

npm i @tiamaes/digital-flop

# 使用
```
<template>
    <digital-flop
     v-for="(num,index) in '1234'"
      :key="index"
      :num="num"
      :fontsize="42"
      :width="32"/>
</template>

import digitalFlop from "@tiamaes/digit-flop"
components: { digitalFlop }
```

#属性
|  属性   | 解释  | 数据类型|
|  ----  | ----  |----|
| num  | 单个翻转数字 |字符串|
| fontsize  | 字体大小 |数字|
| width  | 宽 |数字|
| height  | 高 |数字|
| duration  | 动画时长 |数字|
| fontcolor  | 字体颜色 |字符串（#ffffff）|
| numbg  | 背景颜色 |字符串（#ffffff）|
