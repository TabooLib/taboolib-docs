========
环境部署
========

.. tips::

    本篇内容不限于某个类或方法，而是多个内容组成的一套系统。

环境部署在 common 模块中有着至关重要的作用，能够在项目运行过程中动态加载第三方依赖文件。并对 ``pom`` 文件进行简单的解析，完成依赖传递等一系列逻辑。能够极大程度的减少 ``jar`` 文件的体积，而 TabooLib 中的 Kotlin 环境部署便是由该系统完成。

这套系统大致由两个部分组成，前者用于远程加载依赖文件，后者用于下载资源文件。

* @RuntimeDependency（@RuntimeDependencies）
* @RuntimeResource（@RuntimeResources）

示例：加载 Guava
~~~~~~~~~~~~~~~~~~~

.. code-block:: Kotlin

    @RuntimeDependency("com.google.code.gson:gson:2.8.7")
    class TabooLibCommon

.. tips::
    
    无论这个注解写在哪里，都会在插件启动时被 TabooLib 读取。出于对多人协作的友好性，我们建议写在主类或是显眼的地方，以便他人维护。

这个依赖文件默认从 ``https://maven.aliyun.com/repository/central`` 仓库下载，你也可以通过使用 ``repository`` 参数来修改这个地址。

示例：加载 Guava 前检测重复
~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: Kotlin

    @RuntimeDependency("com.google.code.gson:gson:2.8.7", test = "com.google.gson.JsonElement")
    class TabooLibCommon

使用 ``test`` 参数则会在依赖下载之前检测 ``com.google.gson.JsonElement`` 是否存在并跳过加载过程，防止重复加载产生资源浪费。

示例：加载多个依赖
~~~~~~~~~~~~~~~~~~

.. code-block:: java

    @RuntimeDependency(value = "com.google.guava:guava:21.0", test = "com.google.common.base.Optional")
    @RuntimeDependency(value = "com.google.code.gson:gson:2.8.7", test = "com.google.gson.JsonElement")
    public class TabooLibCommon { }

.. code-block:: kotlin

    @RuntimeDependencies(
        RuntimeDependency("com.google.guava:guava:21.0", test = "com.google.common.base.Optional"),
        RuntimeDependency("com.google.code.gson:gson:2.8.7", test = "com.google.gson.JsonElement")
    )
    class TabooLibCommon

在 Java 和 Kotlin 中加载多个依赖的写法是不同的，注意区分。

示例：如何避免被重定向（relocate）
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

在开发过程中我们可能会使用到 relocate 功能对包名进行重定向，但是这可能会导致 RuntimeDependency 部分出现错误。例如我们在 TabooLib 构建文件中使用了以下配置：

.. code-block:: kotlin

    taboolib {
        relocate("com.google", "com.github.username.library")
    }

可能就会产生下面的结果，导致依赖加载失败：

.. image:: /images/Xnip2021-08-25_16-00-12.png

我们只需要进行一点点改动：

.. code-block:: Kotlin

    @RuntimeDependency("!com.google.code.gson:gson:2.8.7")
    class MyPlugin

在可能会被重定向的路径之前加上 ``!`` 符号，既不影响依赖的加载也能避免被重定向。当然不能是别的符号。