# CSS 选择器（ 只挑   易忘记的 讲  ）

1. ```js
   （1）id选择器（#myid）
   （2）类选择器（.myclassname）
   （3）标签选择器（div,h1,p）
   （4）后代选择器（h1 p）
   （5）子元素选择器（ul>li）
   （6）兄弟选择器（li~a）
   （7）相邻兄弟选择器（li+a）
   （8）属性选择器（a[rel="external"]）
   （9）伪类选择器（a:hover,li:nth-child）
   （10）伪元素选择器（::before、::after）
   （11）通配符选择器（*）
   ```

2.    子元素选择器： `  (ul > li) ` 

3.    兄弟选择器：  ` （li~a） `  ；  相邻兄弟选择器： ` 相邻兄弟选择器（li+a） `

4. ​    属性选择器： ` a[rel="external"] `

## 伪类选择器

### 静态伪类

1. ` ：link` 			  超链接点击之前    ---  用以超链接（**只有 a 标签有 `href`  属性时才有效**）
2. `：visited`         链接被访问后       ----  用以超链接

### 动态伪类   ----   针对所有标签

1. `：hover`   		“ 悬停 ”：鼠标放到标签上的时候
2. `：active`          “ 激活 ”：鼠标点击标签（点击不松手  时，当然你可以按着不放）    
3. `: focus`            某个标签获得焦点时一般都是原生就可以点击的 标签，如：a  input）

### a 标签的伪类

- ` ：link` 	`：visited`  	`：hover`   	`：active`      `: focus` 
-  `a: focus` :    a  标签使用   table 键 使 a 标签获得焦点，就会生效
- <font color=red> a {  }  设置样式 会默认   a: link    a: visited  的样式</font>

### 根元素      `E: root`  

- **在 `html ` 文档内是  `html ` ，在  `xml` 就应该是  `xml`   **

- ```css
  :root{background-color: red;}
  ```

### 排除选择器         `E: not(s)`

- ```css
  // main.css
  // 
  p:not(.p3){
      background-color:red;
      <!-- 为所有  p  标签 设置样式 ,但是排除 p 标签中含有 .p3 类的 p 标签 --> 
  }
  ```

###  被设为 锚点，且因为锚点而聚焦时

- ```html
  //html
  <a href="#div1" > 指向  div1 </a>
  // #div1 不仅仅是标记元素，也为自身制作了一个锚点（name 属性也可以制作锚点）
  // 使用  a 标签的  href 属性就可以绑定一个锚点
  // 绑定了 锚点，点击之后 就会跳到绑定好的 锚点元素
  <div id="div1">
      这里是  div1
  </div>
  ```

- ```css
  // css
  #div1{
      background-color: green;
  }
  #div1:target{
      background-color: red;
  }
  ```

- **当点击  a  标签时，`#div1` 元素的背景色 就会从  绿色  转换为  红色 **

### 子元素选择

1. #### ` first-child`

   - ```css
     // li 是否在 同级元素中排第一  （同级元素：父元素是同一个）
     // 只要判别   : first-child   前面所选择的元素， 是否  紧跟在父元素下面
     li:first-child{
         background-color:red
     }
     ```

2. #### `last-child`

   - ```css
     // li 是否在 同级元素中排最后  （同级元素：父元素是同一个）
     // 只要判别   : last-child   前面所选择的元素， 是否  紧跟在父元素的 闭合标签 上方
     li:last-child{
         background-color:red
     }
     ```

3. #### `only-child`

   - ```css
     // li 是否 为  父元素下的 唯一一个元素
     li:only-child{
         background-color:red
     }
     ```

4. #### `nth-child(n)`

   -  <font color=red> `CSS` 的索引是从  1  开始的 </font>

   - ```css
     // li 是否为  同级元素中  偶数的 位置
     li:nth-child(2n){
         background-color:red
     }
     ```

   - ```html
     //html
     <div>
         <ul>
             <li> 1 </li>
             <li> 2 </li>	// 背景红色
             <li> 3 </li>
         </ul>
     	<li> 4 </li>      	// 背景红色
     </div>
     ```

5. #### `nth-last-child(n)`

   - **与  `nth-first-child(n)`  大同小异，只不过  nth-last-child(1)   是同等级 最后一个元素开始数起**

6. #### ` first-of-type`       

   - **与    ` first-child`   的区别：**
     -    ` first-child` ： 在   **同级元素 **  中的 排在   第一的位置
     -    ` first-of-type`    ：  在 **同级  且   同种元素**  中排在 第一的位置

   - ```CSS
     // CSS
     //  li  是否 为 同级  同种 元素的第一个位置 （同种： 同一种 标签）
     //  简单的说就是： li  父元素下，  li  元素集中  排在第一的  元素（为这个元素设置样式）
     li:first-of-type{
         background-color:red
     }
     ```

7. #### `last-of-type`   ` only-of-type`   `nth-of-type`  `nth-last-of-type`  且都是在   同级   同种  元素中的位置

### 元素状态选择

1. #### `empty`

   - **自身没有  子元素的   **

   - ```css
     //  CSS
     div:empty{
     	background-color:red;
     }
     ```

   - ```html
     ///html
     <div>	
         123
     </div>
     <div>  
          <!-- 
     		自身元素 没有子元素，所以背景色应该为  红色
     		如果
     		-->
     </div>
     
     ```

     

2. #### `checked`   

   - 一般用以  单选框  复选框的 标签中使用

   - ```css
     input:checked{
         width：200px;
         height:200px;
         transition: width ease-in-out 0.5s 0s;
     }
     ```

3. #### `enabled`               `disbaled`

   - 一般用以  表单 标签中使用

   - ```css
     input:disabled{
             <!--
         	<input type="text" disabled="disabled" />
        	 	-->
        background-color:blue;
     }
     input:enabled{
         <!--
         	没有  disabled ，就会有的样式
         -->
        background-color:red;
     }
     ```

     

4. #### `read-only`

   - ```html
     <input  type="test"  readonly="readonly"  />
     ```

5. #### `read-write`

