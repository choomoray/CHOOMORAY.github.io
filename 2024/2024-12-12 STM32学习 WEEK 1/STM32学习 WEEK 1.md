---
title: STM32 学习 WEEK 1
date: 2024-12-06
tag:
- STM32
categories: 
- 学习
- STM32
cover: https://github.com/choomoray/choomoray.github.io/blob/_posts/2024/2024-12-12%20STM32%E5%AD%A6%E4%B9%A0/%E5%B0%81%E9%9D%A2.jpg?raw=true
---







# Day 1 2024-12-06

## 创建STM32工程(...)

{% tabs 创建工程 %}

<!--tab 模板下载-->

工程创建实在是太复杂了，这边建议直接复制以前写好的工程呢【[工程模板下载](https://github.com/choomoray/choomoray.github.io/blob/RII/%E6%96%87%E4%BB%B6/STM32/STM32%E5%B7%A5%E7%A8%8B%E6%A8%A1%E6%9D%BF.zip)】

<!--endtab-->

<!-- tab 详细步骤-->

详细步骤见视频【[江科大STM32](https://www.bilibili.com/video/BV1th411z7sn?t=228.8&p=4)】

<!--endtab-->

<!-- tab VsCode-->

使用官方扩展程序【Keil Assistant】可以在工程项目创建好的情况下写代码，但是文件添加等操作还是要在keil上完成

<!--endtab-->

{% endtabs %}









## 点亮LED

{%tabs 点亮LED%}

<!-- tab 1-->

STM32学习摒弃了C51单片机的寄存器编程，使用更便捷的标准库函数编程

LED小灯有两个针脚，较长的接电源正极，较短的接地

STM32最小系统接通电源时，所有的针脚默认高电平，因此想让LED灯亮起共有两种接法：

1. LED长针脚接电源正极，短针脚接STM32
2. LED短针脚接电源负极，长针脚接STM32

上面两种接法使用到了STM32的两种输出模式，分别是：推挽输出和（...）

1. 长针脚接电源正极，电源供能，因此只需要STM32变换端口高低电平就可控制LED灯的亮灭
2. 长针脚接电源负极，由STM32供能，需要注意的是STM32电压可能不足以让LED亮起，因此需要放大端口电压才能控制LED正常亮灭

<!--endtab-->





<!-- tab 代码实现-->



```c
int main(void)
{
	RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOA, ENABLE);
	
	GPIO_InitTypeDef GPIOA_InitStructure;
	GPIOA_InitStructure.GPIO_Mode = GPIO_Mode_Out_PP;
	GPIOA_InitStructure.GPIO_Pin = GPIO_Pin_0 | GPIO_Pin_2;
	GPIOA_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
	GPIO_Init(GPIOA, &GPIOA_InitStructure);

	GPIO_ResetBits(GPIOA, GPIO_Pin_0);

	while (1)
	{
		
	}
}
```





<!--endtab-->





<!-- tab 要点-->



<!--endtab-->

{%endtabs%}















