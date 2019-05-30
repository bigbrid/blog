## 使用JavaScript将图片拷贝进画布

要想将图片放入画布里，我们使用canvas元素的`drawImage`方法：

```js

function convertImageToCanvas(image) {
	var canvas = document.createElement("canvas");
	canvas.width = image.width;
	canvas.height = image.height;
	canvas.getContext("2d").drawImage(image, 0, 0);

	return canvas;
}
```

这里的`0, 0`参数画布上的坐标点，图片将会拷贝到这个地方。

## 用JavaScript将画布保持成图片格式

如果你的画布上的作品已经完成，你可以用下面简单的方法将canvas数据转换成图片格式：

```js

function convertCanvasToImage(canvas) {
	var image = new Image(); //
	image.src = canvas.toDataURL("image/png");
	return image;
}

```

或者使用集成插件：[html2canvas](http://html2canvas.hertzen.com/)