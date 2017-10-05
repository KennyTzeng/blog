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

## 未完待續
未來有用到其他工具會更新在這裡