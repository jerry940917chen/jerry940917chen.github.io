---
layout : post
title : fluent-bit相關內容
author : Rick Chen
tag : Linux
date : 2022-08-04
---

## fluent-bit 使用狀況
### 官方聲明
* 2020 年 Fluent Bit 部署超過2.2 億次，並且每天繼續部署超過100 萬次。

![image](https://user-images.githubusercontent.com/62127656/182776901-ff986e77-ed10-4b06-9f78-4e518c1ee981.png)

* 使用 apache license2.0，提供個人及商業上使用。

### Google
![image](https://user-images.githubusercontent.com/62127656/182534146-2a53e071-5c88-4dee-8a21-afe19ca72169.png)
![image](https://user-images.githubusercontent.com/62127656/182534604-e409cdcd-f8d3-4d88-93e9-95b09f1ce5d5.png)
### Github 
![image](https://user-images.githubusercontent.com/62127656/182535545-570f5046-2112-4aab-b8fc-4ab98cae041c.png)

### security 
* 支持TLS跟ssl在實現上統稱TLS

![image](https://user-images.githubusercontent.com/62127656/182535795-0c1fa8e2-9092-45ff-9d57-fd4fc20f0823.png)
![image](https://user-images.githubusercontent.com/62127656/182535799-49481b96-2852-47af-b682-0d4d3a4e924e.png)

![image](https://user-images.githubusercontent.com/62127656/182778817-9a99fcc6-d76e-4c3b-b76c-2046beffbbc1.png)
![image](https://user-images.githubusercontent.com/62127656/182778911-8f986452-c1b0-49a8-bce0-546b118e4532.png)
![image](https://user-images.githubusercontent.com/62127656/182779224-b120390e-35ec-4bee-b8b4-2910688ec292.png)
![image](https://user-images.githubusercontent.com/62127656/182779277-184452c7-666f-4a37-a013-8533fc0197f5.png)


## plugins

### CPU 
* 目前只能linux系統
* 以百分比為單位，報告某個period的值

![image](https://user-images.githubusercontent.com/62127656/182537733-e4ef1860-d5ea-4904-b749-b554523d486d.png)
> cpu_p: 整個系統、 user_p: 使用者使用量、 system_p: 核心使用量， cpuN.p_cpu 、 cpuN.p_user 、 cpuN.p_system 是個別的使用量

* 可調參數有三個: 
   * Interval_Sec : 一秒一次，預設為1 (1為true 0為false)
   * Interval_NSec: 一奈秒一次，預設為0 
   * PID: 只針對指定PID的process去進行偵測，沒設就整體電腦

### health 
* tcp port是否開放

![image](https://user-images.githubusercontent.com/62127656/182757795-9600c132-adb8-4ed0-b82c-21f56738b5d0.png)
> 會顯示alive 為true or false

```
[INPUT]
    name health
    tag health.check
    host 192.168.2.157
    port 9487
    interval_sec 1
```

* 可調調參數:
   * Host : ip 或 域名
   * Port : 要偵測的port
   * Interval_Sec : 一秒一次 ,預設為1
   * Interval_NSec : 一奈秒一次，預設為0
   * Alert : 如果是enabled則只有port掛掉才傳message 預設為disabled
   * Add_Host : 如果是true，則添加 hostname欄位，預設為false
   * Add_Port : 如果是true，則添加port欄位，預設為false

### memory
* 監控memory 跟 swap的total used free
* 沒有其它參數可調
```
[INPUT]
    name mem
    tag memory.local
```

![image](https://user-images.githubusercontent.com/62127656/182773694-19c115fb-89e5-4ea2-9de5-ba3c5e79d84b.png)


### disk 
* 監控硬碟讀寫狀況，會有read and write 兩個欄位
* 可調參數:
   * Interval_Sec : 秒為單位紀錄 default 為 1
   * Interval_NSec : 奈秒為單位紀錄 default 為 0
   * Dev_Name : 可以輸入裝置的名稱讓他只讀那個 default 為 all disks

```
[INPUT]
    name disk
    tag disk.local
    interval_sec 1
```

![image](https://user-images.githubusercontent.com/62127656/182774013-2aeb879a-f2ad-428e-bae3-f9f65a37365d.png)

### Exec
* 允許執行外部指令或程式以及蒐集事件的log
* 可調參數
  * command : 要下的指令
  * Parser : 去parser指令後得到的結果
  * Interval_Sec : 以秒為單位執行
  * Interval_NSec : 以奈秒為單位執行
  * Buf_Size : Buffer區的大小
  * Oneshot : 是否只在fluentbit 啟動的時候執行 default為false

```
[INPUT]
    name exec
    tag exec.ls
    command cat /root/test123.log
    interval_sec 1
    Buf_size 8mb
    oneshot false
```
![image](https://user-images.githubusercontent.com/62127656/182776255-4625968a-97ee-4e51-bf41-d4a5a11cbb95.png)


### config 爆掉會crash
