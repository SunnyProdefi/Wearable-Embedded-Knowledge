# 术语速查

## 使用说明

首批 30 个术语，加上 S1-01 新增的 DSP/NPU，共 32 个，面向 Camera 底层软件工作；这是通用概念速查，不是器件参数表。
关联链接指向已存在的模块导航或课程正文；正式讲解后更新相关入口。
术语存在不代表用户已学习或掌握。

| 序号 | 缩写/术语 | 英文全称/名称 | 中文名称 | 简要说明 | 关联文档 |
|---|---|---|---|---|---|
| 1 | CPU | Central Processing Unit | 中央处理器 | 执行指令；需结合其可访问资源理解行为。 | [S1-01](02_Processor_Memory/Processor_Roles.md) |
| 2 | MCU | Microcontroller Unit | 微控制器 | 通常集成处理器、存储与外设，角色和能力取决于芯片。 | [S1-01](02_Processor_Memory/Processor_Roles.md) |
| 3 | AP | Application Processor | 应用处理器 | 承担应用和较复杂系统任务的处理器角色，常指整颗主处理芯片。 | [S1-01](02_Processor_Memory/Processor_Roles.md) |
| 4 | SoC | System on Chip | 片上系统 | 集成多类处理、存储接口和外设模块；与 AP/MCU 不是互斥分类。 | [S1-01](02_Processor_Memory/Processor_Roles.md) |
| 5 | SRAM | Static Random-Access Memory | 静态随机存储器 | 常用于片上运行存储；静态不代表断电后保留。 | [模块入口](02_Processor_Memory/README.md) |
| 6 | DRAM / DDR | Dynamic RAM / Double Data Rate | 动态随机存储器 / 双倍数据率 | DDR 常用于 DRAM 技术名称；DRAM 使用中需要刷新。 | [模块入口](02_Processor_Memory/README.md) |
| 7 | Flash | Flash Memory | 闪存 | 非易失性存储，常用于固件及持久数据；执行方式依平台。 | [模块入口](02_Processor_Memory/README.md) |
| 8 | Cache | Cache Memory | 缓存 | 减少访问较慢存储的开销；与 DMA 共享数据要考虑一致性。 | [模块入口](02_Processor_Memory/README.md) |
| 9 | MMU | Memory Management Unit | 内存管理单元 | 提供地址转换和访问权限等机制，具体功能依架构。 | [模块入口](02_Processor_Memory/README.md) |
| 10 | Register | Register | 寄存器 | 本库重点为硬件配置、状态与数据寄存器；访问规则依器件。 | [模块入口](02_Processor_Memory/README.md) |
| 11 | MMIO | Memory-Mapped I/O | 内存映射 I/O | 通过地址空间中的映射访问硬件；不同于普通 RAM 访问语义。 | [模块入口](02_Processor_Memory/README.md) |
| 12 | DMA | Direct Memory Access | 直接内存访问 | 硬件搬运数据，减少 CPU 逐项搬运；仍需配置、同步及完成处理。 | [模块入口](02_Processor_Memory/README.md) |
| 13 | IRQ | Interrupt Request | 中断请求 | 通知处理器发生事件；实际触发、屏蔽和处理链依平台。 | [模块入口](02_Processor_Memory/README.md) |
| 14 | PMIC | Power Management Integrated Circuit | 电源管理芯片 | 管理电源相关功能的集成电路，不能仅凭名称推定功能范围。 | [模块入口](03_Power_Clock/README.md) |
| 15 | PMU | Power Management Unit | 电源管理单元 | 电源管理功能单元，可能位于 SoC 等器件内部，边界依平台。 | [模块入口](03_Power_Clock/README.md) |
| 16 | LDO | Low-Dropout Regulator | 低压差线性稳压器 | 线性稳压；软件需关注使能、负载、电压和可用条件。 | [模块入口](03_Power_Clock/README.md) |
| 17 | BUCK | Buck Converter | 降压开关变换器 | 开关式降压电路；适用电压、负载和动态行为看器件资料。 | [模块入口](03_Power_Clock/README.md) |
| 18 | Power Rail | Power Rail | 电源轨 | 一路供电网络；不与电源管理域简单等同。 | [模块入口](03_Power_Clock/README.md) |
| 19 | Power Domain | Power Domain | 电源域 | 具有共同电源管理边界的电路集合；具体划分依平台。 | [模块入口](03_Power_Clock/README.md) |
| 20 | AVDD | Analog Supply Voltage（常见命名） | 模拟电源 | 常见模拟部分供电名称，准确含义看器件引脚定义。 | [模块入口](03_Power_Clock/README.md) |
| 21 | DVDD | Digital Supply Voltage（常见命名） | 数字电源 | 常见数字核心供电名称；具体定义依器件。 | [模块入口](03_Power_Clock/README.md) |
| 22 | DOVDD / VDDIO | Digital I/O Supply / I/O Supply Voltage（常见命名） | 数字接口电源 | 常见 I/O 供电命名，不保证两个名称在所有芯片中可互换。 | [模块入口](03_Power_Clock/README.md) |
| 23 | Reset | Reset | 复位 | 使指定硬件进入规定状态；范围、极性、时序及保留项需核对。 | [模块入口](03_Power_Clock/README.md) |
| 24 | Crystal | Quartz Crystal | 晶体 | 通常与振荡电路配合形成时钟；不同于独立完整振荡器。 | [模块入口](03_Power_Clock/README.md) |
| 25 | PLL | Phase-Locked Loop | 锁相环 | 用于时钟合成等功能；锁定与输入条件取决于具体实现。 | [模块入口](03_Power_Clock/README.md) |
| 26 | MCLK | Master Clock（常见命名） | 主时钟 | Camera 中常指 Sensor 外部输入时钟，命名和来源依平台。 | [模块入口](03_Power_Clock/README.md) |
| 27 | GPIO | General-Purpose Input/Output | 通用输入输出 | 控制或采样引脚状态；需核对复用、电平、方向及上下拉。 | [模块入口](04_Hardware_Interfaces/README.md) |
| 28 | I2C | Inter-Integrated Circuit | 集成电路间串行总线 | 常见双线外设控制接口；总线地址与器件寄存器地址不同。 | [模块入口](04_Hardware_Interfaces/README.md) |
| 29 | I3C | Improved Inter-Integrated Circuit | 改进型集成电路间串行总线 | 支持动态地址和带内中断等能力，实际支持需核对版本及器件。 | [模块入口](04_Hardware_Interfaces/README.md) |
| 30 | AON | Always-On | 常开资源或域 | 在指定低功耗状态保留的资源，不能据此推定支持图像采集。 | [模块入口](01_System_Architecture/README.md) |
| 31 | DSP | Digital Signal Processor | 数字信号处理器 | 为滤波等信号计算优化的可编程处理器；职责与工具链依平台。 | [S1-01](02_Processor_Memory/Processor_Roles.md) |
| 32 | NPU | Neural Processing Unit | 神经网络处理单元 | 加速支持的神经网络任务；需要模型适配、运行时和资源管理。 | [S1-01](02_Processor_Memory/Processor_Roles.md) |

## 相关公开依据与边界

- DMA 地址、CPU 地址及映射：见 [S02：Linux DMA 指南](Sources.md#s02-linux-dma-地址与映射)。
- Camera 时钟、电源和软件资源管理的公开实现：见 [S01：Linux Camera Sensor](Sources.md#s01-linux-camera-sensor-驱动)。
- I3C 动态地址、CCC 与 IBI 概览：见 [S03：Linux I3C](Sources.md#s03-linux-i3c-协议概览)。
- AON、电源域、电源引脚名称及复位语义要查目标平台/器件资料；本库尚未指定芯片，未核对任何具体电压或时序。
- PMIC/PMU、AP/MCU 等是功能与集成边界相关概念，不凭缩写推定实际芯片拓扑。

## 下一批术语

规划：ISP、CSI-2、D-PHY、PDM、I2S、Codec、HCI、DAA、CCC、ENTDAA、SETDASA、IBI、ACK/NACK、BootROM、IOMMU、Runtime PM。
这些尚未作为正式速查条目建立；随课程或会议问题查证后补入。

## 速查回答约定

一句话解释 → 核心原理 → 穿戴系统作用 → 与软件的关系 → 关联知识。
总线 ACK 与设备命令完成通知分开解释；厂商 HostCmd 协议没有资料时标记待验证。
