# ios-checkbox

[在线地址](https://ices1.github.io/demo/ios-checkbox-o/index.html)
![图片](https://github.com/ices1/demo/ios-checkbox-o/1.gif)

### What
  纯CSS制作一个 ios 的样式 checkbox

### Which
  伪元素 `::after` ,阴影 `box-shadow` 

### How
  1. `input`与样式展现元素`label` 进行绑定联动
  2. 在`label`中分为两部分，`ios-checkbox` 底框 + 圆形滑扭

### Step
  1. 首先写出 html 部分

  ```html
    <section>
      <input class="ios-checkbox" type="checkbox" name="" id="ios-checkbox">
      <label class="ios-checkbox" for="ios-checkbox"></label>
    </section>
  ```
  2. 部分css展示，调出圆角的checkbox 底框，以及圆形滑扭

  ```css
      label.ios-checkbox{       /*圆角的checkbox 底框*/
        display: inline-block;
        width: 60px;
        height: 30px;
        padding: 2px;
        background: #ddd;
        border-radius: 999px;   /*设定四个角为圆角*/
      }
      label.ios-checkbox::after{   /*圆形滑扭*/
        content: '';
        width: 30px;
        height: 30px; 
        border-radius: 100%;    /*设定滑块为圆形*/
        background-color: #fff;
        left: 2px;
        position: absolute;
        box-shadow: 0 1px 2px #3337;
      }
  ```
  3. 当点击时，设定样式变化

  ```css
      input.ios-checkbox:checked + label.ios-checkbox{ 
        box-shadow: inset 0 0 0 17px #6ddc5f ;    /*设定底框背景动画，往内扩散*/
      }
      input.ios-checkbox:checked + label.ios-checkbox::after{
        left: 32px;   /*设定滑块动画，远离left边*/
      }
  ```
  4. 在对应选择器补上时间； `input` 设定 `display: none` 


### Tips：
  `box-shadow` 默认为 `none` ,语法如下

  ```css
    none | [inset? && [ <offset-x> <offset-y> <blur-radius>? <spread-radius>? <color>? ] ]#

    box-shadow:扩散向（默认外扩），x向阴影，y向阴影，模糊，扩散半径

    /*如以下为内扩散17象素*/
    box-shadow: inset 0 0 0 17px #6ddc5f；
    /*如以下为y方向（向下）1px阴影，模糊面积为2px*/
    box-shadow: 0 1px 2px #3337
  ```

具体如下：

  - inset:
  默认阴影在边框外。使用inset后，阴影在边框内（即使是透明边框），背景之上内容之下。
  - offset-x、 offset-y：
这是头两个 `<length>` 值，用来设置阴影偏移量。`<offset-x>` 设置水平偏移量，如果是负值则阴影位于元素左边。 `<offset-y>` 设置垂直偏移量，如果是负值则阴影位于元素上面。可用单位请查看 `<length>` 。
如果两者都是0，那么阴影位于元素后面。这时如果设置了`<blur-radius>` 或`<spread-radius>` 则有模糊效果。
  - blur-radius：
这是第三个 `<length>` 值。值越大，模糊面积越大，阴影就越大越淡。 不能为负值。默认为0，此时阴影边缘锐利。
  - spread-radius：
这是第四个 `<length>` 值。取正值时，阴影扩大；取负值时，阴影收缩。默认为0，此时阴影与元素同样大。
  - color：
相关事项查看` <color>` 。如果没有指定，则由浏览器决定——通常是color的值，不过目前Safari取透明。

