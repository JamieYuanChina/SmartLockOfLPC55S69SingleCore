Overview
========
The smart_lock project shows how to use lpc5500.

Hardware requirements
=====================
- Micro USB cable
- LPCXpresso55s69 board
- Personal Computer

Board settings
==============
No special is needed.

Prepare the Demo
================
1.  Connect a micro USB cable between the PC host and the LPC-Link USB port (P6) on the board.
2.  Open a serial terminal with the following settings:
    - 115200 baud rate
    - 8 data bits
    - No parity
    - One stop bit
    - No flow control
3.  Download the program to the target board.
4.  Reset the SoC and run the project.

Running the demo
================
When the demo runs successfully, the log would be seen on the terminal like:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Smart Lock project example

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Toolchain supported
===================
- IAR embedded Workbench 


开发板扩展IO引脚使用情况：
================
P17
        1       2
        3       4
        5       6 FC1_TXD 
        7       8
        9       10 FC7_RXD
        11      12 FC7_TXD
        13      14
        15      16
        17      18
        19      20
        
P18
        1       2
FC1_RXD 3       4
        5       6
        7       8
        9       10
        11      12
FC2_TXD 13      14
FC2_RXD 15      16
        17      18
        19      20

串口屏协议：
================
电源5V，通讯3.3V
串口屏协议，发送ASCII码，内容"p0.pic=1"(关闭)或者"p0.pic=2"(打开)来控制界面显示开关状态，
当界面点击开关时，串口会发送0x01(关闭)或者0x02(打开)
串口波特率9600

蓝牙串口协议
================
蓝牙协议，在这里使用HC-08蓝牙模块，电源3.3V，串口通讯
串口波特率为9600
接收到0x30开锁，接收到0x31上锁
同样上锁时同步发送0x31，开锁时同步0x30

WIFI串口协议
================
模块使用ESP-01S，电源3.3V，串口通讯，波特率115200.
共有四部分需要处理
建立连接和接入鉴权等
中断接收需要处理
定时发送状态
状态改变及时同步


主循环逻辑
================
检查调试串口是否收到数据，如果有进行处理
检查WiFi串口是否收到数据，如果有进行处理
检查蓝牙串口是否收到数据，如果有进行处理
检查LCD串口是否收到数据，如果有进行处理
定时发送数据到调试串口
定时发送数据到蓝牙串口
定时发送数据到WiFi串口
定时发送数据到LCD串口
检测锁状态变量的值，根据该值进行处理
如果需要同步，则同步信息到LCD，WIFI，Debug串口等等
延时10ms

文件修改列表
================
1、board/pin_mux.h和pin_mux.h，主要是用来定义IO的功能，这里使用到了LED灯和四个串口
2、doc/readme.txt，主要用来说明本工程的一些信息。
3、Source/Common.h，主要是定义用到的一些数据类型
4、Source/MqttKit.h和MqttKit.c，这两个是连接到OneNET云服务器的协议解析文件，移植自OneNET官方程序
5、Source/smart_lock.c本工程的主要文件，实现了蓝牙连接，调试串口连接，wifi连接到云服务器。

实现的主要功能
================
1、可以通过调试串口进行控制锁状态，
2、可以通过LCD屏幕控制锁状态。
3、可以通过蓝牙控制锁状态。
4、可以通过远程web或者手机app控制锁状态。
5、所有控制途径进行了状态同步，比如在web页面修改状态后，在LCD和蓝牙上会同步状态。

接下来的工作
================
1、整理smart_lock.c文件，增加注释和代码格式整理。
2、实现双核版本的程序，主要是利用core1实现led灯的控制即可。
