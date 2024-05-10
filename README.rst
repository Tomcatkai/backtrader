backtrader
==========

.. image:: https://img.shields.io/pypi/v/backtrader.svg
   :alt: PyPi Version
   :scale: 100%
   :target: https://pypi.python.org/pypi/backtrader/

..  .. image:: https://img.shields.io/pypi/dm/backtrader.svg
       :alt: PyPi Monthly Donwloads
       :scale: 100%
       :target: https://pypi.python.org/pypi/backtrader/

.. image:: https://img.shields.io/pypi/l/backtrader.svg
   :alt: License
   :scale: 100%
   :target: https://github.com/backtrader/backtrader/blob/master/LICENSE
.. image:: https://travis-ci.org/backtrader/backtrader.png?branch=master
   :alt: Travis-ci Build Status
   :scale: 100%
   :target: https://travis-ci.org/backtrader/backtrader
.. image:: https://img.shields.io/pypi/pyversions/backtrader.svg
   :alt: Python versions
   :scale: 100%
   :target: https://pypi.python.org/pypi/backtrader/

**Yahoo API Note 雅虎api说明**:

  [2018-11-16] After some testing it would seem that data downloads can be
  again relied upon over the web interface (or API ``v7``) 经过一些测试，似乎可以再次通过 Web 界面下载数据

**Tickets**

  The ticket system is (was, actually) more often than not abused to ask for
  advice about samples. 票务系统（实际上）经常被滥用来询问有关样品的建议。

For **feedback/questions/...** use the `Community <https://community.backtrader.com>`_ 用来反馈问题

Here a snippet of a Simple Moving Average CrossOver. It can be done in several
different ways. Use the docs (and examples) Luke!
这里是一个简单的移动平均线交叉的片段。它可以通过几种不同的方式完成。使用文档（和示例）Luke！
::

  from datetime import datetime
  import backtrader as bt

  class SmaCross(bt.SignalStrategy):
      def __init__(self):
          sma1, sma2 = bt.ind.SMA(period=10), bt.ind.SMA(period=30)
          crossover = bt.ind.CrossOver(sma1, sma2)
          self.signal_add(bt.SIGNAL_LONG, crossover)

  cerebro = bt.Cerebro()
  cerebro.addstrategy(SmaCross)

  data0 = bt.feeds.YahooFinanceData(dataname='MSFT', fromdate=datetime(2011, 1, 1),
                                    todate=datetime(2012, 12, 31))
  cerebro.adddata(data0)

  cerebro.run()
  cerebro.plot()

Including a full featured chart. Give it a try! This is included in the samples
as ``sigsmacross/sigsmacross2.py``. Along it is ``sigsmacross.py`` which can be
parametrized from the command line.
包括一个功能完整的图表。试一试看！这在samples目录下的 sigsmacross/sigsmacross2.py 文件中。与之相伴的是 sigsmacross.py，它可以从命令行进行参数设置。







Features 特征:
=========

Live Trading and backtesting platform written in Python.用 Python 编写的实时交易和回测平台。

  - Live Data Feed and Trading with

    - Interactive Brokers (needs ``IbPy`` and benefits greatly from an
      installed ``pytz``)
    - *Visual Chart* (needs a fork of ``comtypes`` until a pull request is
      integrated in the release and benefits from ``pytz``)
    - *Oanda* (needs ``oandapy``) (REST API Only - v20 did not support
      streaming when implemented)
  实时数据提供和交易功能，支持：
       交互式Brokers（需要安装 IbPy，且如果安装了 pytz 将大有裨益）
       Visual Chart（需要一个 comtypes 的分支，直到一个拉取请求在发布中被整合，此外还从 pytz 中受益）
       Oanda（需要 oandapy）（仅支持 REST API - 在实现时 v20 不支持流媒体）

  - Data feeds from csv/files, online sources or from *pandas* and *blaze* 数据源自 CSV/文件、在线来源或使用 pandas 和 blaze
  - Filters for datas, like breaking a daily bar into chunks to simulate
    intraday or working with Renko bricks 数据筛选器，如将日线数据分割成块以模拟日内交易或使用 Renko 砖
  - Multiple data feeds and multiple strategies supported 支持多数据源和多策略
  - Multiple timeframes at once 同时使用多时间框架
  - Integrated Resampling and Replaying 集成的重新采样和回放
  - Step by Step backtesting or at once (except in the evaluation of the Strategy)分步回测或一次性完成（在策略评估时除外）
  - Integrated battery of indicators 集成的指标库
  - *TA-Lib* indicator support (needs python *ta-lib* / check the docs) 支持 TA-Lib 指标（需要 Python 的 ta-lib / 查看文档）
  - Easy development of custom indicators 定制指标的简易开发
  - Analyzers (for example: TimeReturn, Sharpe Ratio, SQN) and ``pyfolio``
    integration (**deprecated**) 分析器（例如：TimeReturn, Sharpe Ratio, SQN）和 pyfolio 集成（已弃用）
  - Flexible definition of commission schemes 灵活定义佣金方案
  - Integrated broker simulation with *Market*, *Close*, *Limit*, *Stop*,
    *StopLimit*, *StopTrail*, *StopTrailLimit*and *OCO* orders, bracket order,
    slippage, volume filling strategies and continuous cash adjustmet for
    future-like instruments集成的模拟经纪功能，支持 市价、收盘价、限价、止损、止损限价、追踪止损、追踪止损限价 和 OCO 订单，支架订单，滑点，成交量填充策略以及针对类似期货的金融工具的持续现金调整
  - Sizers for automated staking 自动投注的 Sizers
  - Cheat-on-Close and Cheat-on-Open modes 在收盘和开盘时作弊模式
  - Schedulers 调度器
  - Trading Calendars 交易日历
  - Plotting (requires matplotlib) 绘图（需要 matplotlib）




Documentation 文档
=============

The blog:

  - `Blog <http://www.backtrader.com/blog>`_

Read the full documentation at:

  - `Documentation <http://www.backtrader.com/docu>`_

List of built-in Indicators (122)

  - `Indicators Reference <http://www.backtrader.com/docu/indautoref.html>`_

Python 2/3 Support Python 版本要求
==================

  - Python >= ``3.2``

  - It also works with ``pypy`` and ``pypy3`` (no plotting - ``matplotlib`` is
    not supported under *pypy*) 它也适用于 ''py'' 和 ''pypy3'' （没有绘图 - ''matplotlib'' 在 pypy 下不受支持）

Installation 安装
============

``backtrader`` is self-contained with no external dependencies (except if you
want to plot) ''backtrader'' 是独立的，没有外部依赖关系（除非你想绘制）

From *pypi*: 从pypi安装：

  - ``pip install backtrader``

  - ``pip install backtrader[plotting]``

    If ``matplotlib`` is not installed and you wish to do some plotting

.. note:: The minimum matplotlib version is ``1.4.1`` 最低 matplotlib 版本为 ''1.4.1''

An example for *IB* Data Feeds/Trading: 安装 IB Data FeedsTrading的一个例子：

  - ``IbPy`` doesn't seem to be in PyPi. Do either::

      pip install git+https://github.com/blampe/IbPy.git

    or (if ``git`` is not available in your system)::

      pip install https://github.com/blampe/IbPy/archive/master.zip

For other functionalities like: ``Visual Chart``, ``Oanda``, ``TA-Lib``, check
the dependencies in the documentation. 对于其他功能，例如：“可视化图表”、“Oanda”、“TA-Lib”，请查看文档中的依赖项。

From source: 从源代码安装

  - Place the *backtrader* directory found in the sources inside your project 将 backtrader 目录放在项目中的源代码中

Version numbering 版本号说明
=================

X.Y.Z.I

  - X: Major version number. Should stay stable unless something big is changed
    like an overhaul to use ``numpy`` 主版本号。应该保持稳定，除非有大的变化，比如大修以使用“numpy”
  - Y: Minor version number. To be changed upon adding a complete new feature or
    (god forbids) an incompatible API change. 次要版本号。在添加完整的新功能或（上帝禁止）不兼容的 API 更改时进行更改。
  - Z: Revision version number. To be changed for documentation updates, small
    changes, small bug fixes 修订版本号。要更改文档更新、小更改、小错误修复
  - I: Number of Indicators already built into the platform 平台中已内置的指标数量
