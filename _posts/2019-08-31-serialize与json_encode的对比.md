---
layout:     post
title:      serialize与json_encode的对比
subtitle:   PHP函数
date:       2019-08-31
author:     Wu
header-img: img/post/post-bg-20190831.jpg
catalog: true
tags:
    - PHP
---

serialize与json_encode的对比
===

####相同点：
* 都是把其他数据类型转换成一个可以传输的字符串
* 都是结构性数据

####不同点：
* Serialize序列化后的数据格式保存数据原有类型，Serialize有更加详细的类型区分，而Json只有四种类型，并且是以简单的符号表示。
* JSON数据格式要更简洁相比Serialize序列化之后的数据格式
* Json不管是在速度还是在生成的字符串的大小上都比Serialize要好

####使用场景：
* 序列化使用Serialize，特别是对象的存储，这是其存在的意义。 
* Serialize适合存储带有加密方式的数据串,防止数据被中途截取
* JSON适合数据量大,不要求保留原有数据类型的情况下使用，与对象无关的数据存储可以使用Json。
* 数据交换时使用JSON，这也是其定义所在。

> 本文首次发布于 [Wu Blog](https://blog.wu06.com/), 作者 [@Wu](https://github.com/yuexueyu) ,转载请保留[原文链接](https://blog.wu06.com/2019/08/31/serialize与json_encode的对比)。