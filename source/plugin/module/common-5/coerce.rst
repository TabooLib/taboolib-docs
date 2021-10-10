=======
转换器
=======

用于将未知值强制转换为特定目标类型的实用工具，来自 SpongeAPI。相关文档如下所示：

**Sponge JavaDoc**
https://jd.spongepowered.org/spongeapi/8.0.0-SNAPSHOT/org/spongepowered/api/util/Coerce.html

**Tabnine Code (How to use)**
https://www.tabnine.com/code/java/classes/org.spongepowered.api.util.Coerce

具体使用方式可以表现为以下形式：

.. code-block:: kotlin

    val unknown = "100.0"
    val value = Coerce.toDouble(unknown)
    println(value + 10)