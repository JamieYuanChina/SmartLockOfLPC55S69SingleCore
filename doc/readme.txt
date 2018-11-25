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


��������չIO����ʹ�������
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

������Э�飺
================
��Դ5V��ͨѶ3.3V
������Э�飬����ASCII�룬����"p0.pic=1"(�ر�)����"p0.pic=2"(��)�����ƽ�����ʾ����״̬��
������������ʱ�����ڻᷢ��0x01(�ر�)����0x02(��)
���ڲ�����9600

��������Э��
================
����Э�飬������ʹ��HC-08����ģ�飬��Դ3.3V������ͨѶ
���ڲ�����Ϊ9600
���յ�0x30���������յ�0x31����
ͬ������ʱͬ������0x31������ʱͬ��0x30

WIFI����Э��
================
ģ��ʹ��ESP-01S����Դ3.3V������ͨѶ��������115200.
�����Ĳ�����Ҫ����
�������Ӻͽ����Ȩ��
�жϽ�����Ҫ����
��ʱ����״̬
״̬�ı估ʱͬ��


��ѭ���߼�
================
�����Դ����Ƿ��յ����ݣ�����н��д���
���WiFi�����Ƿ��յ����ݣ�����н��д���
������������Ƿ��յ����ݣ�����н��д���
���LCD�����Ƿ��յ����ݣ�����н��д���
��ʱ�������ݵ����Դ���
��ʱ�������ݵ���������
��ʱ�������ݵ�WiFi����
��ʱ�������ݵ�LCD����
�����״̬������ֵ�����ݸ�ֵ���д���
�����Ҫͬ������ͬ����Ϣ��LCD��WIFI��Debug���ڵȵ�
��ʱ10ms

�ļ��޸��б�
================
1��board/pin_mux.h��pin_mux.h����Ҫ����������IO�Ĺ��ܣ�����ʹ�õ���LED�ƺ��ĸ�����
2��doc/readme.txt����Ҫ����˵�������̵�һЩ��Ϣ��
3��Source/Common.h����Ҫ�Ƕ����õ���һЩ��������
4��Source/MqttKit.h��MqttKit.c�������������ӵ�OneNET�Ʒ�������Э������ļ�����ֲ��OneNET�ٷ�����
5��Source/smart_lock.c�����̵���Ҫ�ļ���ʵ�����������ӣ����Դ������ӣ�wifi���ӵ��Ʒ�������

ʵ�ֵ���Ҫ����
================
1������ͨ�����Դ��ڽ��п�����״̬��
2������ͨ��LCD��Ļ������״̬��
3������ͨ������������״̬��
4������ͨ��Զ��web�����ֻ�app������״̬��
5�����п���;��������״̬ͬ����������webҳ���޸�״̬����LCD�������ϻ�ͬ��״̬��

�������Ĺ���
================
1������smart_lock.c�ļ�������ע�ͺʹ����ʽ����
2��ʵ��˫�˰汾�ĳ�����Ҫ������core1ʵ��led�ƵĿ��Ƽ��ɡ�
