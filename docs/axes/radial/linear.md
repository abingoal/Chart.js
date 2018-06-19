# 线性径向轴

线性刻度用于绘制数字数据。顾名思义，线性插值用于确定值与轴中心的关系。

以下附加配置选项由径向线性刻度提供。

## 配置选项

该轴具有ticks，angle lines（从中心向外显示在雷达图中的线），pointLabels（雷达图中边缘附近的标签）的配置属性。下面文档定义了这些部分中的每个属性。

| 名称          | 类型     | 描述                                                        |
| ------------- | -------- | ----------------------------------------------------------- |
| `angleLines`  | `Object` | 角度线配置 [更多...](#angle-line-options)                   |
| `gridLines`   | `Object` | 网格线配置 [更多...](../styling.md#grid-line-configuration) |
| `pointLabels` | `Object` | 点标签配置 [更多...](#point-label-options)                  |
| `ticks`       | `Object` | 刻度配置 [更多...](#tick-options)                           |

## 刻度选项
以下选项由线性刻度提供。它们都位于`ticks`子选项中。该坐标轴支持[常见的刻度配置](../styling.md#tick-configuration)选项。

| 名称                | 类型      | 默认值                        | 描述                                                                |
| ------------------- | --------- | ----------------------------- | ------------------------------------------------------------------- |
| `backdropColor`     | Color     | `'rgba(255, 255, 255, 0.75)'` | 标签背景色                                                          |
| `backdropPaddingX`  | `Number`  | `2`                           | 水平填充的背景标签                                                  |
| `backdropPaddingY`  | `Number`  | `2`                           | 垂直填充的背景标签                                                  |
| `beginAtZero`       | `Boolean` | `false`                       | 如果为true，当刻度不包含0的时候，自动包含                           |
| `min`               | `Number`  |                               | 用户定义的最小刻度，覆盖数据的最小值[更多...](#axis-range-settings) |
| `max`               | `Number`  |                               | 用户定义的最大刻度，覆盖数据的最大值[更多...](#axis-range-settings) |
| `maxTicksLimit`     | `Number`  | `11`                          | 要显示的最大刻度和网格线数量                                        |
| `stepSize`          | `Number`  |                               | 用户定义的比例尺的固定步长 [更多...](#step-size)                    |
| `suggestedMax`      | `Number`  |                               | 计算最大数据值时使用的调整[更多...](#axis-range-settings)           |
| `suggestedMin`      | `Number`  |                               | 计算最小数据值时使用的调整[更多...](#axis-range-settings)           |
| `showLabelBackdrop` | `Boolean` | `true`                        | 如果为true，则在刻度标签后面绘制背景                                |

## 坐标轴范围设置

考虑到轴范围设置的数量，理解它们如何相互作用是很重要的。

建议的最大和建议的最小设置仅更改用于缩放轴的数据值。这些对于扩展轴的范围同时保持自动贴合行为很有用。

`suggestedMax`和`suggestedMin`设置只用于更改缩放轴的数据值。这些属性对于扩展轴的范围以及保持自动匹配行为是很有帮助的。

```javascript
let minDataValue = Math.min(mostNegativeValue, options.ticks.suggestedMin);
let maxDataValue = Math.max(mostPositiveValue, options.ticks.suggestedMax);
```

在本例中，最大的正值为50，但数据最大值扩大到了100。然而，由于最低数据值低于`suggestedMin`设置，因此该值将被忽略。

```javascript
let chart = new Chart(ctx, {
    type: 'radar',
    data: {
        datasets: [{
            label: 'First dataset',
            data: [0, 20, 40, 50]
        }],
        labels: ['January', 'February', 'March', 'April']
    },
    options: {
        scale: {
            ticks: {
                suggestedMin: 50
                suggestedMax: 100
            }
        }
    }
});
```

与`suggested*`设置相反，`min`和`max`设置显式结束于坐标轴。设置这些属性时，某些数据点可能不可见。

## 步长

如果设置的话，则刻度标记将以stepSize的倍数枚举增加刻度。如果未设置，则使用nice numbers算法自动标记。

本示例使用y轴设置图表，创建`0, 0.5, 1, 1.5, 2, 2.5, 3, 3.5, 4, 4.5, 5`的刻度。

```javascript
let options = {
    scales: {
        yAxes: [{
            ticks: {
                max: 5,
                min: 0,
                stepSize: 0.5
            }
        }]
    }
};
```

## 角度线选项

以下选项用于配置从图表中心向点标签辐射的角度线。它们可以在`angleLines`子选项中找到。请注意，这些选项仅适用于`angleLines.display`为true的情况。

| 名称        | 类型      | 默认值               | 描述                     |
| ----------- | --------- | -------------------- | ------------------------ |
| `display`   | `Boolean` | `true`               | 如果为true，则显示角度线 |
| `color`     | Color     | `rgba(0, 0, 0, 0.1)` | 角度线颜色               |
| `lineWidth` | `Number`  | `1`                  | 角度线宽度               |

## 点标签选项

以下选项用于配置刻度边界上显示的点标签。它们可以在`pointLabels`子选项中找到。请注意，这些选项仅适用于`pointLabels.display`为true的情况。

| 名称         | 类型       | 默认值                                                 | 描述                                                   |
| ------------ | ---------- | ------------------------------------------------------ | ------------------------------------------------------ |
| `callback`   | `Function` |                                                        | 将数据标签转换为点标签的回调函数。默认只返回当前字符串 |
| `fontColor`  | Color      | `'#666'`                                               | 点标签的字体颜色                                       |
| `fontFamily` | `String`   | `"'Helvetica Neue', 'Helvetica', 'Arial', sans-serif"` | 渲染标签时使用的字体                                   |
| `fontSize`   | `Number`   | 10                                                     | 字体大小(以像素为单位)                                 |
| `fontStyle`  | `String`   | `'normal'`                                             | 渲染点标签时使用的字体样式                             |