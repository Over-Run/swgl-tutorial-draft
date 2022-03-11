[上一节](../s03/quad.md)

# 纹理

一个纹理本质上就是一堆颜色排到一起，但我们不可能自己硬编码颜色，因此我们要加载纹理。

<!--\> 你知道吗：几乎只有MC圈的人才会混淆材质和纹理。-->

在正式加载纹理之前，我们先来了解一下纹理的加载流程。
1. 读取图片文件并存到`ByteBuffer`中
2. 生成一个 OpenGL 纹理对象
3. 设置纹理参数
4. 将图片的所有字节转到 OpenGL 格式并完成加载

如果每次都需要经过以上四步，那么无疑是一件麻烦事。幸亏 swgl-core 有`Texture2D`帮我们管理。  
`Texture2D`也需要在程序退出时释放，~~如果直接写到`close`里显得不优雅，~~所以我们使用两个重要的类：`ResManager`与`AssetManager`。

## 资源管理

`ResManager`将`AutoCloseable`（也就是`try(x) {}`里的`x`）的资源收集起来并统一释放。  
要使用`ResManager`，只需要在`start`中添加以下代码即可：
```java
var resManager = new ResManager(this);
```
它会自动调用`Application::addResManager`以便自动管理。

创建完成后，使用`ResManager::addResource`添加要管理的资源。

---

`AssetManager`直接new一个就好了。
```java
var assetMgr = new AssetManager();
```

对于纹理，我们会用更简便的方法添加到`AssetManager`中。

## 加载纹理

TODO

[下一节](../s05/transform.md)
