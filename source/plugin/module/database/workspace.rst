========
工作空间
========

在这一章，你应该已经创建好了需要的前置步骤。
如果你还没有，请先浏览**创建连接**和**创建表**两个文档
值得注意的是，**下面的并不是完整代码**。
你需要根据自己的需求进行更改，好让他可以按照预期工作。

基本使用方法
========

.. code-block:: kotlin

    override fun get(uid: String): Type? {
        // 在给定的工作空间(dataSource)中进行操作
        return type.tableVar().workspace(dataSource) {
            // 选择操作
            select {
                // 指定列
                rows("uid", "data")
                // 限制个数
                limit(1)
                // 条件
                where {
                    "uid" eq uid
                }
            }
        // 返回第一个且可以为null
        }.firstOrNull {
            // 如果你想获得例如data列的数据,可以使用getString("data")来进行获取
            // 也可以使用例如getInt("")的方式来获取一个整数
            // 这里使用了Gson库进行序列化操作
            Gson().fromJson(getString("data"), Type::class.java)
        }
    }
    
    override fun set(type: Type): Boolean {
        // 这里利用返回值可以为空判断了这个uid是否已经存在
        if (get(tpye.uid) == null) {
            type.tableVar().workspace(dataSource) {
                // 这里进行了插入操作
                insert("uid", "data") {
                    value(type.uid, gson.toJson(type))
                }
            }.run()
        } else {
            type.tableVar().workspace(dataSource) {
                // 这里进行了更新操作
                update {
                    where {
                        "uid" eq type.uid
                    }
                    set("data", gson.toJson(type))
                }
            }.run()
        }
        return true
    }
