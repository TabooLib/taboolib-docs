==========
文件监听器
==========

监听文件变动的工具，具体表现在 ``taboolib.common5.FileWatcher`` 类中。

.. code-block:: java

    /**
     * 注册一个文件监听器
     */
    public void addSimpleListener(File file, Runnable runnable);

    /**
     * 注册一个文件监听器
     * 
     * @param runFirst 是否立即运行代码块
     */
    public void addSimpleListener(File file, Runnable runnable, boolean runFirst);

    /**
     * 注销文件的所有监听器
     */
    public void removeListener(File file);

    /**
     * 文件是否拥有监听器
     */
    public boolean hasListener(File file);

    /**
     * 注销所有文件的监听器
     */
    public void unregisterAll();

具体使用方式可以表现为以下形式：

.. code-block:: kotlin

    FileWatcher.INSTANCE.addSimpleListener(file) {
        // ...
    }
