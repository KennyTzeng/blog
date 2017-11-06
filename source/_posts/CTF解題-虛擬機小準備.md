---
title: "CTF解題 虛擬機小準備"
catalog: true
date: 2017-10-05 11:47:50
subtitle: "我的虛擬機需要用到什麼工具呢"
header-img: "Post_header_img.png"
tags:
- "CTF"
- "VM"
- "工具"
categories:
- "CTF"
---

# CTF解題 虛擬機小準備
本篇記錄了自己架設好虛擬機後安裝了哪些工具與其簡單使用指令
+ 虛擬機資訊：Virtual Box, Ubuntu 16.04, 64位元

## vim、git
```
sudo apt-get install vim git
```

## peda
[peda](https://github.com/longld/peda)是進階版的gdb，在使用時直接列出暫存器、Code、Stack等資訊方便有效幫助我們除錯，也新增了一些功能指令

安裝方式：
```
git clone https://github.com/longld/peda.git ~/peda
echo "source ~/peda/peda.py" >> ~/.gdbinit
```

## peda forked by angelboy
[Github](https://github.com/scwuaptx/peda) 這是安傑大大根據peda又自己修改的，也把它裝進來

安裝方式：
```
git clone https://github.com/scwuaptx/peda.git ~/peda-angelboy
echo "source ~/peda-angelboy/peda.py" >> ~/.gdbinit
cp ~/peda/.inputrc ~/
```

## ncat
有時要讓本機架起server掛載執行檔，就需要用到ncat，它包含於nmap之中，因此
```
sudo apt-get install nmap
```
後就能使用了，輸入以下指令
```
ncat -ve ./[執行檔檔名] -kl [port]
```
就能將server架起來了，之後在另一terminal視窗輸入
```
nc 0.0.0.0 [port]
```
便可以連上以進行後續的工作

## 32位元執行檔
有時遇到的檔案是ELF 32-bit可執行檔，但作業系統是64位元的會無法執行
根據[AskUbuntu這篇](https://askubuntu.com/questions/454253/how-to-run-32-bit-app-in-ubuntu-64-bit)安裝了幾個套件後便可以執行囉
```
sudo dpkg --add-architecture i386
sudo apt-get update
sudo apt-get install libc6:i386 libncurses5:i386 libstdc++6:i386
```

## pip2、pip3
ubuntu安裝好後就有內建python2.7.12與python3.5.2了，但是沒有與之對應的pip，因此
```
sudo apt-get install python-pip
sudo apt-get install python3-pip
pip install --upgrade pip
pip3 install --upgrade pip
```

## pwntools
將pwntools裝在python2，有試過裝在python3中，但是在from pwn import * 時會報錯
```
pip2 install --upgrade pwntools
```

## 使用ssh連線至虛擬機
為了要能夠在本機電腦上使用ssh(Windows的putty、Mac可以直接用terminal)連線至虛擬機操作，需要在虛擬機上安裝openssh-server與做一些設定

首先安裝openssh-server
```
sudo apt-get install openssh-server
```
接著是一些網路與連接埠轉送的設定
打開VirtualBox上的設定 -> 網路 -> 「僅限主機」網路，新增一網路，網路卡位址使用預設的192.168.56.1即可
![](vb_setting_01.png)
接著在虛擬機中的terminal輸入`ifconfig`，查看網路位址，這裡是10.0.2.15
![](vm_setting_01.png)
然後去虛擬機的設定值 -> 網路 -> 介面卡，選擇附加到:NAT，並且在連接埠轉送中新增一條規則如圖所示，192.168.56.1:10022轉送至10.0.2.15:22
![](vm_setting_02.png)
最後重開虛擬機，以ssh連線至192.168.56.1:10022即可

Mac的指令是
```
ssh 使用者名稱@192.168.56.1 -p 10022
```
若設定好了仍無法連線，有可能是虛擬機上沒有key，因此在虛擬機terminal上下指令產生一把
```
ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key
```

## 未完待續
未來有用到其他工具會更新在這裡
最後更新時間：2017/10/09
