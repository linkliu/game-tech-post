---
title: Unity 5.x Shaders and Effects Cookbook中文版翻译（第二版）
categories: ["shader"]
tags: ["U3D", "Shader", "Cookbook", "中文版"]
weight: 100
math: true
date: 2023-06-26
---

​		我打算试着翻译这本技术书，目的又两个，1.希望自己能帮助英文不太好的朋友，2.希望自己也学到这些知识，顺便帮助自己提升英语水平。我英语水平不是很好，接下来如果有什么错误的地方，有看到的朋友还请帮忙纠正。我不会web前端技术，我想试着学学markdown语法，尽量让页面好看些但是最重要的还是内容。

  

## Unity 5.x Shaders and Effects Cookbook中文版（第二版）



## 目录表

## [鸣谢](https://linkliu.github.io/game-tech-post/post/shader_book/2020-08-05-%E9%B8%A3%E8%B0%A2/)

## [关于作者](https://linkliu.github.io/game-tech-post/post/shader_book/2020-08-05-%E5%85%B3%E4%BA%8E%E4%BD%9C%E8%80%85/)

## [www.PacktPub.com](https://linkliu.github.io/game-tech-post/post/shader_book/2020-08-06-www.packtpub.com/)

* [电子书, 优惠, 还有其他](https://linkliu.github.io/game-tech-post/post/shader_book/2020-08-06-%E7%94%B5%E5%AD%90%E4%B9%A6-%E4%BC%98%E6%83%A0%E6%8A%98%E6%89%A3-%E4%BB%A5%E5%8F%8A%E6%9B%B4%E5%A4%9A%E4%BF%A1%E6%81%AF/)

* [为什么需要订阅?](https://linkliu.github.io/game-tech-post/post/shader_book/2020-08-06-%E4%B8%BA%E4%BB%80%E4%B9%88%E8%AE%A2%E9%98%85/)

## [前言](https://linkliu.github.io/game-tech-post/post/shader_book/2020-08-06-%E5%89%8D%E8%A8%80/)

- [这本书包含哪些内容](https://linkliu.github.io/game-tech-post/post/shader_book/2020-08-09-%E8%BF%99%E6%9C%AC%E4%B9%A6%E5%8C%85%E5%90%AB%E5%93%AA%E4%BA%9B%E5%86%85%E5%AE%B9/)

- [学习的过程中你需要准备的](https://linkliu.github.io/game-tech-post/post/shader_book/2020-08-10-%E5%AD%A6%E4%B9%A0%E7%9A%84%E8%BF%87%E7%A8%8B%E4%B8%AD%E4%BD%A0%E9%9C%80%E8%A6%81%E5%87%86%E5%A4%87%E7%9A%84/)

- [本书的适合人群](https://linkliu.github.io/game-tech-post/post/shader_book/2020-08-10-%E6%9C%AC%E4%B9%A6%E7%9A%84%E9%80%82%E5%90%88%E4%BA%BA%E7%BE%A4/)

- [内容结构](https://linkliu.github.io/game-tech-post/post/shader_book/2020-08-13-%E5%86%85%E5%AE%B9%E7%BB%93%E6%9E%84/)
  - 始前准备
  - 操作步骤
  - 原理介绍
  - 额外内容
  - 相关补充

- [本书的一些文体说明](https://linkliu.github.io/game-tech-post/post/shader_book/2020-08-13-%E6%9C%AC%E4%B9%A6%E7%9A%84%E4%B8%80%E4%BA%9B%E6%96%87%E4%BD%93%E8%A6%81%E6%B1%82/)

- [读者反馈](https://linkliu.github.io/game-tech-post/post/shader_book/2020-08-13-%E8%AF%BB%E8%80%85%E5%8F%8D%E9%A6%88/)

- [客户支持](https://linkliu.github.io/game-tech-post/post/shader_book/2020-08-13-%E5%AE%A2%E6%88%B7%E6%94%AF%E6%8C%81/)

  - [示例代码下载](https://linkliu.github.io/game-tech-post/post/shader_book/2020-08-13-%E7%A4%BA%E4%BE%8B%E4%BB%A3%E7%A0%81%E4%B8%8B%E8%BD%BD/)

  - [本书一些彩图的下载](https://linkliu.github.io/game-tech-post/post/shader_book/2020-08-13-%E6%9C%AC%E4%B9%A6%E4%B8%80%E4%BA%9B%E5%BD%A9%E5%9B%BE%E7%9A%84%E4%B8%8B%E8%BD%BD/)

  - [勘误表](https://linkliu.github.io/game-tech-post/post/shader_book/2020-08-13-%E5%8B%98%E8%AF%AF%E8%A1%A8/)

  - [盗版声明](https://linkliu.github.io/game-tech-post/post/shader_book/2020-08-13-%E7%9B%97%E7%89%88%E5%A3%B0%E6%98%8E/)

  - [本书有问题请联系](https://linkliu.github.io/game-tech-post/post/shader_book/2020-08-13-%E6%9C%AC%E4%B9%A6%E6%9C%89%E9%97%AE%E9%A2%98%E8%AF%B7%E8%81%94%E7%B3%BB/)

## 1.[创建你的第一个着色器](https://linkliu.github.io/game-tech-post/post/shader_book/2020-08-13-%E7%AC%AC%E4%B8%80%E7%AB%A0.%E5%88%9B%E5%BB%BA%E4%BD%A0%E7%9A%84%E7%AC%AC%E4%B8%80%E4%B8%AA%E7%9D%80%E8%89%B2%E5%99%A8/)
- 介绍
- 创建一个基本的标准着色器
  - 始前准备
  - 操作步骤
  - 原理介绍
  - 相关补充
  
- [如何把Unity 4的旧着色器迁移至Unity 5](https://linkliu.github.io/game-tech-post/post/shader_book/2020-08-15-%E5%A6%82%E4%BD%95%E6%8A%8Aunity-4%E7%9A%84%E6%97%A7%E7%9D%80%E8%89%B2%E5%99%A8%E8%BF%81%E7%A7%BB%E8%87%B3unity-5/)
  - 始前准备
  - 操作步骤
    - 着色器版本的自动升级
    - 使用标准着色器
    - 迁移用户自定义的着色器
  - 原理介绍
  - 相关补充

- [给着色器添加属性](https://linkliu.github.io/game-tech-post/post/shader_book/2020-08-19-%E7%BB%99%E7%9D%80%E8%89%B2%E5%99%A8%E6%B7%BB%E5%8A%A0%E5%B1%9E%E6%80%A7/)
  - 始前准备
  - 操作步骤
  - 原理介绍
  - 相关补充
  
- [使用表面着色器的属性](https://linkliu.github.io/game-tech-post/post/shader_book/2020-09-02-%E4%BD%BF%E7%94%A8%E8%A1%A8%E9%9D%A2%E7%9D%80%E8%89%B2%E5%99%A8%E7%9A%84%E5%B1%9E%E6%80%A7/)
  - 操作步骤
  - 原理介绍
  - 额外内容
  - 相关补充

## 2.[表面着色器和纹理贴图](https://linkliu.github.io/game-tech-post/post/shader_book/2020-10-24-%E8%A1%A8%E9%9D%A2%E7%9D%80%E8%89%B2%E5%99%A8%E5%92%8C%E7%BA%B9%E7%90%86%E8%B4%B4%E5%9B%BE/)
- 介绍
- 漫反射的着色处理
  - 始前准备
  - 操作步骤
  - 原理介绍

- [使用包组](https://linkliu.github.io/game-tech-post/post/shader_book/2020-12-09-%E4%BD%BF%E7%94%A8%E5%8C%85%E7%BB%84%E6%95%B0%E7%BB%84/)
  - 操作步骤
    - 压缩矩阵
  - 相关补充
  
- [向着色器添加纹理](https://linkliu.github.io/game-tech-post/post/shader_book/2020-12-11-%E5%90%91%E7%9D%80%E8%89%B2%E5%99%A8%E6%B7%BB%E5%8A%A0%E7%BA%B9%E7%90%86/)
  - 始前准备
  - 操作步骤
  - 原理介绍
  - 额外内容
  - 相关补充
  
- [通过改变UV值来移动纹理](https://linkliu.github.io/game-tech-post/post/shader_book/2021-01-09-%E9%80%9A%E8%BF%87%E6%94%B9%E5%8F%98uv%E5%80%BC%E6%9D%A5%E7%A7%BB%E5%8A%A8%E8%B4%B4%E5%9B%BE/)
  - 始前准备
  - 操作步骤
  - 原理介绍
  
- [法线贴图](https://linkliu.github.io/game-tech-post/post/shader_book/2021-01-09-%E6%B3%95%E7%BA%BF%E8%B4%B4%E5%9B%BE/)
  - 始前准备
  - 操作步骤
  - 原理介绍
  - 额外内容
  
- [创建一个带透明度的材质](https://linkliu.github.io/game-tech-post/post/shader_book/2021-01-12-%E5%88%9B%E5%BB%BA%E4%B8%80%E4%B8%AA%E5%B8%A6%E9%80%8F%E6%98%8E%E5%BA%A6%E7%9A%84%E6%9D%90%E8%B4%A8/)
  - 始前准备
  - 操作步骤
  - 原理介绍
  
- [创建一个有全息效果的着色器](https://linkliu.github.io/game-tech-post/post/shader_book/2021-01-13-%E5%88%9B%E5%BB%BA%E4%B8%80%E4%B8%AA%E6%9C%89%E5%85%A8%E6%81%AF%E6%95%88%E6%9E%9C%E7%9A%84%E7%9D%80%E8%89%B2%E5%99%A8/)
  - 始前准备
  - 操作步骤
  - 原理介绍
  - 额外内容
  - 相关补充
  
- [纹理的压缩和混合](https://linkliu.github.io/game-tech-post/post/shader_book/2021-01-14-%E7%BA%B9%E7%90%86%E7%9A%84%E5%8E%8B%E7%BC%A9%E5%92%8C%E6%B7%B7%E5%90%88/)
  - 始前准备
  - 操作步骤
  - 原理介绍
  
- [在地形的表面绘制一个圆](https://linkliu.github.io/game-tech-post/post/shader_book/2021-01-16-%E5%9C%A8%E5%9C%B0%E5%BD%A2%E7%9A%84%E8%A1%A8%E9%9D%A2%E7%BB%98%E5%88%B6%E4%B8%80%E4%B8%AA%E5%9C%86/)
  - 始前准备
  - 操作步骤
    - 在表面移动这个圆
  - 原理介绍

## 3. [理解光照模型](https://linkliu.github.io/game-tech-post/post/shader_book/2021-02-22-%E7%90%86%E8%A7%A3%E5%85%89%E7%85%A7%E6%A8%A1%E5%9E%8B/)
- 介绍
- 创建一个自定义的漫反射光照模型
  - 始前准备
  - 操作步骤
  - 原理介绍

- [创建一个Toon风格的着色器](https://linkliu.github.io/game-tech-post/post/shader_book/2021-02-23-%E5%88%9B%E5%BB%BA%E4%B8%80%E4%B8%AAtoon%E9%A3%8E%E6%A0%BC%E7%9A%84%E7%9D%80%E8%89%B2%E5%99%A8/)
  - 始前准备
  - 操作步骤
  - 原理介绍
  - 额外内容

- [创建一个Phong类型类型的高光反射着色器](https://linkliu.github.io/game-tech-post/post/shader_book/2021-02-25-%E5%88%9B%E5%BB%BA%E4%B8%80%E4%B8%AAphong%E9%95%9C%E9%9D%A2%E7%B1%BB%E5%9E%8B%E7%9A%84%E9%AB%98%E5%85%89%E5%8F%8D%E5%B0%84%E7%9D%80%E8%89%B2%E5%99%A8/)
  - 始前准备
  - 操作步骤
  - 原理介绍

- [创建 BlinnPhong 类型的高光反射着色器](https://linkliu.github.io/game-tech-post/post/shader_book/2021-02-25-%E5%88%9B%E5%BB%BA-blinnphong-%E7%B1%BB%E5%9E%8B%E7%9A%84%E9%AB%98%E5%85%89%E5%8F%8D%E5%B0%84%E7%9D%80%E8%89%B2%E5%99%A8/)
  - 始前准备
  - 操作步骤
  - 原理介绍
  - 额外内容

- [创建各向异性类型的高光反射着色器](https://linkliu.github.io/game-tech-post/post/shader_book/2021-02-26-%E5%88%9B%E5%BB%BA%E5%90%84%E5%90%91%E5%BC%82%E6%80%A7%E7%B1%BB%E5%9E%8B%E7%9A%84%E9%AB%98%E5%85%89%E5%8F%8D%E5%B0%84%E7%9D%80%E8%89%B2%E5%99%A8/)
  - 始前准备
  - 操作步骤
  - 原理介绍

## 4.[Unity 5中基于物理原理的渲染](https://linkliu.github.io/game-tech-post/post/shader_book/2021-03-15-unity-5%E4%B8%AD%E5%9F%BA%E4%BA%8E%E7%89%A9%E7%90%86%E5%8E%9F%E7%90%86%E7%9A%84%E6%B8%B2%E6%9F%93/)
- 介绍
- 理解金属质感的设置
  - 始前准备
  - 操作步骤
  - 原理介绍
  - 相关补充

- [向PBR中添加透明度](https://linkliu.github.io/game-tech-post/post/shader_book/2021-03-15-%E5%90%91pbr%E4%B8%AD%E6%B7%BB%E5%8A%A0%E9%80%8F%E6%98%8E%E5%BA%A6/)
  - 始前准备
  - 操作步骤
    - 半透明材质
    - 物体如何消失
    - 如何在显示物体中挖一个孔
  - 相关补充

- [创建镜子和反射面](https://linkliu.github.io/game-tech-post/post/shader_book/2021-05-17-%E5%88%9B%E5%BB%BA%E9%95%9C%E5%AD%90%E5%92%8C%E5%8F%8D%E5%B0%84%E9%9D%A2/)
  - 始前准备
  - 操作步骤
  - 原理介绍
  - 相关补充

- [烘培场景中的光](https://linkliu.github.io/game-tech-post/post/shader_book/2021-05-21-%E7%83%98%E5%9F%B9%E5%9C%BA%E6%99%AF%E4%B8%AD%E7%9A%84%E5%85%89/)
  - 始前准备
  - 操作步骤
    - 场景中静态几何体的设置
    - 光探针的设置
    - 光的烘培
  - 原理介绍
  - 相关补充

## 5.[顶点函数](https://linkliu.github.io/game-tech-post/post/shader_book/2022-06-26-%E9%A1%B6%E7%82%B9%E5%87%BD%E6%95%B0/)
- 介绍
- 在表面着色器中访问顶点颜色
  - 始前准备
  - 操作步骤
  - 原理介绍
  - 额外内容

- [对表面着色器中的顶点使用动画](https://linkliu.github.io/game-tech-post/post/shader_book/2022-07-09-%E5%AF%B9%E8%A1%A8%E9%9D%A2%E7%9D%80%E8%89%B2%E5%99%A8%E4%B8%AD%E7%9A%84%E9%A1%B6%E7%82%B9%E4%BD%BF%E7%94%A8%E5%8A%A8%E7%94%BB/)
  - 始前准备
  - 操作步骤
  - 原理介绍

- [模型挤压](https://linkliu.github.io/game-tech-post/post/shader_book/2022-07-11-%E6%A8%A1%E5%9E%8B%E6%8C%A4%E5%8E%8B/)
  - 始前准备
  - 操作步骤
  - 原理介绍
  - 额外内容
  - 添加形变纹理

- [实现下雪效果着色器](https://linkliu.github.io/game-tech-post/post/shader_book/2022-07-17-%E5%AE%9E%E7%8E%B0%E4%B8%8B%E9%9B%AA%E6%95%88%E6%9E%9C%E7%9D%80%E8%89%B2%E5%99%A8/)
  - 始前准备
  - 操作步骤
  - 原理介绍
    - 为物体表面设置颜色
    - 修改几何体
  - 相关补充

- [实现范围体爆炸](https://linkliu.github.io/game-tech-post/post/shader_book/2022-10-23-%E5%AE%9E%E7%8E%B0%E8%8C%83%E5%9B%B4%E4%BD%93%E7%88%86%E7%82%B8/)
  - 始前准备
  - 操作步骤
  - 原理介绍
  - 额外内容
  - 相关补充

## 6.[片元着色器和抓取通道](https://linkliu.github.io/game-tech-post/post/shader_book/2022-12-03-%E7%89%87%E5%85%83%E7%9D%80%E8%89%B2%E5%99%A8%E5%92%8C%E6%8A%93%E5%8F%96%E9%80%9A%E9%81%93/)
- 介绍
- 理解顶点和片元着色器
  - 始前准备
  - 操作步骤
  - 原理介绍
  - 额外内容
    - 顶点的输入语义
    - 顶点的输出语义
  - 相关补充

- [使用抓取通道](https://linkliu.github.io/game-tech-post/post/shader_book/2023-01-02-%E4%BD%BF%E7%94%A8%E6%8A%93%E5%8F%96%E9%80%9A%E9%81%93/)
  - 始前准备
  - 操作步骤
  - 原理介绍
  - 相关补充

- [实现一个玻璃效果的着色器](https://linkliu.github.io/game-tech-post/post/shader_book/2023-02-10-%E5%AE%9E%E7%8E%B0%E4%B8%80%E4%B8%AA%E7%8E%BB%E7%92%83%E6%95%88%E6%9E%9C%E7%9A%84%E7%9D%80%E8%89%B2%E5%99%A8/)
  - 始前准备
  - 操作步骤
  - 原理介绍
  - 相关补充

- [在2D游戏中实现水效果的着色器](https://linkliu.github.io/game-tech-post/post/shader_book/2023-02-26-%E5%9C%A82d%E6%B8%B8%E6%88%8F%E4%B8%AD%E5%AE%9E%E7%8E%B0%E6%B0%B4%E6%95%88%E6%9E%9C%E7%9A%84%E7%9D%80%E8%89%B2%E5%99%A8/)
  - 始前准备
  - 操作步骤
  - 原理介绍

## 7. [移动设备着色器适配](https://linkliu.github.io/game-tech-post/post/shader_book/2023-02-26-%E7%A7%BB%E5%8A%A8%E8%AE%BE%E5%A4%87%E7%9D%80%E8%89%B2%E5%99%A8%E9%80%82%E9%85%8D/)
- 介绍
- 什么是低成本着色器?
  - 始前准备
  - 操作步骤
  - 原理介绍

- [着色器的性能分析](https://linkliu.github.io/game-tech-post/post/shader_book/2023-03-23-%E7%9D%80%E8%89%B2%E5%99%A8%E7%9A%84%E6%80%A7%E8%83%BD%E5%88%86%E6%9E%90/)
  - 始前准备
  - 操作步骤
  - 原理介绍
  - 额外内容

- [针对移动设备修改着色器](https://linkliu.github.io/game-tech-post/post/shader_book/2023-03-26-%E9%92%88%E5%AF%B9%E7%A7%BB%E5%8A%A8%E8%AE%BE%E5%A4%87%E4%BF%AE%E6%94%B9%E7%9D%80%E8%89%B2%E5%99%A8/)
  - 始前准备
  - 操作步骤
  - 原理介绍

## 8.[通过Unity渲染纹理实现屏幕效果](https://linkliu.github.io/game-tech-post/post/shader_book/2023-04-02-%E9%80%9A%E8%BF%87unity%E6%B8%B2%E6%9F%93%E7%BA%B9%E7%90%86%E5%AE%9E%E7%8E%B0%E5%B1%8F%E5%B9%95%E6%95%88%E6%9E%9C/)
- 介绍
- 设置屏幕效果脚本系统
  - 始前准备
  - 操作步骤
  - 原理介绍
  - 额外内容

- [在屏幕效果中使用亮度, 饱和度和对比度](https://linkliu.github.io/game-tech-post/post/shader_book/2023-04-15-%E5%9C%A8%E5%B1%8F%E5%B9%95%E6%95%88%E6%9E%9C%E4%B8%AD%E4%BD%BF%E7%94%A8%E4%BA%AE%E5%BA%A6-%E9%A5%B1%E5%92%8C%E5%BA%A6%E5%92%8C%E5%AF%B9%E6%AF%94%E5%BA%A6/)
  - 始前准备
  - 操作步骤
  - 原理介绍

- [在屏幕效果中使用基础的类Photoshop混合模式](https://linkliu.github.io/game-tech-post/post/shader_book/2023-04-16-%E5%9C%A8%E5%B1%8F%E5%B9%95%E6%95%88%E6%9E%9C%E4%B8%AD%E4%BD%BF%E7%94%A8%E5%9F%BA%E7%A1%80%E7%9A%84%E7%B1%BBphotoshop%E6%B7%B7%E5%90%88%E6%A8%A1%E5%BC%8F/)
  - 始前准备
  - 操作步骤
  - 原理介绍
  - 额外内容

- [屏幕效果中的覆盖混合模式](https://linkliu.github.io/game-tech-post/post/shader_book/2023-04-18-%E5%B1%8F%E5%B9%95%E6%95%88%E6%9E%9C%E4%B8%AD%E7%9A%84%E8%A6%86%E7%9B%96%E6%B7%B7%E5%90%88%E6%A8%A1%E5%BC%8F/)
  - 始前准备
  - 操作步骤
  - 原理介绍

## 9.[游戏和屏幕效果](https://linkliu.github.io/game-tech-post/post/shader_book/2023-04-20-%E6%B8%B8%E6%88%8F%E5%92%8C%E5%B1%8F%E5%B9%95%E6%95%88%E6%9E%9C/)
- 介绍
- 创建一个老电影屏幕效果
  - 始前准备
  - 操作步骤
  - 原理介绍
  - 相关补充

- [创建一个夜视屏幕效果](https://linkliu.github.io/game-tech-post/post/shader_book/2023-05-02-%E5%88%9B%E5%BB%BA%E4%B8%80%E4%B8%AA%E5%A4%9C%E8%A7%86%E5%B1%8F%E5%B9%95%E6%95%88%E6%9E%9C/)
  - 始前准备
  - 操作步骤
  - 原理介绍
  - 额外内容

## 10.[更高级的着色器技术](https://linkliu.github.io/game-tech-post/post/shader_book/2023-05-03-%E6%9B%B4%E9%AB%98%E7%BA%A7%E7%9A%84%E7%9D%80%E8%89%B2%E5%99%A8%E6%8A%80%E6%9C%AF/)
- 介绍
- 使用Unity内建的CG包含文件功能
  - 始前准备
  - 操作步骤
  - 原理介绍

- [使用CG包含让着色器模块化](https://linkliu.github.io/game-tech-post/post/shader_book/2023-05-03-%E4%BD%BF%E7%94%A8cg%E5%8C%85%E5%90%AB%E8%AE%A9%E7%9D%80%E8%89%B2%E5%99%A8%E6%A8%A1%E5%9D%97%E5%8C%96/)
  - 始前准备
  - 操作步骤
  - 原理介绍

- [实现一个毛皮效果的着色器](https://linkliu.github.io/game-tech-post/post/shader_book/2023-05-03-%E5%AE%9E%E7%8E%B0%E4%B8%80%E4%B8%AA%E6%AF%9B%E7%9A%AE%E6%95%88%E6%9E%9C%E7%9A%84%E7%9D%80%E8%89%B2%E5%99%A8/)
  - 始前准备
  - 操作步骤
  - 原理介绍
  - 额外内容

- [用数组来实现热度图](https://linkliu.github.io/game-tech-post/post/shader_book/2023-05-03-%E7%94%A8%E6%95%B0%E7%BB%84%E6%9D%A5%E5%AE%9E%E7%8E%B0%E7%83%AD%E5%BA%A6%E5%9B%BE/)
  - 始前准备
  - 操作步骤
  - 原理介绍
