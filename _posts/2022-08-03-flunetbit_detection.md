## 探討fluent-bit 使用狀況
### Google
![image](https://user-images.githubusercontent.com/62127656/182534146-2a53e071-5c88-4dee-8a21-afe19ca72169.png)
![image](https://user-images.githubusercontent.com/62127656/182534604-e409cdcd-f8d3-4d88-93e9-95b09f1ce5d5.png)
### Github 
![image](https://user-images.githubusercontent.com/62127656/182535545-570f5046-2112-4aab-b8fc-4ab98cae041c.png)

### security 
* 支持TLS跟ssl在實現上統稱TLS

![image](https://user-images.githubusercontent.com/62127656/182535795-0c1fa8e2-9092-45ff-9d57-fd4fc20f0823.png)
![image](https://user-images.githubusercontent.com/62127656/182535799-49481b96-2852-47af-b682-0d4d3a4e924e.png)

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
