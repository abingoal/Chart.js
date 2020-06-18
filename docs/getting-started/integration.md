# 集成

Chart.js能够和普通JavaScript或模块加载器集成。 下面的例子显示了如何在不同的系统中加载Chart.js。

## ES6 Modules

```javascript
import Chart from 'chart.js';
var myChart = new Chart(ctx, {...});
```

## Script 标签

```html
<script src="path/to/chartjs/dist/Chart.js"></script>
<script>
    var myChart = new Chart(ctx, {...});
</script>
```

## Common JS

```javascript
var Chart = require('chart.js');
var myChart = new Chart(ctx, {...});
```

## Require JS

```javascript
require(['path/to/chartjs/dist/Chart.js'], function(Chart){
    var myChart = new Chart(ctx, {...});
});
```

> **Important:** RequireJS [can **not** load CommonJS module as is](http://www.requirejs.org/docs/commonjs.html#intro), so be sure to require one of the built UMD files instead (i.e. `dist/Chart.js`, `dist/Chart.min.js`, etc.).

## 内容安全策略（CSP）
默认情况下，Chart.js将CSS直接注入DOM。对于使用[内容安全政策（CSP）](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/CSP)保护的网页，这需要允许`style-src 'unsafe-inline'`。而对于仅允许使用`style-src 'self'`的更严格的CSP环境，需要将以下CSS文件手动引入到您的网页：
```html
<link rel="stylesheet" type="text/css" href="path/to/chartjs/dist/Chart.min.css">
```
并且必须在**创建第一个图表之前**关闭样式注入：
```js
// 禁用样式注入
Chart.platform.disableCSSInjection = true;
```