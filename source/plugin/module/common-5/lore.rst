==========
描述匹配器
==========

用于物品描述的前缀识别，具体表现在 ``taboolib.common5.LoreMap`` 类中。在 Map 中储存描述关键词和对象, 然后丢入装备上的描述即可高效返回对象。

用法和 HashMap 类似，适合上百条乃至上千条描述的快速前缀判断。

比如，你有 "物理伤害", "法术伤害", "心理伤害" 等上百种属性，"&b&l[&e&l属性&b&l]&c&l物理伤害: &a20"、"草泥马透透透物理伤害: &b20"。

现在要从中准确提取出 "物理伤害" 和 ":20" (注："物理伤害" 这四个字中间，只允许有空格或颜色代码)，那么用这个LoreMap, 只需调用 getMatchResult(lore)。你将会在几毫秒内得到匹配结果，远远快于循环 contains 和正则表达式。

注意，若要完全匹配则推荐直接用 HashMap 的 containsKey(lore)

具体使用方式可以表现为以下形式：

.. code-block:: java

    // 假定你通过抽象类定义了属性
    public abstract class MyAttribute

    // 并且定义了子类
    public class Damage extend MyAttribute

    public class Health extend MyAttribute

现在可以定义一个 LoreMap 容器，并向其中添加描述和属性：

.. code-block:: java

    // 三个参数为：无视颜色代码，无视前缀，无视空格
    public static LoreMap<MyAttribute> attrMap = new LoreMap(true, true, true);

    static {
        attrMap.put("伤害", new Damage())
        attrMap.put("生命", new Health())
    }

并在之后通过描述随时获取属性：

.. code-block:: java

    for (String lore: meta.getLore()) {
        // 在 LoreMap 中匹配属性
        LoreMap.Result<MyAttribute> matchResult = attrMap.getMatchResult(lore)
        // 如果没匹配到则处理下一条
        if (matchResult.obj == null) {
            continue;
        }
        // 匹配到则取属性
        MyAttribute attr = matchResult.obj;
        // 取属性描述右边剩下没匹配完的
        String remain = matchResult.remain;
        // 没匹配完的啥也没有，说明属性右边没数字，跳过
        if (remain==null) {
            continue;
        }
        // 处理属性
        // ..
    }

.. tips::

    整个过程是线程安全的，你可以在异步线程中使用它。

