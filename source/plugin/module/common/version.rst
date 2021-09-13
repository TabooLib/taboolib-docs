========
版本工具
========

用于识别和比较语义化版本（SemVer）的工具，具体表现为：

.. code-block:: kotlin

    val ver1 = Version("1.0.0")
    val ver2 = Version("1.0.1 beta") // 修订号后被空格或 "-" 分隔的内容会被忽略

    // 可直接使用比较运算符对比版本
    println(ver2 > ver1)

    // 如果版本号只有 2 位，将格式化为 -1.X.X
    val ver3 = Version("2.0") // -1.2.0

    // 如果是其他版本号格式，将抛出 VersionFormatException 异常
    val ver4 = Version("1")