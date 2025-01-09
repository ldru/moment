---
sidebar_position: 1
---

**# Github commands**

+ git config --local --list

+ git config --global --list

+ Generate SSH key

  ssh-keygen -t ed25519 -C "ldru@163.com"
  
  https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent


**# Linux commands**

1.使用ZIP命令创建一个加密的ZIP文件：
  $ zip --password mypasscode all.zip 1.txt 2.txt
    adding: 1.txt (stored 0%)
    adding: 2.txt (stored 0%)

2.解压缩加密文件时，会提示要求输入密码：
  $unzip all.zip
  Archive:  all.zip
  [all.zip] 1.txt password:
