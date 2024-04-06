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
3. [conda-forge/miniforge](https://github.com/conda-forge/miniforge)
4. [pyenv/pyenv](https://github.com/pyenv/pyenv)
5. [pypa/pipx](https://github.com/pypa/pipx)
6. [pyenv/pyenv-virtualenv](https://github.com/pyenv/pyenv-virtualenv)
7. [pypa/virtualenv](https://github.com/pypa/virtualenv)

## 项目模板

1. [cookiecutter/cookiecutter](https://github.com/cookiecutter/cookiecutter)
2. [pyscaffold/pyscaffold](https://github.com/pyscaffold/pyscaffold)
3. [copier-org/copier](https://github.com/copier-org/copier)

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

## 函数装饰器

1. [litl/backoff](https://github.com/litl/backoff)
2. [tkem/cachetools](https://github.com/tkem/cachetools)
3. [madisonmay/Tomorrow](https://github.com/madisonmay/Tomorrow)
4. [snoack/python-goto](https://github.com/snoack/python-goto)
5. [invl/retry](https://github.com/invl/retry)
6. [life4/deal](https://github.com/life4/deal)
7. [pnpnpn/timeout-decorator](https://github.com/pnpnpn/timeout-decorator)
8. [python-cachier/cachier](https://github.com/python-cachier/cachier)
9. [mgedmin/profilehooks](https://github.com/mgedmin/profilehooks)
10. [kata198/func_timeout](https://github.com/kata198/func_timeout)
11. [tantale/deprecated](https://github.com/tantale/deprecated)

## 标准库扩展

1. [mahmoud/boltons](https://github.com/mahmoud/boltons)
2. [pytoolz/toolz](https://github.com/pytoolz/toolz)

## 文件和系统

1. [os](https://docs.python.org/3/library/os.html)
2. [pathlib](https://docs.python.org/3/library/pathlib.html)
3. [shutil](https://docs.python.org/3/library/shutil.html)
4. [gorakhargosh/watchdog](https://github.com/gorakhargosh/watchdog)
5. [tox-dev/filelock](https://github.com/tox-dev/filelock)

## 日期时间

1. [time](https://docs.python.org/3/library/time.html)
2. [datetime](https://docs.python.org/3/library/datetime.html)
3. [arrow-py/arrow](https://github.com/arrow-py/arrow)
4. [sdispater/pendulum](https://github.com/sdispater/pendulum)
5. [python-babel/babel](https://github.com/python-babel/babel)
6. [LKI/chinese-calendar](https://github.com/LKI/chinese-calendar)

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
2. [dylanaraps/pywal](https://github.com/dylanaraps/pywal)
3. [tartley/colorama](https://github.com/tartley/colorama)
4. [sepandhaghighi/art](https://github.com/sepandhaghighi/art)
5. [r1chardj0n3s/parse](https://github.com/r1chardj0n3s/parse)
6. [chubin/pyphoon](https://github.com/chubin/pyphoon)

### 进度条

1. [tqdm/tqdm](https://github.com/tqdm/tqdm)
2. [rsalmei/alive-progress](https://github.com/rsalmei/alive-progress)
3. [noamraph/tqdm](https://github.com/noamraph/tqdm)
4. [verigak/progress](https://github.com/verigak/progress)
5. [wolph/python-progressbar](https://github.com/wolph/python-progressbar)
6. [NiltonVolpato/python-progressbar](https://github.com/NiltonVolpato/python-progressbar)

### 表格

1. [astanin/python-tabulate](https://github.com/astanin/python-tabulate)
2. [jazzband/prettytable](https://github.com/jazzband/prettytable)
3. [posit-dev/great-tables](https://github.com/posit-dev/great-tables)

## 可视化界面

1. [Textualize/textual](https://github.com/Textualize/textual)
2. [chriskiehl/Gooey](https://github.com/chriskiehl/Gooey)
3. [PySimpleGUI/PySimpleGUI](https://github.com/PySimpleGUI/PySimpleGUI)
4. [hoffstadt/DearPyGui](https://github.com/hoffstadt/DearPyGui)
5. [zauberzeug/nicegui](https://github.com/zauberzeug/nicegui)
6. [PyQt5/PyQt](https://github.com/PyQt5/PyQt)
7. [beeware/toga](https://github.com/beeware/toga)
8. [urwid/urwid](https://github.com/urwid/urwid)
9. [nucleic/enaml](https://github.com/nucleic/enaml)
10. [UmSenhorQualquer/pyforms](https://github.com/UmSenhorQualquer/pyforms)
11. [fcollonval/matplotlib_qtquick_playground](https://github.com/fcollonval/matplotlib_qtquick_playground)

## 调试工具

### 日志输出

1. [Delgan/loguru](https://github.com/Delgan/loguru)
2. [cool-RR/pysnooper](https://github.com/cool-RR/pysnooper)
3. [gruns/icecream](https://github.com/gruns/icecream)
4. [hynek/structlog](https://github.com/hynek/structlog)
5. [onelivesleft/PrettyErrors](https://github.com/onelivesleft/PrettyErrors)
6. [laike9m/Cyberbrain](https://github.com/laike9m/Cyberbrain)

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

### 语言性能

1. [numba/numba](https://github.com/numba/numba)
2. [cython/cython](https://github.com/cython/cython)
3. [mozillazg/pypy](https://github.com/mozillazg/pypy)

### 并行计算

1. [taichi-dev/taichi](https://github.com/taichi-dev/taichi)
2. [dask/dask](https://github.com/dask/dask)
3. [modin-project/modin](https://github.com/modin-project/modin)
4. [rapidsai/cudf](https://github.com/rapidsai/cudf)
5. [joblib/joblib](https://github.com/joblib/joblib)
6. [inducer/pycuda](https://github.com/inducer/pycuda)
7. [xorbitsai/xorbits](https://github.com/xorbitsai/xorbits)

## 加密

1. [pyca/cryptography](https://github.com/pyca/cryptography)
2. [Legrandin/pycryptodome](https://github.com/Legrandin/pycryptodome)
3. [pycrypto/pycrypto](https://github.com/pycrypto/pycrypto)

## 序列化

1. [pickle](https://docs.python.org/3/library/pickle.html)
2. [protocolbuffers/protobuf](https://github.com/protocolbuffers/protobuf)
3. [google/flatbuffers](https://github.com/google/flatbuffers)
4. [marshmallow-code/marshmallow](https://github.com/marshmallow-code/marshmallow)
5. [ijl/orjson](https://github.com/ijl/orjson)

## 通信

1. [zeromq/pyzmq](https://github.com/zeromq/pyzmq)

## 分布式任务

1. [celery/celery](https://github.com/celery/celery)

## 中文文本处理

1. [fxsjy/jieba](https://github.com/fxsjy/jieba)
2. [isnowfy/snownlp](https://github.com/isnowfy/snownlp)
3. [mozillazg/python-pinyin](https://github.com/mozillazg/python-pinyin)
4. [lxneng/xpinyin](https://github.com/lxneng/xpinyin)
5. [vinta/pangu.py](https://github.com/vinta/pangu.py)

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
2. [unoconv/unoconv](https://github.com/unoconv/unoconv)
3. [scanny/python-pptx](https://github.com/scanny/python-pptx)
4. [dimastbk/python-calamine](https://github.com/dimastbk/python-calamine)
5. [openpyxl/openpyxl](https://foss.heptapod.net/openpyxl/openpyxl)

## 音视频编辑

### 音频编辑

1. [jiaaro/pydub](https://github.com/jiaaro/pydub)
2. [librosa/librosa](https://github.com/librosa/librosa)

### 视频编辑

1. [Zulko/moviepy](https://github.com/Zulko/moviepy)
2. [kkroening/ffmpeg-python](https://github.com/kkroening/ffmpeg-python)

## 游戏开发

1. [pygame/pygame](https://github.com/pygame/pygame)
2. [pythonarcade/arcade](https://github.com/pythonarcade/arcade)

## 二维码

1. [x-hw/amazing-qr](https://github.com/x-hw/amazing-qr)
2. [lincolnloop/python-qrcode](https://github.com/lincolnloop/python-qrcode)
3. [heuer/segno](https://github.com/heuer/segno)

## 函数式编程

1. [evhub/coconut](https://github.com/evhub/coconut)
2. [kachayev/fn.py](https://github.com/kachayev/fn.py)
3. [EntilZha/PyFunctional](https://github.com/EntilZha/PyFunctional)

## 参考

1. [为什么有些人宁愿花费很多时间去自己手工配置Python环境, 也不用Anaconda?-知乎](https://www.zhihu.com/question/404402864/answer/2954272601)
2. [一文解释conda,pip,anaconda,miniconda,miniforge-撒旦-cc的文章-知乎](https://zhuanlan.zhihu.com/p/518926990)
3. [Anaconda商用要收费了怎么办？没关系，我们有miniforge-风影忍着的文章-知乎](https://zhuanlan.zhihu.com/p/379567315)
4. [哪些Python库让你相见恨晚？-Python小二的回答-知乎](https://www.zhihu.com/question/24590883/answer/1220720307)
5. [哪些Python库让你相见恨晚？-Lingfeng Ai的回答-知乎](https://www.zhihu.com/question/24590883/answer/92420471)
6. [哪些Python库让你相见恨晚？-易执的回答-知乎](https://www.zhihu.com/question/24590883/answer/969106343)
7. [六种酷炫Python运行进度条-腾讯云](https://cloud.tencent.com/developer/article/1661478)
8. [哪些命令行工具让你相见恨晚？-Python与数据挖掘的回答-知乎](https://www.zhihu.com/question/41115077/answer/2302415301)
9. [哪些Python库让你相见恨晚？-高天的回答-知乎](https://www.zhihu.com/question/24590883/answer/1493635700)
