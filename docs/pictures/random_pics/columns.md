---
sidebar_position: 100
---

# 可供查询的数据列

## `size`

类型：`INT`

图片的大小，单位为字节。

## `width`, `height`

类型：`INT`

图片的宽度和高度，单位为像素。

## `ratio`

类型：`DECIMAL(10, 7)`

图片的宽高比。计算方式为 `width / height`。

## `landscape`

类型：`BOOLEAN`

图片是否为横向图片。如果其宽 > 高，则为横向图片，此时 `landscape` 取值为 1；否则为纵向图片，`landscape` 取值为 0。

## `ua`

该项没有值。

当检测到条件中有 `ua` 时，将会根据请求的 `User-Agent` 来判断是否为移动端，如果是移动端，则 `ua` 会被 `landscape = 0` 替换，否则 `ua` 会被 `landscape = 1` 替换。

使用 `ua` 可以实现自动识别移动端和 PC 端。

## `near_square`

类型：`BOOLEAN`

图片是否为近似正方形图片。如果其宽高比在 0.90909 (10/11) 到 1.1 (11/10)  之间，则为近似正方形图片，此时 `near_square` 取值为 1；否则为非近似正方形图片，`near_square` 取值为 0。

## `big_size`, `small_size`, `mid_size`

类型：`BOOLEAN`

- 大文件图片：图片大小大于 600KB ( `size` > 600000 )，此时 `big_size` 取值为 1；否则为 0。
- 小文件图片：图片大小小于 100KB ( `size` < 100000 )，此时 `small_size` 取值为 1；否则为 0。
- 中等文件图片：均不属于前面两种，此时 `mid_size` 取值为 1；否则为 0。

## `big_res`, `small_res`, `mid_res`

类型：`BOOLEAN`

- 高分辨率图片：图片短边大于 1440 像素，此时 `big_res` 取值为 1；否则为 0。
- 低分辨率图片：图片短边小于 640 像素，此时 `small_res` 取值为 1；否则为 0。
- 中等分辨率图片：均不属于前面两种，此时 `mid_res` 取值为 1；否则为 0。

## `bjn`

类型：`BOOLEAN`

bjn 图片是指衣着有些暴露的图片，包括但不限于泳装等。如果图片属于这个类别，那么 `bjn` 取值为 1；否则为 0。

如果对图片的要求较高，可以使用 `bjn = 0` 来过滤掉 bjn 图片。不允许使用 `bjn = 1` 来单独获取 bjn 图片。
