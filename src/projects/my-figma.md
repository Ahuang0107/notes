# My-Figma

该项目尝试基于canvaskit-wasm来实现figma的一些基本功能。

之所以使用canvaskit-wasm，是因为使用浏览器本身的渲染能力，通过编辑html、svg或者2d
canvas有许多bottleneck。对于缩放不友好，不能利用GPU加速，对蒙版、模糊、合成模式等支持不同等。

`<canvas/>` creates the canvas to which CanvasKit will draw. This element is where we control the width and height of 
the drawing buffer,
while it's css style would control any scaling applied after drawing to those pixels.
Despite using a canvas element, CanvasKit isn't calling the HTML canvas's own draw methods.
It is using this canvas element to get a WebGL2 context and performing most of the drawing work in C++ code compiled to
WebAssembly,
then sending commands to the GPU at the end of each frame.

I want to put a `<canvas/>` element into a dynamic re-sizing flex-box container,
make `<canvas/>` always as big as it's parent,
but when I get parent's `width` and `height` by using `getBoundingClientRect()` and set it on `<canvas/>`,
it always makes `<canvas/>` breaking out. I fix it by set `<canvas/>` style with `position:absolute`.

figma的貌似将render都放到了webassembly，其中blog提到了几点提升性能都手段：

- 用32位浮点数甚至字节而不是js都64位浮点数，

关于数据，figma使用基于graphql的数据订阅来实现数据的实时性，db是postgres，
在上一层figma团队自研了一个叫LiveGraph的查询引擎，基于nodejs和go。
客户端通过graphql接口订阅数据。

## reference

[figma developer blog](https://www.figma.com/blog/building-a-professional-design-tool-on-the-web/)

[Bring C++ Graphics to the Web](https://www.codeproject.com/Articles/5163290/Bring-Cplusplus-Graphics-to-the-Web)

[GraphQL, meet LiveGraph: a real-time data system at scale](https://www.figma.com/blog/livegraph-real-time-data-fetching-at-figma/)