# 时间笛卡尔轴

时间刻度用于显示时间和日期。当建立刻度时，它会自动计算出尺度上最合适的单位。

## 刻度配置选项

以下选项由时间刻度提供。它们都位于`time`子选项中。这些选项扩展了[常用刻度配置](README.md#tick-configuration)。

| 名称             | 类型                   | 默认值        | 描述                                                                                                       |
| ---------------- | ---------------------- | ------------- | ---------------------------------------------------------------------------------------------------------- |
| `displayFormats` | `Object`               |               | 设置不同时间单位的显示方式。[更多...](#display-formats)                                                    |
| `isoWeekday`     | `Boolean`              | `false`       | 如果为true并且该单位设置为'week'，则将使用 iso weekdays                                                    |
| `max`            | [Time](#date-formats)  |               | 如果定义，将覆盖数据的最大值                                                                               |
| `min`            | [Time](#date-formats)  |               | 如果定义，这将覆盖数据的最小值                                                                             |
| `parser`         | `String` or `Function` |               | 自定义格式化日期 [更多...](#parser)                                                                        |
| `round`          | `String`               | `false`       | 如果定义，日期将四舍五入到该单位的开始处。请参阅下面的[时间单位](#scales-time-units)以获取所允许使用的单位 |
| `tooltipFormat`  | `String`               |               | tooltip的日期格式化                                                                                        |
| `unit`           | `String`               | `false`       | 如果定义，将强制该单位是某种类型。详细信息请参见下面的[时间单位](#scales-time-units)部分                   |
| `unitStepSize`   | `Number`               | `1`           | 网格线之间的单位数量                                                                                       |
| `minUnit`        | `String`               | `millisecond` | 用于时间单位的最小显示格式                                                                                 |

## 日期格式

在提供时间刻度的数据时，Chart.js支持Moment.js接受的所有格式。有关详细信息，请参阅[Moment.js文档](http://momentjs.com/docs/#/parsing/)。

## 时间单位

支持以下时间单位。将该单位作为字符串传递给`time.unit`以强制使用某个单位。

* millisecond
* second
* minute
* hour
* day
* week
* month
* quarter
* year

例如，要创建一个总是以每月显示单位的时间刻度的图表，可以使用以下配置。

```javascript
var chart = new Chart(ctx, {
    type: 'line',
    data: data,
    options: {
        scales: {
            xAxes: [{
                type: 'time',
                time: {
                    unit: 'month'
                }
            }]
        }
    }
})
```

## 显示格式

以下显示格式用于配置如何将不同时间单位格式化为字符串来作为坐标轴轴刻度。有关允许的格式字符串，请参阅[moment.js](http://momentjs.com/docs/#/displaying/format/)。

| 名称        | 默认值        |
| ----------- | ------------- |
| millisecond | 'SSS [ms]'    |
| second      | 'h:mm:ss a'   |
| minute      | 'h:mm:ss a'   |
| hour        | 'MMM D, hA'   |
| day         | 'll'          |
| week        | 'll'          |
| month       | 'MMM YYYY'    |
| quarter     | '[Q]Q - YYYY' |
| year        | 'YYYY'        |

例如，要将'quarter'单位的显示格式设置为显示月份和年份，则可以进行以下配置。

```javascript
var chart = new Chart(ctx, {
    type: 'line',
    data: data,
    options: {
        scales: {
            xAxes: [{
                type: 'time',
                time: {
                    displayFormats: {
                        quarter: 'MMM YYYY'
                    }
                }
            }]
        }
    }
})
```

## 解析器

如果这个属性被定义为一个字符串，它将被解释为一个自定义的格式，以便用来解析日期。

如果这是一个函数，它必须返回给定相应数据值的moment.js对象。
