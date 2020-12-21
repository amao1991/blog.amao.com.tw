---
title: "Algorithm #1: P, NP, NP Hard, NP Complete Problem"
date: 2017-03-6 12:13:46
tags:
  - algorithm
categories: Algorithm
---

* 決定性、非決定性演算法
* 多項式、非多項式時間
* P Problem
* NP Problem
* NP - Hard Problem
* NP - Complete Problem

<!--more-->

## 決定性、非決定性演算法

決定性演算法 (Deterministic Algorithm)：這類演算法的下一步只有一件事可以做。

非決定性演算法 (Non-deterministic Algorithm)：這類演算法的下一步可能會有無限多件事可以選擇。並且可以分成兩個階段：

* 猜測階段：如果一個問題有正確解的話，此階段一定可以將這個正確解給猜出來；反之，若該問題沒有正確解的話，此階段就會隨便給答案。至於是怎麼將這個答案給找出來的，無從得知（不論所給的解是否為正確解）
* 驗證階段：驗證猜測階段所猜出來的答案是不是對的。

## 多項式、非多項式時間

一個問題的計算時間主要分為多項式時間、非多項式時間，通常用 Big O 表示

多項式時間：O(n)、O(log n)、O(n log n)、O(n^k)

非多項式時間：O(k^n)、O(n!)

## P Problem

Polynomial-time Problem，多項式時間內能得到答案的問題

## NP Problem

Non-deterministic Polynomial-time Problem，不確定在多項式時間內可以得到答案，但有可能的答案可以在多項式時間內驗證出正確與否

例：

問題：81785036517 是否為質數？

此問題不確定能不能在多項式時間內得到答案，但是我們可以猜測一個可能是 81785036517 的因數的數字，像是 277877，而這是可以在多項式時間內驗證出答案的

所以，「81785036517 是否為質數？」屬於 NP Problem，「277877 是否為 81785036517 的因數？」為 P Problem

## NP - Hard Problem

Non-deterministic Polynomial-time Hard Problem，不確定在多項式時間內可以得到答案，也不確定有沒有能在多項式時間內可以被驗證的答案

## NP - Complete Problem

Non-deterministic Polynomial-time Complete Problem，既是 NP Problem 又是 NP - Hard Problem 的問題，就稱為 NP - Complete Problem

**最後用一張維基百科的圖來總結一下**

{% asset_img slug P_np_np-complete_np-hard.png %}

## Reference

[1] http://bluelove1968.pixnet.net/blog/post/222283186-%E8%AB%96p,np,np-hard,np-complete%E5%95%8F%E9%A1%8C

[2] http://www.csie.ntnu.edu.tw/~u91029/AlgorithmAnalysis.html

[3] http://www.wikiwand.com/zh-mo/NP_(%E8%A4%87%E9%9B%9C%E5%BA%A6)

[4] http://www.wikiwand.com/zh-mo/NP%E5%9B%B0%E9%9A%BE

[5] http://smlie-blog.blogspot.tw/2014/10/algorithm-pnpnp-completenp-hard.html

[6] http://www.cnblogs.com/Gavin_Liu/archive/2011/05/04/2012284.html
