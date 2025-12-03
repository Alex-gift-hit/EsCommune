***************************
Intro modern python package
***************************

💌 B站官方 `Python现代包架构 LeRobot环境配置与安装(win) <https://www.bilibili.com/video/BV1rWSyBEEBr/>`_

Module
======

console编写代码关闭后会变量会消失。把代码放到文件中保存，以 ``.py`` 结尾表示是python的文件。这样的文件就是python的 **module**。 [1]_

.. code-block:: python

    # module_test.py
    a = 1
    b = 2
    print(f"a+b = {a + b}")

    d = 4; e = 5;

    def minus(x: int, y: int) -> int :
        print(f"{x} - {y} = {x -y}")
        return x-y

    f = minus(a, b)
    list_1 = [0, 1, 2, 3, 4]
    dict_1 = {"Jan": 31, "Feb": 28}



可以通过 import [7]_ 来导入模块。模块导入时会自动执行。

>>> import module_test
>>> module_test.minus(2, 1)

python会在 sys.path [7]_ 的路径中寻找模块，以及包。

>>> import sys
>>> print(sys.path)


模块，以及字符串代码执行方法。

.. code-block:: sh

    python module_test.py
    python -c "import sys;print(sys.path)"


Package
=======

模块多了不好管理，所以使用文件夹结构来管理模块。在顶层放一个 ``__init__.py`` 来指示这是一个包，下面有很多模块。 ``__init__.py`` 在包被导入时执行。通常会定义一些包级的变量，以及进行一些 模块导入。

.. code-block:: sh

    escommune_pkg
        │  __init__.py
        │
        ├─scripts
        │  │  esc_cli.py
        │
        │
        ├─sub_pkg1
        │  │  mod1.py
        │  │  mod2.py
        │  │  mod3.py
        │  │  __init__.py
        │
        │
        ├─sub_pkg2
        │      mod4.py
        │      mod5.py
        │      __init__.py


pip
===
[2]_ [3]_

.. code-block::

    pip install .
    pip install -e .

pyprject.toml
=============

[4]_ [5]_ [6]_

.. code-block:: python

    [build-system]
    requires = ["setuptools"]
    build-backend = "setuptools.build_meta"

    [project]
    name = "escommune_pkg"
    version = "0.4.3"
    license = {text = "Apache-2.0"}
    description = "For lerobot tutorial"
    readme = "README.rst"
    requires-python = ">=3.10"
    authors = [{name = "alex"}]

    dependencies = [
        "numpy"
    ]

    [project.optional-dependencies]
    scipy = ["scipy"]

    [project.urls]
    homepage = "https://escommune.readthedocs.io/"

    [tools.setuptools.package.find]
    where = ["src"]

    [project.scripts]
    esc-cli = "escommune_pkg.scripts.esc_cli:main"



conda
=====

.. code-block:: sh

    conda create --name lerobot python=3.10
    conda activate lerobot

    conda deactivate
    conda remove --name lerobot --all

Ref
===

.. [1] John Sturtz "module and package" https://realpython.com/python-modules-packages/
.. [2] Alexander Williams "Install Python Package from Local Directory" https://pytutorial.com/install-python-package-from-local-directory/
.. [3] pythontutorials.net https://www.pythontutorials.net/blog/how-to-locally-develop-a-python-package/
.. [4] https://pip.pypa.org.cn/en/stable/reference/build-system/pyproject-toml/
.. [5] python https://packaging.python.org/en/latest/guides/writing-pyproject-toml/
.. [6] https://setuptools.pypa.io/en/latest/userguide/pyproject_config.html
.. [7] Python 3.14 import系统 https://docs.python.org/zh-cn/3.14/reference/import.html#
