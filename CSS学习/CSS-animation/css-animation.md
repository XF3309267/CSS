# CSS-animation

`animation: name duration timing-function delay iteration-count direction fill-mode`

- **name: 动画名称**

  - ```html
    <style>
        // animationName 就是动画的名字
        // @keyframes name{ }  建立动画
        @keyframes animationName{
            to{
                background-color: #f00
            }
        }
        .div{
            // 使用动画
            animation: animationName 2s linear
        }
    </style>
    ```

- **duration: 动画持续时间**

- **timing-funcion: 动画速度曲线**

  - linear

  - ease-in

  - ease-out

  - ease-in-out

  - cubic-bezie(n,n,n,n)   (**有待研究**)

  - steps( stepNum, arg  )  ( 逐帧 动画 )

    - stepNum： 将动画平均分为 几帧

      - **注意：**

        1. ```html
           <style>
               // steps(4,jump-none)
               // 分两种情况：（ 是否用上  % ）
               //	1. 建立动画时，用上了  % 
               //		首先看  使用了 % 将动画分成了 几个过程
               		（ 下面 将代码分成了 3 个过程： 0 - 25 - 50 - 100  ）
               		又因为 steps(4,jump-none),又将 这 3 个过程 均分为 4 步
               		所以 一共  12 步
               //	2. 没有使用  %
               		首先看将 动画分成了几步
               		在没有使用 % 的情况下，只有两个状态 初始状态  和 最终状态
               		而此时 steps(4,jump-none) 将这个过程 均分为 4 步
               .div{
           		anmation: naimatiaonName 2s steps(4,jump-none) infinte;
               }
               @keyframes animationName{
                   20%{
                       background-color:#f00;
                   }
                   50%{
                       background-color:#0f0;
                   }
                   100%{
                       background-color:#00f;
                   }
               }
           </style>
           ```

           

    - arg: jump-start ,  jump-end,   jump-none,  jump-both

      - **jump-start**   跳过 每个过程 的初始状态  （ 初始帧 ）
      - **jump-end**     跳过 每个过程 的最终状态   （  ）
      - **jump-both**    跳过 每个过程 的  初始  和 最终 状态
      - **jump-none**   每个过程 初始状态  和 最终状态都不跳过

    - **注意：**

      - 当 **steps 的 第二个参数的  值  的不同，stepNum 的含义也不同**
      - **stepNum**  ： 除了 跳过的那些帧，动画分为了几帧

    

- **delay: 动画开始的延迟 ( 秒数 或 毫秒数 ) **

- **iteration-count: 动画播放的次数**

-  **direction**

  - normal: 正常播放
  - alternate: 动画轮流反向播放

- **fill-mode**

  - none
  - forwards ( 动画完成后保存最后一个状态 )
    - 最后一个状态：是动画停止的时候的最后一个状态
    - **特例： 当 `direction: alternate`  , iteraiton-count  为 偶数，最后一个状态 就是 初始状态**
  - backwards （ 在 delay 属性有值的情况下，动画开始之前，应用 动画的开始状态  ）
    - ( 在 delay 属性有值的情况下，backwards 属性值才会有效 )
  - both:  forwards  + backwards 