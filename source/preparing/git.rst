========
安装 Git
========

Git 是一个开源的版本控制系统，它极大的方便了开发人员间的合作。

和无数开源项目一样，TabooLib 将它的代码托管在 GitHub 上。因此，Git 是 TabooLib 开发中至关重要的工具。

在 `Git 主页 <https://www.git-scm.com/>`__ 中可以找到大量的文档，以及一系列适用于不同操作系统的 GUI 版客户端。

下载
=====

Windows 平台
~~~~~~~~~~~~

`GitHub Desktop <https://desktop.github.com/>`_ 是一种在 Windows 上简便地安装 Git 的方式，因为 Git 已经被包含其中，作为软件的一部分。

安装完成后重启计算机，Git 即刻就绪。

macOS 平台
~~~~~~~~~

在 macOS 上安装 Git 的方法有很多。

最简单的方法是安装 Xcode Command Line Tools。

.. warning::

   下列内容不适用于比 Mavericks 更老的系统。如果你正在使用一个这样的老系统，请安装 Github 客户端。

1. 启动终端。
#. 执行 ``xcode-select --install``。
#. 等待安装，你可以借机逛逛批哩批哩。
#. 在终端运行 ``git`` 命令。

此外，你也可以通过 `GitHub Desktop <https://desktop.github.com/>`_ 来安装。

安装完成后重启计算机，Git 即刻就绪。

Linux 和 Unix 平台
~~~~~~~~~~~~~~~~~~~

在 Linux 上安装 Git 的最简单方法是使用你的 Linux 发行版的包管理系统。

.. note::

   你也许需要在命令前加上 ``sudo``。

1. 启动终端。
#. 如果你使用 Ubuntu 之类的基于 Debian 的系统，执行 ``apt-get install git``。如果是 Fedora 则执行 ``yun install git``。

GitHub Desktop 客户端有 Windows 和 Mac 版，但没有 Linux 版。

安装完成后重启计算机，Git 即刻就绪。

配置
=====

你是谁？
~~~~~~~

在开始使用 git 和 git 仓库之前，请确保你的 git 配置已设置了你的身份。打开你的 CLI 并输入：

.. code-block:: bash

   git config --list

查找 ``user.name`` 和 ``user.email``。如果它们和你在 GitHub 帐户上的用户名和电子邮件不同，请设置它们：

.. code-block:: bash

   git config --global user.name "John Doe"
   git config --global user.email johndoe@example.com


.. warning::

   在设定完成你的 ``user.name`` 和 ``user.email`` 之前，请不要对 TabooLib 仓库做任何提交。