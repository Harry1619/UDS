# 1、诊断的模式
>诊断：诊断仪器对车辆系统的监控称为诊断。

（1）在线模式：汽车中的仪表对汽车的实时数据的显示

（2）离线模式：利用外接设备通过汽车的UBD接口进行诊断通讯，从而掌握汽车的故障信息和实时数据。

**诊断协议**：外部仪器与汽车通讯的方式所遵循的原则。

诊断协议定义了：

【1】请求和响应的规则。

【2】ECU如何处理这个相应的机制。

【3】请求/响应中报文所在的数据实际内容的物理解析方式。

# 2、诊断协议的分类
（1）ISO 14230：基于K线的诊断协议。KWP2000

（2）ISO 15765:基于CAN线的诊断协议

（3）ISO 15031：排放相关的定义

# 3、ISO 14229

## (1)服务概览
![Aaron Swartz](https://raw.githubusercontent.com/Harry1619/UDS/Develope/Notes/Pictures/1.png)

**注1:NRC参考ISO14229-1 Page229**

**注2：SID总共26种，参考ISO14229-1**

* 有四种不同类型的UDS服务
  
  * SID
  * SID + SF
  * SID + DID
  * SID + SF + DID

**注：SF = Subfunction  DID = Data Identifier**

## (2)#10服务-诊断会话控制 
>为什么存在诊断会话的控制：由于不同的会话中所支持的服务的类型或者数量不同。

当ECU上电时，ECU进入默认会话。此时如果改变ECU的会话状态以实现在此会话状态下的服务，可通过$\color{#FF0000}{10+SF}$ 来进入非默认会话。$\color{#FF0000}{当进入非默认会话时，ECU不会一直停留在此会话状态，在ECU的内部存在一个计时器，当计时器到达相应的时间后，ECU会自动跳转到默认会话状态，如果想要ECU一致保持在非默认会话状态，可通过**3E**服务来保持此当前会话状态}$

![Aaron Swartz](https://raw.githubusercontent.com/Harry1619/UDS/Develope/Notes/Pictures/2.jpg)

## (3)#27服务-安全访问
> ECU中存在很多数据，这些数据是我们整车厂所有的，当这些数据并不希望开放给所有客户，因此就存在了安全访问。

![Aaron Swartz](https://raw.githubusercontent.com/Harry1619/UDS/Develope/Notes/Pictures/3.jpg)


![Aaron Swartz](https://raw.githubusercontent.com/Harry1619/UDS/Pictures/Notes/Pictures/4.jpg)

**注：level n**

## (4)#22服务-通过DID读取数据


![Aaron Swartz](https://raw.githubusercontent.com/Harry1619/UDS/Pictures/Notes/Pictures/5.jpg)

## (5)#2E服务-通过DID写入数据

 ![Aaron Swartz](https://raw.githubusercontent.com/Harry1619/UDS/Pictures/Notes/Pictures/6.jpg)

 ## (6)#19服务-读取DTC（Diagnostic Trouble Code）

在不同的协议中有着不同的DTC格式，一般DTC一共三个字节，前两个字节为$\color{FF0000}{Root DTC}$,后一个字节为$\color{FF0000}{FTB}$(通常还会有一个字节存放状态掩码（Status Mask）)
![Aaron Swartz](https://raw.githubusercontent.com/Harry1619/UDS/Pictures/Notes/Pictures/7.jpg)

![Aaron Swartz](https://raw.githubusercontent.com/Harry1619/UDS/Pictures/Notes/Pictures/8.jpg)


![Aaron Swartz](https://raw.githubusercontent.com/Harry1619/UDS/Pictures/Notes/Pictures/9.jpg)



![Aaron Swartz](https://raw.githubusercontent.com/Harry1619/UDS/Pictures/Notes/Pictures/10.jpg)

**注：DTC Status Byte 参考ISO 14229-1:2013附录D部分**


![Aaron Swartz](https://raw.githubusercontent.com/Harry1619/UDS/Pictures/Notes/Pictures/11.jpg)

## (7)#14服务-清除诊断信息


![Aaron Swartz](https://raw.githubusercontent.com/Harry1619/UDS/Pictures/Notes/Pictures/12.jpg)