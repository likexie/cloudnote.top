#
## 1.超出文本显示省略号
```html

.overstep {
    <!--超出隐藏-->
    overflow: hidden;
    <!--不换行-->
    white-space: nowrap;
    <!--超出部分使用省略号-->
    text-overflow: ellipsis;
}
```
## 2. 指定行数换行省略

```html

.overstep_line_4 {
    display: block;
    overflow: hidden;
    text-overflow: ellipsis;
    /* 作为弹性伸缩盒子模型显示 */
    display: -webkit-box;
    /* 设置伸缩盒子的子元素排列方式--从上到下垂直排列 */
    -webkit-box-orient: vertical;
    /* 显示的行 */
    -webkit-line-clamp: 4;
}
```
# 实例
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<style>
    
.overstep {
    overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
  }
  
.overstep_line_4 {
    display: block;
    overflow: hidden;
    text-overflow: ellipsis;
    /* 作为弹性伸缩盒子模型显示 */
    display: -webkit-box;
    /* 设置伸缩盒子的子元素排列方式--从上到下垂直排列 */
    -webkit-box-orient: vertical;
    /* 显示的行 */
    -webkit-line-clamp: 4;
  }
  .overstep_line_2 {
    display: block;
    overflow: hidden;
    text-overflow: ellipsis;
    /* 作为弹性伸缩盒子模型显示 */
    display: -webkit-box;
    /* 设置伸缩盒子的子元素排列方式--从上到下垂直排列 */
    -webkit-box-orient: vertical;
    /* 显示的行 */
    -webkit-line-clamp: 2;
  }
  div{
      width: 100px;
      border: solid 1px red;
  }
</style>
<body>
    <!-- 1行显示省略号 -->
    <h2>显示省略号：overstep</h2>
    <div class="overstep">
        1行显示省略号1行显示省略号1行显示省略号1行显示省略号
    </div>

    <!-- 2行显示省略号 -->
    <h2>换2行省略号：overstep_line_2</h2>
    <div class="overstep_line_2">
        2行显示省略号2行显示省略号2行显示省略号2行显示省略号2行显示省略号
    </div>

    <!-- 4行显示省略号 -->
    <h2>换4行省略号：overstep_line_4</h2>
    <div class="overstep_line_4">
        4行显示省略号 4行显示省略号 4行显示省略号 4行显示省略号 4行显示省略号
    </div>
</body>
</html>

```
![图片](I:\chrome_down\zabbix.png)