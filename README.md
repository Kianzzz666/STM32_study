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
