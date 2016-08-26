---
id: tutorial
title: Tutorial <br/> 教程
permalink: docs/tutorial.html
prev: getting-started.html
next: thinking-in-react.html
---

We'll be building a simple but realistic comments box that you can drop into a blog, a basic version of the realtime comments offered by Disqus, LiveFyre or Facebook comments.

<i class="icon-circle-arrow-right"></i> 
我们将建立一个你可以放进博客的简单却真实的评论框，一个 Disqus、LiveFyre 或 Facebook comments 提供的实时评论的基础版本。

We'll provide:

<i class="icon-circle-arrow-right"></i> 
我们将提供：

* A view of all of the comments
* 一个所有评论的视图
* A form to submit a comment
* 一个用于提交评论的表单
* Hooks for you to provide a custom backend
* 为你提供制定后台的挂钩(Hooks)


It'll also have a few neat features:

<i class="icon-circle-arrow-right"></i> 
同时也会有一些简洁的功能：

* **Optimistic commenting:** comments appear in the list before they're saved on the server so it feels fast.
* **优化的评论：** 评论在它们保存到服务器之前就显示在列表里,所以感觉很快。
* **Live updates:** other users' comments are popped into the comment view in real time.
* **实时更新：** 其他用户的评论被实时浮现到评论中。
* **Markdown formatting:** users can use Markdown to format their text.
* **Markdown格式化：** 用户可以用Markdown格式化它们的文字。

### Want to skip all this and just see the source?
### 想要跳过所有内容，只查看源代码？

[It's all on GitHub.](https://github.com/reactjs/react-tutorial)

<i class="icon-circle-arrow-right"></i>
[全在 GitHub .](https://github.com/reactjs/react-tutorial)

### Running a server
### 运行服务器

In order to start this tutorial, we're going to require a running server. This will serve purely as an API endpoint which we'll use for getting and saving data. In order to make this as easy as possible, we've created a simple server in a number of scripting languages that does exactly what we need it to do. **You can [view the source](https://github.com/reactjs/react-tutorial/) or [download a zip file](https://github.com/reactjs/react-tutorial/archive/master.zip) containing everything needed to get started.**

<i class="icon-circle-arrow-right"></i> 
为了开始本教程，我们将要需要一个运行着的服务器。这将是我们纯粹用来获取和保存数据的伺服终端。为了让这尽可能的容易，我们已经用许多不同的语言编写了简单的服务器，它正好完成我们需要的事。    **你可以[查看源代码](https://github.com/reactjs/react-tutorial/) 或者 [下载 zip 文件](https://github.com/reactjs/react-tutorial/archive/master.zip) 包括了所有你开始学习需要的东西**

For sake of simplicity, the server we will run uses a `JSON` file as a database. You would not run this in production but it makes it easy to simulate what you might do when consuming an API. Once you [start the server](https://github.com/reactjs/react-tutorial/#to-use), it will support our API endpoint and it will also serve the static pages we need.

<i class="icon-circle-arrow-right"></i> 
为了简单起见，我们将要运行的服务器使用 `JSON` 文件作为数据库。你不会在生产环境运行这个，但是它让我们更容易模拟使用一个API时你可能会做的事。一旦你启动服务器，它将会支持我们的API终端,同时也将伺服我们需要的静态页面。

### Getting started
### 开始

For this tutorial, we're going to make it as easy as possible. Included in the server package discussed above is an HTML file which we'll work in. Open up `public/index.html` in your favorite editor. It should look something like this:

<i class="icon-circle-arrow-right"></i> 
对于此教程,我们将使它尽可能的容易。被包括在上面讨论的服务器包里的是一个我们将在其中工作的 HTML 文件。在你最喜欢的编辑器里打开 `public/index.html`。它应该看起来像这样 （可能有一些小的不同，稍后我们将添加一个额外的 `<script>` 标签）：

```html
<!-- index.html -->
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>React Tutorial</title>
    <script src="https://npmcdn.com/react@{{site.react_version}}/dist/react.js"></script>
    <script src="https://npmcdn.com/react-dom@{{site.react_version}}/dist/react-dom.js"></script>
    <script src="https://npmcdn.com/babel-core@5.8.38/browser.min.js"></script>
    <script src="https://npmcdn.com/jquery@3.1.0/dist/jquery.min.js"></script>
    <script src="https://npmcdn.com/remarkable@1.6.2/dist/remarkable.min.js"></script>
  </head>
  <body>
    <div id="content"></div>
    <script type="text/babel" src="scripts/example.js"></script>
    <script type="text/babel">
      // To get started with this tutorial running your own code, simply remove
      // the script tag loading scripts/example.js and start writing code here.
    </script>
  </body>
</html>
```

For the remainder of this tutorial, we'll be writing our JavaScript code in this script tag. We don't have any advanced live-reloading so you'll need to refresh your browser to see updates after saving. Follow your progress by opening `http://localhost:3000` in your browser (after starting the server). When you load this for the first time without any changes, you'll see the finished product of what we're going to build. When you're ready to start working, just delete the preceding `<script>` tag and then you can continue.

<i class="icon-circle-arrow-right"></i> 
在本教程剩余的部分，我们将在此 script 标签中编写我们的 JavaScript 代码。我们没有任何高级的实时加载，所以在保存以后你需要手动刷新浏览器来观察更新。通过在浏览器打开 `http://localhost:3000` 关注你的进展。当你没有任何修改第一次加载时，你将看到我们将要准备建立的已经完成的产品。当你准备开始工作，请删除前面的 `<script>` 标签然后你就可以继续了。

> Note:
> 注意：
>
> We included jQuery here because we want to simplify the code of our future AJAX calls, but it's **NOT** mandatory for React to work.
> 
> <i class="icon-circle-arrow-right"></i>
> 我们在这里引入 jQuery 是因为我们想简化我们未来的 ajax 请求，但这对 React 的正常工作 **不是** 必要的。

### Your first component
### 你的第一个组件

React is all about modular, composable components. For our comment box example, we'll have the following component structure:

<i class="icon-circle-arrow-right"></i> 
React 中都是一系列的模块化、可组装的组件。以我们的评论框为例，我们将有如下的组件结构：

```
- CommentBox
  |- CommentList
  |   |- Comment
  |- CommentForm
```

Let's build the `CommentBox` component, which is just a simple `<div>`:

<i class="icon-circle-arrow-right"></i> 
让我们构造 `CommentBox` 组件，仅是一个简单的 `<div>` ：

```javascript
// tutorial1.js
var CommentBox = React.createClass({
  render: function() {
    return (
      <div className="commentBox">
        Hello, world! I am a CommentBox.
      </div>
    );
  }
});
ReactDOM.render(
  <CommentBox />,
  document.getElementById('content')
);
```

Note that native HTML element names start with a lowercase letter, while custom React class names begin with an uppercase letter.

<i class="icon-circle-arrow-right"></i> 
注意原生的HTML元素以小写开头，而自定义的 React 类以大写开头。

#### JSX Syntax
#### JSX 语法

The first thing you'll notice is the XML-ish syntax in your JavaScript. We have a simple precompiler that translates the syntactic sugar to this plain JavaScript:

<i class="icon-circle-arrow-right"></i> 
首先你会注意到你的 JavaScript 中 XML 式的语法。我们有一个简单的预编译器，将语法糖转换成这种纯的JavaScript：

```javascript
// tutorial1-raw.js
var CommentBox = React.createClass({displayName: 'CommentBox',
  render: function() {
    return (
      React.createElement('div', {className: "commentBox"},
        "Hello, world! I am a CommentBox."
      )
    );
  }
});
ReactDOM.render(
  React.createElement(CommentBox, null),
  document.getElementById('content')
);
```

Its use is optional but we've found JSX syntax easier to use than plain JavaScript. Read more on the [JSX Syntax article](/react/docs/jsx-in-depth.html).

<i class="icon-circle-arrow-right"></i> 
它的使用是可选的，但是我们发现 JSX 语法比单纯的 JavaScript 更加容易使用。阅读更多关于[JSX 语法的文章](/react/docs/jsx-in-depth-zh-CN.html)。

#### What's going on
#### 发生了什么

We pass some methods in a JavaScript object to `React.createClass()` to create a new React component. The most important of these methods is called `render` which returns a tree of React components that will eventually render to HTML.

<i class="icon-circle-arrow-right"></i> 
我们在一个 JavaScript 对象中传递一些方法到 `React.createClass()` 来创建一个新的React组件。这些方法中最重要的是 `render`，该方法返回一颗 React 组件树，这棵树最终将会渲染成 HTML。

The `<div>` tags are not actual DOM nodes; they are instantiations of React `div` components. You can think of these as markers or pieces of data that React knows how to handle. React is **safe**. We are not generating HTML strings so XSS protection is the default.

<i class="icon-circle-arrow-right"></i> 
这个 `<div>` 标签不是真实的DOM节点；他们是 React `div` 组件的实例化。你可以把这些看做是React知道如何处理的标记或者是一些数据 。React 是**安全的**。我们不生成 HTML 字符串，因此默认具有 XSS 防护的特性。

You do not have to return basic HTML. You can return a tree of components that you (or someone else) built. This is what makes React **composable**: a key tenet of maintainable frontends.

<i class="icon-circle-arrow-right"></i> 
你没有必要返回基本的 HTML。你可以返回一个你（或者其他人）创建的组件树。从而实现了 React 的**组件化**：一个可维护前端的关键原则。

`ReactDOM.render()` instantiates the root component, starts the framework, and injects the markup into a raw DOM element, provided as the second argument.

<i class="icon-circle-arrow-right"></i> 
`ReactDOM.render()` 实例化根组件，启动框架，根据第二个参数提供的值，将标记注入到原始的 DOM 元素中。

The `ReactDOM` module exposes DOM-specific methods, while `React` has the core tools shared by React on different platforms (e.g., [React Native](http://facebook.github.io/react-native/)).

<i class="icon-circle-arrow-right"></i> 
`ReactDOM` 模块暴露了 DOM 相关的方法， 而 `React` 具有被不同平台的 React 共享的核心工具 （例如 [React Native](http://facebook.github.io/react-native/)）。

It is important that `ReactDOM.render` remain at the bottom of the script for this tutorial. `ReactDOM.render` should only be called after the composite components have been defined.

<i class="icon-circle-arrow-right"></i> 
在本教程中， `ReactDOM.render` 保持在脚本底部是很重要的。`ReactDOM.render` 应该只在复合组件被定义之后再被调用。

## Composing components
## 组合组件

Let's build skeletons for `CommentList` and `CommentForm` which will, again, be simple `<div>`s. Add these two components to your file, keeping the existing `CommentBox` declaration and `ReactDOM.render` call:

<i class="icon-circle-arrow-right"></i> 
让我们开始构建 `CommentList` 和 `CommentForm` ，它们将会，再一次的，是一些简单的 `<div>`。添加这两个组件到你的文件里，保持现存的 `CommentBox` 声明和 `ReactDOM.render` 调用:

```javascript
// tutorial2.js
var CommentList = React.createClass({
  render: function() {
    return (
      <div className="commentList">
        Hello, world! I am a CommentList.
      </div>
    );
  }
});

var CommentForm = React.createClass({
  render: function() {
    return (
      <div className="commentForm">
        Hello, world! I am a CommentForm.
      </div>
    );
  }
});
```

Next, update the `CommentBox` component to use these new components:

<i class="icon-circle-arrow-right"></i> 
接着，更新 `CommentBox` 以使用这些新的组件：

```javascript{6-8}
// tutorial3.js
var CommentBox = React.createClass({
  render: function() {
    return (
      <div className="commentBox">
        <h1>Comments</h1>
        <CommentList />
        <CommentForm />
      </div>
    );
  }
});
```

Notice how we're mixing HTML tags and components we've built. HTML components are regular React components, just like the ones you define, with one difference. The JSX compiler will automatically rewrite HTML tags to `React.createElement(tagName)` expressions and leave everything else alone. This is to prevent the pollution of the global namespace.

<i class="icon-circle-arrow-right"></i> 
注意我们是如何混合 HTML 标签和我们建立的组件。HTML 组件是正常的 React 组件，就和你定义的一样，只有一个区别。JSX 编译器会自动重写 HTML 标签为 `React.createElement(tagName)` 表达式，其它什么都不做。这是为了避免污染全局命名空间。

### Using props
### 使用 props

Let's create the `Comment` component, which will depend on data passed in from its parent. Data passed in from a parent component is available as a 'property' on the child component. These 'properties' are accessed through `this.props`. Using props, we will be able to read the data passed to the `Comment` from the `CommentList`, and render some markup:

<i class="icon-circle-arrow-right"></i> 
让我们创建 `Comment` 组件，它将依赖于从父级传来的数据。从父级传来的数据在子组件里作为 '属性' 可供使用。 这些 '属性' 可以通过 `this.props` 访问。使用属性，我们将能读取从 `CommentList` 传递给 `Comment` 的数据，并且渲染一些标记：

```javascript
// tutorial4.js
var Comment = React.createClass({
  render: function() {
    return (
      <div className="comment">
        <h2 className="commentAuthor">
          {this.props.author}
        </h2>
        {this.props.children}
      </div>
    );
  }
});
```

By surrounding a JavaScript expression in braces inside JSX (as either an attribute or child), you can drop text or React components into the tree. We access named attributes passed to the component as keys on `this.props` and any nested elements as `this.props.children`.

<i class="icon-circle-arrow-right"></i> 
在 JSX 中,通过将 JavaScript 表达式放在大括号中（作为属性或者子节点）,你可以把文本或者 React 组件放置到树中。我们以 `this.props` 的 keys 访问传递给组件的命名属性，以 `this.props.children` 访问任何嵌套的元素。

### Component Properties
### 组件的属性

Now that we have defined the `Comment` component, we will want to pass it the author name and comment text. This allows us to reuse the same code for each unique comment. Now let's add some comments within our `CommentList`:

<i class="icon-circle-arrow-right"></i> 
既然我们已经定义了 `Comment` 组件，我们将要传递作者名和评论文字给它。这允许我们为每个评论重用相同的代码。现在让我们在我们的 `CommentList` 里添加一些评论。

```javascript{6-7}
// tutorial5.js
var CommentList = React.createClass({
  render: function() {
    return (
      <div className="commentList">
        <Comment author="Pete Hunt">This is one comment</Comment>
        <Comment author="Jordan Walke">This is *another* comment</Comment>
      </div>
    );
  }
});
```

Note that we have passed some data from the parent `CommentList` component to the child `Comment` components. For example, we passed *Pete Hunt* (via an attribute) and *This is one comment* (via an XML-like child node) to the first `Comment`. As noted above, the `Comment` component will access these 'properties' through `this.props.author`, and `this.props.children`.

<i class="icon-circle-arrow-right"></i> 
注意，我们已经从 `CommentList`  组件传递了一些数据到 `Comment` 组件。例如，我们传递了 *Pete Hunt* （通过属性）和 *This is one comment* (通过 XML-风格的子节点)给第一个 `Comment`。如上面提到的那样， `Comment` 组件将会通过 `this.props.author` 和 `this.props.children` 访问 这些 '属性'。

### Adding Markdown
### 添加 Markdown

Markdown is a simple way to format your text inline. For example, surrounding text with asterisks will make it emphasized.

<i class="icon-circle-arrow-right"></i> 
Markdown 是一种简单的内联格式化你的文字的方法。例如，用星号包围文本将会使其强调突出。

In this tutorial we use a third-party library **remarkable** which takes Markdown text and converts it to raw HTML. We already included this library with the original markup for the page, so we can just start using it. Let's convert the comment text to Markdown and output it:

<i class="icon-circle-arrow-right"></i> 
在本教程中我们使用第三方库 **remarkable**，它接受 Markdown 文本并且转换为原始的 HTML。我们已经在初始的页面标记里包含了这个库，所以我们可以直接开始使用它，让我们转换评论文本为 Markdown 并输出它：

```javascript{4,10}
// tutorial6.js
var Comment = React.createClass({
  render: function() {
    var md = new Remarkable();
    return (
      <div className="comment">
        <h2 className="commentAuthor">
          {this.props.author}
        </h2>
        {md.render(this.props.children.toString())}
      </div>
    );
  }
});
```

All we're doing here is calling the remarkable library. We need to convert `this.props.children` from React's wrapped text to a raw string that remarkable will understand so we explicitly call `toString()`.

<i class="icon-circle-arrow-right"></i> 
我们在这里唯一做的就是调用 remarkable 库。我们需要把 从 React 的包裹文本来的 `this.props.children` 转换成 remarkable 能理解的原始字符串，所以我们显示地调用了`toString()`。

But there's a problem! Our rendered comments look like this in the browser: "`<p>`This is `<em>`another`</em>` comment`</p>`". We want those tags to actually render as HTML.

<i class="icon-circle-arrow-right"></i> 
但是这里有一个问题！我们渲染的评论在浏览器里看起来像这样： "`<p>`This is `<em>`another`</em>` comment`</p>`" 。我们想让这些标签真正地渲染为 HTML。

That's React protecting you from an [XSS attack](https://en.wikipedia.org/wiki/Cross-site_scripting). There's a way to get around it but the framework warns you not to use it:

<i class="icon-circle-arrow-right"></i> 
那是 React 在保护你免受 [XSS 攻击](https://en.wikipedia.org/wiki/Cross-site_scripting)。有一个方法解决这个问题，但是框架会警告你别使用这种方法：

```javascript{3-7,15}
// tutorial7.js
var Comment = React.createClass({
  rawMarkup: function() {
    var md = new Remarkable();
    var rawMarkup = md.render(this.props.children.toString());
    return { __html: rawMarkup };
  },

  render: function() {
    return (
      <div className="comment">
        <h2 className="commentAuthor">
          {this.props.author}
        </h2>
        <span dangerouslySetInnerHTML={this.rawMarkup()} />
      </div>
    );
  }
});
```

This is a special API that intentionally makes it difficult to insert raw HTML, but for remarkable we'll take advantage of this backdoor.

<i class="icon-circle-arrow-right"></i> 
这是一个特殊的 API，故意让插入原始的 HTML 变得困难，但是对于 remarkable 我们将利用这个后门。

**Remember:** by using this feature you're relying on remarkable to be secure. In this case, remarkable automatically strips HTML markup and insecure links from the output.

<i class="icon-circle-arrow-right"></i> 
**记住：** 使用这个功能你会依赖于 remarkable 是安全的。

### Hook up the data model
### 挂钩数据模型

So far we've been inserting the comments directly in the source code. Instead, let's render a blob of JSON data into the comment list. Eventually this will come from the server, but for now, write it in your source:

<i class="icon-circle-arrow-right"></i> 
到目前为止我们已经完成了在源码里直接插入评论。作为替代，让我们渲染一团 JSON 数据到评论列表里。最终数据将会来自服务器，但是现在，写在你的源代码中：

```javascript
// tutorial8.js
var data = [
  {id: 1, author: "Pete Hunt", text: "This is one comment"},
  {id: 2, author: "Jordan Walke", text: "This is *another* comment"}
];
```

We need to get this data into `CommentList` in a modular way. Modify `CommentBox` and the `ReactDOM.render()` call to pass this data into the `CommentList` via props:

<i class="icon-circle-arrow-right"></i> 
我们需要以一种模块化的方式将这个数据传入到 `CommentList`。修改 `CommentBox` 和 `ReactDOM.render()` 方法，以便于通过 props 传入数据到 `CommentList`：

```javascript{7,15}
// tutorial9.js
var CommentBox = React.createClass({
  render: function() {
    return (
      <div className="commentBox">
        <h1>Comments</h1>
        <CommentList data={this.props.data} />
        <CommentForm />
      </div>
    );
  }
});

ReactDOM.render(
  <CommentBox data={data} />,
  document.getElementById('content')
);
```

Now that the data is available in the `CommentList`, let's render the comments dynamically:

<i class="icon-circle-arrow-right"></i> 
既然现在数据在 `CommentList` 中可用了，让我们动态地渲染评论：

```javascript{4-10,13}
// tutorial10.js
var CommentList = React.createClass({
  render: function() {
    var commentNodes = this.props.data.map(function(comment) {
      return (
        <Comment author={comment.author} key={comment.id}>
          {comment.text}
        </Comment>
      );
    });
    return (
      <div className="commentList">
        {commentNodes}
      </div>
    );
  }
});
```

That's it!

<i class="icon-circle-arrow-right"></i> 
好了，就这些！

### Fetching from the server
### 从服务器获取数据

Let's replace the hard-coded data with some dynamic data from the server. We will remove the data prop and replace it with a URL to fetch:

<i class="icon-circle-arrow-right"></i> 
让我们用一些来自服务器的动态数据替换硬编码的数据。我们将移除数据的prop，用获取数据的URL来替换它：

```javascript{3}
// tutorial11.js
ReactDOM.render(
  <CommentBox url="/api/comments" />,
  document.getElementById('content')
);
```

This component is different from the prior components because it will have to re-render itself. The component won't have any data until the request from the server comes back, at which point the component may need to render some new comments.

<i class="icon-circle-arrow-right"></i> 
这个组件不同于和前面的组件，因为它必须重新渲染自己。该组件将不会有任何数据，直到请求从服务器返回，此时该组件或许需要渲染一些新的评论。

Note: the code will not be working at this step.

<i class="icon-circle-arrow-right"></i> 
注意： 此代码在这个阶段不会工作。

### Reactive state
### 可变的 state

So far, based on its props, each component has rendered itself once. `props` are immutable: they are passed from the parent and are "owned" by the parent. To implement interactions, we introduce mutable **state** to the component. `this.state` is private to the component and can be changed by calling `this.setState()`. When the state updates, the component re-renders itself.

<i class="icon-circle-arrow-right"></i> 
迄今为止,基于它自己的props，每个组件都渲染了自己一次。`props` 是不可变的：它们从父级传来并被父级“拥有”。为了实现交互，我们给组件引进了可变的 **state**。`this.state` 是组件私有的，可以通过调用 `this.setState()` 改变它。每当state更新，组件就重新渲染自己。

`render()` methods are written declaratively as functions of `this.props` and `this.state`. The framework guarantees the UI is always consistent with the inputs.

<i class="icon-circle-arrow-right"></i> 
`render()` 方法被声明为一个带有 `this.props` 和 `this.state` 的函数。框架保证了 UI 总是与输入一致。

When the server fetches data, we will be changing the comment data we have. Let's add an array of comment data to the `CommentBox` component as its state:

<i class="icon-circle-arrow-right"></i> 
当服务器获取数据时，我们将会改变我们已有的评论数据。让我们给 `CommentBox` 组件添加一组评论数据作为它的状态：

```javascript{3-5,10}
// tutorial12.js
var CommentBox = React.createClass({
  getInitialState: function() {
    return {data: []};
  },
  render: function() {
    return (
      <div className="commentBox">
        <h1>Comments</h1>
        <CommentList data={this.state.data} />
        <CommentForm />
      </div>
    );
  }
});
```

`getInitialState()` executes exactly once during the lifecycle of the component and sets up the initial state of the component.

<i class="icon-circle-arrow-right"></i> 
`getInitialState()` 在生命周期里只执行一次，并设置组件的初始状态。

#### Updating state
#### 更新状态

When the component is first created, we want to GET some JSON from the server and update the state to reflect the latest data. We're going to use jQuery to make an asynchronous request to the server we started earlier to fetch the data we need. The data is already included in the server you started (based on the `comments.json` file), so once it's fetched, `this.state.data` will look something like this:

<i class="icon-circle-arrow-right"></i> 
当组件第一次创建时，我们想从服务器获取一些 JSON 并且更新状态以反映最新的数据。我们将用 jQuery 来发送一个异步请求到我们刚才启动的服务器以获取我们需要的数据。这些数据已经被包含在了你已启动的服务器里（基于`comments.json`文件），所以一旦被获取，`this.state.data` 会看起来像这样：

```json
[
  {"id": "1", "author": "Pete Hunt", "text": "This is one comment"},
  {"id": "2", "author": "Jordan Walke", "text": "This is *another* comment"}
]
```

```javascript{6-18}
// tutorial13.js
var CommentBox = React.createClass({
  getInitialState: function() {
    return {data: []};
  },
  componentDidMount: function() {
    $.ajax({
      url: this.props.url,
      dataType: 'json',
      cache: false,
      success: function(data) {
        this.setState({data: data});
      }.bind(this),
      error: function(xhr, status, err) {
        console.error(this.props.url, status, err.toString());
      }.bind(this)
    });
  },
  render: function() {
    return (
      <div className="commentBox">
        <h1>Comments</h1>
        <CommentList data={this.state.data} />
        <CommentForm />
      </div>
    );
  }
});
```

Here, `componentDidMount` is a method called automatically by React after a component is rendered for the first time. The key to dynamic updates is the call to `this.setState()`. We replace the old array of comments with the new one from the server and the UI automatically updates itself. Because of this reactivity, it is only a minor change to add live updates. We will use simple polling here but you could easily use WebSockets or other technologies.

<i class="icon-circle-arrow-right"></i> 
这里， `componentDidMount` 是一个当组件被渲染时被Ｒeact自动调用的方法。动态更新的关键是对 `this.setState()` 的调用。我们用新的从服务器来的替换掉旧的评论组，然后UI自动更新自己。因为这种反应性，仅是一个微小的变化就添加了实时更新。我们这里将用简单的轮询，但是你可以容易的使用 WebSockets 或者其他技术。

```javascript{3,15,20-21,35}
// tutorial14.js
var CommentBox = React.createClass({
  loadCommentsFromServer: function() {
    $.ajax({
      url: this.props.url,
      dataType: 'json',
      cache: false,
      success: function(data) {
        this.setState({data: data});
      }.bind(this),
      error: function(xhr, status, err) {
        console.error(this.props.url, status, err.toString());
      }.bind(this)
    });
  },
  getInitialState: function() {
    return {data: []};
  },
  componentDidMount: function() {
    this.loadCommentsFromServer();
    setInterval(this.loadCommentsFromServer, this.props.pollInterval);
  },
  render: function() {
    return (
      <div className="commentBox">
        <h1>Comments</h1>
        <CommentList data={this.state.data} />
        <CommentForm />
      </div>
    );
  }
});

ReactDOM.render(
  <CommentBox url="/api/comments" pollInterval={2000} />,
  document.getElementById('content')
);

```

All we have done here is move the AJAX call to a separate method and call it when the component is first loaded and every 2 seconds after that. Try running this in your browser and changing the `comments.json` file (in the same directory as your server); within 2 seconds, the changes will show!

<i class="icon-circle-arrow-right"></i> 
我们在这里做的全部事情是把 AJAX 调用移动到独立的方法里，然后在组件第一次加载时及其后每2秒 调用它。试着在你的浏览器里运行它并且改变 `comments.json` 文件（在你的服务器的相同目录）；2秒内，变化将会显现！

### Adding new comments
### 添加新评论

Now it's time to build the form. Our `CommentForm` component should ask the user for their name and comment text and send a request to the server to save the comment.

<i class="icon-circle-arrow-right"></i> 
现在是时候建立表单了，我们的 `CommentForm` 组件应该询问用户他们的名字和评论文本然后发送一个请求到服务器来保存评论.

```javascript{5-9}
// tutorial15.js
var CommentForm = React.createClass({
  render: function() {
    return (
      <form className="commentForm">
        <input type="text" placeholder="Your name" />
        <input type="text" placeholder="Say something..." />
        <input type="submit" value="Post" />
      </form>
    );
  }
});
```

#### Controlled components
#### 受控组件

With the traditional DOM, `input` elements are rendered and the browser manages the state (its rendered value). As a result, the state of the actual DOM will differ from that of the component. This is not ideal as the state of the view will differ from that of the component. In React, components should always represent the state of the view and not only at the point of initialization.

<i class="icon-circle-arrow-right"></i> 
对于传统的 DOM， `input` 元素被渲染并且浏览器管理它的状态（它的渲染值）。结果是，DOM的实际值会和组件不同。这是不理想的，因为视图的值会和组件的值不同。在React中，组件应该总是表示视图的值而不只是在初始化时。

Hence, we will be using `this.state` to save the user's input as it is entered. We define an initial `state` with two properties `author` and `text` and set them to be empty strings. In our `<input>` elements, we set the `value` prop to reflect the `state` of the component and attach `onChange` handlers to them. These `<input>` elements with a `value` set are called controlled components. Read more about controlled components on the [Forms article](/react/docs/forms.html#controlled-components).

<i class="icon-circle-arrow-right"></i> 
因此，我们将使用 `this.state` 来在用户输入时保存输入。我们定义一个初始 `state`，它带有 `author` 和 `text` 两个属性并将他们设置为空字符串。在我们的 `<input>` 元素里，我们设置 `value` prop 来反映组件的 `state` 并给他们附加 `onChange` 事件处理。这些带有设置了 `value` 的  `<input>` 元素被称为受控组件。更多关于受控组件请阅读 [Forms article](/react/docs/forms.html#controlled-components)。

```javascript{3-11,15-26}
// tutorial16.js
var CommentForm = React.createClass({
  getInitialState: function() {
    return {author: '', text: ''};
  },
  handleAuthorChange: function(e) {
    this.setState({author: e.target.value});
  },
  handleTextChange: function(e) {
    this.setState({text: e.target.value});
  },
  render: function() {
    return (
      <form className="commentForm">
        <input
          type="text"
          placeholder="Your name"
          value={this.state.author}
          onChange={this.handleAuthorChange}
        />
        <input
          type="text"
          placeholder="Say something..."
          value={this.state.text}
          onChange={this.handleTextChange}
        />
        <input type="submit" value="Post" />
      </form>
    );
  }
});
```

#### Events
#### 事件

React attaches event handlers to components using a camelCase naming convention. We attach `onChange` handlers to the two `<input>` elements. Now, as the user enters text into the `<input>` fields, the attached `onChange` callbacks are fired and the `state` of the component is modified. Subsequently, the rendered value of the `input` element will be updated to reflect the current component `state`.

<i class="icon-circle-arrow-right"></i> 
React使用小驼峰命名规范(camelCase)给组件绑定事件处理器。我们附加 `onChange` 给两个 `<input>` 元素。现在，当用户输入文本到 `<input>` 中，被附加的 `onChange` 回调函数被激发并且组件的 `state` 被修改。然后，被渲染的 `input` 元素的值将会更新以反映当前组件的 `state`。

(The astute reader may be surprised that these event handlers work as described, given that the method references are not explicitly bound to `this`. `React.createClass(...)` [automatically binds](/react/docs/interactivity-and-dynamic-uis.html#under-the-hood-autobinding-and-event-delegation) each method to its component instance, obviating the need for explicit binding.)

#### Submitting the form
#### 提交表单

Let's make the form interactive. When the user submits the form, we should clear it, submit a request to the server, and refresh the list of comments. To start, let's listen for the form's submit event and clear it.

<i class="icon-circle-arrow-right"></i> 
让我们使表单具有交互性。当用户提交表单时，我们应该清除它，提交一个请求到服务器，并刷新评论列表。让我们监听表单的提交事件并清除它。

```javascript{12-21,24}
// tutorial17.js
var CommentForm = React.createClass({
  getInitialState: function() {
    return {author: '', text: ''};
  },
  handleAuthorChange: function(e) {
    this.setState({author: e.target.value});
  },
  handleTextChange: function(e) {
    this.setState({text: e.target.value});
  },
  handleSubmit: function(e) {
    e.preventDefault();
    var author = this.state.author.trim();
    var text = this.state.text.trim();
    if (!text || !author) {
      return;
    }
    // TODO: send request to the server
    this.setState({author: '', text: ''});
  },
  render: function() {
    return (
      <form className="commentForm" onSubmit={this.handleSubmit}>
        <input
          type="text"
          placeholder="Your name"
          value={this.state.author}
          onChange={this.handleAuthorChange}
        />
        <input
          type="text"
          placeholder="Say something..."
          value={this.state.text}
          onChange={this.handleTextChange}
        />
        <input type="submit" value="Post" />
      </form>
    );
  }
});
```

We attach an `onSubmit` handler to the form that clears the form fields when the form is submitted with valid input.

<i class="icon-circle-arrow-right"></i> 
我们给表单绑定一个`onSubmit`处理器，它在表单提交了合法的输入后清空表单字段。

Call `preventDefault()` on the event to prevent the browser's default action of submitting the form.

<i class="icon-circle-arrow-right"></i> 
在事件中调用`preventDefault()`来阻止浏览器提交表单的默认行为。

#### Callbacks as props
#### 回调函数作为属性

When a user submits a comment, we will need to refresh the list of comments to include the new one. It makes sense to do all of this logic in `CommentBox` since `CommentBox` owns the state that represents the list of comments.

<i class="icon-circle-arrow-right"></i> 
当用户提交评论时，我们需要刷新评论列表来包含这条新评论。在`CommentBox`中完成所有逻辑是有道理的，因为`CommentBox` 拥有代表了评论列表的状态(state)。

We need to pass data from the child component back up to its parent. We do this in our parent's `render` method by passing a new callback (`handleCommentSubmit`) into the child, binding it to the child's `onCommentSubmit` event. Whenever the event is triggered, the callback will be invoked:

<i class="icon-circle-arrow-right"></i> 
我们需要从子组件传回数据到它的父组件。我们在父组件的`render`方法中以传递一个新的回调函数（`handleCommentSubmit`）到子组件完成这件事，绑定它到子组件的 `onCommentSubmit` 事件上。无论事件什么时候触发，回调函数都将被调用：

```javascript{16-18,31}
// tutorial18.js
var CommentBox = React.createClass({
  loadCommentsFromServer: function() {
    $.ajax({
      url: this.props.url,
      dataType: 'json',
      cache: false,
      success: function(data) {
        this.setState({data: data});
      }.bind(this),
      error: function(xhr, status, err) {
        console.error(this.props.url, status, err.toString());
      }.bind(this)
    });
  },
  handleCommentSubmit: function(comment) {
    // TODO: submit to the server and refresh the list
  },
  getInitialState: function() {
    return {data: []};
  },
  componentDidMount: function() {
    this.loadCommentsFromServer();
    setInterval(this.loadCommentsFromServer, this.props.pollInterval);
  },
  render: function() {
    return (
      <div className="commentBox">
        <h1>Comments</h1>
        <CommentList data={this.state.data} />
        <CommentForm onCommentSubmit={this.handleCommentSubmit} />
      </div>
    );
  }
});
```

Now that `CommentBox` has made the callback available to `CommentForm` via the `onCommentSubmit` prop, the `CommentForm` can call the callback when the user submits the form:

<i class="icon-circle-arrow-right"></i> 
既然 `CommentBox` 已经通过 `onCommentSubmit` prop 使回调函数对于 `CommentForm` 可用，`CommentForm` 就可以在用户提交表单时调用回调函数：

```javascript{19}
// tutorial19.js
var CommentForm = React.createClass({
  getInitialState: function() {
    return {author: '', text: ''};
  },
  handleAuthorChange: function(e) {
    this.setState({author: e.target.value});
  },
  handleTextChange: function(e) {
    this.setState({text: e.target.value});
  },
  handleSubmit: function(e) {
    e.preventDefault();
    var author = this.state.author.trim();
    var text = this.state.text.trim();
    if (!text || !author) {
      return;
    }
    this.props.onCommentSubmit({author: author, text: text});
    this.setState({author: '', text: ''});
  },
  render: function() {
    return (
      <form className="commentForm" onSubmit={this.handleSubmit}>
        <input
          type="text"
          placeholder="Your name"
          value={this.state.author}
          onChange={this.handleAuthorChange}
        />
        <input
          type="text"
          placeholder="Say something..."
          value={this.state.text}
          onChange={this.handleTextChange}
        />
        <input type="submit" value="Post" />
      </form>
    );
  }
});
```

Now that the callbacks are in place, all we have to do is submit to the server and refresh the list:

<i class="icon-circle-arrow-right"></i> 
既然现在回调函数已经就绪，我们所需要做的就是提交到服务器然后刷新列表：

```javascript{17-28}
// tutorial20.js
var CommentBox = React.createClass({
  loadCommentsFromServer: function() {
    $.ajax({
      url: this.props.url,
      dataType: 'json',
      cache: false,
      success: function(data) {
        this.setState({data: data});
      }.bind(this),
      error: function(xhr, status, err) {
        console.error(this.props.url, status, err.toString());
      }.bind(this)
    });
  },
  handleCommentSubmit: function(comment) {
    $.ajax({
      url: this.props.url,
      dataType: 'json',
      type: 'POST',
      data: comment,
      success: function(data) {
        this.setState({data: data});
      }.bind(this),
      error: function(xhr, status, err) {
        console.error(this.props.url, status, err.toString());
      }.bind(this)
    });
  },
  getInitialState: function() {
    return {data: []};
  },
  componentDidMount: function() {
    this.loadCommentsFromServer();
    setInterval(this.loadCommentsFromServer, this.props.pollInterval);
  },
  render: function() {
    return (
      <div className="commentBox">
        <h1>Comments</h1>
        <CommentList data={this.state.data} />
        <CommentForm onCommentSubmit={this.handleCommentSubmit} />
      </div>
    );
  }
});
```

### Optimization: optimistic updates
### 优化: 优化的更新

Our application is now feature complete but it feels slow to have to wait for the request to complete before your comment appears in the list. We can optimistically add this comment to the list to make the app feel faster.

<i class="icon-circle-arrow-right"></i> 
我们的应用现在已经功能完备，但是它感觉很慢，因为在评论出现在列表前必须等待请求完成。我们可以优化添加这条评论到列表以使应用感觉更快。

```javascript{17-23,33}
// tutorial21.js
var CommentBox = React.createClass({
  loadCommentsFromServer: function() {
    $.ajax({
      url: this.props.url,
      dataType: 'json',
      cache: false,
      success: function(data) {
        this.setState({data: data});
      }.bind(this),
      error: function(xhr, status, err) {
        console.error(this.props.url, status, err.toString());
      }.bind(this)
    });
  },
  handleCommentSubmit: function(comment) {
    var comments = this.state.data;
    // Optimistically set an id on the new comment. It will be replaced by an
    // id generated by the server. In a production application you would likely
    // not use Date.now() for this and would have a more robust system in place.
    comment.id = Date.now();
    var newComments = comments.concat([comment]);
    this.setState({data: newComments});
    $.ajax({
      url: this.props.url,
      dataType: 'json',
      type: 'POST',
      data: comment,
      success: function(data) {
        this.setState({data: data});
      }.bind(this),
      error: function(xhr, status, err) {
        this.setState({data: comments});
        console.error(this.props.url, status, err.toString());
      }.bind(this)
    });
  },
  getInitialState: function() {
    return {data: []};
  },
  componentDidMount: function() {
    this.loadCommentsFromServer();
    setInterval(this.loadCommentsFromServer, this.props.pollInterval);
  },
  render: function() {
    return (
      <div className="commentBox">
        <h1>Comments</h1>
        <CommentList data={this.state.data} />
        <CommentForm onCommentSubmit={this.handleCommentSubmit} />
      </div>
    );
  }
});
```

### Congrats!
### 祝贺!

You have just built a comment box in a few simple steps. Learn more about [why to use React](/react/docs/why-react.html), or dive into the [API reference](/react/docs/top-level-api.html) and start hacking! Good luck!

<i class="icon-circle-arrow-right"></i> 
你刚刚通过几个简单的步骤建立了一个评论框。学习更多关于[为什么使用 React](/react/docs/why-react-zh-CN.html), 或者深入 [API 参考](/react/docs/top-level-api.html) 开始钻研！祝你好运！
