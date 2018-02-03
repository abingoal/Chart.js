# 柱状/条形图

柱状/条形图提供了一种以竖线表示数据值的显示方式。用来显示数据趋势，并排比较多个数据集。

{% chartjs %}
{
"type": "bar",
"data": {
"labels": [
"January",
"February",
"March",
"April",
"May",
"June",
"July"
],
"datasets": [{
"label": "My First Dataset",
"data": [65, 59, 80, 81, 56, 55, 40],
"fill": false,
"backgroundColor": [
"rgba(255, 99, 132, 0.2)",
"rgba(255, 159, 64, 0.2)",
"rgba(255, 205, 86, 0.2)",
"rgba(75, 192, 192, 0.2)",
"rgba(54, 162, 235, 0.2)",
"rgba(153, 102, 255, 0.2)",
"rgba(201, 203, 207, 0.2)"
],
"borderColor": [
"rgb(255, 99, 132)",
"rgb(255, 159, 64)",
"rgb(255, 205, 86)",
"rgb(75, 192, 192)",
"rgb(54, 162, 235)",
"rgb(153, 102, 255)",
"rgb(201, 203, 207)"
],
"borderWidth": 1
}]
},
"options": {
"scales": {
"yAxes": [{
"ticks": {
"beginAtZero": true
}
}]
}
}
}
{% endchartjs %}

## 示例用法

```javascript
var myBarChart = new Chart(ctx, {
	type: "bar",
	data: data,
	options: options
});
```

## 数据集属性

柱状/条形图允许为每个数据集指定一些属性用于显示特定数据集一些属性可以被指定为一个数组。如果这些设置为数组值，则第一个值应用于第一个节点，第二个值应用于第二个节点，依此类推。

| 名称                   | 类型              | 描述                                                                    |
| ---------------------- | ----------------- | ----------------------------------------------------------------------- |
| `label`                | `String`          | 在图例和工具提示中显示的数据集标签                                      |
| `xAxisID`              | `String`          | 绘制此数据集的 x 轴的 ID。如果未指定，则默认为第一个找到的 x 轴的 ID 。 |
| `yAxisID`              | `String`          | 绘制该数据集的 y 轴的 ID。如果未指定，则默认为第一个找到的 y 轴的 ID。  |
| `backgroundColor`      | `Color/Color[]`   | 柱状/条形图填充色. 参考 [颜色(Colors)](../general/colors.md#colors)     |
| `borderColor`          | `Color/Color[]`   | 边框色 参考 [颜色(Colors)](../general/colors.md#colors)                 |
| `borderWidth`          | `Number/Number[]` | 边框宽度(以像素为单位)                                                  |
| `borderSkipped`        | `String`          | 不绘制边框 [更多...](#borderSkipped)                                    |
| `hoverBackgroundColor` | `Color/Color[]`   | 悬浮时的填充色                                                          |
| `hoverBorderColor`     | `Color/Color[]`   | 悬浮时的边框色                                                          |
| `hoverBorderWidth`     | `Number/Number[]` | 悬浮时边框宽度                                                          |

### borderSkipped

此设置用于避免基线被填充。一般来说，除非创建从柱状/条形图派生的图表类型，否则不需要更改。

选项:

* 'bottom'
* 'left'
* 'top'
* 'right'

## 配置选项

柱状/条形图定义了以下配置选项。这些选项与全局图表配置选项`Chart.defaults.global`合并，形成最终传递给图表的选项。

| 名称                        | 类型      | 默认值 | 描述                                                                                                                                                                                                                                |
| --------------------------- | --------- | ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `barPercentage`             | `Number`  | `0.9`  | Percent (0-1) of the available width each bar should be within the category percentage. 1.0 will take the whole category width and put the bars right next to each other. [more...](#bar-chart-barpercentage-vs-categorypercentage) |
| `categoryPercentage`        | `Number`  | `0.8`  | Percent (0-1) of the available width (the space between the gridlines for small datasets) for each data-point to use for the bars. [more...](#bar-chart-barpercentage-vs-categorypercentage)                                        |
| `barThickness`              | `Number`  |        | Manually set width of each bar in pixels. If not set, the bars are sized automatically using `barPercentage` and `categoryPercentage`;                                                                                              |
| `maxBarThickness`           | `Number`  |        | Set this to ensure that the automatically sized bars are not sized thicker than this. Only works if barThickness is not set (automatic sizing is enabled).                                                                          |
| `gridLines.offsetGridLines` | `Boolean` | `true` | If true, the bars for a particular data point fall between the grid lines. If false, the grid line will go right down the middle of the bars. [more...](#offsetGridLines)                                                           |

### offsetGridLines

If true, the bars for a particular data point fall between the grid lines. If false, the grid line will go right down the middle of the bars. It is unlikely that this will ever need to be changed in practice. It exists more as a way to reuse the axis code by configuring the existing axis slightly differently.

This setting applies to the axis configuration for a bar chart. If axes are added to the chart, this setting will need to be set for each new axis.

```javascript
options = {
	scales: {
		xAxes: [
			{
				gridLines: {
					offsetGridLines: true
				}
			}
		]
	}
};
```

## Default Options

It is common to want to apply a configuration setting to all created bar charts. The global bar chart settings are stored in `Chart.defaults.bar`. Changing the global options only affects charts created after the change. Existing charts are not changed.

## barPercentage vs categoryPercentage

The following shows the relationship between the bar percentage option and the category percentage option.

```text
// categoryPercentage: 1.0
// barPercentage: 1.0
Bar:        | 1.0 | 1.0 |
Category:   |    1.0    |
Sample:     |===========|

// categoryPercentage: 1.0
// barPercentage: 0.5
Bar:          |.5|  |.5|
Category:  |      1.0     |
Sample:    |==============|

// categoryPercentage: 0.5
// barPercentage: 1.0
Bar:            |1.||1.|
Category:       |  .5  |
Sample:     |==============|
```

## Data Structure

The `data` property of a dataset for a bar chart is specified as a an array of numbers. Each point in the data array corresponds to the label at the same index on the x axis.

```javascript
data: [20, 10];
```

# Stacked Bar Chart

Bar charts can be configured into stacked bar charts by changing the settings on the X and Y axes to enable stacking. Stacked bar charts can be used to show how one data series is made up of a number of smaller pieces.

```javascript
var stackedBar = new Chart(ctx, {
	type: "bar",
	data: data,
	options: {
		scales: {
			xAxes: [
				{
					stacked: true
				}
			],
			yAxes: [
				{
					stacked: true
				}
			]
		}
	}
});
```

## Dataset Properties

The following dataset properties are specific to stacked bar charts.

| Name    | Type     | Description                                                                                              |
| ------- | -------- | -------------------------------------------------------------------------------------------------------- |
| `stack` | `String` | The ID of the group to which this dataset belongs to (when stacked, each group will be a separate stack) |

# Horizontal Bar Chart

A horizontal bar chart is a variation on a vertical bar chart. It is sometimes used to show trend data, and the comparison of multiple data sets side by side.
{% chartjs %}
{
"type": "horizontalBar",
"data": {
"labels": ["January", "February", "March", "April", "May", "June", "July"],
"datasets": [{
"label": "My First Dataset",
"data": [65, 59, 80, 81, 56, 55, 40],
"fill": false,
"backgroundColor": [
"rgba(255, 99, 132, 0.2)",
"rgba(255, 159, 64, 0.2)",
"rgba(255, 205, 86, 0.2)",
"rgba(75, 192, 192, 0.2)",
"rgba(54, 162, 235, 0.2)",
"rgba(153, 102, 255, 0.2)",
"rgba(201, 203, 207, 0.2)"
],
"borderColor": [
"rgb(255, 99, 132)",
"rgb(255, 159, 64)",
"rgb(255, 205, 86)",
"rgb(75, 192, 192)",
"rgb(54, 162, 235)",
"rgb(153, 102, 255)",
"rgb(201, 203, 207)"
],
"borderWidth": 1
}]
},
"options": {
"scales": {
"xAxes": [{
"ticks": {
"beginAtZero": true
}
}]
}
}
}
{% endchartjs %}

## Example

```javascript
var myBarChart = new Chart(ctx, {
	type: "horizontalBar",
	data: data,
	options: options
});
```

## Config Options

The configuration options for the horizontal bar chart are the same as for the [bar chart](../bar/config-options.md#config-options). However, any options specified on the x axis in a bar chart, are applied to the y axis in a horizontal bar chart.

The default horizontal bar configuration is specified in `Chart.defaults.horizontalBar`.
