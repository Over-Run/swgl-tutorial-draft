[上一节](../s01/window.md)

# 一个三角形

如果我只说是一个三角形，你可能已经退出了。那如果我说是一个彩色的呢？

要添加一个彩色的三角形并不难。下面让我们来看一下实现。
```java
public class OutFirstApplication /* ... */ {
    /* ... */

    @Override
    public void run() {
        /* ... */
        lglBegin(GLDrawMode.TRIANGLES);
        lglColor(1.0f, 0.0f, 0.0f);
        lglVertex(0.0f, 0.5f);
        lglEmit();
        lglColor(0.0f, 1.0f, 0.0f);
        lglVertex(-0.5f, -0.5f);
        lglEmit();
        lglColor(0.0f, 0.0f, 1.0f);
        lglVertex(0.5f, -0.5f);
        lglEmit();
        lglEnd();
    }

    /* ... */
}
```
如果你研究过 OpenGL 的直接模式，你可能会觉得有点熟悉。没错，这是 swgl-core 包含的 **IMS**。IMS，即立即模式模拟器(**I**mmediate **M**ode **S**imulator)。IMS 的方法都以`lgl`开头。  
下面让我们来熟悉一下这段代码。

- `lglBegin`指示<!--断句-->我们要开始绘画了。`GLDrawMode.TRIANGLES`则说明我们要画的是三角形。`GLDrawMode`里还有许多其他的图形，例如`POINTS`, `LINES`等。  
- 接下来是`lglColor`。`lglColor`替换上次设置的颜色，比如，如果`lglColor`调用了两次，那么`lglEmit`使用的是后一次设置的颜色。  
- 然后是`lglVertex`。它和color差不多，只是设置的是顶点位置。  
- 接着是`lglEmit`。`lglEmit`是非常重要的一个方法，它将设置的顶点数据发送到 IMS。如果某个图形没有绘制出来，那么应该检查是否使用了emit。
- 最后是`lglEnd`。结束绘图，并显示到屏幕上。

现在你已经学会如何绘制三角形▲了，启动程序，然后你会看到一个彩色的三角形。

![A colorful triangle](colorful-triangle.png)

[下一节](../s03/quad.md)
