========
文件相关
========

关于文件的部分工具，具体表现为以下顶级或扩展函数：

.. code-block:: kotlin

    /**
     * 声明一个文件
     *
     * @param file 所属文件
     * @param path 文件路径
     * @param create 若文件不存在是否新建（默认为是）
     * @param folder 该文件是否为文件夹（默认为否）
     * @return 该文件自身
     */
    fun newFile(file: File, path: String, create: Boolean = true, folder: Boolean = false): File

    /**
     * 声明一个文件
     *
     * @param path 文件路径
     * @param create 若文件不存在是否新建（默认为是）
     * @param folder 该文件是否为文件夹（默认为否）
     * @return 该文件自身
     */
    fun newFile(path: String, create: Boolean = true, folder: Boolean = false): File

    /**
     * 声明一个文件
     *
     * @param file 文件
     * @param create 若文件不存在是否新建（默认为是）
     * @param folder 该文件是否为文件夹（默认为否）
     * @return 该文件自身
     */
    fun newFile(file: File, create: Boolean = true, folder: Boolean = false): File

    /**
     * 删除特定文件夹下的所有子文件
     */
    fun File.deepDelete()

    /**
     * 复制文件或文件夹
     * 若目标为文件夹则复制其所有子文件
     */
    fun File.deepCopyTo(target: File)
    
    /**
     * 取字符串的数字签名
     * @param algorithm 算法类型（可使用：md5, sha-1, sha-256 等）
     */
    fun String.digest(algorithm: String): String

    /**
     * 取文件的数字签名
     * @param algorithm 算法类型（可使用：md5, sha-1, sha-256 等）
     */
    fun File.digest(algorithm: String): String

    /**
     * 压缩文件
     * @param target 压缩后的文件
     * @param skipParent 是否跳过该文件，从子文件开始压缩
     */
    fun File.zip(target: File, skipParent: Boolean = false)
    
    /**
     * 解压文件
     * @param target 解压后的文件
     */
    fun File.unzip(target: File)

    /**
     * 解压文件
     * @param destDirPath 解压后的文件路径
     */
    fun File.unzip(destDirPath: String)

    /**
     * 使用 GZIP 算法压缩字节
     */
    fun ByteArray.zip(): ByteArray
    
    /**
     * 使用 GZIP 算法解压字节
     */
    fun ByteArray.unzip(): ByteArray