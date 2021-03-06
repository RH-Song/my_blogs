---
title: 软件测试——静态黑盒测试
date: 2017-02-13 20:08:38
tags: 测试基础
categories: Software Testing
---

摘要：
软件测试的基础，至少需要了解以下四种：
- 静态黑盒测试是纸检查产品说明书，并在软件编写之前找出问题
- 动态黑盒测试是指在不了解软件如何工作的前提下进行测试
- 静态白盒测试是指通过正式审查和检验检查代码的细节
- 动态白盒测试，是指在看到软件的工作方式时，根据获得的信息对软件进行测试
本文讲到的是第一种，静态黑盒测试。

<!--more-->


在摘要中提到几个名词：静态、动态、黑盒测试、白盒测试，我们首先来看这几个名词的大致意思。

## 什么是黑盒测试
黑盒测试又叫功能性测试或者行为测试。在黑盒测试中，软件测试员只知道软件要做什么，无法看到盒子里的软件是如何运行的。给了软件输出，得到相应的结果，不知道如何得到这个结果，仅仅知道软件做了什么。

## 什么是白盒测试
白盒测试又叫透明盒测试。测试员可以通过访问程序员的代码，并通过检查代码协助测试，也就是可以看到盒子里面。

## 静态测试与动态测试的区别
静态测试指测试不运行的部分——只是检查和审核。动态测试是指通常意义上的测试——使用和运行软件。

## 静态黑盒测试
- 静态黑盒测试主要任务就是检查产品说明书并据此在编码之前找出软件缺陷。

- 审查产品说明书有哪些高级技巧
首先要明确测试产品说明书属于静态黑盒测试。审查产品说明书是为了找出根本性的问题、疏忽或遗漏之处。
  + 可以假设自己是客户，站在这个角度去审核产品说明书。此时，就是要避免因为已经接触过软件而产生的一些先入为主的、认为理所当然的东西，重新去审核产品说明书。
  + 研究现有的标准和规范。通过研究现有的标准和规范，比如：公司惯用语和约定、行业要求、政府标准、图形用户界面、安全标准等等，然后“检查”采用的标准是否正确、有无遗漏、是否与标准和规范相抵触，把标准和规范视为产品说明书的一部分。
  + 审查和测试类似软件。类似软件有助于设计测试条件和测试方法，还可能暴露意想不到的潜在问题。此过程值得注意的有：规模、复杂性、测试性、质量和可靠性、安全性。
  + 产品说明书属性检查。优秀的产品说明书应该是完整、准确、精确、一致、贴切、合理、代码无关的、具有可测试性的。
  + 产品说明书术语检查。从上面的一条可以知道产品说明书是不能含糊的，所有有些用词是需要注意的。比如：面对“总是、每一种、所有、没有、从不”这一类，要进行核实，如果有“某些、有时、通常、大多、几乎”，还有“等等、诸如此类、以此类推、例如”这一类都是模糊不清无法测试的。如果看到“良好、迅速、廉价、高效、小、稳定”这一类，会因为无法量化而无法测试。如果使用了“如果...那么...”应该考虑如果不是会发生什么，因为这种陈述缺少“否则”。
- 在详细审查产品说明书的时应该注意哪些特殊的问题
  + 代码无关：说明书是用来定义产品的，跟代码，系统，架构无关。
  + 可测试性：有时，大多，无法测试；良好，高效，小，稳定，这些也是模糊无法量化的，无法测试。

