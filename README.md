# STM32_study
logs of personal study of STM32 

先初始化RCC  
NVIC不需要开启时钟  
**最好不要在中断函数和主函数调用相同的函数或操作同一个硬件，因为外部硬件在进入中断时并没有现场保护  

TIM定时器  
16位计数器、预分频器、自动重装寄存器（计数目标值 ）的时基单元，在72MHz技术时钟下可以实现最大59.65的定时  
不仅具备基本的定时中断功能，而且还包含内外时钟选择、输入捕获（测量方波频率）、输出比较（产生PWM波形）、编码器接口（更加方便读取正交编码器的输出波形）、主从触发模式等多种功能  
根据复杂度和应用场景分为了高级定时器、通用定时器、基本定时器三种类型  
![image](https://github.com/user-attachments/assets/12eabac5-59cf-4c47-82e8-cfdec10bb9f1)

IC(Input Capture) 输入捕获  
-输入捕获模式下，当通道输入引脚出现指定电平跳变时，当前CNT的值被锁存到CCR中，可用于测量PWM波形的频率、占空比、脉冲间隔、电平持续时间等参数  
-每个高级定时器和通用定时器都拥有4个输入捕获通道  
-可配置为PWMI模式，同时测量频率和占空比  
-可配合主从触发模式，实现硬件全自动测量  
第一步，RCC开启时钟（GPIO和TIM）  
第二步，GPIO初始化，配置GPIO模式  
第三步，配置时基单元，让CNT计数器在内部时钟的驱动下自增运行  
第四步，配置输入捕获单元，包括滤波器、极性、通道、分频器等参数  
第五步，选择从模式触发源  
第六步，选择触发之后执行的操作  
最后,调用TIM_Cmd开启时钟  
![image](https://github.com/user-attachments/assets/089d9ffd-1625-499c-af1f-90db9f603606)

Encoder Interface 编码器接口  
自动给编码器进行计次 相比中断节省了软件资源  
-编码器接口可以接收增量（正交）编码器的信号，根据编码器旋转产生的正交信号脉冲，自动控制CNT自增或自减，从而指示编码器的位置、旋转方向和旋转速度  
-每个高级定时器和通用定时器都拥有1个编码器接口  
-两个输入引脚借用了输入捕获的通道1和通道2（CH1和CH2）  
*编码器接口就是一个带方向控制的外部时钟  
第一步，RCC开启时钟  
第二步，GPIO初始化，配置GPIO模式  
第三步，配置时基单元，让CNT计数器在内部时钟的驱动下自增运行  
第四步，配置输入捕获单元  
第五步，配置编码器接口模式  
最后，TMI_cmd启动时钟

ADC转换器  
-12逐次逼近型ADC，1us转换时间  
-输入电压范围：0-3.3v，转换结果范围：0-4095  
-18个输入通道，可测量16个外部和2个内部信号源  
-规则组和注入组两个转换单元  
-模拟看门狗自动检测输入电压范围  
![image](https://github.com/user-attachments/assets/a8ba2fd5-80cf-46b7-81aa-93b585db173f)

DMA（Direct Memory Access）直接存储器存取  
DMA可以提供外设和存储器（SRAM或FLASH）或者存储器和存储器之间的高速数据传输，无需CPU干预，节省了CPU的资源  
12个独立可配置的通道：DMA1（7个通道），DMA2（5个通道）  
每个通道都支持软件触发和特定的硬件触发  
![image](https://github.com/user-attachments/assets/ceb16176-084e-4f31-883d-61820a6453c3)

通信接口  
通信的目的：将一个设备的数据传送到另一个设备，扩展硬件系统
![image](https://github.com/user-attachments/assets/1aebbf22-569a-4f2a-a8bb-f05958054fcd)

在大机器人更换电池时，拆下旧电池后的大机器人无法自己装上新电池，因此这时需要一个小机器人来辅助  
在串口烧录中，程序的烧录本身也是程序，因此串口烧录就像大机器人更换电池，需要BootLoader此时作为一个小机器人来辅助烧录
![image](https://github.com/user-attachments/assets/29c65cd5-56a5-4cdd-a1c2-5bb6f3f7aa40)

I2C通信协议  
时序基本单元
![image](https://github.com/user-attachments/assets/91361a6b-317b-4e3e-8e3e-b917a01336c9)
![image](https://github.com/user-attachments/assets/5557eee9-3227-4809-bb91-183ee82468e2)

SPI通信协议 Serial Peripheral Interface  
![image](https://github.com/user-attachments/assets/71551cb6-46fb-42ee-902d-284549a208f2)

![image](https://github.com/user-attachments/assets/9f545244-6874-40af-b071-e920bdfec045)













