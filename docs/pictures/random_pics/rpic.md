---
sidebar_position: 1
---

# 普通版

返回一张随机图片的 API。功能选择较为有限，但是上手简单。

## 基础 URL

https://pictures.myapi.com/pics/rpic

在所有的图片中，返回一张随机图片。

## 最佳示例

### 电脑端

横向、非低分辨率且非 bjn 的图片：

https://pictures.myapi.com/pics/rpic?landscape=1&small_res=0&nobjn

### 手机端

纵向、非低分辨率、不是大文件且非 bjn 的图片：

https://pictures.myapi.com/pics/rpic?landscape=0&small_res=0&big_size=0&nobjn

## 参数格式

在 URL 查询字符串中，参数格式为 `<参数名>=<1或者0>`；多个参数之间使用 `&` 连接。

当指定多个参数时，它们的关系是“和，并且”（即 SQL 中的 `AND`）。

## 查询参数

### `landscape`

如果不提供该参数，那么默认两种图片都有，也就是sql语句中不会有该条件。

- 1: 横向图片
- 非1: 纵向图片

### `near_square`

如果不提供该参数，那么默认两种图片都有，也就是sql语句中不会有该条件。

- 1: 近方形图片，即宽高比在 0.909 ~ 1.1 之间的图片
- 非1: 非近方形图片，即宽高比不在 0.909 ~ 1.1 之间的图片

### `big_size`, `mid_size`, `small_size`

如果不提供该参数，那么默认三种图片都有，也就是sql语句中不会有该条件。

哪一项为1，就会查询出该尺寸的图片；哪一项为非1，就不会查询出该尺寸的图片。

### `big_res`, `mid_res`, `small_res`

如果不提供该参数，那么默认三种图片都有，也就是sql语句中不会有该条件。

哪一项为1，就会查询出该分辨率的图片；哪一项为非1，就不会查询出该分辨率的图片。

### `nobjn`

如果不提供该参数，那么默认两种图片都有，也就是sql语句中不会有该条件。否则，将过滤掉 bjn 图片。

bjn (比基尼) 图片是指有些性吸引力，但是主要用于突出艺术气息的图片，包括但不限于泳装等。若对此类图片有所顾虑，可以使用该参数。