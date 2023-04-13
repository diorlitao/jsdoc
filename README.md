1. 安装 JSDoc
   使用 npm 安装：

```shell
npm install -g jsdoc
```

2. 注释代码
   在源代码的函数、方法、类等定义前添加注释说明其用途、参数、返回值等信息。JSDoc 注释的格式如下：

```javascript
/**
 * This is a description of what the function does.
 * @param {type} parameterName - Description of the parameter.
 * @returns {type} Description of what the function returns.
 码*/
注释中的注解说明：

@param 描述函数的参数，包括参数名和它的描述；
@returns 描述函数返回的内容；
@type 描述函数的参数或是返回值的类型；
@description 描述函数的详细说明；
@example 举例说明函数的使用方法。
```

下面是一个例子：

```javascript
/**
 * Returns the result of adding two numbers.
 * @param {number} a - The first number to add.
 * @param {number} b - The second number to add.
 * @returns {number} The sum of a and b.
 */
function addNumbers(a, b) {
  return a + b;
}
```

3. 生成文档
   在命令行中执行如下命令：

```shell
jsdoc path/to/your/javascript/files
```

其中 path/to/your/javascript/files 是你需要生成文档的 JavaScript 文件所在的目录或单个文件的路径。

生成的文档将会被存储在一个名为 out 的目录下。

如果你想将生成的文档保存到名为 doc 的目录下而不是默认的 out 目录中，你可以使用 -d 或 --destination 标志，如下所示：

```shell
 jsdoc path/to/your/javascript/files -d doc
```

将生产的文档保存到名为 doc 的目录中。

4. 查看文档
   使用浏览器打开生成的 HTML 文件：

doc/index.html
你可以在其中查看您的代码和注释。由于 JSDoc 遵循标准的注释风格，JSDoc 注释也可以作为你的源代码中的文档

5. 配置文件
   为了方便配置 JSDoc 生成文档，你可以创建一个 JSDoc 配置文件。配置文件是一个 JSON 或者 YAML 文件，它指定了生成文档的各种选项。你可以把这些选项放到配置文件中，以便 JSDoc 在生成文档时自动使用这些选项，而无需在命令行中指定这些选项。下面是一个示例配置文件 jsdoc.config.json，它具有一些常见的选项：

```json
{
  "source": {
    "include": ["src"],
    "exclude": ["src/file-to-exclude.js"],
    "includePattern": ".+\\.js(doc)?$",
    "excludePattern": "(^|\\/|\\\\)_"
  },
  "opts": {
    "destination": "./doc/",
    "recurse": true,
    "template": "node_modules/minami",
    "verbose": true
  }
}
```

其中：

source：指定要包含和排除的源文件和目录以及包含和排除它们的名称模式。
opts：指定生成文档的属性，例如输出目录、模板、是否递归等。
有了配置文件，你就可以在命令行中使用以下命令来生成文档：

```shell
jsdoc -c path/to/config/file/jsdoc.config.json
```

它告诉 JSDoc 使用 jsdoc.config.json 文件中的选项来生成文档。

如果您在 opts 中设置了 template 属性，那么您需要安装该模板。模板用于组织和美化您生成的文档，因此至少应该使用一个模板来增强您的文档的可读性和可用性。JSDoc 包含一些默认模板以供您使用，但也可通过模板网站找到自定义模板。

要安装模板，请在命令行中使用以下命令：

```shell
npm install <template-name>
```

例如，如果您想使用名为 'minami' 的模板，则应使用以下命令：

```shell
npm install minami
```

安装完成后，在配置文件中设置 template 属性：

```json
"opts": {
    "template": "node_modules/minami"
}
```

接着，再次运行 JSDoc 命令来生成文档，JSDoc 将会使用您指定的模板生成一份美观、易读的文档。

运行打包会报错
Cannot find module 'taffydb' 错误可能是因为 minami 模板依赖于 TaffyDB，但它没有自动安装。

你可以像下面这样手动安装 TaffyDB：

```shell
npm install taffydb
```

然后重新运行 JSDoc 命令：

```shell
jsdoc your_sourcecode.js -t node_modules/minami -d doc
```

注意，在命令行中指定了使用 -t 标志来指定模板的路径，node_modules/minami 是 minami 模板在 node_modules 目录中的路径。

之后，JSDoc 就会使用指定的模板并顺利生成文档。

除了 minami 模板以外，还有以下一些常见的 JSDoc 模板：

jsdoc-default-template：这是默认的 JSDoc 模板，它是一个简单的、基本的模板。

docdash：一个流行的、美观的模板，文档风格类似于 dash API。

docstrap：此模板在 Bootstrap 框架上的基础上构建，提供了丰富的自定义选项和风格。

ink-docstrap：docstrap 的一个修改版本，使用较少的依赖项和自定义样式表。

tui-jsdoc-template：一个显示清晰且具有样式引导的简单模板。

请注意，每个模板都有自己的特点和使用方式，并且可能需要某些依赖项。在选择模板时要仔细考虑，并确保它们符合您的需求和技术栈，并支持您使用的 JSDoc 版本。
