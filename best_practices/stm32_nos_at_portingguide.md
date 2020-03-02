# 基于STM32+Nos+EC20的SDK移植

## STM32F103

* Arm M3核 72 Mhz

* 128 Kbytes Falsh

* 20 Kbytes SRAM

* 支持ST-LINK调试

我们将在STM32F103上移植C-SDK，使用AT指令控制移远EC20模组收发MQTT消息，本次仅演示移植MQTT收发消息部分。

## 使用STM32CubeMX工具生成新工程

新建工程

![](/images/stm32f1新建工程.png)

设置新增一个用于输出的打印串口，USART1用于打印输出，USART2用于ST-Link调试，USART3用于控制EC20

![](/images/stm32f1新增打印串口.png)

设置新增一个用于与AT模组通信的控制串口

![](/images/stm32f1新增模组控制串口.png)

增加堆栈，填写项目名称等信息，点击生成代码

![](/images/stm32f1增大堆栈.png)

抽取C-SDK中的代码。

![](/images/stm32f1抽取代码.png)

其中at文件夹下可以根据实际使用的模组选择文件夹，不用的模组可以删除，本次使用EC20

![](/images/stm32f1根据使用模组选择文件夹.png)

抽取需要的文件夹

![](/images/stm32f1抽取代码2.png)

本案例中使用AT模组连接tcp，不需要HAL_TCP_nos.c文件

![](/images/stm32f1抽取代码3.png)

将抽取的文件夹加入STM32CubeMX生成的工程

![](/images/stm32f1将代码加入工程.png)

配置编译宏和添加头文件

![](/images/stm32f1增加编译宏和头文件.png)

部分代码依赖STM32平台，使用不同型号开发板时需要修改

![](/images/stm32f1修改代码.png)

修改stm32f1中的串口中断处理接口，让EC20传给mcu的数据直接存在ringbuff中

```
#include "stm32f1xx_hal.h"
#include "at_ringbuff.h"

.........

extern sRingbuff g_ring_buff;    
/**
  * @brief  Receives an amount of data in non blocking mode
  * @param  huart  Pointer to a UART_HandleTypeDef structure that contains
  *                the configuration information for the specified UART module.
  * @retval HAL status
  */
static HAL_StatusTypeDef UART_Receive_IT(UART_HandleTypeDef *huart)
{
  uint16_t *tmp;
  uint8_t ch;

  /* Check that a Rx process is ongoing */
  if (huart->RxState == HAL_UART_STATE_BUSY_RX)
  {
    if (huart->Init.WordLength == UART_WORDLENGTH_9B)
    {
      tmp = (uint16_t *) huart->pRxBuffPtr;
      if (huart->Init.Parity == UART_PARITY_NONE)
      {
        *tmp = (uint16_t)(huart->Instance->DR & (uint16_t)0x01FF);
        huart->pRxBuffPtr += 2U;
      }
      else
      {
        *tmp = (uint16_t)(huart->Instance->DR & (uint16_t)0x00FF);
        huart->pRxBuffPtr += 1U;
      }
    }
    else
    {
      if (huart->Init.Parity == UART_PARITY_NONE)
      {
		ch = (uint8_t) READ_REG(huart->Instance->DR)&0xFF;
        ring_buff_push_data(&g_ring_buff, &ch, 1);
      }
      else
      {
        *huart->pRxBuffPtr++ = (uint8_t)(huart->Instance->DR & (uint8_t)0x007F);
      }
    }
#if 0
    if (--huart->RxXferCount == 0U)
    {
      /* Disable the UART Data Register not empty Interrupt */
      __HAL_UART_DISABLE_IT(huart, UART_IT_RXNE);

      /* Disable the UART Parity Error Interrupt */
      __HAL_UART_DISABLE_IT(huart, UART_IT_PE);

      /* Disable the UART Error Interrupt: (Frame error, noise error, overrun error) */
      __HAL_UART_DISABLE_IT(huart, UART_IT_ERR);

      /* Rx process is completed, restore huart->RxState to Ready */
      huart->RxState = HAL_UART_STATE_READY;

#if (USE_HAL_UART_REGISTER_CALLBACKS == 1)
      /*Call registered Rx complete callback*/
      huart->RxCpltCallback(huart);
#else
      /*Call legacy weak Rx complete callback*/
      HAL_UART_RxCpltCallback(huart);
#endif /* USE_HAL_UART_REGISTER_CALLBACKS */

      return HAL_OK;
    }
#endif    
    return HAL_OK;
  }
  else
  {
    return HAL_BUSY;
  }
}
```

修改在hal_at.c文件下的AT读写接口适配stm32f1

![](/images/stm32f1根据平台修改底层读写代码.png)

```
#include <stdio.h>
#include <string.h>
#include "stm32f1xx_hal.h"
#include "utils_net.h"
#include "at_ringbuff.h"
#include "at_client.h"
#include "uiot_import.h"

extern UART_HandleTypeDef huart3;
static UART_HandleTypeDef *pAtUart = &huart3;
extern sRingbuff g_ring_tcp_buff[];    

void HAL_AT_Init()
{
    /* 配置串口接收buf的存储位置 */    
    HAL_UART_Receive_IT(pAtUart, g_ring_buff.buffer, 1);
    return;
}


int HAL_AT_Read(_IN_ utils_network_pt pNetwork, _OU_ unsigned char *buffer, _IN_ size_t len)
{
    return ring_buff_pop_data(&(g_ring_tcp_buff[pNetwork->handle-1]), buffer, len);
    return 0;
}

int HAL_AT_Write(_IN_ unsigned char *buffer, _IN_ size_t len)
{   
    return HAL_UART_Transmit_IT(pAtUart, buffer, len);
    return 0;
}

```

根据C-SDK中的ucloud-iot-device-sdk-c\samples\mqtt\mqtt_sample.c修改main.c函数，编译运行。

![](/images/stm32f1编译运行.png)
