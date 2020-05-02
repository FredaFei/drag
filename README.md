### 拖动

### 效果预览
+ 单个拖动
  + [top](https://fredafei.github.io/drag/src/drag-scope-result.html)
  + [translate](https://fredafei.github.io/drag/src/drag-scope-translate-result.html)
+ 多个多动
  + [top](https://fredafei.github.io/drag/src/drag-scope-multiple.html)
  + [translate](https://fredafei.github.io/drag/src/drag-scope-translate-multiple.html)

#### 交互场景：
+ 鼠标点击被拖拽的元素
+ 鼠标按住不放，移动被拖拽的元素
+ 鼠标松开，被拖拽的元素停留在该松开位置

#### 实现思路：
+ 鼠标点击被拖拽的元素。绑定 `mousedown`事件
  + 设置当前拖拽状态为 true
  + 记录当前鼠标坐标
  + 记录当前被拖拽元素坐标
+ 鼠标按住不放，移动被拖拽的元素。document绑定 `mousemove`事件
  + 记录当前鼠标坐标
  + 若当前拖拽状态为true，元素的位移（坐标）= 当前鼠标坐标 - 初始鼠标坐标 + 被拖拽元素坐标（开始拖拽时初始坐标）
+ 鼠标松开，被拖拽的元素停留在该松开位置。document绑定 `mouseup`事件
  + 设置当前拖拽状态为 false

#### 注意事项：
+ 被拖拽元素的`postion`属性须设置为`relative`/`absolute`
+ 鼠标坐标获取方式 `event.clientX/event.clientY`

[drag-simple](https://github.com/FredaFei/drag/blob/master/src/drag-simple.html)

以上实现上拖拽没问题，但拖拽范围过大。

#### 如何实现在指定的区域（父元素区域）内拖动？

  + 获取拖拽元素和它的父元素宽高，父与子宽高两两相减，其结果为最大位移
  + 若当前拖拽状态为true，真实元素的位移（坐标）= 当前鼠标坐标 - 初始鼠标坐标 + 被拖拽元素坐标（开始拖拽时初始坐标）
  + 最终位移 = Math.min(最大位移坐标, Math.max( 0, 真实元素的位移（坐标）)) + 'px'

[drag-scope](https://github.com/FredaFei/drag/blob/master/src/drag-scope.html)

总结以上功能，封装开箱即用。[drag-scope-result](https://github.com/FredaFei/drag/blob/master/src/drag-scope-result.html)

#### 以上拖动均采用`top/left`，有没有动画性能更好的实现。
使用`translate`替代`top/left`

[drag-scope-translate](https://github.com/FredaFei/drag/blob/master/src/drag-scope-translate.html)
总结以上功能，封装开箱即用。[drag-scope-translate-result](https://github.com/FredaFei/drag/blob/master/src/drag-scope-translate-result.html)

#### 若需要实现多个元素拖动
思路：每次鼠标按下时，利用this更新当前操作元素

总结以上功能，封装开箱即用。

+ top [drag-scope-multiple](https://github.com/FredaFei/drag/blob/master/src/drag-scope-multiple.html)
+ translate [drag-scope-translate-multiple](https://github.com/FredaFei/drag/blob/master/src/drag-scope-translate-multiple.html)





