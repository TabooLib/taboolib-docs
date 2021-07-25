=========
插件元数据
=========

添加插件的元数据（Metadata）可以通过给予他们在运行时检查插件的名称、版本、描述、甚至是作者等。帮助用户更容易地识别你的插件。

.. note::

    不同的平台存在不同的元数据规范，但是 TabooLib 中我们统一在构建文件 (build.gradle) 中编辑。目前支持以下类型的插件元数据，但是受运行平台影响，部分元数据会在其他不受支持的运行平台中被抹去。

全平台
~~~~~~

* 说明（插件描述）
* 作者
* 依赖
* 链接（例如网站）

Bukkit、Nukkit
~~~~~~~~~~~~~~~

* 前缀
* 加载阶段
* api 版本

书写规范
~~~~~~~~

**说明**

.. code-block:: groovy

    taboolib {
        description {
            desc '我是插件的说明'
        }
    }

**作者**

.. code-block:: groovy

    taboolib {
        description {
            contributors {
                // 作者名称
                name 'Bkm016'
                // 说明（仅在 Sponge 平台有效）
                name 'Bkm016' description 'TabooLib Devoloper'
            }
        }
    }

**依赖**

.. code-block:: groovy
    
    taboolib {
        description {
            dependencies {
                // 插件名称
                name 'Chemdah'
                // 限制平台（该依赖会在其他平台被抹去）
                name 'Chemdah' with 'bukkit'
                // 版本（仅在 Sponge7/8 平台有效）
                name 'Chemdah' version '1.0.0'
                // 在该插件之后加载（仅在 Sponge8 平台有效）
                name 'Chemdah' loadafter true
                // 在该插件之前加载（仅在 Bukkit、Nukkit 平台有效）
                name 'Chemdah' loadbefore true
                // 软依赖（仅在 Bukkit、Nukkit、Bungee、Sponge8 平台有效）
                name 'Chemdah' optional true
                // 模组依赖（仅在 Sponge7 平台有效）
                name 'Chemdah' mod true
            }
        }
    }

依赖的扩展选项大多数可以同时存在，如下所示：

.. code-block:: groovy

    taboolib {
        description {
            dependencies {
                name 'Adyeshach' optional true
                name 'Chemdah' with 'bukkit' optional true
                name 'spongeapi' version '7.2.0' with 'sponge7'
                name 'spongeapi' version '8.0.0' with 'sponge8' loadafter true
                name 'ic3' with 'sponge7' mod true
            }
        }
    }

**链接**

.. code-block:: groovy
    
    taboolib {
        description {
            links {
                // 在非 Sponge8 平台下只保留 homepage 链接
                name 'homepage' url 'https://example.com'
                name 'source' url 'https://example.com/source'
                name 'issues' url 'https://example.com/issues'
            }
        }
    }

**前缀**

.. code-block:: groovy

    taboolib {
        description {
            prefix 'Example'
        }
    }

**加载阶段**

.. code-block:: groovy
    
    taboolib {
        description {
            // START 表示这个插件在服务器启动时就开始加载。
            // POSTWORLD 表示这个插件在第一个世界加载完成后开始加载。
            load 'START'
        }
    }

**api 版本**

.. code-block:: groovy
    
    taboolib {
        description {
            // 这些是默认存在的，若没有改动可以省略
            bukkitApi '1.13'
            nukkitApi '1.0.0'
        }
    }
