# 	CSS 媒体查询

## 1. 根据设备的不同

1. **screen**  (默认值：计算机屏幕  )

2. **其他设备**

   1. tty    		电传打字机 等
   2. print         打印预览模式 / 打印页
   3. ......

3. **all**

4. **示例**

   ```html
   // 针对设备的不同进行的筛选
   <style media="screen">
   	//  当是 屏幕设备时会应用到的样式
       .box{ background-color: #f00 }
   </style>
   ```

## 2. 根据媒体属性进行筛选

- **媒体属性是 CSS3 新增的内容**

- **有如下常用属性：**

  - min- ：表示符合条件的最小值
  - max- ：表示符合条件的最大值

  1. `width|min-width|max-width`

  2. `height|min-height|max-height`

  3. `device-width|min-device-width|max-device-width`

  4. `device-height|min-device-height|max-device-height`

  5. `aspect-ratio|min-aspect-ratio|max-aspect-ratio`

     - 输出设备的 目标显示区域的 宽高比

     - ```html
       <style>
           @media (min-aspect-ratio: 1/1){
               // 表示目标显示区域的  宽高比 应该大于 1
               // 即 区域是正方形  或者 区域的 宽 大于 高
               .box{background-color: #00f 
               }
           }
       </style>
       ```

  6. `device-aspect-ratio|min-device-aspect-ratio|max-device-aspect-ratio`

     - 设备的 宽高比

  7. `orientation`  设备方向：landscape ( 横屏 )  和  portrait ( 竖屏 )

  8. `resolution`  分辨率： 每英寸像素的点数

  9. ..... 

- **媒体属性的使用**

  - 使用 **screen**  时，必须使用  **only** 

    - ```html
<style>
          @media screen and (max-width: 1200px){
          
          }
    </style>
      //  上述 媒体查询，在老式浏览器中会忽略  后面的 逻辑表达式，所以没有针对筛选就去赋予了样式。
      <style>
          @media only screen and (max-width: 1200px){
              
          }
      </style>
      // 加上  only ，老式浏览器 会把 only 识别为一种设备，而因为没有 only 这个设备名称，而不会去应用样式
      ```
      
    - **总结：在筛选 screen 时，必须加上 `only` 。除非 只是针对 屏幕设备（screen)  进行筛选，没有其他的逻辑表达式。 **
    
  - 符合条件的前提下，后者  覆盖 前者
  
  - 对于  min-   和  max-  的使用

  - ```html
    <style>
        // min-  使用的注意事项
        <!--
        	min-  使用注意事项
        	1. 必须大的值放在最前面
        	2. 后者会覆盖前者
        -->
        @media only screen and (min-width: 1200px){
            
        }
        @media only screen and (min-width:	960px) and (max-width:1199px) {
            
        }
        @media only screen and (min-width: 768px) and (max-width: 959px) {
            
        }
    </style>
  ```
  
  - ```html
    <style>
        // max-  使用的注意事项
        <!--
        	max-  使用注意事项
        	1. 必须大的值放在最前面
        -->
        @media only screen and (max-width: 1200px){
            
        }
    
        @media only screen and (min-width:	960px) and (max-width:1199px) {
            
        }
    	 @media only screen and (max-width: 768px)  {
            
        }
    </style>
    ```
  
- **额外拓展  （ 1 英寸 == 2.54厘米 ） **

  - **屏幕尺寸：屏幕对角线的长度**
  - **分辨率 （ 屏幕上的像素点的多少 ） **
    - 1920px * 1080px  ：高  1920 个像素 ， 宽 1080 个像素
  - **分辨率比  （ 高 宽 像素点  的比，也是屏幕尺寸比 ）**
    - 1920 * 1080 ，16:9 ；16:9 就是分辨率比（ 高 比 宽 ）
  - **屏幕像素密度  （ 每英寸屏幕所拥有的像素数量，PPI ）**
    - 一个对角线 长度为 1 英寸的 正方形内所拥有的像素数量
  - <img src="\01.jpg" style="zoom:25%;" />
    - X：屏幕像素长度
    - Y：屏幕像素宽度
  - **屏幕的清晰度取决于  屏幕像素密度**
  - 我们会看到大多数的屏幕都是 1920 * 1080，但是屏幕的尺寸却不同。说明：在不同大小的屏幕里，像素的大小可以不同。**PPI 就是说明的这个，每英寸的像素数量。**
  - 对于电脑的分辨率的调整，只是 系统提供 相应的 宽 高 像素个数，其他多余的像素个数由系统自行决定。往往分辨率的调整 只会往小了 调整。