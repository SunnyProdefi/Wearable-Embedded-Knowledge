# 硬件接口与总线协议

## 本模块目标

将电气特性、协议事务、控制器执行和驱动 API 分层，解释请求如何变成信号及错误如何上报。

- 深度：I2C/I3C 与 Camera 接口深入；其他接口按工程需求扩展。
- 前置：S1-04～S1-06；电平、时钟与复位条件。
- 课程位置：关联基础课 S1-05；S2-05～S2-08；S3-03、S3-06。
- 状态：S2-05～S2-08 正文已建立，列入 [本轮连贯阅读](../Study_Pack_S1-08_S2.md)；其他子系统接口仍按阶段深化。
- 学习掌握情况以 [Progress.md](../Progress.md) 为准。

## 主题与拟建文档

| 拟建文件 | 内容范围 | 建设状态 |
|---|---|---|
| [GPIO_PWM_ADC_DAC.md](GPIO_PWM_ADC_DAC.md) | S2-05：方向/复用/上下拉、电平、PWM 和模拟数字转换 | 正文已建立 |
| [I2C.md](I2C.md) | S2-06：Controller/Target、ACK/NACK、事务与错误分层 | 正文已建立 |
| [I3C.md](I3C.md) | S2-07：DAA、ENTDAA/SETDASA、CCC、IBI、Bus Busy 与版本边界 | 正文已建立 |
| [SPI_UART.md](SPI_UART.md) | S2-08：SPI/UART 机制及 CSI-2/DSI、USB/SDIO/PCIe 位置 | 正文已建立 |
| `MIPI_CSI2_DSI.md` | 协议与物理层深入；接口位置已在 S2-08 概览 | 深入正文待创建 |
| `I2S_PCM_PDM_TDM.md` | 音频数据、时钟、通道与帧结构 | 待创建 |
| `USB_SDIO_PCIe.md` | Host 接口深入；位置已在 S2-08 概览 | 深入正文待创建 |

文件名是规划，不是不存在正文的链接。正式编写后更新本导航。

## 软硬件关联重点

应用/服务 → 驱动 → 控制器 → 引脚/总线 → 外设 → 状态/IRQ/数据返回；DMA 按控制器能力选择，不作统一假设。

## 工程问题入口

C02 I3C Bus Busy、C03 Chip ID 失败；区分地址、总线状态、器件可用性与事务错误。

案例定义和建设状态见 [工程案例导航](../10_Engineering_Cases/README.md)。

## 理解检查方向

能解释 CPU 与控制器的分工，并区分总线 ACK、IBI 与厂商命令完成通知。

## 关联知识与资料

- [电源与时钟](../03_Power_Clock/README.md)
- [Camera](../05_Camera/README.md)
- [音频](../06_Audio/README.md)
- [课程路线](../Roadmap.md)
- [术语速查](../Glossary.md)
- [公开资料索引](../Sources.md)
- 已核对的相关公开资料：[S03 I3C 概览](../Sources.md#s03-linux-i3c-协议概览)、[S04 CSI-2 介绍](../Sources.md#s04-mipi-csi-2-官方介绍)。详细实现仍按资料版本和平台核对。
