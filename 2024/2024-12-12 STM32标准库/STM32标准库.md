---
title: STM32标准库
date: 2024-12-12
tag:
- STM32
- 手册
cover: https://github.com/choomoray/choomoray.github.io/blob/article/2024/2024-12-12%20STM32%E6%A0%87%E5%87%86%E5%BA%93/%E5%B0%81%E9%9D%A2.png?raw=true
---

# GPIO通用输入/输出

GPIO驱动可以用作多个用途，包括管脚设置，单位设置/重置，锁定机制，从端口管脚读入或者向端口管脚写入数据



{% tabs GPIO %}

<!-- tab 库函数 -->

{% note 'fab fa-github' modern%}

**[stm32f10x_gpio.h](https://github.com/choomoray/choomoray.github.io/blob/RII/%E6%96%87%E4%BB%B6/STM32/Library/stm32f10x_gpio.h)**

{% endnote %} {% note 'fab fa-github' modern%}

**[stm32f10x_gpio.c](https://github.com/choomoray/choomoray.github.io/blob/RII/%E6%96%87%E4%BB%B6/STM32/Library/stm32f10x_gpio.c)**

{% endnote %}



| 函数名                      | 描述                                                     |
| --------------------------- | -------------------------------------------------------- |
| GPIO_DeInit                 | 将外设 GPIOx 寄存器重设为缺省值                          |
| GPIO_AFIODeInit             | 将复用功能（重映射事件控制和 EXTI 设置）重设为缺省值     |
| **[GPIO_Init](#GPIO-Init)** | 根据 GPIO_InitStruct 中指定的参数初始化外设 GPIOx 寄存器 |
| GPIO_StructInit             | 把 GPIO_InitStruct 中的每一个参数按缺省值填入            |
| GPIO_ReadInputDataBit       | 读取指定端口管脚的输入                                   |
| GPIO_ReadInputData          | 读取指定的 GPIO 端口输入                                 |
| GPIO_ReadOutputDataBit      | 读取指定端口管脚的输出                                   |
| GPIO_ReadOutputData         | 读取指定的 GPIO 端口输出                                 |
| GPIO_SetBits                | 设置指定的数据端口位                                     |
| GPIO_ResetBits              | 清除指定的数据端口位                                     |
| GPIO_WriteBit               | 设置或者清除指定的数据端口位                             |
| GPIO_Write                  | 向指定 GPIO 数据端口写入数据                             |
| GPIO_PinLockConfig          | 锁定 GPIO 管脚设置寄存器                                 |
| GPIO_EventOutputConfig      | 选择 GPIO 管脚用作事件输出                               |
| GPIO_EventOutputCmd         | 使能或者失能事件输出                                     |
| GPIO_PinRemapConfig         | 改变指定管脚的映射                                       |
| GPIO_EXTILineConfig         | 选择 GPIO 管脚用作外部中断线路                           |



<!-- endtab -->

<!-- tab 寄存器 -->

| 寄存器 | 描述                          |
| ------ | ----------------------------- |
| CRL    | 端口配置低寄存器              |
| CRH    | 端口配置高寄存器              |
| IDR    | 端口输入数据寄存器            |
| ODR    | 端口输出数据寄存器            |
| BSRR   | 端口位设置/复位寄存器         |
| BRR    | 端口位复位寄存器              |
| LCKR   | 端口配置锁定寄存器            |
| EVCR   | 事件控制寄存器                |
| MAPR   | 复用重映射和调试I/O配置寄存器 |
| EXTICR | 外部中断线路0-15配置寄存器    |



```c
typedef struct {
    vu32 CRL;
    vu32 CRH;
    vu32 IDR;
    vu32 ODR;
    vu32 BSRR;
    vu32 BRR;
    vu32 LCKR;
}
GPIO_TypeDef;
typedef struct {
    vu32 EVCR;
    vu32 MAPR;
    vu32 EXTICR[4];
}
AFIO_TypeDef;
```





<!-- endtab -->

{% endtabs %}



## GPIO_Init



{%tabs GPIO_Init%}

<!--tab 函数-->

| 函数原形   | void GPIO_Init(GPIO_TypeDef* GPIOx, GPIO_InitTypeDef* GPIO_InitStruct) |
| ---------- | ------------------------------------------------------------ |
| 功能描述   | 根据 GPIO_InitStruct 中指定的参数初始化外设 GPIOx 寄存器     |
| 输入参数 1 | GPIOx：x 可以是 A，B，C，D 或者 E，来选择 GPIO 外设          |
| 输入参数 2 | GPIO_InitStruct：指向结构 GPIO_InitTypeDef 的指针，包含了外设 GPIO 的配置信息 |
| 输出参数   | 无                                                           |
| 返回值     | 无                                                           |
| 先决条件   | 无                                                           |
| 被调用函数 | 无                                                           |

### **GPIO_InitTypeDef structure**
GPIO_InitTypeDef 定义于文件“stm32f10x_gpio.h”：

```c
typedef struct {
    u16 GPIO_Pin;
    GPIOSpeed_TypeDef GPIO_Speed;
    GPIOMode_TypeDef GPIO_Mode;
}
GPIO_InitTypeDef;
```



{%tabs GPIO_InitTypeDef, 2%}

<!--tab Pin-->

该参数选择待设置的 GPIO 管脚，使用操作符“`|`”可以一次选中多个管脚。可以使用下表中的任意组合。

| GPIO_Pin      | 描述         |
| ------------- | ------------ |
| GPIO_Pin_None | 无管脚被选中 |
| GPIO_Pin_0    | 选中管脚 0   |
| GPIO_Pin_1    | 选中管脚 1   |
| GPIO_Pin_2    | 选中管脚 2   |
| GPIO_Pin_3    | 选中管脚 3   |
| GPIO_Pin_4    | 选中管脚 4   |
| GPIO_Pin_5    | 选中管脚 5   |
| GPIO_Pin_6    | 选中管脚 6   |
| GPIO_Pin_7    | 选中管脚 7   |
| GPIO_Pin_8    | 选中管脚 8   |
| GPIO_Pin_9    | 选中管脚 9   |
| GPIO_Pin_10   | 选中管脚 10  |
| GPIO_Pin_11   | 选中管脚 11  |
| GPIO_Pin_12   | 选中管脚 12  |
| GPIO_Pin_13   | 选中管脚 13  |
| GPIO_Pin_14   | 选中管脚 14  |
| GPIO_Pin_15   | 选中管脚 15  |
| GPIO_Pin_All  | 选中全部管脚 |


 <!--endtab-->

<!--tab Speed-->

| GPIO_Speed       | 描述               |
| ---------------- | ------------------ |
| GPIO_Speed_10MHz | 最高输出速率 10MHz |
| GPIO_Speed_20MHz | 最高输出速率 20MHz |
| GPIO_Speed_50MHz | 最高输出速率 50MHz |

<!--endtab-->

<!--tab Mode-->

GPIO_Mode 用以设置选中管脚的工作状态。

| GPIO_Speed            | 描述         |
| --------------------- | ------------ |
| GPIO_Mode_AIN         | 模拟输入     |
| GPIO_Mode_IN_FLOATING | 浮空输入     |
| GPIO_Mode_IPD         | 下拉输入     |
| GPIO_Mode_IPU         | 上拉输入     |
| GPIO_Mode_Out_OD      | 开漏输出     |
| GPIO_Mode_Out_PP      | 推挽输出     |
| GPIO_Mode_AF_OD       | 复用开漏输出 |
| GPIO_Mode_AF_PP       | 复用推挽输出 |

{% note warning flat %}

* 当某管脚设置为上拉或者下拉输入模式，使用寄存器 Px_BSRR 和 PxBRR

* GPIO_Mode 允许同时设置 GPIO 方向（输入/输出）和对应的输入/输出设置，：位[7:4]对应 GPIO 方向，位[4:0]对应配置。GPIO 方向有如下索引

  * GPIO 输入模式 = 0x00

  * GPIO 输出模式 = 0x01

{% endnote %}

| GPIO方向    | 索引 | 名称 | 模式                  | 设置 | 模式代码 |
| ----------- | ---- | ---- | --------------------- | ---- | -------- |
| GPIO Input  | 0x00 |      | GPIO_Mode_AIN         | 0x00 | 0x00     |
|             |      |      | GPIO_Mode_IN_FLOATING | 0x04 | 0x04     |
|             |      |      | GPIO_Mode_IPD         | 0x08 | 0x28     |
|             |      |      | GPIO_Mode_IPU         | 0x08 | 0x48     |
| GPIO Output | 0x01 |      | GPIO_Mode_Out_OD      | 0x04 | 0x14     |
|             |      |      | GPIO_Mode_Out_PP      | 0x00 | 0x10     |
|             |      |      | GPIO_Mode_AF_OD       | 0x0C | 0x1C     |
|             |      |      | GPIO_Mode_AF_PP       | 0x08 | 0x18     |

<!--endtab-->

{%endtabs%}

 



<!--endtab-->

<!--tab 源码-->

```c
void GPIO_Init(GPIO_TypeDef* GPIOx, GPIO_InitTypeDef* GPIO_InitStruct);
```

```c
/**
 * @brief  Initializes the GPIOx peripheral according to the specified
 *         parameters in the GPIO_InitStruct.
 * @param  GPIOx: where x can be (A..G) to select the GPIO peripheral.
 * @param  GPIO_InitStruct: pointer to a GPIO_InitTypeDef structure that
 *         contains the configuration information for the specified GPIO peripheral.
 * @retval None
 */
void GPIO_Init(GPIO_TypeDef * GPIOx, GPIO_InitTypeDef * GPIO_InitStruct) {
    uint32_t currentmode = 0x00, currentpin = 0x00, pinpos = 0x00, pos = 0x00;
    uint32_t tmpreg = 0x00, pinmask = 0x00;
    /* Check the parameters */
    assert_param(IS_GPIO_ALL_PERIPH(GPIOx));
    assert_param(IS_GPIO_MODE(GPIO_InitStruct -> GPIO_Mode));
    assert_param(IS_GPIO_PIN(GPIO_InitStruct -> GPIO_Pin));

    /*---------------------------- GPIO Mode Configuration -----------------------*/
    currentmode = ((uint32_t) GPIO_InitStruct -> GPIO_Mode) & ((uint32_t) 0x0F);
    if ((((uint32_t) GPIO_InitStruct -> GPIO_Mode) & ((uint32_t) 0x10)) != 0x00) {
        /* Check the parameters */
        assert_param(IS_GPIO_SPEED(GPIO_InitStruct -> GPIO_Speed));
        /* Output mode */
        currentmode |= (uint32_t) GPIO_InitStruct -> GPIO_Speed;
    }
    /*---------------------------- GPIO CRL Configuration ------------------------*/
    /* Configure the eight low port pins */
    if (((uint32_t) GPIO_InitStruct -> GPIO_Pin & ((uint32_t) 0x00FF)) != 0x00) {
        tmpreg = GPIOx -> CRL;
        for (pinpos = 0x00; pinpos < 0x08; pinpos++) {
            pos = ((uint32_t) 0x01) << pinpos;
            /* Get the port pins position */
            currentpin = (GPIO_InitStruct -> GPIO_Pin) & pos;
            if (currentpin == pos) {
                pos = pinpos << 2;
                /* Clear the corresponding low control register bits */
                pinmask = ((uint32_t) 0x0F) << pos;
                tmpreg &= ~pinmask;
                /* Write the mode configuration in the corresponding bits */
                tmpreg |= (currentmode << pos);
                /* Reset the corresponding ODR bit */
                if (GPIO_InitStruct -> GPIO_Mode == GPIO_Mode_IPD) {
                    GPIOx -> BRR = (((uint32_t) 0x01) << pinpos);
                } else {
                    /* Set the corresponding ODR bit */
                    if (GPIO_InitStruct -> GPIO_Mode == GPIO_Mode_IPU) {
                        GPIOx -> BSRR = (((uint32_t) 0x01) << pinpos);
                    }
                }
            }
        }
        GPIOx -> CRL = tmpreg;
    }
    /*---------------------------- GPIO CRH Configuration ------------------------*/
    /* Configure the eight high port pins */
    if (GPIO_InitStruct -> GPIO_Pin > 0x00FF) {
        tmpreg = GPIOx -> CRH;
        for (pinpos = 0x00; pinpos < 0x08; pinpos++) {
            pos = (((uint32_t) 0x01) << (pinpos + 0x08));
            /* Get the port pins position */
            currentpin = ((GPIO_InitStruct -> GPIO_Pin) & pos);
            if (currentpin == pos) {
                pos = pinpos << 2;
                /* Clear the corresponding high control register bits */
                pinmask = ((uint32_t) 0x0F) << pos;
                tmpreg &= ~pinmask;
                /* Write the mode configuration in the corresponding bits */
                tmpreg |= (currentmode << pos);
                /* Reset the corresponding ODR bit */
                if (GPIO_InitStruct -> GPIO_Mode == GPIO_Mode_IPD) {
                    GPIOx -> BRR = (((uint32_t) 0x01) << (pinpos + 0x08));
                }
                /* Set the corresponding ODR bit */
                if (GPIO_InitStruct -> GPIO_Mode == GPIO_Mode_IPU) {
                    GPIOx -> BSRR = (((uint32_t) 0x01) << (pinpos + 0x08));
                }
            }
        }
        GPIOx -> CRH = tmpreg;
    }
}
```

<!--endtab -->

<!-- tab 使用-->

```c
void main(void)
{
    RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOB, ENABLE);

    // 1.声明 GPIOB_InitStructure
    GPIO_InitTypeDef GPIOB_InitStructure;
    
    // 2.配置 GPIOB_InitStructure
    GPIOB_InitStructure.GPIO_Mode = GPIO_Mode_IPU;
    GPIOB_InitStructure.GPIO_Pin = GPIO_Pin_12 | GPIO_Pin_15;
    GPIOB_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
    
    // 3.配置 GPIO_Init
    GPIO_Init(GPIOB, &GPIOB_InitStructure);
}
```



<!--endtab-->

{% endtabs %}
