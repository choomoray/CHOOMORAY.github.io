---
title: STM32标准库
date: 2024-12-12
tag:
- STM32
- 手册
categories:
- STM32
top_img: false
cover: https://raw.githubusercontent.com/choomoray/choomoray.github.io/refs/heads/_posts/2024/2024-12-12%20STM32%E6%A0%87%E5%87%86%E5%BA%93/%E5%B0%81%E9%9D%A2.webp
---

# GPIO通用输入/输出

GPIO驱动可以用作多个用途，包括管脚设置，单位设置/重置，锁定机制，从端口管脚读入或者向端口管脚写入数据



{% tabs GPIO %}

<!-- tab 库函数 -->

{% note 'fab fa-github' modern%}

**[stm32f10x_gpio.h](https://github.com/choomoray/choomoray.github.io/blob/_posts/2024/2024-12-12%20STM32%E6%A0%87%E5%87%86%E5%BA%93/Library/stm32f10x_gpio.h)**

{% endnote %} {% note 'fab fa-github' modern%}

**[stm32f10x_gpio.c](https://github.com/choomoray/choomoray.github.io/blob/_posts/2024/2024-12-12%20STM32%E6%A0%87%E5%87%86%E5%BA%93/Library/stm32f10x_gpio.c)**

{% endnote %}



| 函数名                                                | 描述                                                     |
| ----------------------------------------------------- | -------------------------------------------------------- |
| **[GPIO_DeInit](#GPIO-DeInit)**                       | 将外设 GPIOx 寄存器重设为缺省值                          |
| **[GPIO_AFIODeInit](#GPIO_AFIODeInit)**               | 将复用功能（重映射事件控制和 EXTI 设置）重设为缺省值     |
| **[GPIO_Init](#GPIO-Init)**                           | 根据 GPIO_InitStruct 中指定的参数初始化外设 GPIOx 寄存器 |
| **[GPIO_StructInit](#GPIO-StructInit)**               | 把 GPIO_InitStruct 中的每一个参数按缺省值填入            |
| **[GPIO_ReadInputDataBit](#GPIO-ReadInputDataBit)**   | 读取指定端口管脚的输入                                   |
| **[GPIO_ReadInputData](#GPIO-ReadInputData)**         | 读取指定的 GPIO 端口输入                                 |
| **[GPIO_ReadOutputDataBit](#GPIO-ReadOutputDataBit)** | 读取指定端口管脚的输出                                   |
| **[GPIO_ReadOutputData](#GPIO-ReadOutputData)**       | 读取指定的 GPIO 端口输出                                 |
| **[GPIO_SetBits](#GPIO-SetBits)**                     | 设置指定的数据端口位                                     |
| **[GPIO_ResetBits](#GPIO-ResetBits)**                 | 清除指定的数据端口位                                     |
| **[GPIO_WriteBit](#GPIO-WriteBit)**                   | 设置或者清除指定的数据端口位                             |
| **[GPIO_Write](#GPIO-Write)**                         | 向指定 GPIO 数据端口写入数据                             |
| **[GPIO_PinLockConfig](#GPIO-PinLLockConfig)**        | 锁定 GPIO 管脚设置寄存器                                 |
| **[GPIO_EventOutputConfig](#GPIO-EventOutputConfig)** | 选择 GPIO 管脚用作事件输出                               |
| **[GPIO_EventOutputCmd](#GPIO-EventOutputCmd)**       | 使能或者失能事件输出                                     |
| **[GPIO_PinRemapConfig](#GPIO-PinRemapConfig)**       | 改变指定管脚的映射                                       |
| **[GPIO_EXTILineConfig](#GPIO-EXITLineConfig)**       | 选择 GPIO 管脚用作外部中断线路                           |



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



## GPIO_DeInit

{%tabs%}

<!--tab 函数-->

| 函数原形   | void GPIO_DeInit(GPIO_TypeDef* GPIOx)               |
| ---------- | --------------------------------------------------- |
| 功能描述   | 将外设 GPIOx 寄存器重设为缺省值                     |
| 输入参数   | GPIOx：x 可以是 A，B，C，D 或者 E，来选择 GPIO 外设 |
| 输出参数   | 无                                                  |
| 返回值     | 无                                                  |
| 先决条件   | 无                                                  |
| 被调用函数 | RCC_APB2PeriphResetCmd()                            |

<!--endtab--> <!--tab 源码-->

```c
/**
 * @brief  Deinitializes the GPIOx peripheral registers to their default reset values.
 * @param  GPIOx: where x can be (A..G) to select the GPIO peripheral.
 * @retval None
 */
void GPIO_DeInit(GPIO_TypeDef *GPIOx)
{
    /* Check the parameters */
    assert_param(IS_GPIO_ALL_PERIPH(GPIOx));

    if (GPIOx == GPIOA)
    {
        RCC_APB2PeriphResetCmd(RCC_APB2Periph_GPIOA, ENABLE);
        RCC_APB2PeriphResetCmd(RCC_APB2Periph_GPIOA, DISABLE);
    }
    else if (GPIOx == GPIOB)
    {
        RCC_APB2PeriphResetCmd(RCC_APB2Periph_GPIOB, ENABLE);
        RCC_APB2PeriphResetCmd(RCC_APB2Periph_GPIOB, DISABLE);
    }
    else if (GPIOx == GPIOC)
    {
        RCC_APB2PeriphResetCmd(RCC_APB2Periph_GPIOC, ENABLE);
        RCC_APB2PeriphResetCmd(RCC_APB2Periph_GPIOC, DISABLE);
    }
    else if (GPIOx == GPIOD)
    {
        RCC_APB2PeriphResetCmd(RCC_APB2Periph_GPIOD, ENABLE);
        RCC_APB2PeriphResetCmd(RCC_APB2Periph_GPIOD, DISABLE);
    }
    else if (GPIOx == GPIOE)
    {
        RCC_APB2PeriphResetCmd(RCC_APB2Periph_GPIOE, ENABLE);
        RCC_APB2PeriphResetCmd(RCC_APB2Periph_GPIOE, DISABLE);
    }
    else if (GPIOx == GPIOF)
    {
        RCC_APB2PeriphResetCmd(RCC_APB2Periph_GPIOF, ENABLE);
        RCC_APB2PeriphResetCmd(RCC_APB2Periph_GPIOF, DISABLE);
    }
    else
    {
        if (GPIOx == GPIOG)
        {
            RCC_APB2PeriphResetCmd(RCC_APB2Periph_GPIOG, ENABLE);
            RCC_APB2PeriphResetCmd(RCC_APB2Periph_GPIOG, DISABLE);
        }
    }
}
```

<!--endtab--> <!--tab 使用-->

```c
GPIO_DeInit(GPIOA);
```

<!--endtab-->

{%endtabs%}

## GPIO_AFIODeInit

{%tabs%}

<!--tab 函数-->

| 函数原形   | void GPIO_AFIODeInit(void)                           |
| ---------- | ---------------------------------------------------- |
| 功能描述   | 将复用功能（重映射事件控制和 EXTI 设置）重设为缺省值 |
| 输入参数   | 无                                                   |
| 输出参数   | 无                                                   |
| 返回值     | 无                                                   |
| 先决条件   | 无                                                   |
| 被调用函数 | RCC_APB2PeriphResetCmd()                             |

<!--endtab--><!--tab 源码-->

```c
/**
 * @brief  Deinitializes the Alternate Functions (remap, event control
 *   and EXTI configuration) registers to their default reset values.
 * @param  None
 * @retval None
 */
void GPIO_AFIODeInit(void)
{
    RCC_APB2PeriphResetCmd(RCC_APB2Periph_AFIO, ENABLE);
    RCC_APB2PeriphResetCmd(RCC_APB2Periph_AFIO, DISABLE);
}
```

<!--endtab--><!--tab 使用-->

```c
GPIO_AFIODeInit();
```

<!--endtab-->

{%endtabs%}



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

{%note info no-icon%}

GPIO口的驱动电路响应速度，不是输出信号的速度。

输出信号的速度与程序有关，通过选择速度来选择不同的驱动电路，降低功耗控制噪声。

{%endnote%}

| GPIO_Speed       | 描述               |
| ---------------- | ------------------ |
| GPIO_Speed_10MHz | 最高输出速率 10MHz |
| GPIO_Speed_2MHz  | 最高输出速率 2MHz  |
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

{% note warning no-icon %}

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

## GPIO_StructInit

{%tabs%}

<!--tab 函数-->

| 函数原形   | void GPIO_StructInit(GPIO_InitTypeDef* GPIO_InitStruct)     |
| ---------- | ----------------------------------------------------------- |
| 功能描述   | 把 GPIO_InitStruct 中的每一个参数按缺省值填入               |
| 输入参数   | GPIO_InitStruct：指向结构 GPIO_InitTypeDef 的指针，待初始化 |
| 输出参数   | 无                                                          |
| 返回值     | 无                                                          |
| 先决条件   | 无                                                          |
| 被调用函数 | 无                                                          |

<!--endtab--><!--tab 源码-->

```c
/**
 * @brief  Fills each GPIO_InitStruct member with its default value.
 * @param  GPIO_InitStruct : pointer to a GPIO_InitTypeDef structure which will
 *         be initialized.
 * @retval None
 */
void GPIO_StructInit(GPIO_InitTypeDef *GPIO_InitStruct)
{
    /* Reset GPIO init structure parameters values */
    GPIO_InitStruct->GPIO_Pin = GPIO_Pin_All;
    GPIO_InitStruct->GPIO_Speed = GPIO_Speed_2MHz;
    GPIO_InitStruct->GPIO_Mode = GPIO_Mode_IN_FLOATING;
}
```

<!--endtab--><!--tab 使用-->

```c
GPIO_InitTypeDef GPIO_InitStructure;
GPIO_StructInit(&GPIO_InitStructure);
```

<!--endtab-->

{%endtabs%}



## GPIO_ReadInputDataBit

{%tabs%}

<!--tab 函数-->

| 函数原形   | u8 GPIO_ReadInputDataBit(GPIO_TypeDef* GPIOx, u16 GPIO_Pin) |
| ---------- | ----------------------------------------------------------- |
| 功能描述   | 读取指定端口管脚的输入                                      |
| 输入参数 1 | GPIOx：x 可以是 A，B，C，D 或者 E，来选择 GPIO 外设         |
| 输入参数 2 | GPIO_Pin：待读取的端口位                                    |
| 输出参数   | 无                                                          |
| 返回值     | 输入端口管脚值                                              |
| 先决条件   | 无                                                          |
| 被调用函数 | 无                                                          |

<!--endtab--><!--tab 源码-->

```c
/**
 * @brief  Reads the specified input port pin.
 * @param  GPIOx: where x can be (A..G) to select the GPIO peripheral.
 * @param  GPIO_Pin:  specifies the port bit to read.
 *   This parameter can be GPIO_Pin_x where x can be (0..15).
 * @retval The input port pin value.
 */
uint8_t GPIO_ReadInputDataBit(GPIO_TypeDef *GPIOx, uint16_t GPIO_Pin)
{
    uint8_t bitstatus = 0x00;

    /* Check the parameters */
    assert_param(IS_GPIO_ALL_PERIPH(GPIOx));
    assert_param(IS_GET_GPIO_PIN(GPIO_Pin));

    if ((GPIOx->IDR & GPIO_Pin) != (uint32_t)Bit_RESET)
    {
        bitstatus = (uint8_t)Bit_SET;
    }
    else
    {
        bitstatus = (uint8_t)Bit_RESET;
    }
    return bitstatus;
}
```

<!--endtab--><!--tab 使用-->

```c
u8 ReadValue;
ReadValue = GPIO_ReadInputDataBit(GPIOB, GPIO_Pin_7);
```

<!--endtab-->

{%endtabs%}



## GPIO_ReadInputData

{%tabs%}

<!--tab 函数-->

| 函数原形   | u16 GPIO_ReadInputData(GPIO_TypeDef* GPIOx)         |
| ---------- | --------------------------------------------------- |
| 功能描述   | 读取指定的 GPIO 端口输入                            |
| 输入参数   | GPIOx：x 可以是 A，B，C，D 或者 E，来选择 GPIO 外设 |
| 输出参数   | 无                                                  |
| 返回值     | GPIO 输入数据端口值                                 |
| 先决条件   | 无                                                  |
| 被调用函数 | 无                                                  |

<!--endtab--><!--tab 源码-->

```c
/**
 * @brief  Reads the specified GPIO input data port.
 * @param  GPIOx: where x can be (A..G) to select the GPIO peripheral.
 * @retval GPIO input data port value.
 */
uint16_t GPIO_ReadInputData(GPIO_TypeDef *GPIOx)
{
    /* Check the parameters */
    assert_param(IS_GPIO_ALL_PERIPH(GPIOx));

    return ((uint16_t)GPIOx->IDR);
}
```

<!--endtab--><!--tab 使用-->

```c
u16 ReadValue;
ReadValue = GPIO_ReadInputData(GPIOC);
```

<!--endtab-->

{%endtabs%}



## GPIO_ReadOutputDataBit

{%tabs%}

<!--tab 函数-->

| 函数原形   | u8 GPIO_ReadOutputDataBit(GPIO_TypeDef* GPIOx, u16 GPIO_Pin) |
| ---------- | ------------------------------------------------------------ |
| 功能描述   | 读取指定端口管脚的输出                                       |
| 输入参数1  | GPIOx：x可以是A，B，C，D或者E，来选择 GPIO 外设              |
| 输入参数2  | GPIO_Pin：待读取的端口位                                     |
| 输出参数   | 无                                                           |
| 返回值     | 输出端口管脚值                                               |
| 先决条件   | 无                                                           |
| 被调用函数 | 无                                                           |

<!--endtab--><!--tab 源码-->

```c
/**
 * @brief  Reads the specified output data port bit.
 * @param  GPIOx: where x can be (A..G) to select the GPIO peripheral.
 * @param  GPIO_Pin:  specifies the port bit to read.
 *   This parameter can be GPIO_Pin_x where x can be (0..15).
 * @retval The output port pin value.
 */
uint8_t GPIO_ReadOutputDataBit(GPIO_TypeDef *GPIOx, uint16_t GPIO_Pin)
{
    uint8_t bitstatus = 0x00;
    /* Check the parameters */
    assert_param(IS_GPIO_ALL_PERIPH(GPIOx));
    assert_param(IS_GET_GPIO_PIN(GPIO_Pin));

    if ((GPIOx->ODR & GPIO_Pin) != (uint32_t)Bit_RESET)
    {
        bitstatus = (uint8_t)Bit_SET;
    }
    else
    {
        bitstatus = (uint8_t)Bit_RESET;
    }
    return bitstatus;
}
```

<!--endtab--><!--tab 使用-->

```c
u8 ReadValue;
ReadValue = GPIO_ReadOutputDataBit(GPIOB, GPIO_Pin_7);
```

<!--endtab-->

{%endtabs%}



## GPIO_ReadOutputData

{%tabs%}

<!--tab 函数-->

| 函数原形   | u16 GPIO_ReadOutputData(GPIO_TypeDef* GPIOx)   |
| ---------- | ---------------------------------------------- |
| 功能描述   | 读取指定的 GPIO 端口输出                       |
| 输入参数   | GPIOx：x可以是A，B，C，D或者E，来选择GPIO 外设 |
| 输出参数   | 无                                             |
| 返回值     | GPIO 输出数据端口值                            |
| 先决条件   | 无                                             |
| 被调用函数 | 无                                             |

<!--endtab--><!--tab 源码-->

```c
/**
 * @brief  Reads the specified GPIO output data port.
 * @param  GPIOx: where x can be (A..G) to select the GPIO peripheral.
 * @retval GPIO output data port value.
 */
uint16_t GPIO_ReadOutputData(GPIO_TypeDef *GPIOx)
{
    /* Check the parameters */
    assert_param(IS_GPIO_ALL_PERIPH(GPIOx));

    return ((uint16_t)GPIOx->ODR);
}
```

<!--endtab--><!--tab 使用-->

```c
u16 ReadValue;
ReadValue = GPIO_ReadOutputData(GPIOC);
```

<!--endtab-->

{%endtabs%}



## GPIO_SetBits

{%tabs GPIO_SetBits%}

<!--tab 函数-->

| 函数原形   | void GPIO_SetBits(GPIO_TypeDef* GPIOx, u16 GPIO_Pin)         |
| ---------- | ------------------------------------------------------------ |
| 功能描述   | 设置指定的数据端口位                                         |
| 输入参数 1 | GPIOx：x 可以是 A，B，C，D 或者 E，来选择 GPIO 外设          |
| 输入参数 2 | GPIO_Pin：待设置的端口位<br/>该参数可以取 GPIO_Pin_x(x 可以是 0-15)的任意组合 |
| 输出参数   | 无                                                           |
| 返回值     | 无                                                           |
| 先决条件   | 无                                                           |
| 被调用函数 | 无                                                           |

 <!--endtab--><!--tab 源码-->

```c
/**
  * @brief  Sets the selected data port bits.
  * @param  GPIOx: where x can be (A..G) to select the GPIO peripheral.
  * @param  GPIO_Pin: specifies the port bits to be written.
  *   This parameter can be any combination of GPIO_Pin_x where x can be (0..15).
  * @retval None
  */
void GPIO_SetBits(GPIO_TypeDef* GPIOx, uint16_t GPIO_Pin)
{
  /* Check the parameters */
  assert_param(IS_GPIO_ALL_PERIPH(GPIOx));
  assert_param(IS_GPIO_PIN(GPIO_Pin));
  
  GPIOx->BSRR = GPIO_Pin;
}
```

<!--endtab--><!--tab 使用-->

```c
GPIO_SetBits(GPIOA, GPIO_Pin_10 | GPIO_Pin_15);
```

<!--endtab-->

{%endtabs%}

## GPIO_ResetBits

{%tabs GPIO_SetBits%}

<!--tab 函数-->

| 函数原形   | void GPIO_ResetBits(GPIO_TypeDef* GPIOx, u16 GPIO_Pin)       |
| ---------- | ------------------------------------------------------------ |
| 功能描述   | 清除指定的数据端口位                                         |
| 输入参数 1 | GPIOx：x 可以是 A，B，C，D 或者 E，来选择 GPIO 外设          |
| 输入参数 2 | GPIO_Pin：待清除的端口位<br/>该参数可以取 GPIO_Pin_x(x 可以是 0-15)的任意组合 |
| 输出参数   | 无                                                           |
| 返回值     | 无                                                           |
| 先决条件   | 无                                                           |
| 被调用函数 | 无                                                           |

<!--endtab--><!--tab 源码-->

```c
/**
  * @brief  Clears the selected data port bits.
  * @param  GPIOx: where x can be (A..G) to select the GPIO peripheral.
  * @param  GPIO_Pin: specifies the port bits to be written.
  *   This parameter can be any combination of GPIO_Pin_x where x can be (0..15).
  * @retval None
  */
void GPIO_ResetBits(GPIO_TypeDef* GPIOx, uint16_t GPIO_Pin)
{
  /* Check the parameters */
  assert_param(IS_GPIO_ALL_PERIPH(GPIOx));
  assert_param(IS_GPIO_PIN(GPIO_Pin));
  
  GPIOx->BRR = GPIO_Pin;
}
```

<!--endtab--><!--tab 使用-->

```c
GPIO_ResetBits(GPIOA, GPIO_Pin_10 | GPIO_Pin_15);
```

<!--endtab-->

{%endtabs%}



## GPIO_WriteBit

{%tabs%}

<!--tab 函数-->

| 函数原形   | void GPIO_WriteBit(GPIO_TypeDef* GPIOx, u16 GPIO_Pin, BitAction BitVal) |
| ---------- | ------------------------------------------------------------ |
| 功能描述   | 设置或者清除指定的数据端口位                                 |
| 输入参数1  | GPIOx：x可以是A，B，C，D或者E，来选择 GPIO 外设              |
| 输入参数2  | GPIO_Pin：待设置或者清除指的端口位<br/>该参数可以取 GPIO_Pin_x(x 可以是 0-15)的任意组合 |
| 输入参数3  | BitVal: 该参数指定了待写入的值（该参数必须取枚举 BitAction 的其中一个值）<br/>Bit_RESET: 清除数据端口位<br/>Bit_SET: 设置数据端口位 |
| 输出参数   | 无                                                           |
| 返回值     | 无                                                           |
| 先决条件   | 无                                                           |
| 被调用函数 | 无                                                           |

<!--endtab--><!--tab 源码-->

```c
/**
 * @brief  Sets or clears the selected data port bit.
 * @param  GPIOx: where x can be (A..G) to select the GPIO peripheral.
 * @param  GPIO_Pin: specifies the port bit to be written.
 *   This parameter can be one of GPIO_Pin_x where x can be (0..15).
 * @param  BitVal: specifies the value to be written to the selected bit.
 *   This parameter can be one of the BitAction enum values:
 *     @arg Bit_RESET: to clear the port pin
 *     @arg Bit_SET: to set the port pin
 * @retval None
 */
void GPIO_WriteBit(GPIO_TypeDef *GPIOx, uint16_t GPIO_Pin, BitAction BitVal)
{
    /* Check the parameters */
    assert_param(IS_GPIO_ALL_PERIPH(GPIOx));
    assert_param(IS_GET_GPIO_PIN(GPIO_Pin));
    assert_param(IS_GPIO_BIT_ACTION(BitVal));

    if (BitVal != Bit_RESET)
    {
        GPIOx->BSRR = GPIO_Pin;
    }
    else
    {
        GPIOx->BRR = GPIO_Pin;
    }
}
```

<!--endtab--><!--tab 使用-->

```c
GPIO_WriteBit(GPIOA, GPIO_Pin_15, Bit_SET);
```

<!--endtab-->

{%endtabs%}



## GPIO_Write

{%tabs%}

<!--tab 函数-->

| 函数原形   | void GPIO_Write(GPIO_TypeDef* GPIOx, u16 PortVal) |
| ---------- | ------------------------------------------------- |
| 功能描述   | 向指定GPIO数据端口写入数据                        |
| 输入参数1  | GPIOx：x可以是A，B，C，D或者E，来选择GPIO 外设    |
| 输入参数2  | PortVal:待写入端口数据寄存器的值                  |
| 输出参数   | 无                                                |
| 返回值     | 无                                                |
| 先决条件   | 无                                                |
| 被调用函数 | 无                                                |

<!--endtab--><!--tab 源码-->

```c
/**
 * @brief  Writes data to the specified GPIO data port.
 * @param  GPIOx: where x can be (A..G) to select the GPIO peripheral.
 * @param  PortVal: specifies the value to be written to the port output data register.
 * @retval None
 */
void GPIO_Write(GPIO_TypeDef *GPIOx, uint16_t PortVal)
{
    /* Check the parameters */
    assert_param(IS_GPIO_ALL_PERIPH(GPIOx));

    GPIOx->ODR = PortVal;
}
```

<!--endtab--><!--tab 使用-->

```c
GPIO_Write(GPIOA, 0x1101);
```

<!--endtab-->

{%endtabs%}



## GPIO_PinLockConfig

{%tabs%}

<!--tab 函数-->

| 函数原形   | void GPIO_PinLockConfig(GPIO_TypeDef* GPIOx, u16 GPIO_Pin)   |
| ---------- | ------------------------------------------------------------ |
| 功能描述   | 锁定GPIO管脚设置寄存器                                       |
| 输入参数1  | GPIOx：x可以是A，B，C，D或者E，来选择 GPIO 外设              |
| 输入参数2  | GPIO_Pin：待锁定的端口位<br/>该参数可以取 GPIO_Pin_x(x可以是 0-15)的任意组合 |
| 输出参数   | 无                                                           |
| 返回值     | 无                                                           |
| 先决条件   | 无                                                           |
| 被调用函数 | 无                                                           |

<!--endtab--><!--tab 源码-->

```c
/**
 * @brief  Locks GPIO Pins configuration registers.
 * @param  GPIOx: where x can be (A..G) to select the GPIO peripheral.
 * @param  GPIO_Pin: specifies the port bit to be written.
 *   This parameter can be any combination of GPIO_Pin_x where x can be (0..15).
 * @retval None
 */
void GPIO_PinLockConfig(GPIO_TypeDef *GPIOx, uint16_t GPIO_Pin)
{
    uint32_t tmp = 0x00010000;

    /* Check the parameters */
    assert_param(IS_GPIO_ALL_PERIPH(GPIOx));
    assert_param(IS_GPIO_PIN(GPIO_Pin));

    tmp |= GPIO_Pin;
    /* Set LCKK bit */
    GPIOx->LCKR = tmp;
    /* Reset LCKK bit */
    GPIOx->LCKR = GPIO_Pin;
    /* Set LCKK bit */
    GPIOx->LCKR = tmp;
    /* Read LCKK bit*/
    tmp = GPIOx->LCKR;
    /* Read LCKK bit*/
    tmp = GPIOx->LCKR;
}
```

<!--endtab--><!--tab 使用-->

```c
GPIO_PinLockConfig(GPIOA, GPIO_Pin_0 | GPIO_Pin_1);
```

<!--endtab-->

{%endtabs%}



## GPIO_EventOutputConfig

{%tabs%}

<!--tab 函数-->

| 函数原形   | void GPIO_EventOutputConfig(u8 GPIO_PortSource, u8 GPIO_PinSource) |
| ---------- | ------------------------------------------------------------ |
| 功能描述   | 选择GPIO管脚用作事件输出                                     |
| 输入参数1  | GPIO_PortSource:选择用作事件输出的 GPIO 端口                 |
| 输入参数2  | GPIO_PinSource：事件输出的管脚<br/>该参数可以取GPIO_PinSourcex(x可以是0-15) |
| 输出参数   | 无                                                           |
| 返回值     | 无                                                           |
| 先决条件   | 无                                                           |
| 被调用函数 | 无                                                           |



### GPIO_PortSource

GPIO_PortSource 用以选择用作事件输出的 GPIO 端口。Table 199. 给出了该参数可取的值

| GPI0 PortSource      | 描述       |
| -------------------- | ---------- |
| GPIO PortSourceGPIOA | 选择 GPIOA |
| GPIO PortSourceGPIOB | 选择 GPIOB |
| GPIO PortSourceGPIOC | 选择 GPIOC |
| GPIO PortSourceGPIOD | 选择 GPIOD |
| GPIO PortSourceGPIOE | 选择 GPIOE |

<!--endtab--><!--tab 源码-->

```c
/**
 * @brief  Selects the GPIO pin used as Event output.
 * @param  GPIO_PortSource: selects the GPIO port to be used as source
 *   for Event output.
 *   This parameter can be GPIO_PortSourceGPIOx where x can be (A..E).
 * @param  GPIO_PinSource: specifies the pin for the Event output.
 *   This parameter can be GPIO_PinSourcex where x can be (0..15).
 * @retval None
 */
void GPIO_EventOutputConfig(uint8_t GPIO_PortSource, uint8_t GPIO_PinSource)
{
    uint32_t tmpreg = 0x00;
    /* Check the parameters */
    assert_param(IS_GPIO_EVENTOUT_PORT_SOURCE(GPIO_PortSource));
    assert_param(IS_GPIO_PIN_SOURCE(GPIO_PinSource));

    tmpreg = AFIO->EVCR;
    /* Clear the PORT[6:4] and PIN[3:0] bits */
    tmpreg &= EVCR_PORTPINCONFIG_MASK;
    tmpreg |= (uint32_t)GPIO_PortSource << 0x04;
    tmpreg |= GPIO_PinSource;
    AFIO->EVCR = tmpreg;
}
```

<!--endtab--><!--tab 使用-->

```c
GPIO_EventOutputConfig(GPIO_PortSourceGPIOE, GPIO_PinSource5);
```

<!--endtab-->

{%endtabs%}



## GPIO_EventOutputCmd

{%tabs%}

<!--tab 函数-->

| 函数原形   | void GPIO_EventOutputCmd(FunctionalState NewState)           |
| ---------- | ------------------------------------------------------------ |
| 功能描述   | 使能或者失能事件输出                                         |
| 输入参数1  | NewState：事件输出的新状态<br/>这个参数可以取：ENABLE或者DISABLE |
| 输出参数   | 无                                                           |
| 返回值     | 无                                                           |
| 先决条件   | 无                                                           |
| 被调用函数 | 无                                                           |

<!--endtab--><!--tab 源码-->

```c
/**
 * @brief  Enables or disables the Event Output.
 * @param  NewState: new state of the Event output.
 *   This parameter can be: ENABLE or DISABLE.
 * @retval None
 */
void GPIO_EventOutputCmd(FunctionalState NewState)
{
    /* Check the parameters */
    assert_param(IS_FUNCTIONAL_STATE(NewState));

    *(__IO uint32_t *)EVCR_EVOE_BB = (uint32_t)NewState;
}
```

<!--endtab--><!--tab 使用-->

```c
GPIO_EventOutputConfig(GPIO_PortSourceGPIOC, GPIO_PinSource6);
GPIO_EventOutputCmd(ENABLE);
```

<!--endtab-->

{%endtabs%}



## GPIO_PinRemapConfig

{%tabs%}

<!--tab 函数-->

| 函数原形   | void GPIO_PinRemapConfig(u32 GPIO_Remap, FunctionalState NewState) |
| ---------- | ------------------------------------------------------------ |
| 功能描述   | 改变指定管脚的映射                                           |
| 输入参数1  | GPIO_Remap:选择重映射的管脚                                  |
| 输入参数2  | NewState:管脚重映射的新状态<br/>这个参数可以取：ENABLE或者DISABLE |
| 输出参数   | 无                                                           |
| 返回值     | 无                                                           |
| 先决条件   | 无                                                           |
| 被调用函数 | 无                                                           |

### GPIO_Remap

| GPI0_Remap                 | 描述                               |
| -------------------------- | ---------------------------------- |
| GPIO_Remap_SPI1            | SPI1 复用功能映射                  |
| GPIO_Remap_I2C1            | I2C1复用功能映射                   |
| GPIO_Remap_USART1          | USART1 复用功能映射                |
| GPIO_PartialRemap_USART3   | USART2 复用功能映射                |
| GPIO_FullRemap_USART3      | USART3 复用功能完全映射            |
| GPIO_PartialRemap_TIM1     | USART3 复用功能部分映射            |
| GPIO FullRemap_TIM1        | TIM1 复用功能完全映射              |
| GPIO_PartialRemap1_TIM2    | TIM2 复用功能部分映射1             |
| GPIO_PartialRemap2_TIM2    | TIM2复用功能部分映射2              |
| GPIO_FullRemap_TIM2        | TIM2 复用功能完全映射              |
| GPIO_PartialRemap_TIM3     | TIM3复用功能部分映射               |
| GPIO_FullRemap_TIM3        | TIM3 复用功能完全映射              |
| GPIO_Remap_TIM4            | TIM4 复用功能映射                  |
| GPI0_Remap1_CAN            | CAN 复用功能映射1                  |
| GPIO_Remap2_CAN            | CAN复用功能映射2                   |
| GPIO_Remap_PD01            | PD01 复用功能映射                  |
| GPIO_Remap_SWJ_NoJTRST     | 除JTRST外 SWJ完全使能（JTAG+SW-DP) |
| GPIO_Remap_SWJ_JTAGDisable | JTAG-DP 失能+ SW-DP 使能           |
| GPIO_Remap_SWJ_Disable     | SWJ完全失能（JTAG+SW-DP)           |

<!--endtab--><!--tab 源码-->

```c
/**
 * @brief  Changes the mapping of the specified pin.
 * @param  GPIO_Remap: selects the pin to remap.
 *   This parameter can be one of the following values:
 *     @arg GPIO_Remap_SPI1             : SPI1 Alternate Function mapping
 *     @arg GPIO_Remap_I2C1             : I2C1 Alternate Function mapping
 *     @arg GPIO_Remap_USART1           : USART1 Alternate Function mapping
 *     @arg GPIO_Remap_USART2           : USART2 Alternate Function mapping
 *     @arg GPIO_PartialRemap_USART3    : USART3 Partial Alternate Function mapping
 *     @arg GPIO_FullRemap_USART3       : USART3 Full Alternate Function mapping
 *     @arg GPIO_PartialRemap_TIM1      : TIM1 Partial Alternate Function mapping
 *     @arg GPIO_FullRemap_TIM1         : TIM1 Full Alternate Function mapping
 *     @arg GPIO_PartialRemap1_TIM2     : TIM2 Partial1 Alternate Function mapping
 *     @arg GPIO_PartialRemap2_TIM2     : TIM2 Partial2 Alternate Function mapping
 *     @arg GPIO_FullRemap_TIM2         : TIM2 Full Alternate Function mapping
 *     @arg GPIO_PartialRemap_TIM3      : TIM3 Partial Alternate Function mapping
 *     @arg GPIO_FullRemap_TIM3         : TIM3 Full Alternate Function mapping
 *     @arg GPIO_Remap_TIM4             : TIM4 Alternate Function mapping
 *     @arg GPIO_Remap1_CAN1            : CAN1 Alternate Function mapping
 *     @arg GPIO_Remap2_CAN1            : CAN1 Alternate Function mapping
 *     @arg GPIO_Remap_PD01             : PD01 Alternate Function mapping
 *     @arg GPIO_Remap_TIM5CH4_LSI      : LSI connected to TIM5 Channel4 input capture for calibration
 *     @arg GPIO_Remap_ADC1_ETRGINJ     : ADC1 External Trigger Injected Conversion remapping
 *     @arg GPIO_Remap_ADC1_ETRGREG     : ADC1 External Trigger Regular Conversion remapping
 *     @arg GPIO_Remap_ADC2_ETRGINJ     : ADC2 External Trigger Injected Conversion remapping
 *     @arg GPIO_Remap_ADC2_ETRGREG     : ADC2 External Trigger Regular Conversion remapping
 *     @arg GPIO_Remap_ETH              : Ethernet remapping (only for Connectivity line devices)
 *     @arg GPIO_Remap_CAN2             : CAN2 remapping (only for Connectivity line devices)
 *     @arg GPIO_Remap_SWJ_NoJTRST      : Full SWJ Enabled (JTAG-DP + SW-DP) but without JTRST
 *     @arg GPIO_Remap_SWJ_JTAGDisable  : JTAG-DP Disabled and SW-DP Enabled
 *     @arg GPIO_Remap_SWJ_Disable      : Full SWJ Disabled (JTAG-DP + SW-DP)
 *     @arg GPIO_Remap_SPI3             : SPI3/I2S3 Alternate Function mapping (only for Connectivity line devices)
 *                                        When the SPI3/I2S3 is remapped using this function, the SWJ is configured
 *                                        to Full SWJ Enabled (JTAG-DP + SW-DP) but without JTRST.
 *     @arg GPIO_Remap_TIM2ITR1_PTP_SOF : Ethernet PTP output or USB OTG SOF (Start of Frame) connected
 *                                        to TIM2 Internal Trigger 1 for calibration (only for Connectivity line devices)
 *                                        If the GPIO_Remap_TIM2ITR1_PTP_SOF is enabled the TIM2 ITR1 is connected to
 *                                        Ethernet PTP output. When Reset TIM2 ITR1 is connected to USB OTG SOF output.
 *     @arg GPIO_Remap_PTP_PPS          : Ethernet MAC PPS_PTS output on PB05 (only for Connectivity line devices)
 *     @arg GPIO_Remap_TIM15            : TIM15 Alternate Function mapping (only for Value line devices)
 *     @arg GPIO_Remap_TIM16            : TIM16 Alternate Function mapping (only for Value line devices)
 *     @arg GPIO_Remap_TIM17            : TIM17 Alternate Function mapping (only for Value line devices)
 *     @arg GPIO_Remap_CEC              : CEC Alternate Function mapping (only for Value line devices)
 *     @arg GPIO_Remap_TIM1_DMA         : TIM1 DMA requests mapping (only for Value line devices)
 *     @arg GPIO_Remap_TIM9             : TIM9 Alternate Function mapping (only for XL-density devices)
 *     @arg GPIO_Remap_TIM10            : TIM10 Alternate Function mapping (only for XL-density devices)
 *     @arg GPIO_Remap_TIM11            : TIM11 Alternate Function mapping (only for XL-density devices)
 *     @arg GPIO_Remap_TIM13            : TIM13 Alternate Function mapping (only for High density Value line and XL-density devices)
 *     @arg GPIO_Remap_TIM14            : TIM14 Alternate Function mapping (only for High density Value line and XL-density devices)
 *     @arg GPIO_Remap_FSMC_NADV        : FSMC_NADV Alternate Function mapping (only for High density Value line and XL-density devices)
 *     @arg GPIO_Remap_TIM67_DAC_DMA    : TIM6/TIM7 and DAC DMA requests remapping (only for High density Value line devices)
 *     @arg GPIO_Remap_TIM12            : TIM12 Alternate Function mapping (only for High density Value line devices)
 *     @arg GPIO_Remap_MISC             : Miscellaneous Remap (DMA2 Channel5 Position and DAC Trigger remapping,
 *                                        only for High density Value line devices)
 * @param  NewState: new state of the port pin remapping.
 *   This parameter can be: ENABLE or DISABLE.
 * @retval None
 */
void GPIO_PinRemapConfig(uint32_t GPIO_Remap, FunctionalState NewState)
{
    uint32_t tmp = 0x00, tmp1 = 0x00, tmpreg = 0x00, tmpmask = 0x00;

    /* Check the parameters */
    assert_param(IS_GPIO_REMAP(GPIO_Remap));
    assert_param(IS_FUNCTIONAL_STATE(NewState));

    if ((GPIO_Remap & 0x80000000) == 0x80000000)
    {
        tmpreg = AFIO->MAPR2;
    }
    else
    {
        tmpreg = AFIO->MAPR;
    }

    tmpmask = (GPIO_Remap & DBGAFR_POSITION_MASK) >> 0x10;
    tmp = GPIO_Remap & LSB_MASK;

    if ((GPIO_Remap & (DBGAFR_LOCATION_MASK | DBGAFR_NUMBITS_MASK)) == (DBGAFR_LOCATION_MASK | DBGAFR_NUMBITS_MASK))
    {
        tmpreg &= DBGAFR_SWJCFG_MASK;
        AFIO->MAPR &= DBGAFR_SWJCFG_MASK;
    }
    else if ((GPIO_Remap & DBGAFR_NUMBITS_MASK) == DBGAFR_NUMBITS_MASK)
    {
        tmp1 = ((uint32_t)0x03) << tmpmask;
        tmpreg &= ~tmp1;
        tmpreg |= ~DBGAFR_SWJCFG_MASK;
    }
    else
    {
        tmpreg &= ~(tmp << ((GPIO_Remap >> 0x15) * 0x10));
        tmpreg |= ~DBGAFR_SWJCFG_MASK;
    }

    if (NewState != DISABLE)
    {
        tmpreg |= (tmp << ((GPIO_Remap >> 0x15) * 0x10));
    }

    if ((GPIO_Remap & 0x80000000) == 0x80000000)
    {
        AFIO->MAPR2 = tmpreg;
    }
    else
    {
        AFIO->MAPR = tmpreg;
    }
}
```

<!--endtab--><!--tab 使用-->

```c
GPIO_PinRemapConfig(GPIO_Remap_I2C1, ENABLE);
```

<!--endtab-->

{%endtabs%}



## GPIO_EXITLineConfig

{%tabs%}

<!--tab 函数-->

| 函数原形   | void GPIO_EXTILineConfig(u8 GPIO_PortSource, u8 GPIO_PinSource) |
| ---------- | ------------------------------------------------------------ |
| 功能描述   | 选择GPIO管脚用作外部中断线路                                 |
| 输入参数1  | GPIO_PortSource:选择用作外部中断线源的GPIO端口               |
| 输入参数2  | GPIO_PinSource：待设置的外部中断线路<br/>该参数可以取GPIO_PinSourcex(x可以是0-15) |
| 输出参数   | 无                                                           |
| 返回值     | 无                                                           |
| 先决条件   | 无                                                           |
| 被调用函数 | 无                                                           |

<!--endtab--><!--tab 源码-->

```c
/**
 * @brief  Selects the GPIO pin used as EXTI Line.
 * @param  GPIO_PortSource: selects the GPIO port to be used as source for EXTI lines.
 *   This parameter can be GPIO_PortSourceGPIOx where x can be (A..G).
 * @param  GPIO_PinSource: specifies the EXTI line to be configured.
 *   This parameter can be GPIO_PinSourcex where x can be (0..15).
 * @retval None
 */
void GPIO_EXTILineConfig(uint8_t GPIO_PortSource, uint8_t GPIO_PinSource)
{
    uint32_t tmp = 0x00;
    /* Check the parameters */
    assert_param(IS_GPIO_EXTI_PORT_SOURCE(GPIO_PortSource));
    assert_param(IS_GPIO_PIN_SOURCE(GPIO_PinSource));

    tmp = ((uint32_t)0x0F) << (0x04 * (GPIO_PinSource & (uint8_t)0x03));
    AFIO->EXTICR[GPIO_PinSource >> 0x02] &= ~tmp;
    AFIO->EXTICR[GPIO_PinSource >> 0x02] |= (((uint32_t)GPIO_PortSource) << (0x04 * (GPIO_PinSource & (uint8_t)0x03)));
}
```

```c
/**
 * @brief  Selects the Ethernet media interface.
 * @note   This function applies only to STM32 Connectivity line devices.
 * @param  GPIO_ETH_MediaInterface: specifies the Media Interface mode.
 *   This parameter can be one of the following values:
 *     @arg GPIO_ETH_MediaInterface_MII: MII mode
 *     @arg GPIO_ETH_MediaInterface_RMII: RMII mode
 * @retval None
 */
void GPIO_ETH_MediaInterfaceConfig(uint32_t GPIO_ETH_MediaInterface)
{
    assert_param(IS_GPIO_ETH_MEDIA_INTERFACE(GPIO_ETH_MediaInterface));

    /* Configure MII_RMII selection bit */
    *(__IO uint32_t *)MAPR_MII_RMII_SEL_BB = GPIO_ETH_MediaInterface;
}
```



<!--endtab--><!--tab 使用-->

```c
GPIO_EXTILineConfig(GPIO_PortSource_GPIOB, GPIO_PinSource8);
```

<!--endtab-->

{%endtabs%}

