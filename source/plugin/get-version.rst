========
获取版本
========

.. csv-table::
    :header: "构建版本", "发行时间", "发行者", "插件版本"
    :widths: 3, 5, 5, 3

    "|version-latest|", "|version-latest-date|", "|version-latest-author|", "|version-plugin|"
    
.. |version-latest| image:: https://img.shields.io/badge/dynamic/json?label=Version&query=%24.tag_name&url=https%3A%2F%2Fapi.github.com%2Frepos%2FTabooLib%2FTabooLib%2Freleases%2Flatest

.. |version-latest-date| image:: https://img.shields.io/badge/dynamic/json?label=Date&query=%24.created_at&url=https%3A%2F%2Fapi.github.com%2Frepos%2FTabooLib%2FTabooLib%2Freleases%2Flatest

.. |version-latest-author| image:: https://img.shields.io/badge/dynamic/json?label=Author&query=%24.author.login&url=https%3A%2F%2Fapi.github.com%2Frepos%2FTabooLib%2FTabooLib%2Freleases%2Flatest

.. |version-plugin| image:: https://img.shields.io/badge/dynamic/json?label=Plugin&query=%24.tag_name&url=https%3A%2F%2Fapi.github.com%2Frepos%2FTabooLib%2Ftaboolib-gradle-plugin%2Freleases%2Flatest

我们在开发过程中，应当使用较新的构建版本。

.. code-block:: kotlin

    plugins {
        // id("io.izzel.taboolib") version "1.26"
        id("io.izzel.taboolib") version "插件版本"
    }

    taboolib {
        // version = "6.0.0-27"
        version = "构建版本"
    }

你可以使用旧版本的 TabooLib 来开发插件，但是我们始终建议更新到最新稳定版本。
