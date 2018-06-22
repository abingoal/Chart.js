# 区域图表

[折线图](line.md)和[雷达图](radar.md)都支持数据集对象上的`fill`选项，该选项可用于创建两个数据集之间的区域或数据集与边界之间的区域，例如，比例尺`origin`, `start` or `end`（参见[filling modes](filling-modes)）。

> **注意:** 这个功能是由 [`filler` plugin](https://github.com/chartjs/Chart.js/blob/master/src/plugins/plugin.filler.js)实现的。

## 填充模式

| 模式 | 类型 | 值 |
| :--- | :--- | :--- |
| 绝对数据集索引 <sup>1</sup> | `Number` | `1`, `2`, `3`, ... |
| 相对数据集索引 <sup>1</sup> | `String` | `'-1'`, `'-2'`, `'+1'`, ... |
| 边界 <sup>2</sup> | `String` | `'start'`, `'end'`, `'origin'` |
| 禁用 <sup>3</sup> | `Boolean` | `false` |

> <sup>1</sup> 在2.2.0版中引入了数据集填充模式<br>
> <sup>2</sup> 2.6.0之前的版本, 边界值为 `'zero'`, `'top'`, `'bottom'` (已废弃)<br>
> <sup>3</sup> 对于向后兼容性, `fill: true` (默认值) 相当于`fill: 'origin'`<br>

**示例**
```javascript
new Chart(ctx, {
    data: {
        datasets: [
            {fill: 'origin'},      // 0: fill to 'origin'
            {fill: '+2'},          // 1: fill to dataset 3
            {fill: 1},             // 2: fill to dataset 1
            {fill: false},         // 3: no fill
            {fill: '-2'}           // 4: fill to dataset 2
        ]
    }
})
```

## 配置
| 选项 | 类型 | 默认值 | 描述 |
| :--- | :--- | :--- | :--- |
| [`plugins.filler.propagate`](#propagate) | `Boolean` | `true` | 隐藏数据集时的填充

### propagate
Boolean (默认值: `true`)

如果为`true`，则填充区域将递归地扩展到由隐藏数据集目标的`fill`值所定义的可见目标：

**示例**
```javascript
new Chart(ctx, {
    data: {
        datasets: [
            {fill: 'origin'},   // 0: fill to 'origin'
            {fill: '-1'},       // 1: fill to dataset 0
            {fill: 1},          // 2: fill to dataset 1
            {fill: false},      // 3: no fill
            {fill: '-2'}        // 4: fill to dataset 2
        ]
    },
    options: {
        plugins: {
            filler: {
                propagate: true
            }
        }
    }
})
```

`propagate: true`:
- 如果数据集2被隐藏，则数据集4将填充到数据集1
- 如果数据集2和1被隐藏，则数据集4将填充到`'origin'`

`propagate: false`:
- 如果数据集2和/或4被隐藏，则数据集4将不被填充
