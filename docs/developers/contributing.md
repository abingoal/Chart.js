# 贡献

我们欢迎您对类库的贡献，但我们要求您遵循以下准则：

- 使用制表符缩进，而不是空格
- 只更改`/src`中的单个文件
- `gulp lint`会为你运行`eslint`来检查你的代码是否会通过代码标准
- `gulp test`检查你的代码是否会通过测试
- 保持pull请求简洁，并在相关的`.md`文件中记录新的功能
- 考虑到您的更改是否对所有用户有用，否则可以考虑是否创建Chart.js[插件](plugins.md)更合适
- 除非有即将发布的主要版本，否则不要重复更改。 我们鼓励为大多数新的高级功能编写插件以关注向后兼容性。


# 加入该项目

请活跃的提交者和贡献者介绍自己并请求提交对此项目的访问权限。我们有一个非常活跃的Slack社区，您可以在[这里](https://chartjs-slack.herokuapp.com/)加入。如果您认为您可以提供帮助，我们很乐意为您服务！

# 构建和测试

Chart.js使用[gulp](http://gulpjs.com/)将库建立到单个JavaScript文件中。
首先，我们需要确保安装开发依赖项。在安装了node和npm之后，将Chart.js库克隆到本地目录，然后在命令行中导航到该目录，我们可以运行以下命令：

```bash
> npm install
> npm install -g gulp
```
这将安装Chart.js的本地开发依赖项，以及JavaScript自动化工具[gulp](http://gulpjs.com/) CLI。

可以在仓库根目录执行以下命令:

```bash
> gulp build                // 在./dist中构建Chart.js
> gulp unittest             // 从./test/specs运行测试
> gulp unittest --watch     // 运行测试并观察源代码更改
> gulp unittest --coverage  // 运行测试并在./coverage中生成覆盖率报告e
> gulp lint                 // 执行代码检查（ESLint）
> gulp test                 // 执行代码检查并运行单元测试
> gulp docs                 // 在./dist/docs中构建文档
```

更多信息可以在[gulpfile.js](https://github.com/chartjs/Chart.js/blob/master/gulpfile.js)中找到。

# 错误和问题

请在<a href="https://github.com/chartjs/Chart.js" target="_blank">github.com/chartjs/Chart.js</a>GitHub页面上反馈。请不要将issues用于支持请求。有关使用Chart.js的帮助，请查看Stack Overflow上的[chartjs](http://stackoverflow.com/questions/tagged/chartjs)标签。

结构良好的详细错误报告对于该项目非常有价值。

报告错误指南：
 - 搜索issue以查看它是否已被反馈
 - 将问题隔离到一个简单的测试用例
 - 请在[JS Bin](http://jsbin.com/)，[JS Fiddle](http://jsfiddle.net/)或[Codepen](http://codepen.io/pen/)等网站上演示此bug。 ([模板](http://codepen.io/pen?template=JXVYzq))

请提供与错误相关的任何其他详细信息，是否是浏览器或特殊的屏幕分辨率，或只发生在特定的配置或数据。