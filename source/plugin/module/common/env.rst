========
环境部署
========

.. tips::

    本篇内容不限于某个类或方法，而是多个内容组成的一套系统。

环境部署在 common 模块中有着至关重要的作用，能够在项目运行过程中动态加载第三方依赖文件。并对 ``pom`` 文件进行简单的解析，完成依赖传递等一系列逻辑。极大程度的减少 ``jar`` 文件的体积，并且 TabooLib 中的 Kotlin 环境部署便是由该系统完成。

这套系统大致由两个部分组成，前者用于远程加载依赖文件，后者用于下载资源文件。

* @RuntimeDependency（@RuntimeDependencies）
* @RuntimeResource（@RuntimeResources）

**示例：加载 Guava**

.. code-block:: Kotlin

    @RuntimeDependency("com.google.code.gson:gson:2.8.7")
    class TabooLibCommon

.. tips::
    
    无论这个注解写在哪里，都会在插件启动时被 TabooLib 读取。出于对多人协作的友好性，我们建议写在主类或是显眼的地方，以便他人维护。

依赖文件默认从 ``https://maven.aliyun.com/repository/central`` 仓库下载，也可以通过 ``repository`` 参数来修改这个地址。

**示例：加载 Guava 前检测重复**

.. code-block:: Kotlin

    @RuntimeDependency("com.google.code.gson:gson:2.8.7", test = "com.google.gson.JsonElement")
    class TabooLibCommon

使用 ``test`` 参数会在依赖下载之前检测 ``com.google.gson.JsonElement`` 是否存在并跳过加载过程，防止重复加载依赖产生资源浪费。

**示例：加载多个依赖**

Java：
.. code-block:: java

    @RuntimeDependency(value = "com.google.guava:guava:21.0", test = "com.google.common.base.Optional")
    @RuntimeDependency(value = "com.google.code.gson:gson:2.8.7", test = "com.google.gson.JsonElement")
    public class TabooLibCommon { }

Kotlin：
.. code-block:: kotlin

    @RuntimeDependencies(
        RuntimeDependency("com.google.guava:guava:21.0", test = "com.google.common.base.Optional"),
        RuntimeDependency("com.google.code.gson:gson:2.8.7", test = "com.google.gson.JsonElement")
    )
    class TabooLibCommon

两种语言的写法有细微的差别，注意区分。

**示例：避免重定向（relocate）**

在开发过程中我们可能会使用到 relocate 功能对包名进行重定向，这可能会出现一些问题。例如我们在 TabooLib 构建文件中使用了以下配置：

.. code-block:: kotlin

    taboolib {
        relocate("com.google", "com.github.username.library")
    }

就会产生下面的效果导致依赖加载失败：

.. image:: /images/Xnip2021-08-25_16-00-12.png

我们只需要进行一点点改动，在可能会被重定向的路径之前加上 ``!``。

.. code-block:: Kotlin

    @RuntimeDependency("!com.google.code.gson:gson:2.8.7")
    class MyPlugin

**示例：依赖传递**

在默认情况下，我们会对 ``pom`` 文件进行解析并同时加载它的其他依赖。例如 ``asm-commons`` 的依赖关系如下：

.. code-block:: xml

    <dependencies>
        <dependency>
            <groupId>org.ow2.asm</groupId>
            <artifactId>asm</artifactId>
            <version>9.2</version>
            <scope>compile</scope>
        </dependency>
        <dependency>
            <groupId>org.ow2.asm</groupId>
            <artifactId>asm-tree</artifactId>
            <version>9.2</version>
            <scope>compile</scope>
        </dependency>
        <dependency>
            <groupId>org.ow2.asm</groupId>
            <artifactId>asm-analysis</artifactId>
            <version>9.2</version>
            <scope>compile</scope>
        </dependency>
    </dependencies>

当我们使用 ``@RuntimeDependency("org.ow2.asm:asm-commons:9.2")`` 时，会同时加载它其他的 ``编译`` 及 ``运行`` 依赖。

* org.ow2.asm:asm:9.2
* org.ow2.asm:asm-tree:9.2
* org.ow2.asm:asm-commons:9.2
* org.ow2.asm:asm-analysis:9.2

通过 ``transitive`` 参数便可以关闭依赖传递。

.. code-block:: Kotlin

    @RuntimeDependency("org.ow2.asm:asm-commons:9.2", transitive = false)
    class MyPlugin

默认情况下我们不会传递被标注为可选（optional）的依赖，通过关闭 ``ignoreOptional`` 参数来跳过这一限制。

.. code-block:: Kotlin

    @RuntimeDependency("org.ow2.asm:asm-commons:9.2", ignoreOptional = false)
    class MyPlugin

不仅如此还可以通过修改 ``scopes`` 参数来决定加载特定范围的依赖。

    @RuntimeDependency("org.ow2.asm:asm-commons:9.2", scopes = {DependencyScope.RUNTIME})
    class MyPlugin