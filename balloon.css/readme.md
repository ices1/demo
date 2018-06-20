## Balloon.css
[在线地址](https://ices1.github.io/demo/balloon.css/index.html)
[Balloon页面仿做](https://ices1.github.io/demo/balloon.css/balloon-clone.html)
![balloon.css](https://raw.githubusercontent.com/ices1/demo/master/balloon.css/balloon.gif)

### What
实现元素 `hover` 时 弹出 `tooltip` 提示框

### which
伪元素、 `Transform` 变换、 `flex` 自适应、 `@media` 响应式

### How
`data-balloon` ->提示内容 `data-balloon-length`-> 提示长度 `data-balloon-pos`-> 提示方向 
```html
<button data-balloon-length="small" data-balloon="Hi." data-balloon-pos="up">Hover me!</button>
```
### Step
 - 通过要`data-balloon::after`、`data-balloon::before` 伪元素分别生成tooltip提示窗的小三角、内容区
 - 分别对不同方向，大小编写样式
 - 补充完善缺省时默认样式，并在其他状态时清除默认样式

### Tips
 - 当[data-balloon-pos="up"]时，需要将存放内容的伪元素 `data-balloon::before` 相对元素居中上移：
 ```css
	/*居中对齐*/
	left: 50%;
	transform: translateX(-50%);
	bottom: 100%;
 ```
 - 当元素hover时，display: none|block 不能渐变，visibility: visible|hidden 可以渐变

 ```css

	/*hover前*/
	  opacity: 0;
	  visibility: hidden;
	  transition: .2s;
	/*hover时*/
	  opacity: 1;
	  visibility: visible;
 ```

 - 注意 translate(tx[, ty]), 若ty没指定将默认设定0， 以下两个不一样

  ```css
  transform: translate(-50%);	/*等效于translate(-50%,0)*/
  transform: translate(-50%,-50%);
  ```

### Balloon页面-响应式布局

```css
	/*容器 > 768px时*/
	.empty-block{			/*width:242px --> 0px   常用隐藏元素方式（或display:none）*/
	  width: 242px;		
	}
	iframe{
	  position: absolute;	/*position:absolute --> relative & margin  根据页面大小改变定位方式（灵活）*/
	  margin-top: -3.2rem;
	  margin-left: 29rem;
	}
	.sample{
	  display: flex;
	  margin-bottom: 2rem;	/*flex-direction: row --> column  根据页面大小改变flex排序方式（灵活）*/
	}
	.example{
	  width: 30%;
	  text-align: center;	/*width:30% --> 100%   类似栅格布局（常用）*/
	}

	/*容器 <= 768px时*/
	@media (max-width: 768px) {
	  .empty-block{
	    width: 0;
	  }
	  iframe{
	    position: relative;
	    margin-top: 3rem;
	    margin-left: 0;
	  }
	  .sample{
	    flex-direction: column;
	  }
	  .sample pre{
	    width: 100%;
	  }
	  .example{
	    width: 100%;
	  }
	}
```


