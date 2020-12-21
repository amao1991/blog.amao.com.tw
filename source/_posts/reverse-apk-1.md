---
title: "Android #2: Reverse APK"
date: 2019-03-12 16:48:09
tags:
  - android
  - reverse
  - apk
categories: Android
---

## 前情提要

無聊下載到一個奮 game，玩一玩開始覺得有機會 reverse 做修改，就這樣。

<!--more-->

## 簡單流程

apk reverse 需要用到以下三個工具

1. apktool (unzip apk)
2. dex2jar (decompile dex to jar)
3. JdGUI (jar to java code)

以上皆支援 windows 及 MAC OS

apk 可以右鍵直接解壓縮，也可以用 apktool 解開，其中的差異如下

|unzip|apktool|
|:-|:-|
|assets<br>lib<br><font color="red">META-INF</font><br>res<br>AndroidManifest.xml<br><font color="red">classes.dex</font><br><font color="red">resources.arsc</font>|assets<br>lib<br><font color="red">original</font><br>res<br><font color="red">smali</font><br>AndroidManifest.xml<br><font color="red">apktool.yml</font>

apktool.yml 是用 apktool 解壓縮時產生的，最後包裝回去需要用到，少了此檔案會失敗出錯

source code 就在 smali 中，看得懂的可以直接改，我是看得沒有很懂啦，所以需要 unzip 後的 classes.dex，再還原成 java code 去看

用 dex2jar 將 dex 還原成 jar，再用 JdGUI 將 jar 還原成 java，這就易讀多了

基本上流程是先透過 java 看懂程式，找出欲修改的地方並對應 smali 去修改，最後再用 apktool 包裝成 apk

所以大概是這樣：

直接對 apk unzip，把裡面的 classes.dex 檔拖到 dex2jar 底下，用 dex2jar 把 dex 還原成 jar

```
$ d2j-dex2jar.bat classes.dex
```

再用 JdGUI 把 jar 還原成 java code

用 apktool 解壓縮

```
$ apktool d [apkname].apk -o [foldername]
```

專案中的 smali 對應 java code 做新增刪除修改，包裝回 apk

```
$ apktool b [foldername] -o [apkname].apk
```

## 實作紀錄

很不巧地這次 reverse 的對象程式主要的 code 不在 classes.dex，而是在 library 中，瞬間走歪，開始著手進行第一次的 dll reverse，一開始是用 [dotPeek](https://www.jetbrains.com/decompiler/) 做 decompile，但很快就跳去用 [dnSpy](https://github.com/0xd4d/dnSpy)，個人是覺得無論視覺化還是功能面上都好用很多。

> dotPeek 好像只能 view 不能 edit?
> anyway 到要修改的階段已經在用 dnSpy 了

改一改存檔後就可以包回 apk 了，但安裝時出現無法安裝的問題，還以為是亂按了什麼改壞了，後來發現是因為沒有憑證

電腦有安裝 JDK 的話，bin 裡面有 keytool.exe 和 jarsigner.exe，前者產金鑰、後者產憑證

```
# gen certificate
keytool -genkey -v -keystore my-release-key.keystore -alias alias_name -keyalg RSA -keysize 2048 -validity 10000
```

中間資訊都可以不輸入，記得最後的密碼就好，簽署時會問

```
# sign apk
jarsigner -verbose -sigalg SHA1withRSA -digestalg SHA1 -keystore my-release-key.keystore [apk_name].apk alias_name
```

簽署完會有一行警告說是 self-certified（自簽憑證），這是因為可信任憑證要由可信任第三方或是專門賣憑證的公司幫忙簽署，如果自己產憑證自己簽署，就像是自己做的產品自己做檢驗然後保證他沒問題一樣，嚴格說起來完全沒信任價值（？），安裝時會跳出可能不安全的警告但可以忽略（反正我也沒有要丟上 google play XD）

## 後記

在模擬器上執行完還蠻成功的，還因此想不開買了台便宜的安卓手機，想繼續歡樂下去，但意外的發現無法運行，直接從 google play 下載安裝原版的也一樣無法運行，獲得了 `null pointer dereference` 的 error code，故事就先暫時停擺了，希望之後還會有續集(?)
