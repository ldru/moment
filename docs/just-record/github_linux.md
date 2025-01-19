---
sidebar_position: 1
---

**# Github commands**

+ git config --local --list

+ git config --global --list

+ git checkout .  (清除所有已修改的文件)

+ git reset HEAD . (清除所有已加到暂存区的文件)

+ Set git editor to VSCode: git config --global core.editor "code --wait"
  
+ git branch -M main

+ git remote add origin git@github.com:Lu-Derik/arec-sol-demo.git

+ git push -u origin main

+ Generate SSH key

  ssh-keygen -t ed25519 -C "ldru@163.com"
  
  https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent


**# Linux commands**

1. 使用ZIP命令创建一个加密的ZIP文件：
  $ zip --password mypasscode all.zip 1.txt 2.txt
    adding: 1.txt (stored 0%)
    adding: 2.txt (stored 0%)

2. 解压缩加密文件时，会提示要求输入密码：
  $unzip all.zip
  Archive:  all.zip
  [all.zip] 1.txt password:

3. How to share folders between your Ubuntu Virtualbox and your host machine
  + https://itsolutiondesign.wordpress.com/2021/08/05/how-to-share-folders-between-your-ubuntu-virtualbox-and-your-host-machine/

  + steps
    1. 启动虚机。
    2. 虚机运行主界面, 选择 "设备" -> "分配光驱"。
    3. 弹出界面中选择 "VBoxGuestAdditions.iso"
    4. 虚机运行主界面, 选择 "设备" -> "Insert Quest VBoxGuestAdditions"
    5. 安装即可
