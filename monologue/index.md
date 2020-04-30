# 💬 Monologue

![](https://img.shields.io/badge/front-Vue.js-brightgreen?style=flat&logo=vue.js)
![](https://img.shields.io/badge/back-python-blue?style=flat&logo=python)

![main.png](https://i.loli.net/2020/04/11/CAD8nRzkWmxSFKU.png)

**Monologue** 是一个用于管理项目体验并对外展示的 Vue 程序，后端使用 Python 开发。Monologue 包含大部分 Oasis 先前拥有的功能。这是 Monologue 的 Wiki 页面，你可以在这里找到有关 Monologue 的指南和提示。

## 概述

Monologue 能用来做些什么？想象一下，如果此时我们有一个项目，我们需要记录它的一举一动，有时还需要去调查一些用户的使用体验，我们会做些什么？我们会去设计问卷、设计投票，但这些体验却又显得十分松散。我们无法找到一个同时包含这些功能的主体，更无法用自己的方式来存储和获取这些数据。那么，Monologue 就是为收集这些功能而诞生的。

使用 Monologue 可以做到以上几乎所有功能，但大部分目前还仍处于开发中。我们可以发布「事件」来使其显示在时间线上，这样用户便可以清楚地看到项目的发展；我们可以设计和发布问卷给用户填写，也可以通过投票来调研，然后我们便可以归档这些数据，生成为其它格式的数据，永远保存下来。除此之外还有更多可以拓展的功能，因为这是我们「自己」的制作。

?> 🍃 Monologue 是开放性软体，你可以将其部署到自己的服务器上，无需担心数据被窃取。

## 结构

Monologue 是一个简单的前后端分离项目，前端使用 Vue.js 进行开发，后端则使用 Python 的 Flask 开发 API。通过 `POST` 和 `GET` 操作对后端进行通讯。目前通讯还没有可靠的验证策略，不建议投入隐私项目中使用。

若要进一步了解如何进行部署，可根据需要选择[开发部署](/monologue/development.md)或[生产化部署](/monologue/production.md)。

## 协议

使用 Apache-2.0 协议开源于 GitHub。
