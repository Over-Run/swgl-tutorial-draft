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

TODO
