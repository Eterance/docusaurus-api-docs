---
sidebar_position: 4
---

# 高级版 - 教程

下面将会详细讲解怎么构造 URL 来精细选定图片范围。

## 转义与还原 URL 中的特殊字符

SQL 中的特殊字符，例如空格、括号等，都需要进行转义，否则会被视为非法输入。

下面的小工具可以转义或者还原 URL 中的特殊字符（开启转义英文圆括号）：

https://tools.eterance.com/zh-cn/url-encode

## 结构

简单来说，就是通过构造 SQL 语句的 where 条件来筛选图片。如果你对 SQL 语法不熟悉，请参见：https://www.runoob.com/mysql/mysql-where-clause.html

URL 构造的格式为：

```text
https://pictures.myapi.com/pics/rpicpro?<表名1>=<SQL WHERE1>&<表名2>=<SQL WHERE2>&...
```

从URL `https://pictures.myapi.com/pics/rpicpro` 之后，以 `?` 开始。如果需要多个表（图片集），那么使用 `&` 连接。

## 参数语法

下面从一个示例开始：

```url
https://pictures.myapi.com/pics/rpicpro?pixiv= ( landscape = 0 and near_square = 0 ) and ( small_res = 0 and size < 400000 )
```

对应 SQL：

```sql
select `url` from `pixiv` where ( `landscape` = 0 and `near_square` = 0 ) and ( `small_res` = 0 and `size` < 400000 )
```

这个语句的意思是：在 `pixiv` 所有的图片中，返回一张随机图片，但是这张图片不能是横向图片，也不能是近似正方形图片，也不能是低分辨率图片，也不能是小文件图片，且图片大小不能超过 400KB。

我们可以看到：

- 只需要写表名和 where 条件，不需要写 `select` 、 `from` 和被选择的列。
- where 条件里的所有单词、运算符、括号都需要用空格隔开。没有空格的会被视为一个单词。
- 所有的列名和表名都会自动添加反引号 " ` "。

如果指定了表名但是没有任何 where 条件指定，比如：

```url
https://pictures.myapi.com/pics/rpicpro?pixiv
```

那么会返回这个表中的所有图片。

## 允许输入的内容

为了防止 SQL 注入攻击，where 条件输入的内容被严格限制。目前，允许输入的内容为：

- 允许输入的列名吗，参见：[可供查询的数据列](columns)
- 允许输入的运算符：`=`, `<>`, `>`, `<`, `>=`, `<=`
- 允许输入的逻辑运算符：`and`, `or`, `not`，必须是小写
- 英文小括号：`(`, `)`

除此之外，任何其他内容都会被视为非法输入。

## 其他查询参数

### `all`

当指定了 `all` 参数时，会在所有的图片集中搜索，并使用在 `all` 参数中指定的 where 条件。例如：

```text
https://pictures.myapi.com/pics/rpicpro?all= landscape = 1
```

将会返回所有图片集中的所有横向图片。

如果既指定了 `all` 参数，又指定了其他图片集，那么在其他图片集中指定的 where 条件会覆盖 `all` 参数中的 where 条件。例如：

```text

https://pictures.myapi.com/pics/rpicpro?all= landscape = 1&pixiv= landscape = 0
```

将会返回 `pixiv` 图片集中的所有纵向图片 + 所有其他图片集中的所有横向图片。也就是说，尽管 `all` 参数中指定了 `landscape = 1`，但是在 `pixiv` 图片集中，`pixiv` 的 where 条件会覆盖 `all` 参数中的 where 条件。

### `count`

返回符合条件的图片数量。例如：

```text
https://pictures.myapi.com/pics/rpicpro?count&pixiv= ( landscape = 0 and near_square = 0 ) and ( small_res = 0 and size < 400000 )
```

### `debug`

返回构建的 SQL 语句。例如：

```text
https://pictures.myapi.com/pics/rpicpro?debug&pixiv= ( landscape = 0 and near_square = 0 ) and ( small_res = 0 and size < 400000 )
```

当你的提供的 where 条件报错时，可以使用这个参数来查看构建的 SQL 语句是否正确。
