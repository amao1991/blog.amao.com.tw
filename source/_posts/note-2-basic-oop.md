---
title: "Note #2: 惡補物件導向基本知識"
date: 2019-05-09 10:44:46
tags:
  - note
  - programming
categories: Note
---

Hummmm...這欠債的部分...被截圖存證了只好認命連在火車上都拿出來敲敲打打（話說在火車上掏出電腦別有一番風味呢）
此篇為上篇在理解 PHP Deserialization 時，除了智商問題、天份問題，還缺乏很多物件導向程式設計 (Object-oriented programming, OOP) 的基礎知識，筆記於此。

<!--more-->

## 物件導向 - 繼承、封裝、多型

屬於物件導向的程式語言，皆具有三大特性：繼承、封裝、多型。

**繼承 (Inheritance)**

以生物老師的角度，不考慮先後天性意外的話，物種為人的就有兩隻腳、物種為狗的就有四條腿、物種為章魚的就有八條...腕？

以公民老師的角度，類似族譜，不談論倫理道德的話，爸爸姓什麼，小孩就會繼承爸爸的姓氏。

以岸本齊史的角度，就是血繼限界，不討論天份能力的話，宇智波一族的孩子就擁有寫輪眼。

以程式語言的角度，子類別可以使用（呼叫）父類別的函式、參數等。

> Java 中只允許單繼承，一個子類別只能擁有一個父類別。

**封裝 (Encapsulation)**

以現實生活中例子，自動販賣機，假如你想買一瓶無糖綠茶，就投 25 元，燈亮，點無糖綠，無糖綠掉出來。

但你不需要去理解機器怎麼處理收到錢之後燈亮的步驟，選完綠茶後機器又是怎樣的構造讓綠茶掉出來。

以程式語言來舉例，雜湊演算法，以 MD5 為🌰，很多開法者都呼叫過這個 function，但在收到要做雜湊的字串後，是做了什麼樣的數學運算而得到雜湊值，大部分的開發者並不會知道。

因為實作 MD5 的細節跟過程被封裝起來了。

**多型 (Polymorphism)**

> 同樣的類別，但用不同的實作方式（用繼承區別）

目前覺得最好理解的舉例就是多邊形 (Polygon) 面積計算

ref: http://www.cplusplus.com/doc/tutorial/polymorphism/

```c++
class Polygon {
  protected:
    int width, height;
  public:
    void set_values (int a, int b)
      { width = a; height = b; }
};

class Rectangle: public Polygon {
  public:
    int area()
      { return width * height; }
};

class Triangle: public Polygon {
  public:
    int area()
      { return width * height / 2; }
};
```

同樣都是要獲得面積，但是多邊形有很多種，就像矩形、三角形計算面積的方法本身就不一樣（不同的實作方式）。

## 泛型 (Generics)

在程式語言中，宣告變數的時候通常也會宣告型別，在寫 function 時，也會設定好 i/o 的型別，

若同一種實作方式，有可能用到不同型別的時候，就會用到泛型，

（如果沒有泛型，就要寫很多相同實作方式的 function）

以泛型的方式設定 function，就可以 input 任意型別讓系統去實作。

## Public、Private、Protected

public: 誰都能呼叫

private: 只能在該 class 中呼叫

protected: 和 private 的不同在於有繼承功能