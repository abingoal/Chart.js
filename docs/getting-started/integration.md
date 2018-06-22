# 集成

Chart.js可以与JavaScript集成或与不同的模块加载器集成。 下面的例子显示了如何在不同的方式中加载Chart.js。

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
