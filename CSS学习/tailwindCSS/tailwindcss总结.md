- spacing: width height margin padding

- variant( 变量 ) ：

  ```js
  // tailwind.config.js
  module.exports = {
       variants: {
          accessibility: ['responsive', 'focus-within', 'focus'],
          alignContent: ['responsive'],
          backgroundColor: ['responsive', 'dark', 'group-hover', 'focus-within', 'hover', 'focus','required'],
       }
  }
  // variants
  // 如上述的 backgroundColor 对应的数组中
  // 数组中元素表示：哪些属性可以 以 XX:backgroundColor 的形式 定义样式
  // hover:bg-red-300 ( 表示：鼠标悬浮在改元素时，该元素的背景颜色变为 淡红色 )
  // 
  ```

  