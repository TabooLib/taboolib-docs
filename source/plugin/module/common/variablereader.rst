========
变量工具
========

.. warning::

    本文章已过时，正在等待更新，下面是原始内容。

读取并替换字符串中的变量，具体表现为：

.. code-block:: kotlin

    val str = "这是字符串中的 {{ test }} 变量，我不需要识别的变量 \\{\\{ test }}"

    // 新建 VariableReader 并定义变量格式
    // repeat 为前后缀的重复次数
    // 如果你在本次变量读取过程中使用 "{" 作为前缀
    // 那么字符串中的所有 "{" 符号均会被替换，非变量意义的 "{" 则需要使用转义符。
    val reader = VariableReader(str, '{', '}', repeat = 2)

    // 遍历所有内容
    reader.parts.forEach {
        if (it.isVariable) {
            println(it.text) // 此处输出为 "test"
        }
    }

代码节选自 ``kether`` 模块。

.. code-block:: kotlin

    fun String.toFunction(): Function {
        val element = VariableReader(this, '{', '}', 2).parts.map {
            Element(it.text, it.isVariable)
        }
        return Function(element, element.filter { it.isFunction }.joinToString(" ") {
            "set ${it.hash} to ${it.value}"
        })
    }
