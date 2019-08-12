---
layout: post
title: Jupyter lab 介绍
category: 技术
tags: jupyter
---

# Jupyter Lab


## 介绍

![](https://jupyter.org/assets/labpreview.png)

Jupyter Lab 1.0 近日已发布，作为 Jupyter Notebook 的接班人，在功能上有很大的提升，目前插件也已形成不错的生态。

下文将总结最近的一些使用情况、技巧。

## 安装

[官网](https://jupyter.org/install.html)推荐使用`conda`或`pip`进行安装。

- conda
```
conda install -c conda-forge jupyterlab
```
- pip
```
pip install jupyterlab
```

## 使用

安装或升级成功后，与 notebook 使用方法类似，在命令行输入 `jupyter lab` 启动。

- 与 notebook 不同，lab将侧边栏利用了起来，这样切换文件等操作在同一窗口就可完成，使其向IDE又近了一步。
- lab基本的操作与快捷键与notebook保持一致，在cell中输入代码，shift enter运行。
- 对cell可进行拖拽操作，可实现多窗口排列效果，右键可清除输出等操作。


## 插件

目前 Jupyter lab 已有丰富的插件支持，并且再逐步丰富。[awesome-jupyterlab](https://github.com/mauhai/awesome-jupyterlab) 总结了常用的一些，每个插件项目都有详细的安装配置教程。

其实在最新版本中，jupyter lab 自带了一个插件管理器，默认是关闭状态，开启后只需在管理中便可方便的安装、升级、删除插件。

下面介绍几个实用插件：

- [Table of Contents](https://github.com/ian-r-rose/jupyterlab-toc)，目录展示，使用 markdown 进行编辑
- [Go to definition](https://github.com/krassowski/jupyterlab-go-to-definition)，`alt+click` 实现函数及变量定义跳转
![](https://raw.githubusercontent.com/krassowski/jupyterlab-go-to-definition/master/examples/demo.gif)

- [Code Formatter](https://github.com/ryantam626/jupyterlab_code_formatter)，规范代码
- [jupyterlab-variableInspector](https://github.com/lckr/jupyterlab-variableInspector)，变量监控，支持 numpy、pandas、tensorflow，目前还不支持 pytorch，实用方法见下图
![](https://github.com/lckr/jupyterlab-variableInspector/raw/master/early_demo.gif)