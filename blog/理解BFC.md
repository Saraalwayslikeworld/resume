### BFC是什么
- BFC 即为block formatting context，块级格式化上下文。格式化上下文（formatting context）决定子元素的定位，以及和其他元素的关系和相互作用。块级元素是那些被视觉上展现为块的元素，比如 display 默认为 block、list-item、table的元素。只包含块级元素的块容器即为BFC。
### BFC的创建
1. 根元素；
2. float属性不为none；
3. position为absolute或fixed；
4. display为inline-block, flex, 或者inline-flex；
5. overflow不为visible；
### BFC的作用
1. 由于BFC内的元素不与外部元素相互作用，因此可解决margin合并的问题。
2. 由于BFC的区域不会与float box重叠，因此可达到清除浮动的效果。
如：
```
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>JS Bin</title>
  <style>
    .box1{
        float:right;}
    .container{
      overflow:hidden;
      background:pink;}
</style>
</head>
<body>
<div class="container">
<div class="box1">box1</div>
</div>
</body>
</html>
```