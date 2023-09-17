---
sidebar_position: 3
---

# 高级版 - 初见

返回一张随机图片的 API。功能相较于普通版更为强大，但是上手难度较高，需要有 SQL 基础。

请注意：这里的“高级”是指可以通过构造更复杂的查询语句来选取更加精细、更符合要求的图片随机范围，而不是有更多高级图片——实际上，高级版和普通版的总的图片范围是一样的。

## 基础 URL

https://pictures.myapi.com/pics/rpicpro

在 `pixiv` 和 `imas` 图片集中，返回一张随机图片。

## 最佳示例

对于实际使用，请复制转义后的 URL。转义前的 URL 仅用于方便理解其 SQL 语句。

### 电脑端

范围：在 `pixiv` 和 `imas` 图片集中，横向图片且不是低分辨率图片。

- 转义前：[https://pictures.myapi.com/pics/rpicpro?pixiv= ( landscape = 1 and small_res = 0 )&imas](https://pictures.myapi.com/pics/rpicpro?pixiv=%20%28%20landscape%20=%201%20and%20small_res%20=%200%20%29&imas)
- 转义后：https://pictures.myapi.com/pics/rpicpro?pixiv=%20%28%20landscape%20=%201%20and%20small_res%20=%200%20%29&imas

### 手机端

范围：在 `pixiv` 图片集中，纵向图片、不是低分辨率且大小小于 400KB 图片，因为考虑到手机移动网络可能网速较慢，过大的图片会加载很久。

- 转义前：[https://pictures.myapi.com/pics/rpicpro?pixiv= ( landscape = 0 and small_res = 0 and size < 400000 )](https://pictures.myapi.com/pics/rpicpro?pixiv=%20%28%20landscape%20=%200%20and%20small_res%20=%200%20and%20size%20%3C%20400000%20%29)
- 转义后：https://pictures.myapi.com/pics/rpicpro?pixiv=%20%28%20landscape%20=%200%20and%20small_res%20=%200%20and%20size%20%3C%20400000%20%29

### 风景图

范围：在 `scenery` 图片集中，随机返回一张。

https://pictures.myapi.com/pics/rpicpro?scenery