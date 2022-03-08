# 窗口

恭喜你来到 SWGL 的世界。在这里，我们假设读者没有 OpenGL 的基础。  
在本章，我们将创建一个窗口。

## 配置环境

又到了配置环境的时候。配置环境总是容易劝退新人，但是我们会以简单的方式完成复杂的工作。

swgl-core 模块给了我们非常方便的配置方式。我们只需要在 IDE 中创建一个 Gradle 项目，往`dependencies`块中添加依赖即可。
```groovy
dependencies {
    implementation 'io.github.over-run:swgl-core:0.1.0'
}
```
记得把`0.1.0`换成 swgl-core 的当前版本哦。在 [这里](https://github.com/Over-Run/swgl-core/releases) 查找到最新的版本。

将依赖库添加好后，刷新你的项目（IDEA 中在右侧 Gradle 栏中点击刷新图标），看到`BUILD SUCCESSFUL`后就可以开始我们的 SWGL 之旅了。

swgl-core 模块会自动给我们添加 LWJGL 以及其他必要的库，这些就不需要读者操心了。

## 真·窗口

现在让我们创建一个窗口。

在 SWGL 中，一个程序的主体是`Application`，而在其下有一个`GlfwApplication`。[GLFW](https://www.glfw.org/), 是一个非常方便的窗口库，它能为我们提供 OpenGL 的上下文创建，以及其他~~乱七八糟~~的功能。  
我们将使用`GlfwApplication`来创建我们的**应用程序**（注：此时已经是一个应用程序而不只是窗口了）。

首先，我们创建一个主类，它将负责执行我们的程序，我们管他叫`Main`。
```java
public class Main {
    public static void main(String[] args) {
        var app = OurFirstApplication();
        app.boot();
    }
}
```

非常简单的主类。我们使用`var`自动推断`app`的类型，然后使用`boot`启动。

接下来，让我们来看一下`OurFirstApplication`是怎样的。
```java
public class OurFirstApplication extends GlfwApplication {
    @Override
    public void start() {
        lglRequestContext();
        clearColor(0.0f, 0.0f, 0.0f, 1.0f);
    }

    @Override
    public void run() {
        clear(COLOR_BUFFER_BIT);
    }

    @Override
    public void onResize(int width, int height) {
        glViewport(0, 0, width, height);
    }

    @Override
    public void close() {
        lglDestroyContext();
    }
}
```

你可以看到，我们覆盖了4个方法。

在`start`中，我们使用了`lglRequestContext`来获取 IMS 的上下文。IMS 是 SWGL 对现代 OpenGL 的封装，适用于不熟悉现代 OpenGL 或希望快速制作游戏的开发者。  
我们还使用了`clearColor`来设置“背景颜色”。每一个参数都是一个在[0.0..1.0]之间的浮点数，并能通过将 rgb 值除以 255.0 得到。

在`run`中，我们使用了`clear`来清除帧缓冲，`COLOR_BUFFER_BIT`指示我们将帧缓冲的颜色清除到我们之前设置的“背景颜色”。

剩下两个就没什么好说的了，根据字面意思，`glViewport`设置视口大小（试想如果一个1440x900的窗口的视口只有800x600），`lglDestroyContext`将之前 request 的上下文给删掉并释放内存，避免内存泄露。

到了这里，这个程序就算能够运行了。启动我们的程序（`Main`），然后你会得到一个黑色的窗口。起飞:rocket:！  
如果出现错误，请检查是否有哪些地方写错了。

[下一节](../s02/triangle.md)
