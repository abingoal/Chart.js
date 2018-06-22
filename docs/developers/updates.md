# 更新 Charts

在创建图表后更新图表是非常常见的。图表数据更改后，Chart.js 将动画显示新的数据值。

## 添加或移除数据

通过更改数据数组来支持添加和删除数据。要添加数据，只需将数据添加到数据数组中，如本例所示。

```javascript
function addData(chart, label, data) {
	chart.data.labels.push(label);
	chart.data.datasets.forEach(dataset => {
		dataset.data.push(data);
	});
	chart.update();
}

function removeData(chart) {
	chart.data.labels.pop();
	chart.data.datasets.forEach(dataset => {
		dataset.data.pop();
	});
	chart.update();
}
```

## 更新选项

更新选项支持选择已有选择属性或传递新选项对象。

- 如果选项发生了变化，则会保留其他选项属性，包括由Chart.js计算的选项属性。
- 如果创建为新对象 - 旧选项将被丢弃。

```javascript
function updateConfigByMutating(chart) {
    chart.options.title.text = 'new title';
    chart.update();
}

function updateConfigAsNewObject(chart) {
    chart.options = {
        responsive: true,
        title:{
            display:true,
            text: 'Chart.js'
        },
        scales: {
            xAxes: [{
                display: true
            }],
            yAxes: [{
                display: true
            }]
        }
    }
    chart.update();
}
```

可以单独更新比例尺而不更改其他选项。
要更新比例，请传入包含所有定制的对象，包括那些不变的数据。

使用新的`id`或更改后的`type`更新比例后，引用`chart.scales`中的任何一个的变量将会丢失。

```javascript
function updateScales(chart) {
    var xScale = chart.scales['x-axis-0'];
    var yScale = chart.scales['y-axis-0'];
    chart.options.scales = {
        xAxes: [{
            id: 'newId',
            display: true
        }],
        yAxes: [{
            display: true,
            type: 'logarithmic'
        }]
    }
    chart.update();
    // need to update the reference
    xScale = chart.scales['newId'];
    yScale = chart.scales['y-axis-0'];
}
```

你也可以通过指定其索引或ID来更新特定比例。

```javascript
function updateScale(chart) {
    chart.options.scales.yAxes[0] = {
        type: 'logarithmic'
    }
    chart.update();
}
```
用于更新选项的代码示例可以在[toggle-scale-type.html](../../samples/scales/toggle-scale-type.html)中找到。

## 阻止动画

有时当图表更新时，您可能不需要动画。为此，你可以设置`update` 的持续时间为 `0`.这将会同步渲染图表，而不需要动画。
