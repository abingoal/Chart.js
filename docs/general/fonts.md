# 字体

共有4个特殊的全局设置更改图表上的字体。这些选项在`Chart.defaults.global`中。全局字体设置仅适用于配置中不包含更多特定选项的情况。

例如，在这个图表中，除了图例中的标签外，文本都是红色的。

```javascript
Chart.defaults.global.defaultFontColor = 'red';
let chart = new Chart(ctx, {
    type: 'line',
    data: data,
    options: {
        legend: {
            labels: {
                // 这个更具体的字体属性覆盖全局属性
                fontColor: 'black'
            }
        }
    }
});
```

| 名称 | 类型 | 默认值 | 描述
| ---- | ---- | ------- | -----------
| `defaultFontColor` | `Color` | `'#666'` | 默认字体颜色
| `defaultFontFamily` | `String` | `"'Helvetica Neue', 'Helvetica', 'Arial', sans-serif"` | 默认字体集
| `defaultFontSize` | `Number` | `12` | 文本的默认字体大小（以px为单位）。不适用于径向线性刻度标签。
| `defaultFontStyle` | `String` | `'normal'` | 默认字体样式。不适用于工具提示标题或页脚。不适用于图表标题。

## 不存在的字体

如果为系统上存在的图表指定了字体，则浏览器在设置时不会应用该字体。 如果您发现图表中出现奇怪的字体，请检查您正在应用的字体是否存在于您的系统中。 有关更多详细信息，请参见[issue 3318]((https://github.com/chartjs/Chart.js/issues/3318)。
