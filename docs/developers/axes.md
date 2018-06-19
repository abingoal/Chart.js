# 新的坐标轴(New Axes)

Chart.js 中的坐标轴可以单独扩展。坐标轴应始终来自`Chart.Scale`，但并非强制性的要求。

```javascript
let MyScale = Chart.Scale.extend({
	/* extensions ... */
});

// MyScale现在从Chart.Scale派生而来
```
一旦创建了scale类，就需要将其注册到全局图表对象以便可以使用它。注册构造函数时可以提供一个默认的比例配置。注册函数的第一个参数是一个string key，用于标识之后图表用哪个缩放类型。

```javascript
Chart.scaleService.registerScaleType("myScale", MyScale, defaultConfigObject);
```
要使用新比例，只需在创建图表时将string key传递给配置。

```javascript
var lineChart = new Chart(ctx, {
	data: data,
	type: "line",
	options: {
		scales: {
			yAxes: [
				{
					type: "myScale" // 这是传递给registerScaleType函数的相同key
				}
			]
		}
	}
});
```

## 比例属性

在拟合过程中给出缩放实例的如下属性。

```javascript
{
    left: Number, // 比例边框的左边
    right: Number, // 比例边框的右边
    top: Number,
    bottom: Number,
    width: Number, // 同 right - left
    height: Number, // 同 bottom - top

	// 每个边的边距，同css，此处是外边距
    margins: {
        left: Number,
        right: Number,
        top: Number,
        bottom: Number,
    },

	// 边框的内间距（同CSS）
    paddingLeft: Number,
    paddingRight: Number,
    paddingTop: Number,
    paddingBottom: Number,
}
```

## 比例接口

要使用Chart.js，自定义比例类型必须实现以下接口。

```javascript
{
	// 确定数据限制。应该将this.min和this.max设置为数据最大/最小值
    determineDataLimits: function() {},

	// 生成刻度标记。 this.chart是图表实例。数据对象可以通过this.chart.data访问
	// 如果你打算使用基类中的任何实现则buildTicks（）应该在坐标轴实例上创建一个ticks数组
    buildTicks: function() {},

	// 获取在给定数据集的给定索引处显示数据的值，即this.chart.data.datasets[datasetIndex].data [index]
    getLabelForIndex: function(index, datasetIndex) {},

	// 获取给定值的像素（水平轴的x坐标，垂直轴的y坐标）
    // @param index: 刻度数组中的索引
    // @param includeOffset: 如果为true，则在给定刻度与下一个刻度之间获得像素半径
    getPixelForTick: function(index, includeOffset) {},

    // 获取给定值的像素（水平轴的x坐标，垂直轴的y坐标）
    // @param value : 获取像素的值
    // @param index : 数据值在数据数组中的索引
    // @param datasetIndex : 索引的数据来源
    // @param includeOffset : 如果为true，则在给定刻度与下一个刻度之间获得像素半径
    getPixelForValue: function(value, index, datasetIndex, includeOffset) {}

    // 获取给定像素的值（水平轴的x坐标，垂直轴的y坐标）
    // @param pixel : 像素值
    getValueForPixel: function(pixel) {}
}
```
可选地，以下方法也可能被覆盖，但`Chart.Scale`基类已经提供了一个实现。

```javascript
	// 将缩放实例的刻度数组转换为字符串。默认实现简单地调用this.options.ticks.callback（numericalTick，index，ticks）
    convertTicksToLabels: function() {},

	// 确定标签将旋转多少。默认实现将只在标尺水平时旋转标签。
    calculateTickRotation: function() {},

	// 依canvas适配比例
	// this.maxWidth和this.maxHeight会告诉你scale实例可以达到的最大尺寸。比例尺应尽可能使用画布空间。
	// this.margins是您可以扩展到的scale两侧的空间量。这已经用于计算最佳标签旋转。
    // 必须将this.minSize设置为您的比例尺寸。它必须是包含2个属性的对象：width和height。
    // 必须将this.width设置为宽度，this.height为scale的高度
    fit: function() {},
	// 将比例绘制到canvas上。this.(left|right|top|bottom)将被填充以告诉你canvas上的区域进行绘制
    // @param chartArea : 一个包含四个属性的对象：left, right, top, bottom。折线图，条形图等将被绘制在该区域。例如，它可以用于绘制网格线。
    draw: function(chartArea) {},
```

Core.Scale基类还有一些实用功能，可能会对你有所帮助。

```javascript
{
    // 如果scale实例是水平的，则返回true
    isHorizontal: function() {},

    // 从this.chart.data.datasets [x] .data []中获取正确的值
    // 如果dataValue是一个对象，则返回.x或.y，具体取决于isHorizo​​ntal（）的返回值
    // 如果该值未定义，则返回NaN
    // 否则返回该值
    // 请注意，在任何情况下，返回的值不能保证一定是个数字
    getRightValue: function(dataValue) {},
}
```
