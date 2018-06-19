# 样式(Styling)

有许多选项可用于设置坐标轴的样式。以下是设置[网格线](#grid-line-configuration)和[刻度](#tick-configuration)的配置。

## 网格线配置

网格线配置嵌套在`gridLines`配置下。它定义垂直于轴线的网格线的选项。

| 名称                       | 类型                 | 默认值                  | 描述                                                                                                                                                |
| -------------------------- | -------------------- | ----------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| `display`                  | `Boolean`            | `true`                  | 如果为false，则不显示该轴的网格线                                                                                                                   |
| `color`                    | `Color or Color[]`   | `'rgba(0, 0, 0, 0.1)'`  | 网格线的颜色。如果指定为数组，则第一种颜色适用于第一个网格线，第二种适用于第二个网格线，依此类推                                                    |
| `borderDash`               | `Number[]`           | `[]`                    | 网格线上的折号的长度和间距。 参看 [MDN](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/setLineDash)                      |
| `borderDashOffset`         | `Number`             | `0`                     | 线破折号的偏移量 参见 [MDN](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/lineDashOffset)                               |
| `lineWidth`                | `Number or Number[]` | `1`                     | 网格线的行程宽度                                                                                                                                    |
| `drawBorder`               | `Boolean`            | `true`                  | 如果为true，则在坐标轴和图表区域之间的边缘绘制边框                                                                                                  |
| `drawOnChartArea`          | `Boolean`            | `true`                  | 如果为true，则在轴线内的图表区域绘制线条。当有多个轴并且您需要控制绘制哪些网格线时，该选项将会很有帮助                                              |
| `drawTicks`                | `Boolean`            | `true`                  | 如果为true，则在图表旁边的轴区域中的刻度旁绘制线条                                                                                                  |
| `tickMarkLength`           | `Number`             | `10`                    | 绘制到坐标轴区域内的网格线的长度(以像素为单位)                                                                                                      |
| `zeroLineWidth`            | `Number`             | `1`                     | 第一个索引（索引0）的网格线的行绘制宽度                                                                                                             |
| `zeroLineColor`            | Color                | `'rgba(0, 0, 0, 0.25)'` | 第一个索引（索引0）的网格线的绘制颜色                                                                                                               |
| `zeroLineBorderDash`       | `Number[]`           | `[]`                    | 第一个索引（索引0）的网格线的连接号的长度和间距。请参阅[MDN](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/setLineDash) |
| `zeroLineBorderDashOffset` | `Number`             | `0`                     | 第一个索引（索引0）的网格线的连接号。请参阅[MDN](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/lineDashOffset)          |
| `offsetGridLines`          | `Boolean`            | `false`                 | 如果为true，则将标签移动到网格线之间。一般用于条形图中，通常不应使用。              `                                                               |

##  刻度配置

tick配置嵌套在`ticks`配置下的scale配置。其定义了坐标轴生成的刻度线的选项。

| 名称         | 类型       | 默认值                                                 | 描述                                                                                                           |
| ------------ | ---------- | ------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------- |
| `callback`   | `Function` |                                                        | 返回应在图表上显示的刻度值(字符串表示形式) 参考 [callback](../axes/labelling.md#creating-custom-tick-formats). |
| `display`    | `Boolean`  | `true`                                                 | 如果为true，则显示刻度标记                                                                                     |
| `fontColor`  | Color      | `'#666'`                                               | 刻度标签字体颜色                                                                                               |
| `fontFamily` | `String`   | `"'Helvetica Neue', 'Helvetica', 'Arial', sans-serif"` | 刻度标签的字体，遵循CSS字体家族选项                                                                            |
| `fontSize`   | `Number`   | `12`                                                   | 刻度标签的字体大小                                                                                             |
| `fontStyle`  | `String`   | `'normal'`                                             | 刻度标签的字体样式，遵循CSS字体样式选项（即normal, italic, oblique, initial, inherit)                          |
| `reverse`    | `Boolean`  | `false`                                                | 刻度标签反序                                                                                                   |
