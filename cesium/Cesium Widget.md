# Cesium Widget

B 站 | [Cesium 快速上手](https://www.bilibili.com/video/BV1B7411G7HP?t=902)

[本地服务器 Cesium Widget 案例](http://localhost:8080/Apps/Sandcastle/index.html?src=Cesium%20Widget.html)

## Widget 与 Viewer 区别

- Cesium Widget 这个案例展示了一个 Cesium 的简化窗体。
- Cesium.Viewer 这个窗体组件，包含了非常丰富的组件内容。、
- Cesium.CesiumWidget 可以说是其简化版本，不包含动画、图层选择等等其他组件内容，仅仅显示一个三维数字地球。默认情况下也不会包含 Cesium 地形的图层。
- 网上很多的关于如何在 Cesium.Viewer 组件中隐藏所有的元素，直接用 Cesium.CesiumWidget 这个组件就可以了。

> 这个示例在 Cesium 的 Sandcastle 当中,但是非常不起眼,很多人容易忽略掉。
> 因为这几乎是唯一使用 CesiumWidget 来创建 Cesium 三维应用的示例了。
> 但这并不代表它不重要,相反，它才是真正创建 Cesium 三维窗口的核心类。

## Cesium Widget 内部创建的对象

- clock 记录时间 进行场景动态展示 通过时间来确定某一帧的绘制内容
- 传入的 div(container) 构造函数的参数 传入的 div
- canvas 在 div(container)上构建的 Canvas 类的对象
- screenSpaceEventHandler 对 Canvas 对象上各种鼠标的交互事件的封装 | 集合 传给应用场景触发其他事件
- scene 承载整个三维场景中的对象

> scene和时间参数没有任何关系 没有时间概念

## scene

### 内置的图元对象

- 地球（globle）、skyBox（天空盒）、sun（太阳）、moon（月亮）等等
- 用户自行控制存放对象的数组：primitives 和 groundPrimitives。

### 图元类对应一个三维渲染对象

- 图元是Cesium用来绘制三维对象的一个独立的结构。图元类有：Globe、Model、Primitive、BillboardCollection、ViewportQuad等。

> 一个图元对应多个同一批绘制的对象