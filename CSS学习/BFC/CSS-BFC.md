# CSS   BFC

### 1.  什么叫   BFC

- 格式化上下文
- web页面中盒模型布局的 CSS 渲染模式
- 一个独立的渲染区域

### 2.  形成  BFC 的条件

- float 的值不为 none
- position 的值为 absolute 或  fixed
-  overflow  的值不为  visible
- display 的值为：inline-block、inline-flex、flex、table-cell、table-caption

### 3. BFC   的特性

- 浮动元素的高度会算入其中（即  浮动元素会 撑开 父级元素）
- 

