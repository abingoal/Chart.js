# 新的图表(New Charts)

Chart.js 2.0为每个数据集引入了控制器的概念。像scales一样，可以根据需要编写新的控制器。

```javascript
Chart.controllers.MyType = Chart.DatasetController.extend({});

// 现在我们可以使用Chart.js API创建图表的一个新实例
new Chart(ctx, {
	// 这是构造函数注册的字符串，即Chart.controllers.MyType
	type: "MyType",
	data: data,
	options: options
});
```

## 数据集控制器接口

数据集控制器必须实现以下接口

```javascript
{
    // 为数据集中的每条数据创建元素。将数据集中的元素作为dataset.metaData存储在数据集中
    addElements: function() {},

    // 为给定索引处的数据创建单个元素并重置其状态
    addElementAndReset: function(index) {},

    // 绘制数据集的表示形式
    // @param ease : 如果指定该参数，则此数字代表转换元素的距离。在任何提供的控制器中查看 draw（）的实现以了解如何使用它
    draw: function(ease) {},

    // 从给定元素删除悬停样式
    removeHoverStyle: function(element) {},

    // 将悬停样式添加到给定的元素
    setHoverStyle: function(element) {},

    // 更新元素以响应新数据
    // @param reset : 如果为true，则将元素置于复位状态，以便它们可以持续动画直到其最终值
    update: function(reset) {},
}
```

派生数据集控制器可以选择覆盖以下方法

```javascript
{
    // 初始化控制器
    initialize: function(chart, datasetIndex) {},

	// 确保由此控制器表示的数据集链接到一个scale。覆盖极地图的helpers.noop和doughnut控制器
    // 使用单一比例的图表类型
    linkScales: function() {},

	// 当更新被触发时，由主图表控制器调用。默认实现处理更改数据点的数量并适当地创建元素。
    buildOrUpdateElements: function() {}
}
```

## 扩展现有的图表类型

扩展或替换现有的控制器类型非常简单。只需用您自己的内置类型替换其中一种内置类型的构造函数即可。

内置的控制器类型:

* `Chart.controllers.line`
* `Chart.controllers.bar`
* `Chart.controllers.radar`
* `Chart.controllers.doughnut`
* `Chart.controllers.polarArea`
* `Chart.controllers.bubble`

例如，要派生一个从气泡图扩展而来的新图表类型，您可以执行以下操作。

```javascript
// 将'derivedBubble'的默认配置设置为与气泡值默认值相同。
// 我们通过执行Chart.defaults [chartType]来查找默认值
// 这里好像是个bug，当默认值不存在的时候
Chart.defaults.derivedBubble = Chart.defaults.bubble;

// 我认为推荐使用Chart.controllers.bubble.extend（{extensions here};
var custom = Chart.controllers.bubble.extend({
	draw: function(ease) {
		// 先调用super方法
		Chart.controllers.bubble.prototype.draw.call(this, ease);

		// 现在我们可以为这个数据集做一些自定义绘图。在这里我们将围绕每个数据集中的第一个点绘制一个红色框
		var meta = this.getMeta();
		var pt0 = meta.data[0];
		var radius = pt0._view.radius;

		var ctx = this.chart.chart.ctx;
		ctx.save();
		ctx.strokeStyle = "red";
		ctx.lineWidth = 1;
		ctx.strokeRect(
			pt0._view.x - radius,
			pt0._view.y - radius,
			2 * radius,
			2 * radius
		);
		ctx.restore();
	}
});

// 存储控制器以便图表初始化程序可以查找它
// Chart.controllers[type]
Chart.controllers.derivedBubble = custom;

// 现在我们可以创建和使用我们的新图表类型
new Chart(ctx, {
	type: "derivedBubble",
	data: data,
	options: options
});
```

### 条形图控制器

条形图控制器有一个你应该知道的特殊属性。要正确计算条形的宽度，控制器必须确定映射到条的数据集的数量。为此，条形控制器在初始化期间将属性`bar`附加到数据集。当创建或更新条形控制器时，使用这种方式来做。以确保具有常规条形图和新的派生条形的图表能够无缝工作。