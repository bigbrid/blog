很多设计师很喜欢设计圆环形进度条；

虽然可以用CSS3来实现，但是在需要交互时，还是比较麻烦的；

下面是在一个项目中使用了SVG来实现圆环形进度条。



```
<div class="svg-grounp">
    <svg width="440" height="440" viewbox="0 0 440 440">
    <circle cx="220" cy="220" r="170" stroke-width="10" stroke="#D1D3D7" fill="none"></circle>
    <circle cx="220" cy="220" r="170" stroke-width="10" stroke="#6c7386" fill="none" transform="matrix(0,-1,1,0,0,440)" stroke-dasharray="1069 0"></circle>
    </svg>
    <p class="load-value"></p>
</div>
```

```
run:function(value){
    var percent = value , //图片预加载的进度
    perimeter = Math.PI * 2 * 170,//圆的周长
    circle = document.getElementsByTagName("circle")[1];
    console.log();
    var loadText = Math.floor(percent*100)  //进度显示文字
    circle.setAttribute('stroke-dasharray', perimeter * percent + " " + perimeter * (1- percent));
},
```



### circles.js 插件

circles是一款基于HTML5SVG的轻量级JavaScript圆形进度条插件。该圆形进度条具有响应式，可动画等特点，并且可以制作出圆形进度条进入视口才开始动画的效果。

###  使用方法

使用该圆形进度条需要引入circles.js（或circles.min.js）文件。

```
`<``script` `src``=``"js/circles.min.js"``></``script``>              `
```

#####  HTML结构

该圆形进度条的HTML结构使用一个空的`<div>`即可。

```
`<``div` `class``=``"circle"` `id``=``"circles-1"``></``div``>      `
```

#####  初始化插件

在页面DOM元素加载完毕之后，可以通过下面的方法来初始化该圆形进度条插件。`id`参数必须和容器中的id相同。

```
`var` `myCircle = Circles.create({``  ``id:                  ``'circles-1'``,``  ``radius:              60,``  ``value:               43,``  ``maxValue:            100,``  ``width:               10,``  ``text:                ``function``(value){``return` `value + ``'%'``;},``  ``colors:              [``'#D3B6C6'``, ``'#4B253A'``],``  ``duration:            400,``  ``wrpClass:            ``'circles-wrp'``,``  ``textClass:           ``'circles-text'``,``  ``valueStrokeClass:    ``'circles-valueStroke'``,``  ``maxValueStrokeClass: ``'circles-maxValueStroke'``,``  ``styleWrapper:        ``true``,``  ``styleText:           ``true``});               `
```

###  配置参数

该圆形进度条的可用配置参数如下：

- `id`：包裹圆形进度条的DOM元素的ID。

- `radius`：圆形进度条的半径。

- `value`：圆形进度条的初始值，默认值为0。

- `maxValue`：圆形进度条的最大值，默认值为100。

- `width`：圆环的宽度，如果没有指定，值为10。

- `colors`：一个颜色数组，第一个颜色是整个圆环的颜色，如果没有指定，值为`['#EEE', '#F00']`。也可以是rgba()值，例如`['rgba(255,255,255,0.25)', 'rgba(125,125,125,0.5)']`。

- `duration`：动画的持续时间，默认为500.如果传入0或`null`，就不会有动画效果。

- `wrpClass`：包裹整个圆形进度条的元素的class名称。

- `textClass`：圆形进度条中文本的class名称。

- `valueStrokeClass`：用于`value`值的SVG path元素的class名称。

- `maxValueStrokeClass`：用于`maxValue`值的SVG path元素的class名称。

- `styleWrapper`：是否在包裹元素上添加行内(inline)样式，默认值为`true`。

- `styleText`：是否在文本元素上添加行内(inline)样式，默认值为`true`。

- ```
  text
  ```

  ：圆形简单中间显示的文本。不设置文本可以设置为

  ```
  null
  ```

  。它也可以是一个函数，函数的返回值将显示在圆形进度条的中间，例如：

  `// Example 1``function``(currentValue) {``  ``return` `'$'``+currentValue;``}``// Example 2``function``() {``  ``return` `this``.getPercent() + ``'%'``;``}  `

  ```
  // Example 1
  function(currentValue) {
    return '$'+currentValue;
  }
  // Example 2
  function() {
    return this.getPercent() + '%';
  }  
  	
  ```

###  API

```
`myCircle.updateRadius(Number radius)`
```

通过给定的`radius`更新圆形进度条，例如制作响应式的圆形进度条。

```
`myCircle.updateWidth(Number width)`
```

通过给定的`width`更新圆形进度条。

```
`myCircle.updateColors(Array colors)`
```

更新圆形进度条的颜色。

```
`myCircle.update(Number value [, Number duration])`
```

为圆形进度条设置值。动画将使用`duration`毫秒来执行。如果`duration`没有指定，在构造函数中设置的`duration`值将被使用。如果不需要`duration`值，设置为0。

```
`myCircle.update(Boolean force)`
```

如果`force`设置为`true`，则强制重绘圆形进度条。

```
`myCircle.getPercent()`
```

返回基于当前值和最大值的圆形进度条的百分比值。

```
`myCircle.getValue()`
```

返回圆形进度条的值。

```
`myCircle.getMaxValue()`
```

返回圆形进度条的最大值。

```
`myCircle.getValueFromPercent(Number percentage)`
```

返回基于`percentage`和最大值的圆形进度条的百分比值。

```
`myCircle.htmlifyNumber(Number number[, integerPartClass, decimalPartClass])`
```

Returned HTML representation of given `number` with given classes names applied on tags。

###  CSS样式

圆形进度条的样式被指定为内联模式，你可以通过下面的CSS class类来覆盖要设置的样式。

- `circles-wrp`：包裹整个圆形进度条的元素的class类。
- `circles-text`：包裹文本的容器的class类。
- `circles-integer`：包裹在原点符号之前的文本的容器的class类。
- `circles-decimals`：包裹小数部分文本的容器的class类。

###  浏览器兼容

桌面设备浏览器：

- Firefox 3+
- Chrome 4+
- Safari 3.2+
- Opera 9+
- IE9 +

移动设备浏览器：

- iOS Safari 3.2+
- Android Browser 3+
- Opera Mobile 10+
- Chrome for Android 18+
- Firefox for Android 15+

circles圆形进度条插件的github地址为：<https://github.com/lugolabs/circles>

转载：<http://www.htmleaf.com/html5/SVG/201512162908.html>