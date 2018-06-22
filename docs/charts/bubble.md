# 气泡图(Bubble Chart)

气泡图用于同时显示三维数据。气泡的位置由前两个维度以及相应的水平和垂直轴线确定。第三个维度由单个气泡的大小来表示。

{% chartjs %}
{
"type": "bubble",
"data": {
"datasets": [{
"label": "First Dataset",
"data": [{
"x": 20,
"y": 30,
"r": 15
}, {
"x": 40,
"y": 10,
"r": 10
}],
"backgroundColor": "rgb(255, 99, 132)"
}]
},
}
{% endchartjs %}

## 示例用法

```javascript
// For a bubble chart
var myBubbleChart = new Chart(ctx, {
	type: "bubble",
	data: data,
	options: options
});
```

## 数据集属性

气泡图允许为每个数据集指定许多属性。这些用于设置特定数据集的显示属性。

| 名称 | 类型 | [可脚本化](../general/options.md#scriptable-options) | [可索引](../general/options.md#indexable-options) |  默认值
| ---- | ---- | :----: | :----: | ----
| [`backgroundColor`](#styling) | [`Color`](../general/colors.md) | 是 | 是 | `'rgba(0,0,0,0.1)'`
| [`borderColor`](#styling) | [`Color`](../general/colors.md) | 是 | 是 | `'rgba(0,0,0,0.1)'`
| [`borderWidth`](#styling) | `Number` | Yes | Yes | `3`
| [`data`](#data-structure) | `Object[]` | - | - | **required**
| [`hoverBackgroundColor`](#interactions) | [`Color`](../general/colors.md) | 是 | 是 | `undefined`
| [`hoverBorderColor`](#interactions) | [`Color`](../general/colors.md) | 是 | 是 | `undefined`
| [`hoverBorderWidth`](#interactions) | `Number` | 是 | 是 | `1`
| [`hoverRadius`](#interactions) | `Number` | 是 | 是 | `4`
| [`hitRadius`](#interactions) | `Number` | 是 | 是 | `1`
| [`label`](#labeling) | `String` | - | - | `undefined`
| [`pointStyle`](#styling) | `String` | 是 | 是 | `circle`
| [`radius`](#styling) | `Number` | 是 | 是 | `3`

### 标签

`label`定义了与数据集关联的文本，并且出现在legend和tooltips中。

### 样式

每个气泡的风格可以通过以下属性进行控制：

| 名称 | 描述
| ---- | ----
| `backgroundColor` | 七宝背景色
| `borderColor` | 气泡边框色
| `borderWidth` | 气泡边框宽度 (以像素为单位)
| `pointStyle` | 气泡[形状样式](../configuration/elements#point-styles)
| `radius` | 气泡半径（以像素为单位）

All these values, if `undefined`, fallback to the associated [`elements.point.*`](../configuration/elements.md#point-configuration) options.
如果这些值是`undefined`，则回退到相关的[`elements.point.*`](../configuration/elements.md#point-configuration)选项。

### 交互

与每个气泡的相互作用可以通过以下属性进行控制：

| 名称 | 描述
| ---- | -----------
| `hoverBackgroundColor` | 悬停时气泡背景色
| `hoverBorderColor` | 悬停时气泡边框色
| `hoverBorderWidth` | 悬停时气泡边框宽度 (以像素为单位)
| `hoverRadius` | 气泡悬停时 **额外**半径 (以像素为单位)
| `hitRadius` | 气泡悬停时 **额外**命中检测半径 (以像素为单位)

如果这些值是`undefined`，都会回退到相关的[`elements.point.＊`](../configuration/elements.md#point-configuration)选项。

## 默认选项

我们也可以更改气泡图表类型的默认值。这样做会使所有在这个点之后创建的气泡图表成为新的默认值。气泡图的默认配置可以在`Chart.defaults.bubble`中访问。

## 数据结构

对于气泡图，数据集需要包含一组数据点。每个点必须实现[气泡数据对象](#bubble-data-object)接口。

### 气泡数据对象

气泡图的数据以对象的形式传递。该对象必须实现以下接口。请注意，半径属性`r` **不会**被图表缩放。它是在 canvas 上绘制的气泡的像素的原始半径。

```javascript
{
    // X Value
    x: <Number>,

    // Y Value
    y: <Number>,

    // 气泡半径，不可缩放
    r: <Number>
}
```
