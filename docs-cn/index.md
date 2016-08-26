---
layout: page
title: A JavaScript library for building user interfaces
id: home
---

<section class="light home-section">
  <div class="marketing-row">
    <div class="marketing-col">
      <h3>Declarative</h3>
      <p>React makes it painless to create interactive UIs. Design simple views for each state in your application, and React will efficiently update and render just the right components when your data changes.</p>
      <p>Declarative views make your code more predictable and easier to debug.</p>
    </div>
    <div class="marketing-col">
      <h3>Component-Based</h3>
      <p>Build encapsulated components that manage their own state, then compose them to make complex UIs.</p>
      <p>Since component logic is written in JavaScript instead of templates, you can easily pass rich data through your app and keep state out of the DOM.</p>
    </div>
    <div class="marketing-col">
      <h3>Learn Once, Write Anywhere</h3>
      <p>We don't make assumptions about the rest of your technology stack, so you can develop new features in React without rewriting existing code.</p>
      <p>React can also render on the server using Node and power mobile apps using <a href="https://facebook.github.io/react-native/">React Native</a>.</p>
    </div>
  </div>
</section>
<hr class="home-divider" />
<section class="home-section">
  <div id="examples">
    <div class="example">
      <h3>A Simple Component<br/><div class="c3">一个简单的组件</div></h3>
      <p>
        React components implement a `render()` method that takes input data and
        returns what to display. This example uses an XML-like syntax called
        JSX. Input data that is passed into the component can be accessed by
        `render()` via `this.props`.
      </p>
      <p class="c3">
        React组件通过一个 <code>render()</code> 方法，接受输入的参数并返回展示的对象。 <br/>
        以下这个例子使用了JSX，它类似于XML的语法<br/>
        输入的参数通过 <code>render()</code> 传入组件后，将存储在<code>this.props</code>
      </p>
      <p>
        <strong>JSX is optional and not required to use React.</strong> Try
        clicking on "Compiled JS" to see the raw JavaScript code produced by
        the JSX compiler.
      </p>
      <p class="c3">
        <strong>JSX是可选的，并不强制要求使用。</strong><br/>
        点击 &quot;Compiled JS&quot; 可以看到JSX编译之后的JavaScript代码
      </p>
      <div id="helloExample"></div>
    </div>
    <div class="example">
      <h3>A Stateful Component<br/><div class="c3">一个有状态的组件</div></h3>
      <p>
        In addition to taking input data (accessed via `this.props`), a
        component can maintain internal state data (accessed via `this.state`).
        When a component's state data changes, the rendered markup will be
        updated by re-invoking `render()`.
      </p>
      <p class="c3">
        除了接受输入数据（通过 <code>this.props</code> ），组件还可以保持内部状态数据（通过 <code>this.state</code> ）。当一个组件的状态数据的变化，展现的标记将被重新调用 <code>render()</code> 更新。
      </p>
      <div id="timerExample"></div>
    </div>
    <div class="example">
      <h3>An Application<br/><div class="c3">一个应用程序</div></h3>
      <p>
        Using `props` and `state`, we can put together a small Todo application.
        This example uses `state` to track the current list of items as well as
        the text that the user has entered. Although event handlers appear to be
        rendered inline, they will be collected and implemented using event
        delegation.
      </p>
      <p class="c3">
          通过使用 <code>props</code> 和 <code>state</code>, 我们可以组合构建一个小型的Todo程序。<br/>
          下面例子使用 <code>state</code> 去监测当前列表的项以及用户已经输入的文本。
          尽管事件绑定似乎是以内联的方式，但他们将被收集起来并以事件代理的方式实现。
        </p>
      <div id="todoExample"></div>
    </div>
    <div class="example">
      <h3>A Component Using External Plugins<br/><div class="c3">一个使用外部插件的组件</div></h3>
      <p>
        React is flexible and provides hooks that allow you to interface with
        other libraries and frameworks. This example uses **remarkable**, an
        external Markdown library, to convert the textarea's value in real time.
      </p>
      <p class="c3">
        React是灵活的，并且提供方法允许你跟其他库和框架对接。<br/>
        下面例子展现了一个案例，使用外部库Markdown实时转化textarea的值。
      </p>
      <div id="markdownExample"></div>
    </div>
  </div>
  <script src="/react/js/remarkable.min.js"></script>
  <script src="/react/js/examples/hello.js"></script>
  <script src="/react/js/examples/timer.js"></script>
  <script src="/react/js/examples/todo.js"></script>
  <script src="/react/js/examples/markdown.js"></script>
</section>
<hr class="home-divider" />
<section class="home-bottom-section">
  <div class="buttons-unit">
    <a href="docs/getting-started.html" class="button">Get Started
    <br/><div class="c2">快速入门</div></a>
    <a href="downloads.html" class="button">Download React v{{site.react_version}}
    <br/><div class="c2">下载 React v{{site.react_version}}</div></a>
  </div>
</section>
