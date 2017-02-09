# border实现圆角效果

在IE7，8中，dotted类型的边框为圆形

```html
<html>
	<head>
		<style>
			#div1
			{
				width: 100%;
				height: 100%;
				border: 99px dotted black;
			}
			#box
			{
				width: 100px;
				height: 100px;
				margin: 200px auto;
				overflow: hidden;
			}
		</style>
	</head>
	<body>
		<div id="box">
			<div id="div1">
		</div>
		</div>>
	</body>
</html>
```