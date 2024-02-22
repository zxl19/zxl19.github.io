---
layout: post
title: 高质量Python包存档
date: 2023-03-28
author: zxl19
tags: [Python, Archive]
comments: true
toc: true
pinned: false
---

一些高质量Python包存档。

<!-- more -->

## 包管理

### 基于pip

```text
不要给我讲什么docker容器、miniconda，老夫写python就是一把梭！
pip install，pip uninstall，拿起pip就是干！
赢了安装新库，输了系统重装！
```

1. [pypa/pip](https://github.com/pypa/pip)
2. [tox-dev/pipdeptree](https://github.com/tox-dev/pipdeptree)
3. [damnever/pigar](https://github.com/damnever/pigar)

### 依赖项管理

1. [python-poetry/poetry](https://github.com/python-poetry/poetry)
2. [pypa/pipenv](https://github.com/pypa/pipenv)
3. [mitsuhiko/rye](https://github.com/mitsuhiko/rye)
4. [pdm-project/pdm](https://github.com/pdm-project/pdm)
5. [pypa/hatch](https://github.com/pypa/hatch)

### 虚拟环境管理

1. [venv](https://docs.python.org/3/library/venv.html)
2. [conda/conda](https://github.com/conda/conda)
3. [pyenv/pyenv](https://github.com/pyenv/pyenv)
4. [pypa/pipx](https://github.com/pypa/pipx)
5. [pyenv/pyenv-virtualenv](https://github.com/pyenv/pyenv-virtualenv)
6. [pypa/virtualenv](https://github.com/pypa/virtualenv)

## 项目模板

1. [cookiecutter/cookiecutter](https://github.com/cookiecutter/cookiecutter)
2. [pyscaffold/pyscaffold](https://github.com/pyscaffold/pyscaffold)

## 项目管理

1. [python-attrs/attrs](https://github.com/python-attrs/attrs)
2. [python-attrs/cattrs](https://github.com/python-attrs/cattrs)
3. [python-rope/rope](https://github.com/python-rope/rope)
4. [mitmproxy/pdoc](https://github.com/mitmproxy/pdoc)
5. [pybuilder/pybuilder](https://github.com/pybuilder/pybuilder)

## 打包

1. [pyinstaller/pyinstaller](https://github.com/pyinstaller/pyinstaller)
2. [Nuitka/Nuitka](https://github.com/Nuitka/Nuitka)
3. [brentvollebregt/auto-py-to-exe](https://github.com/brentvollebregt/auto-py-to-exe)
4. [marcelotduarte/cx_Freeze](https://github.com/marcelotduarte/cx_Freeze)
5. [py2exe/py2exe](https://github.com/py2exe/py2exe)
6. [ronaldoussoren/py2app](https://github.com/ronaldoussoren/py2app)

## 交互式解释器

1. [ipython/ipython](https://github.com/ipython/ipython)
2. [prompt-toolkit/ptpython](https://github.com/prompt-toolkit/ptpython)
3. [bpython/bpython](https://github.com/bpython/bpython)

## 文件和系统

1. [os](https://docs.python.org/3/library/os.html)
2. [pathlib](https://docs.python.org/3/library/pathlib.html)
3. [shutil](https://docs.python.org/3/library/shutil.html)
4. [gorakhargosh/watchdog](https://github.com/gorakhargosh/watchdog)

## 日期时间

1. [time](https://docs.python.org/3/library/time.html)
2. [datetime](https://docs.python.org/3/library/datetime.html)
3. [arrow-py/arrow](https://github.com/arrow-py/arrow)

## 参数读取

### 命令行参数

1. [argparse](https://docs.python.org/3/library/argparse.html)
2. [google/python-fire](https://github.com/google/python-fire)
3. [pallets/click](https://github.com/pallets/click)
4. [abseil/abseil-py](https://github.com/abseil/abseil-py)
5. [kislyuk/argcomplete](https://github.com/kislyuk/argcomplete)
6. [google/python-gflags](https://github.com/google/python-gflags)

### 配置文件参数

#### `.ini`文件

1. [configparser](https://docs.python.org/3/library/configparser.html)
2. [pyscaffold/configupdater](https://github.com/pyscaffold/configupdater)

#### `.yaml`文件

1. [yaml/pyyaml](https://github.com/yaml/pyyaml)

#### `.toml`文件

1. [uiri/toml](https://github.com/uiri/toml)
2. [sdispater/tomlkit](https://github.com/sdispater/tomlkit)
3. [hukkin/tomli](https://github.com/hukkin/tomli)
4. [bobfang1992/pytomlpp](https://github.com/bobfang1992/pytomlpp)

#### 其他类型

1. [facebookresearch/hydra](https://github.com/facebookresearch/hydra)
2. [google/fiddle](https://github.com/google/fiddle)

## 数值运算

1. [numpy/numpy](https://github.com/numpy/numpy)
2. [scipy/scipy](https://github.com/scipy/scipy)
3. [sympy/sympy](https://github.com/sympy/sympy)
4. [cupy/cupy](https://github.com/cupy/cupy)
5. [cvxpy/cvxpy](https://github.com/cvxpy/cvxpy)
6. [pydata/numexpr](https://github.com/pydata/numexpr)
7. [cvxopt/cvxopt](https://github.com/cvxopt/cvxopt)

## 数据分析

1. [pandas-dev/pandas](https://github.com/pandas-dev/pandas)
2. [apache/superset](https://github.com/apache/superset)
3. [great-expectations/great_expectations](https://github.com/great-expectations/great_expectations)
4. [geopandas/geopandas](https://github.com/geopandas/geopandas)

## 可视化

### 数据可视化

1. [matplotlib/matplotlib](https://github.com/matplotlib/matplotlib)
2. [mwaskom/seaborn](https://github.com/mwaskom/seaborn)
3. [bokeh/bokeh](https://github.com/bokeh/bokeh)
4. [plotly/plotly.py](https://github.com/plotly/plotly.py)
5. [pyecharts/pyecharts](https://github.com/pyecharts/pyecharts)
6. [altair-viz/altair](https://github.com/altair-viz/altair)
7. [d3blocks/d3blocks](https://github.com/d3blocks/d3blocks)
8. [wordcloud](https://pypi.org/project/wordcloud)

### 深度学习可视化

1. [fossasia/visdom](https://github.com/fossasia/visdom)
2. [lanpa/tensorboardX](https://github.com/lanpa/tensorboardX)
3. [tensorflow/tensorboard](https://github.com/tensorflow/tensorboard)
4. [facebookresearch/hiplot](https://github.com/facebookresearch/hiplot)
5. [lucasjinreal/alfred](https://github.com/lucasjinreal/alfred)

### 地理信息可视化

1. [python-visualization/folium](https://github.com/python-visualization/folium)
2. [SciTools/cartopy](https://github.com/SciTools/cartopy)
3. [holoviz/geoviews](https://github.com/holoviz/geoviews)

## 图论

### 图分析

1. [graphlib](https://docs.python.org/3/library/graphlib.html)
2. [networkx/networkx](https://github.com/networkx/networkx)
3. [igraph/python-igraph](https://github.com/igraph/python-igraph)

### 图可视化

1. [xflr6/graphviz](https://github.com/xflr6/graphviz)
2. [WestHealth/pyvis](https://github.com/WestHealth/pyvis)
3. [pydot/pydot](https://github.com/pydot/pydot)
4. [pygraphviz/pygraphviz](https://github.com/pygraphviz/pygraphviz)

## 命令行输出

### 输出样式

1. [Textualize/rich](https://github.com/Textualize/rich)
2. [tartley/colorama](https://github.com/tartley/colorama)
3. [sepandhaghighi/art](https://github.com/sepandhaghighi/art)
4. [chubin/pyphoon](https://github.com/chubin/pyphoon)

### 进度条

1. [tqdm/tqdm](https://github.com/tqdm/tqdm)
2. [rsalmei/alive-progress](https://github.com/rsalmei/alive-progress)
3. [noamraph/tqdm](https://github.com/noamraph/tqdm)
4. [verigak/progress](https://github.com/verigak/progress)
5. [wolph/python-progressbar](https://github.com/wolph/python-progressbar)
6. [NiltonVolpato/python-progressbar](https://github.com/NiltonVolpato/python-progressbar)

### 表格

1. [jazzband/prettytable](https://github.com/jazzband/prettytable)

## 可视化界面

1. [Textualize/textual](https://github.com/Textualize/textual)
2. [PySimpleGUI/PySimpleGUI](https://github.com/PySimpleGUI/PySimpleGUI)
3. [hoffstadt/DearPyGui](https://github.com/hoffstadt/DearPyGui)
4. [PyQt5/PyQt](https://github.com/PyQt5/PyQt)
5. [zauberzeug/nicegui](https://github.com/zauberzeug/nicegui)
6. [urwid/urwid](https://github.com/urwid/urwid)
7. [nucleic/enaml](https://github.com/nucleic/enaml)

## 调试工具

### 日志输出

1. [Delgan/loguru](https://github.com/Delgan/loguru)
2. [gruns/icecream](https://github.com/gruns/icecream)

### 性能分析

1. [timeit](https://docs.python.org/3/library/timeit.html)
2. [gaogaotiantian/viztracer](https://github.com/gaogaotiantian/viztracer)
3. [cpcloud/ipython-autotime](https://github.com/cpcloud/ipython-autotime)

## 图像处理

1. [python-pillow/Pillow](https://github.com/python-pillow/Pillow)
2. [scikit-image/scikit-image](https://github.com/scikit-image/scikit-image)
3. [opencv/opencv-python](https://github.com/opencv/opencv-python)
4. [colour-science/colour](https://github.com/colour-science/colour)

## 机器学习&深度学习

1. [pytorch/pytorch](https://github.com/pytorch/pytorch)
2. [tensorflow/tensorflow](https://github.com/tensorflow/tensorflow)
3. [keras-team/keras](https://github.com/keras-team/keras)
4. [scikit-learn/scikit-learn](https://github.com/scikit-learn/scikit-learn)

### 数据增强

#### 多模态数据

1. [facebookresearch/AugLy](https://github.com/facebookresearch/AugLy)
2. [google-research/uda](https://github.com/google-research/uda)

#### 图像数据

1. [aleju/imgaug](https://github.com/aleju/imgaug)
2. [albumentations-team/albumentations](https://github.com/albumentations-team/albumentations)
3. [mdbloice/Augmentor](https://github.com/mdbloice/Augmentor)

## 数据生成

1. [joke2k/faker](https://github.com/joke2k/faker)
2. [lk-geimfari/mimesis](https://github.com/lk-geimfari/mimesis)

## 代码生成

1. [microsoft/lida](https://github.com/microsoft/lida)
2. [visualpython/visualpython](https://github.com/visualpython/visualpython)
3. [chapyter/chapyter](https://github.com/chapyter/chapyter)

## 代码加速

1. [numba/numba](https://github.com/numba/numba)
2. [cython/cython](https://github.com/cython/cython)
3. [rapidsai/cudf](https://github.com/rapidsai/cudf)
4. [xorbitsai/xorbits](https://github.com/xorbitsai/xorbits)

## 加密

1. [pyca/cryptography](https://github.com/pyca/cryptography)
2. [Legrandin/pycryptodome](https://github.com/Legrandin/pycryptodome)
3. [pycrypto/pycrypto](https://github.com/pycrypto/pycrypto)

## 通信

1. [zeromq/pyzmq](https://github.com/zeromq/pyzmq)

## 文档处理

### PDF

1. [py-pdf/pypdf](https://github.com/py-pdf/pypdf)
2. [euske/pdfminer](https://github.com/euske/pdfminer)
3. [pdfminer/pdfminer.six](https://github.com/pdfminer/pdfminer.six)
4. [jorisschellekens/borb](https://github.com/jorisschellekens/borb)
5. [pdfarranger/pdfarranger](https://github.com/pdfarranger/pdfarranger)
6. [ArtifexSoftware/pdf2docx](https://github.com/ArtifexSoftware/pdf2docx)

### Office文档

1. [python-openxml/python-docx](https://github.com/python-openxml/python-docx)
2. [scanny/python-pptx](https://github.com/scanny/python-pptx)

## 音视频编辑

1. [Zulko/moviepy](https://github.com/Zulko/moviepy)
2. [jiaaro/pydub](https://github.com/jiaaro/pydub)

## 二维码

1. [lincolnloop/python-qrcode](https://github.com/lincolnloop/python-qrcode)
2. [heuer/segno](https://github.com/heuer/segno)

## 函数式编程

1. [evhub/coconut](https://github.com/evhub/coconut)
2. [kachayev/fn.py](https://github.com/kachayev/fn.py)
3. [EntilZha/PyFunctional](https://github.com/EntilZha/PyFunctional)

## 参考

1. [为什么有些人宁愿花费很多时间去自己手工配置Python环境, 也不用Anaconda?-知乎](https://www.zhihu.com/question/404402864/answer/2954272601)
2. [哪些Python库让你相见恨晚？-Python小二的回答-知乎](https://www.zhihu.com/question/24590883/answer/1220720307)
3. [哪些Python库让你相见恨晚？-Lingfeng Ai的回答-知乎](https://www.zhihu.com/question/24590883/answer/92420471)
4. [哪些Python库让你相见恨晚？-易执的回答-知乎](https://www.zhihu.com/question/24590883/answer/969106343)
5. [六种酷炫Python运行进度条-腾讯云](https://cloud.tencent.com/developer/article/1661478)
6. [哪些命令行工具让你相见恨晚？-Python与数据挖掘的回答-知乎](https://www.zhihu.com/question/41115077/answer/2302415301)
7. [哪些Python库让你相见恨晚？-高天的回答-知乎](https://www.zhihu.com/question/24590883/answer/1493635700)
