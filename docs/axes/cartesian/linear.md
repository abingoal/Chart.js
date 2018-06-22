# 线性笛卡尔轴

线性刻度用于绘制数字数据。它可以放置在x或y轴上。散点图类型在x轴上使用此刻度后可以自动配置为折线图。顾名思义，线性插值用于确定数值在轴上的位置。

## 刻度配置选项

以下选项由linear scale提供。它们都位于`ticks`子选项中。这些选项扩展了[常用的刻度配置](README.md#tick-configuration)。

| 名称            | 类型      | 默认值 | 描述                                                                 |
| --------------- | --------- | ------ | -------------------------------------------------------------------- |
| `beginAtZero`   | `Boolean` |        | 如果为 true,则刻度会在还没设置0的时候包含0                           |
| `min`           | `Number`  |        | 用户定义的最小刻度，覆盖数据的最小值 [更多...](#axis-range-settings) |
| `max`           | `Number`  |        | 用户定义的最大刻度，覆盖数据的最大值 [更多...](#axis-range-settings) |
| `maxTicksLimit` | `Number`  | `11`   | 要显示的最大刻度和网格线数量                                         |
| `stepSize`      | `Number`  |        | 用户定义的比例尺的固定步长 [更多...](#step-size)                     |
| `suggestedMax`  | `Number`  |        | 匹配计算最大数据值时使用[more...](#axis-range-settings)              |
| `suggestedMin`  | `Number`  |        | 匹配计算最小数据值时使用[more...](#axis-range-settings)              |

## 轴范围设置
给坐标轴设定数值范围，了解它们之间的相互作用非常重要。

该例子中，最大的正值为50，但数据最大值扩大到了100。然而，由于最低数据值低于`suggestedMin`设置，因此该值将被忽略。

```javascript
let chart = new Chart(ctx, {
    type: 'line',
    data: {
        datasets: [{
            label: 'First dataset',
            data: [0, 20, 40, 50]
        }],
        labels: ['January', 'February', 'March', 'April']
    },
    options: {
        scales: {
            yAxes: [{
                ticks: {
                    suggestedMin: 50,
                    suggestedMax: 100
                }
            }]
        }
    }
});
```
与`suggested*`设置相反，`min`和`max`设置显式结束于坐标轴。设置这些时，某些数据点可能不可见。

## 步长

如果设置该属性，则刻度标记将以stepSize的倍数枚举增加每一个刻度。如果未设置，则使用nice numbers算法自动标记。
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