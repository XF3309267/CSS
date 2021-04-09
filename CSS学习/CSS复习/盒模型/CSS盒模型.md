# CSS 盒模型（w3c 盒模型  、  IE 盒模型 ）

- **盒模型由四部分组成：margin    border    padding    content**

1. **W3C 盒模型 ===  box-sizing: content-box**
   - 给 元素 设置的 宽高，只为  content 提供，padding  border 会另外生成 “ 面积 ”
2. **IE  盒模型 === box-sizing:  border-box**
   - 给元素设置的宽高，还会被  padding  border  占取
3. **两者  盒模型的  区别**
   1. **在元素 固定  宽高的情况下，w3C 盒模型还有机会 增加 宽高，而  IE 盒模型没有机会增加元素宽高。 **
   2. **<font color=blue> 自我感觉，IE 盒模型更好，毕竟一旦给 元素设置宽高，就不会有意料之外的事情发生（比如 元素的宽高 超出预料）；但是  IE 盒模型 就必须 事先计算好  padding border 会占据的  宽高大小，以便  content 能够如期 渲染。 </font>**