---
title: STM32 学习 WEEK 1
date: 2025-01-02
tag:
- STM32
categories: 
- 学习
top_img: false
---

# Day 1 2024-12-06

## 创建STM32工程

{% tabs 创建工程 %}


<!--tab 模板下载-->

工程创建实在是太复杂了，这边建议直接复制以前写好的工程【[工程模板下载](https://github.com/choomoray/choomoray.github.io/raw/refs/heads/file/STM32/STM32%E5%B7%A5%E7%A8%8B%E6%A8%A1%E6%9D%BF.zip)】

<!--endtab-->

<!-- tab 详细步骤-->

详细步骤见视频【[江科大STM32](https://www.bilibili.com/video/BV1th411z7sn?t=228.8&p=4)】

<!--endtab-->

<!-- tab VsCode-->

使用官方扩展程序【Keil Assistant】可以在工程项目创建好的情况下写代码，但是文件添加等操作还是要在keil上完成

<!--endtab-->

{% endtabs %}



## 成就：点灯大师

{%tabs 点亮一颗LED%}

<!-- tab 点亮一颗LED-->

{%note no-icon%}

* STM32最小系统接通电源时，所有的针脚默认高电平
* LED小灯有两个针脚，较长的接电源正极，较短的接电源负极

{%endnote%}

知道了怎么接电可以让LED点亮，就延申出长短针脚分别接STM32的两种接法，都是正确可行的，但存在些微区别：控制LED亮灭的电平信号不同。

1. 接线：

   STM32插在面包板中间，从STM32的GND各VCC接口引出两根线接在面包板一侧的电源线上，LED长脚接在面包板+上，短脚接在STM32 A0口上。

2. 写程序

   1. 打开GPIOA所在的RCC时钟，想要使用GPIOA端口，首先要打开所在时钟让其运行，据stm32f10x_rcc.c文件知需要使用`RCC_APB2PeriphClockCmd`函数
   2. 初始化GPIOA，使用到`GPIO_Init`函数
   3. 设置Pin_0口电平来点亮LED，根据接线赋对应电平。



<!--endtab--> <!-- tab 代码实现-->



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

{%endtabs%}



## 感应灯

{%note no-icon%}

<center>项目要求</center>

1. 可以通过按键控制LED亮灭
2. 暗光环境LED亮起（可通过按键关闭LED）
3. 使用**定时器**而非Delay函数

{%endnote%}











