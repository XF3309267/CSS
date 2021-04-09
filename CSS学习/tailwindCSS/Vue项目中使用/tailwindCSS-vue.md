# 在 Vue 项目中使用  tailwindCSS 

## 1. 在 Vue 项目中 配置  tailwindCSS

1. 安装 tailwindcss 及其 依赖

   - `npm install -D tailwindcss@latest  postcss@latest  autoprefixer@latest`

2. 建立 postcss.config.js 文件  和  tailwindcss.config.js

   - `npx tailwindcss init -p`    

   - 使用  `npx tailwindcss init --full` (  完成 tailwind.config.js 基础配置 )

   - tailwindcss.config.js      用以设置 样式的基本单位

     - ```js
       module.exports = {
           // 在 purge数组中 设置需要使用到  tailwindcss 的文件
           // 以便 在 tree-shake 中去除没有使用过的 样式
           purge:['./index.html','./src/**/*.{vue,js,ts,jsx,tsx}']
       }
       ```

       

   - postcss.config.js            用以 配置 tailwindcss 、autoprefixer  等其他插件

3. 在 vue项目中 引入 tailwindcss 

   1. 建立一个 css 文件

      - ```css
        @tailwind base;
        @tailwind components;
        @tailwind utilities;
        ```

   2. 将上述的 css 文件，在 main.js 中引入

      - ```js
        //  main.js
        // 如果上述的 css 文件路径为：'@/assets/css/index.css'
        import '@/assets/css/index.css'
        ```

## 2. 使用 tailwindcss

### 1. 响应式布局

1. <table style="text-align:center"> 
       <thead>
       	<tr>  
               <th> 断点前缀 </th> 
               <th> 最小宽度 </th> 
               <th> 适用的媒体查询 </th>
           <tr/> 
       </thead>
       <tbody>
       	<tr>
               <td> sm </td>
               <td> 640px </td>
               <td>  @media(min-width: 640px){}  </td>
           </tr>
           <tr>
               <td> md </td>
               <td> 768px </td>
               <td>  @media(min-width: 768px){}  </td>
           </tr>
           <tr>
               <td> lg </td>
               <td> 1024px </td>
               <td>  @media(min-width: 1024px){}  </td>
           </tr>
           <tr>
               <td> xl </td>
               <td> 1280px </td>
               <td>  @media(min-width: 1280px){}  </td>
           </tr>
           <tr>
               <td> 2xl </td>
               <td> 1536px </td>
               <td>  @media(min-width: 1536px){}  </td>
           </tr>
       </tbody>

2. 根据设备屏幕宽度设置样式

   - ```html
     <div class="md:w-56">
         当 设备视宽 大于等于 768px 时，屏幕宽度为  56em
     </div>
     ```

3. 响应式布局

   - ```html
     <div class="text-center sm:text-left ">
         当屏幕大于等于 640px 时，文字居左
         小于 640px ，文字居中
     </div>
     
     ```

   - 编写响应式布局原则

     - 先设定所有断点都适用的 样式，后 在经过 tailwind 断点进行 样式覆盖

### 2. 伪类等修改 元素样式

1. hover   active  focus 等元素 如何修改元素样式

   - ```js
     // tailwind.config.js
     
     // variants: 变体（可变的属性）
     
     // >>>>>>>>>>>>>>>>>>>>>>>>>>>>
     // 对于属性配置变体之前，必须在 tailwind.config.js 的 variantOrder 中 有所添加
     //	
     
     variants:{	// 配置可变的属性
         // backgroundColor 属性可变，且在满足 数组中的状态
         //	responsive: 响应符合断点的时候
         //	dark:		暗黑主题的时候
         //	hover:		鼠标悬浮的时候
         //	focus:		被聚焦的时候（一般是表单元素）
         backgroundColor:['responsive','dark','hover','focus']
     }
     ```

2.  有哪些  属性可以去修改  元素的样式

   1. CSS 中的 伪类 

      - hover  
   
      - focus  （ 鼠标聚焦的时候 ）

      - active  （ 鼠标点击的时候的 ）

      - disabled ( 表单元素不可用的状态下 )

      - visited    ( 超链接被点击过的样式 )

      - checked ( 表单元素：单选框 复选框 被选中的情况下 )
   
      - 子元素
   
        - first:  当自己是 父元素下的 第一个子元素时
   
        - **且不包括 文本节点 **
   
        - ```html
          <div>
              //  会将整体元素 以 元素中心点为元素，顺时针方向 旋转 45度
              123
              // 123 不是父元素的第一个子元素
              <button class="transform first:rotate-45" >
                  123
              </button>
              <button>
                  456
              </button>
          </div>
          
          // 因为 123 是父元素的第一个子元素，所以 button 不会旋转
          <div>
              <span> 123 </span>
           // 123 会将整体元素 以 元素中心点为元素，顺时针方向 旋转 45度
              <button class="transform first:rotate-45" >
                  123
              </button>
              <button>
                  456
              </button>
          </div>
          
          
          ```
   
        - last   最后一个子元素
   
        - odd   在相同父元素的情况下，父元素下序列为 奇数 的子元素
   
        - even  在相同父元素的情况下，父元素下序列为 偶数 的子元素  
   
   2. tailwindcss 特有的
   
      - group
   
        - 当鼠标 悬停一个 元素，要求其 子元素发生样式改变
   
          ```html
          <div class="group" >
              // p 元素
              // 字体样式：颜色 黑色
              // 当鼠标悬停在 div.group 元素，且为该元素的父元素的时候，字体样式：颜色 红色
              <p class="text-black-600 group-hover:text-red-200" >
                  
              </p>
          </div>
          <div>
              // group-focus 只能用于 父元素是 表单元素的
              // 因为 focus 只能用于表单元素
              <button class="group" >
                  <svg class="text-white group-focus:text-blue-200">
                  </svg>
              </button>
          </div>
          
          
          // tailwind.config.js
          module.exports = {
          	variants:{
          		textColor:['responsive','group-hover']
          	}
   }
          ```
      
   3. motion-safe
   
      - 如果用户 在系统上启用了 "motion-reduce"( 减少动画 )时，应该应用的样式
   
      - ```html
        
        <div class="text-blue-200 motion-safe:text-red-200" >
            
        </div>
        
        // tailwind.config.js
        
        module.export = {
        	....
        	// 因为 variantOrder 中 初始化配置中没有 motion变体
        	//	所以 在 variantOrder 中添加，然后在 variants 中配置
        	variantOrder:[
        		...
        		'motion-safe',
        		'motion-reduce'
        	],
        	variants:{
        		textColor:['motion-safe','motion-reduce']
        	}
        }
        
        ```
   
        
   
   4. motion-reduce
   
      - 如果用户在系统上**未**启用 “motion-reduce” （ 减少动画 ），应该应用的样式
   
      - ```html
        
        <div class="text-blue-200 motion-safe:text-red-200" >
            
        </div>
        ```
   
      - **默认没有打开  ``motion-reduce **
   
   5. focus-within
   
      - 当子元素有  表单元素，且被 聚焦的时候，该元素样式的变化
   
      - ```html
        <div class="text-blue-200 focus-within:text-red-200">
            <input class="text-blue-200 focus: text-red-200" />
        </div>
        // 注意： variantOrder 中是否有添加
        // 注意： variants 中是否有配置
        ```
   
   6. <span style="color:red;font-weight:bold" >focus-visible  ( 有待探索 )  </span>
   
   7. **多重筛选**
   
      ```html
      <button class="hover:bg-green-500 sm:hover:bg-blue-500">
          btn
      </button>
      ```
   
   8.  **生成自定义实用程序的变体**      **不懂  ？？？？？？？？？？？？？？？？？**
   
      - https://tailwindcss.com/docs/hover-focus-and-other-states
   
      - ```js
        /* Input: */
        @variants group-hover, hover, focus {
          .banana {
            color: yellow;
          }
        }
        
        /* Output: */
        .banana {
          color: yellow;
        }
        .group:hover .group-hover\:banana {
          color: yellow;
        }
        .hover\:banana:hover {
          color: yellow;
        }
        .focus\:banana:focus {
          color: yellow;
        }
        ```
   
   9. 创建自定义变体
   
      - tailwind.config.js 中 variantOrder 属性中的可选值是定死的（  即  variantOrder  中只能选择内部已经定义好的，而并非只是一个名字 ）。 **variants 中的可 填的变体名称，有两种，一：是 variantOrder 中的值，二：创建好的自定义变量名，但这个名字必须是  dom 元素所有的，不然 自定义的变体永远排不上用场  **
   
      - ```js
        // tailwind.config.js
        const plugin = require('tailwindcss/plugin')
        
        module.exports = {
          plugins: [
            plugin(function({ addVariant, e }) {
              addVariant('required', ({ modifySelectors, separator }) => {
                modifySelectors(({ className }) => {
                  return `.${e(`required${separator}${className}`)}:required`
                })
              })
            })
          ]
        }
        ```
   
   
   ### 3. 黑暗模式
   
   - 黑暗模式有两种
   
     ```js
     // tailwind.config.js
     module.exports = {
        // 1. darkMode:'class'
         	class 模式：父元素的 class 中有 'dark' 值，子元素才能使用暗模式
        // 2. darkMode:'media'
         	media 模式：在任何地方都可以使用 暗模式，但是 暗模式 的 class 是否生效，取决		  于系统。 
     }
     ```
   
   - 如何使用暗模式
   
     1. `darkMode:'class' `  （ tailwind.config.js ）
   
        ```html
        <div class="dark">
            <div class="bg-blue-400 dark:bg-black-40">
                <span class="text-black  dark:text-white-600"></span>
            </div>
        </div>
        ```
   
     2. `darkMode:'media' `  （ tailwind.config.js ）**？？？？？？？？？？**
   
        ```html
        // 前提是 用户的操作系统中 启用了暗模式
        <div>
            <div class="bg-blue-400 dark:bg-black-40">
                <span class="text-black  dark:text-white-600"></span>
            </div>	
        </div>
        // window.matchMedia('(prefers-color-scheme: dark)').matches 可以检测是否开启了 暗模式
        // 关于如何 打开系统的  暗模式，有待 研究
        // ？？？？？？？？？？？？？？？？？？？？？？？？？
        ```
   
     3. 暗模式 与 其他变体 组合筛选
   
        ```html
        <div>
            <div class="bg-blue-400 md:dark:bg-gray-400 lg:dark:bg-black-400  ">
                <span class="text-black  dark:text-white-600"></span>
            </div>
        </div>
        ```
   
     4. 暗模式 前提下 修改  其他 class，必须在 class 的变体列表中 加入 'dark' ( 暗模式 )
   
        ```js
        // tailwind.config.js
        module.exports = {
          // ...
          variants: { 
            extend: {
              textOpacity: ['dark']
            }
          }
        }
        ```

### 4.  设置 标签默认样式

- 定义标签默认样式

  ```css
  @tailwind base;
  @tailwind components;
  @tailwind utilities;
  // 在修改默认样式时，建议 只是去 引用 tailwindcss 基类样式 
  // 即 只使用 @apply  和 theme() ,这两个建立自己的样式
  //	而不是 自行写样式
  
  @layer base {
    h1 {
      @apply text-2xl;
    }
    h2 {
      @apply text-xl;
    }
  }
  ```

- 定义字体

  ```CSS
  @layer base{
      @font-face{
          font-family: Proxima Nova;
          font-weight: 400;
          src: url(/fonts/proxima-nova/400-regular.woff) format("woff");
      }
  }
  ```

- tailwind.config.js  批量 定义默认样式 

  ```js
  // tailwind.config.js
  // 因为 tailwind.config.js 中定义了 tailwindcss 基本样式
  // 所以 如果需要在 其他项目中共享样式
  // 将 默认样式 写在 tailwind.config.js 是个不错的选择
  const plugin = require('tailwindcss/plugin')
  
  module.exports = {
    plugins: [
        plugin(function({addBase,theme}){
            addBase({
                'h1':{fontSize:theme('fontSize.2xl')},
                'h2':{fontSize:theme('fontSize.xl')}
            })
        })
    ]
  }
  ```

### 5.  自定义 样式

-  组件内部的  style 中 定义样式

  ```html
  <button class="btn-indigo">
    Click me
  </button>
  <style>
    .btn-indigo {
      @apply py-2 px-4 bg-indigo-500 text-white font-semibold rounded-lg shadow-md hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-indigo-400 focus:ring-opacity-75;
    }
  </style>
  ```

- 公共样式

  ```js
  // tailwind  建议，当给组件 设定样式时，如下设置
  // tailwind.config.js
  @tailwind base;
  @tailwind components;
  @tailwind utilities;
  
  @layer components {
      .btn-blue{
          @apply py-2 px-4
      }
  }
  ```

- 将自定样式 写在 `tailwind.congif.js`  中

  ```js
  // tailwind.config.js
  // 如果其他项目中 需要共享 该样式，建议将 公共样式 写在 tailwind.config.js 中
  module.exports = {
      plugin:[
          plugin(function({addComponent,theme}){
              const button = {
                  '.btn':{
                      padding:`${theme('spacing-2')}   ${theme('spacing.4')} `
                  }
              }
          })
      ]
  }
  ```

  

