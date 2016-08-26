---
id: getting-started
title: Getting Started <br/> 快速开始
permalink: docs/getting-started.html
next: tutorial.html
redirect_from: "docs/index.html"
---

## JSFiddle

The easiest way to start hacking on React is using the following JSFiddle Hello World examples:

<i class="icon-circle-arrow-right"></i> 
开始学习 React 最简单的方式是使用如下JSFiddle的 Hello World例子：


 * **[React JSFiddle](https://jsfiddle.net/reactjs/69z2wepo/)**
 * [React JSFiddle without JSX](https://jsfiddle.net/reactjs/5vjqabv3/)


## Starter Pack <br/> 初学者教程包

If you're just getting started, you can download the starter kit. The starter kit includes prebuilt copies of React and React DOM for the browser, as well as a collection of usage examples to help you get started.

<i class="icon-circle-arrow-right"></i> 
作为初学者，可以先使用下面的入门包(starter kit)，里头包含有 React, React DOM 以及几个入门的例子。

<div class="buttons-unit downloads">
  <a href="/react/downloads/react-{{site.react_version}}.zip" class="button">
    Download Starter Kit {{site.react_version}}
    <br/>下载入门套件 {{site.react_version}}
  </a>
</div>

In the root directory of the starter kit, create a `helloworld.html` with the following contents.

<i class="icon-circle-arrow-right"></i> 
在入门教程包的根目录，创建一个含有如下代码的 `helloworld.html`。

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>Hello React!</title>
    <script src="build/react.js"></script>
    <script src="build/react-dom.js"></script>
    <script src="https://npmcdn.com/babel-core@5.8.38/browser.min.js"></script>
  </head>
  <body>
    <div id="example"></div>
    <script type="text/babel">
      ReactDOM.render(
        <h1>Hello, world!</h1>,
        document.getElementById('example')
      );
    </script>
  </body>
</html>
```

The XML syntax inside of JavaScript is called JSX; check out the [JSX syntax](/react/docs/jsx-in-depth.html) to learn more about it. In order to translate it to vanilla JavaScript we use `<script type="text/babel">` and include Babel to actually perform the transformation in the browser. Open the html from a browser and you should already be able to see the greeting!

<i class="icon-circle-arrow-right"></i> 
在 JavaScript 代码里写着 XML 格式的代码称为 JSX；可以去 [JSX 语法](/react/docs/jsx-in-depth.html) 里学习更多 JSX 相关的知识。为了把 JSX 转成标准的 JavaScript，我们用 `<script type="text/babel">` 标签，并引入 Babel 来完成在浏览器里的代码转换。在浏览器里打开这个html，你应该可以看到成功的消息！

### Separate File <br/> 分离文件

Your React JSX code can live in a separate file. Create the following `src/helloworld.js`.

<i class="icon-circle-arrow-right"></i>
你的 React JSX 代码文件可以写在另外的文件里。新建下面的 `src/helloworld.js`。

```javascript
ReactDOM.render(
  <h1>Hello, world!</h1>,
  document.getElementById('example')
);
```

Then reference it from `helloworld.html`:

<i class="icon-circle-arrow-right"></i>
然后在 `helloworld.html` 引用该文件：

```html{10}
<script type="text/babel" src="src/helloworld.js"></script>
```

Note that some browsers (Chrome, e.g.) will fail to load the file unless it's served via HTTP.

<i class="icon-circle-arrow-right"></i>
注意一些浏览器（比如 Chrome ）会在使用 HTTP 以外的协议加载文件时失败。

## Using React with npm or Bower <br/> 通过 npm 或 Bower 来使用 React

You can also use React with package managers like npm or Bower. You can learn more in our [Package Managers](/react/docs/package-management.html) section.

<i class="icon-circle-arrow-right"></i>
还可以通过包管理器，如 npm 或 Bower 来使用 React。更多详情，请参考[包管理器](/react/docs/package-management.html) 章节的内容。

## Next Steps <br/> 下一步

Check out [the tutorial](/react/docs/tutorial.html) and the other examples in the starter kit's `examples` directory to learn more.

<i class="icon-circle-arrow-right"></i>
去看看[入门教程](/react/docs/tutorial.html) 和入门教程包 `examples` 目录下的其它例子学习更多。

Good luck, and welcome!

<i class="icon-circle-arrow-right"></i>
恭喜你，欢迎来到 React 的世界。