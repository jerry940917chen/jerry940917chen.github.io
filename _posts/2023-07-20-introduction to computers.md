---
layout: post
title: 計算機概論台大開放課程
author: jerry chen
tags:
- 資訊基礎
date: 2023-07-20 04:17 
---
:::success
**計算機概論台大開放課程**
>[name=陳宏哲]
:::
# 第一課

---

### main memory and address
- one dimensional
- random accssible
- accress the content by the address(practically,also in binary)
- recall the pointer in C/C++
### 主存和地址
一維
隨機訪問
通過地址訪問內容
（實際上，也是二進制的）
回憶一下C/C++中的指標
address 地址

---

### memory techniques
- random access memory(RAM):memory in which individual cells can be easily accessed in any order
    - static memory(SRAM):like flip-flop
    - dynamic memory(DRAM):tiny capacitors replenished regulaarly by refresh circuit
    - double data rate(DDR)
    - dual/triple channel
- capacity
    - KB:2^10^bytes~=10^3^
    - MB:2^20^bytes~=10^6^
    - GB:2^30^bytes~=10^9^
### 記憶技巧
- 隨機存取存儲器（RAM）：可以以任何順序輕鬆訪問單個單元的存儲器
     - 靜態存儲器（SRAM）：類似觸發器
     - 動態存儲器（DRAM）：微型電容器通過刷新電路定期補充
     - 雙倍數據速率(DDR)
     - 雙/三通道
- 容量
     - KB:2^10^字節~=10^3^
     - MB:2^20^字節~=10^6^
     - GB:2^30^字節~=10^9^
techniques 技巧
random 隨機
access 存取
accress 訪問
individual 個人
static 靜態
dynamic 動態
tiny 微小的
capacitors 電容器
replenished 定期
regulaarly補充
refresh 刷新
circuit 電路
rate 速率
dual/triple 兩/三倍


---

### mass storage
- properties(compared with main memory)
    - larger capacity
    - less volatility
    - slower
    - on-line or off-line
- types
    - magnetic systems(hard disk,tape)
    - optical systems(CD,DVD)
    - flash drives
### 大容量儲存
- 屬性（與主存相比）
     - 容量更大
     - 揮發性性較小
     - 慢點
     - 在線或離線
- 類型
     - 磁性系統（硬盤、磁帶）
     - 光學系統（CD、DVD）
     - 閃存驅動器
mass 大量的
storage 儲存
properties 屬性
compared 比較
capacity 容量
volatility 揮發性
magnetic 磁
optical 光學
flash 閃

---

### magnetic disk storage system
- head,track,sector,cylinder
- access time=seek time+rotation delay/latency time
- transfer rate(SATA 1.5/3/6,etc)
### 磁盤存儲系統
- 磁頭、磁道、扇區、柱面
- 存取時間=尋找時間+旋轉延遲/延遲時間
- 傳輸速率（SATA 1.5/3/6等）
sector 扇形
cylinder 柱面
seek 尋找
rotation 旋轉
latency 延遲
transfer 傳輸
fragmentation 碎片化

---

### buffer 
- purpose:to synchronize(or to make compatible) different R/W mechanisms and rates
- a memoy area used for the temporary storage of data(usually as a step in transferring the data)
- blocks of data compatible with physical records can be transferred between buffers and the mass storage system
- data in buffer can be referenced in terms of logical records
### 緩衝區
- 目的：同步（或兼容）不同的R/W機制和速率
- 用於臨時存儲數據的內存區域（通常作為傳輸數據的一個步驟）
- 與物理記錄兼容的數據塊可以在緩衝區和大容量存儲系統之間傳輸
- 緩衝區中的數據可以通過邏輯記錄來引用
purpose　目的
synchronize　同步
compatible　兼容
mechanisms 機制
memoy 記憶
area 區域
memoy area 內存區域
temporary 臨時的
storage 儲存
step 步驟
transferring the data 傳輸數據
physical records 物理記錄
transferred 轉移
referenced 引用的
terms 術語
logical records 邏輯記錄

---

### from decimal to binary
- just as in decimal, keep dividing the number by 2 and record the remainders
- be careful about the order
### 從十進製到二進制
- 就像十進制一樣，繼續將數字除以 2 並記錄餘數
- 注意順序
decimal 十進位、小數
dividing 除法
record 紀錄
remainders 餘數

---

# 第二課
### representing sounds
- sampling
    - sampling
    - bit resolution
    - bit rate(sampling rate X bit resolution)
- MIDI(synthesis)
### 代表聲音
- 取樣
     - 抽樣
     - 位分辨率
     - 比特率（採樣率X比特分辨率）
- MIDI（合成）
representing 代表
sampling 取樣
resolution 辨識

### binary system revisited
- addition

- Two's commplement encoding
    - 遇到1開始換
    - 用n-1的補數+1
        - n bit 取-2，就是得到2^n^+(-2)的二進位 
- excess
    - 平移4格(4變成0)
- Fixed-point
- floating point
    - +1*2^-10^
revisited 重新考慮
addition 加法
excess 剩餘的
Fixed-point 定點數

---

# 第三課
### 資料儲存方法
- 壓縮方法

    - Huffman
        - 類似樹
        - 越長出現次數越少(越上面，數字越少)
        - AAABCCCCCCCCC
    - LZW
        - 字典法(重複的就變成新類型)
        - 不須把字典傳送給對方
        - 
---

### communication Errors
- compression
    - remove redundancy
- error detection & correction
    - add redundancy to prevent errors
- error detection: check code
    - cannor correct errors, but can check if errors occur
    - ID numbers
    - LSBN
    - parity code
- error correcting
    - an correct errors(to some degree)
### 通訊錯誤
- 壓縮
     - 刪除冗餘
- 錯誤檢測和糾正
     - 添加冗餘以防止錯誤
- 錯誤檢測：檢查代碼
     - 無法糾正錯誤，但可以檢查是否發生錯誤
     - 身份證號碼
     - LSBN
     - 奇偶校驗碼
- 錯誤更正
     - 糾正錯誤（在某種程度上）
communication 通訊
compression 壓縮
redundancy 過多
detection 檢測
correction 糾正
prevent 防止、避免
occur 發生
parity 奇偶數
degree 程度

---

# 第四課
### computer architecture 
- CPU(central processing unit)
- registers 寄存器
- memory
- bus 匯流排
- motherboard 主板

---

### machine instruction
- data transfer
    - LOAD
    - STORE
    - I/O
- arithmetic/logic
    - AND、OR、ADD、SUB、etc
    - SHUFT、ROTATE
- control
    - JUMP
    - HALT
- RISC(reduced instruction set computing)(PRC SPARC) VS CISC(complex instruction set computing)(x85,x886-64)
### 機器指令
- 數據傳輸
     - 加載
     - 貯存
     - 輸入/輸出
- 算術/邏輯
     - AND、OR、ADD、SUB、等等
     - 平移、旋轉
- 控制
     - 跳躍
     - 停
- RISC(精簡指令集計算)(PRC SPARC) VS CISC(複雜指令集計算)(x85,x886-64)
程式的function是用跳過去那邊使用的
transfer 傳輸
arithmetic 算數
etc 等等
HALT 停
reduced 精簡
complex 複雜
computing 計算
instruction 指令

---

# Pipelining
- throughput increeased
    - total amount of work accomplished given amount of time
- example: pre-fetching
    - lssue com]nditional jump

pipeline 管道
throughput
increeased
amount
accomplished
amount
pre-fetching
lssue

# parallel/distributed computing
- parallel
    - multiprocessor
    - MIMD,SISD,SIMD
- distributed
    - linking serveral computers via network
    - separte processors,separate memory
- lssues
    - data dependency
    - load dependency
    - load balancing
    - synchonization
    - reliability

---

平行是人工做的，目前電腦難做到自動化
平行不一定好，可能花時間同步
parallel
multiproessor
distributed
serveral
via
separte 
processors
separate
lssues
denpendency
load dependency
balancing
stynchoniztion
relibility

---

# batch processing
- computer operators
- first-in first-out(FIFO)
作業系統是物超所值去使用硬體
terminal的名稱來源是因為有好多節點
# innteractive processing
- OS with remote terminals

# different types of OS
- batch
- interctive
- real-time
    - response time is critical
- time-sharing and is criticl
    - dividing time into intrvaals
    - only one task is being performed at any given time
- multiprocessor
    - load balancting
    - scaling
---

# shells
- commmunication with users
    - text based
    - GUI(graphics user interface), such as window manager

---

# kernel
- file manager
    - directory/folder,path
- device deivers 
- memory manager
    - allocating main memory
    - paging,virtul memory
- scheduler
- dispatcher
- can you recognize these shell and kernel components on your PC?

linux比較少人用
檔案破碎問題
dir 列表
cd \ 到根目錄
memory manager 記憶體管理
虛擬記憶體(硬碟) 把還未需要執行的程式放在這邊準備，等需要再放到主記憶做使用

---

# linux world
- originally made by liuns torvalds in 1991
- freeware & open-source
- many distro(linux distributionns)
    - for beginner:linux mint
    - personal favorite:Gentoo
- in fact,linux means only kernel
- better call it GNU/linux?
- servers,,PCs,embedded systems(android's kernel is based on linux)
- apple use BSD
- boot strappintg(booting)
- you may change the booting sequence in BIOS(basic input/output system)
linux老師推薦試試看Gentoo筆電不適合，因為需要重複的讀寫

7-zip可以去用（免費）
boot loader 電腦一進來最新執行

---

# process(要記得是執行中的)
- process
    - the activity of executing a program
- process state
    - program coounter
    - general purpose registers
    - assoiated memory cells
- process table 
    - memory area assigned to the process
- process table
    - memory are assigned to the process
    - priority
    - ready/waiting
---
# process administration
- scheduler
    - maintains the process table
        - introduces new processes
        - removes completed processes
        - decides whether a prcess is ready or waiting
- dispatcher
    - really execute the program
        - controls the allocation of time slices to the processes in th process table
        - process switch(context switch) by calling interrupt

scheduler 行程
calling interrupt  調用中斷 

#semaphores
- a visual signaling apparatus with flags, light, or mechanically moving arm, as one on a railrod
- atomic TEST-AND-SET
- critical region
- mutual exclusion

---

# prerequisites for deadlock
- deadlock may occur only if three of the following(necessary but insufficient) conditions are satisfied:
    - competition for non-shareabl resoources
    - resource are requested on a partial basis; this is, having received some resources, a process will return  later to request more
    - once a resource has been allocated; it cannot be forcibly retrieved

# deadlock VS. starvation
- starvation: process cannot get the resources needed for a long time because the resoureces are being allocated to other processes
- aging:adding an aging factor to the prioripy of each request


死結對上飢餓

---

# security
- insecure passwords & bad habits
- auditing software(record and analyze activities)
- snifing software
- virus/worms/trojan horses
- privilege levels & privileged in strctions


# network classifications
- scope
    - LAN:local area netwook
    - MAN:metroplitan area network
    - WAN:wide area network
- ownership
    - closed
    - open
- topology

# protocols
- token ring 
    - popular in ring topology
    - toke and messages are passed in one direction
    - only the machine that gets the token can trnsmit its own message
- CSMA/CD(carrier sense, multiple)
    - populsr in bus machines wait for a brieff random timme before trying again
    - CSMA/CA(carrier sense, multiple access with collision voidnce)
- CSMA/CA(carrier sense, muoltiple aaccess with collision avoidance)
    - populaar in wireless Ethernet
    - broadcsting
    - detect if a chnnell is idle, if so, wit for a brief random time and then detect again. if the channel is stil idle, start sending
