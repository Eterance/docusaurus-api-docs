---
sidebar_position: 2
---

# 高级版

返回一张随机图片的 API。功能相较于普通版更为强大，但是上手难度较高，需要有 SQL 基础。

请注意：这里的“高级”是指可以通过构造更复杂的查询语句来选取更加精细、更符合要求的图片随机范围，而不是有更多高级图片——实际上，高级版和普通版的总的图片范围是一样的。

## 基础 URL

https://pictures.myapi.com/pics/rpicpro

在所有的图片中，返回一张随机图片。

## 最佳示例

对于实际使用，请复制转义后的 URL。转义前的 URL 仅用于方便理解其 SQL 语句。

### 电脑端

范围：横向图片且不是低分辨率图片。考虑到横向图片数量相对较少，添加了一个 `or` 条件，使得可以额外返回纵向且宽度大于 1200 像素的图片。

- 转义前：[https://pictures.myapi.com/pics/rpicpro?sql= ( landscape = 1 and small_res = 0 ) or ( landscape = 0 and width > 1200 )](https://pictures.myapi.com/pics/rpicpro?sql=%20%28%20landscape%20=%201%20and%20small_res%20=%200%20%29%20or%20%28%20landscape%20=%200%20and%20width%20%3E%201200%20%29)
- 转义后：https://pictures.myapi.com/pics/rpicpro?sql=%20%28%20landscape%20=%201%20and%20small_res%20=%200%20%29%20or%20%28%20landscape%20=%200%20and%20width%20%3E%201200%20%29

### 手机端

范围：纵向图片、不是低分辨率且大小小于 400KB 图片，因为考虑到手机移动网络可能网速较慢，过大的图片会加载很久。

- 转义前：[https://pictures.myapi.com/pics/rpicpro?sql= ( landscape = 0 and small_res = 0 and size < 400000 )](https://pictures.myapi.com/pics/rpicpro?sql=%20%28%20landscape%20=%200%20and%20small_res%20=%200%20and%20size%20%3C%20400000%20%29)
- 转义后：https://pictures.myapi.com/pics/rpicpro?sql=%20%28%20landscape%20=%200%20and%20small_res%20=%200%20and%20size%20%3C%20400000%20%29

## 转义与还原 URL 中的特殊字符

SQL 中的特殊字符，例如空格、括号等，都需要进行转义，否则会被视为非法输入。

下面的小工具可以转义或者还原 URL 中的特殊字符（开启转义英文圆括号）：

https://tools.eterance.com/zh-cn/url-encode

## 传递 SQL 参数

可以通过在 `sql` 参数中构造 SQL 语句的 where 来筛选图片。

如果你对 SQL 语法不熟悉，请参见：https://www.runoob.com/mysql/mysql-where-clause.html

建议在继续往下看之前，请先查看：[可供查询的数据列](columns)

## 参数语法

下面从一个示例开始：

```
https://pictures.myapi.com/pics/rpicpro?sql= ( landscape = 0 and near_square = 0 ) and ( small_res = 0 and size < 400000 )
```

对应 SQL where：

```sql
where (landscape=0 and near_square=0) and (small_res=0 and size<400000)
```

这个语句的意思是：在所有的图片中，返回一张随机 ACG 图片，但是这张图片不能是横向图片，也不能是近似正方形图片，也不能是低分辨率图片，也不能是小文件图片，且图片大小不能超过 400KB。

我们可以看到，在 URL 中，使用 `?sql=` 传递条件，并且所有的符号和词语都使用空格隔开。

## 允许输入的内容

为了防止 SQL 注入攻击，输入的内容被严格限制。目前，我们允许输入的内容为：

- 允许输入的列名
- 允许输入的运算符：`=`, `<>`, `>`, `<`, `>=`, `<=`
- 允许输入的逻辑运算符：`and`, `or`, `not`，必须是小写
- 英文小括号：`(`, `)`

除此之外，任何其他内容都会被视为非法输入。

## 其他查询参数

### `count`

返回符合条件的图片数量。例如：

```
https://pictures.myapi.com/pics/rpicpro?count&sql= ( landscape = 0 and near_square = 0 ) and ( small_res = 0 and size < 400000 )
```

### `debug`

返回构建的 SQL 语句 where 部分。例如：

```
https://pictures.myapi.com/pics/rpicpro?debug&sql= ( landscape = 0 and near_square = 0 ) and ( small_res = 0 and size < 400000 )
```

当你的提供的 where 条件报错时，可以使用这个参数来查看构建的 SQL 语句是否正确。

