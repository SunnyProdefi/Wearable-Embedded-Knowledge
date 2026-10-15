# Camera 系统

## 本模块目标

贯通 Sensor 控制、图像接收、ISP、DMA/Buffer 与 HAL/Framework，按分层证据定位异常。

- 深度：专业主线，深入源码、状态机、寄存器和系统设计。
- 前置：寄存器、电源/时钟/复位、I2C/I3C、DMA 与地址空间；按具体章节补齐。
- 课程位置：S3-01～S3-05；S4-07；S5-05。
- 状态：仅导航与主题规划；下列详细文档尚未创建。
- 学习掌握情况以 [Progress.md](../Progress.md) 为准。

## 主题与拟建文档

| 拟建文件 | 内容范围 | 建设状态 |
|---|---|---|
| `Sensor_Basics_and_Timing.md` | CMOS、RAW/Bayer、曝光/增益、帧率与时序 | 待创建 |
| `Sensor_Power_and_Register_Control.md` | 电源、复位、MCLK、Chip ID、寄存器与模式设置 | 待创建 |
| `CSI_Receiver_and_ISP.md` | CSI-2、物理层、接收配置、ISP Pipeline 与格式 | 待创建 |
| `Capture_Buffers_and_Bandwidth.md` | DMA、内存、Buffer 生命周期、带宽与丢帧 | 待创建 |
| `Driver_HAL_Framework.md` | 分层职责、初始化和采集调用链 | 待创建 |
| `Streaming_State_Machine.md` | 资源获取/配置/开流/停流/释放及失败回退 | 待创建 |
| `AON_Camera.md` | 低功耗采集的完整路径、触发、存储与 AP 协同 | 待创建 |

文件名是规划，不是不存在正文的链接。正式编写后更新本导航。

## 软硬件关联重点

分别画 Sensor 控制路径与图像数据路径；核对 API 状态、Sensor 输出、接收端、ISP 与 Buffer 完成证据。

## 工程问题入口

C01/C03/C05/C06/C09；电源正常、寄存器可读与图像链正常需要分别验证。

案例定义和建设状态见 [工程案例导航](../10_Engineering_Cases/README.md)。

## 理解检查方向

能解释成功读 Chip ID 为什么仍可能无法出图，并设计接收路径的分层验证。

## 关联知识与资料

- [DMA 与内存](../02_Processor_Memory/README.md)
- [电源与时钟](../03_Power_Clock/README.md)
- [接口](../04_Hardware_Interfaces/README.md)
- [低功耗方案](../11_System_Design/README.md)
- [课程路线](../Roadmap.md)
- [术语速查](../Glossary.md)
- [公开资料索引](../Sources.md)
- 已核对的相关公开资料：[S01 Linux Camera Sensor](../Sources.md#s01-linux-camera-sensor-驱动)、[S02 DMA](../Sources.md#s02-linux-dma-地址与映射)、[S04 CSI-2](../Sources.md#s04-mipi-csi-2-官方介绍)。详细实现仍按资料版本和平台核对。
