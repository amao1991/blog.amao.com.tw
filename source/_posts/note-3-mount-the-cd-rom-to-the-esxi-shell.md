---
title: "Note #3: Read the CD-ROM files in the ESXi shell"
date: 2020-01-17 16:19:27
tags:
  - note
  - ESXi
  - mount
  - CD-ROM
categories: Note
---

台北影像的底片洗出來都是給光碟片，雖然可以帶 USB 給他存但每次都忘記，而公司唯一一台能讀光碟的機器是裝了 ESXi 的 R610，然後每次都忘記指令。

<!--more-->

> 不負責任步驟：放入光碟 -> mount -> scp -> unmount -> 拿出光碟

## Step

原本 `/vmfs/volumes/` 路徑下

{% asset_img slug 222.png %}

1. Load [iso9660](#iso9660) module

```
~ # vmkload_mod iso9660
Module iso9660 loaded successfully
```

2. 查詢 CD-ROM 的 device name

```
~ # esxcfg-mpath -l | grep -i cd-rom
Device Display Name: Local TSSTcorp CD-ROM (mpx.vmhba1:C0:T0:L0)
```

3. Mount CD-ROM

```
vsish -e set /vmkModules/iso9660/mount mpx.vmhba1:C0:T0:L0
```

4. 路徑下多了一個 folder

{% asset_img slug 111.png %}

5. 從 local 把 remote 整個 folder 拉下來

（每次從 remote 傳檔案回 local 都失敗）

```
$ scp -r <username>@<remote_ip>:<file_path> <path_to_save>
```

6. Unmount CD-ROM

```
~ # vsish -e set /vmkModules/iso9660/umount mpx.vmhba1:C0:T0:L0
```

7. Unload [iso9660](#iso9660) module

```
~ # vmkload_mod -u iso9660
Module iso9660 successfully unloaded
```

<h2 id="iso9660">ISO 9660</h2>

又被稱作 CDFS (光碟檔案系統)，由國際標準化組織 (ISO) 為光碟媒介發佈的檔案系統。

目的是能夠跨平台交換資料。

以上取自維基百科

## Reference

整篇參考 [How to Mount the Host CD-ROM to the ESXi Shell](https://www.techcrumble.net/2017/05/how-to-mount-the-host-cd-rom-to-the-esxi-shell/)