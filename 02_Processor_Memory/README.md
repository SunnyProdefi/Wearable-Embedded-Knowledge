# 处理器与存储系统

## 本模块目标

建立 CPU 执行、地址空间、寄存器、DMA/IRQ 与存储可用条件的模型，连接代码和数据的真实访问路径。

- 深度：深入，第一阶段主模块。
- 前置：C/C++ 基础；具体课程依赖见 Roadmap。
- 课程位置：S1-01～S1-08；S4-03、S4-04。
- 状态：S1-01～S1-04 已建立；其余详细内容仍为规划。
- 学习掌握情况以 [Progress.md](../Progress.md) 为准。

## 主题与拟建文档

| 拟建文件 | 内容范围 | 建设状态 |
|---|---|---|
| [Processor_Roles.md](Processor_Roles.md) | S1-01：CPU/MCU/AP/SoC、Cortex-M/A 定位、DSP/NPU；MPU 与异构执行细节后续补充 | S1-01 正文已建立 |
| [Memory_and_Address_Spaces.md](Memory_and_Address_Spaces.md) | S1-02：SRAM/DRAM/DDR/Flash/ROM、代码与数据放置、掉电与采集恢复 | S1-02 正文已建立 |
| [Address_Spaces_and_Mapping.md](Address_Spaces_and_Mapping.md) | S1-03：地址上下文、VA/PA、RAM/MMIO/Sensor 编号与跨处理器访问 | S1-03 正文已建立 |
| [Registers_and_MMIO.md](Registers_and_MMIO.md) | S1-04：MMIO 控制链、位域、RW/W1C/读副作用、完成判据与 Linux 访问机制 | S1-04 正文已建立 |
| `Interrupts_and_DMA.md` | 事件产生、IRQ、轮询、搬运与完成处理 | 待创建 |
| `Cache_MMU_and_DMA_Mapping.md` | CPU 地址、DMA 地址、Cache、一致性、MMU/IOMMU | 待创建 |
| `Boot_and_Heterogeneous_Execution.md` | BootROM/Bootloader/Firmware、运行前提与多核协同 | 待创建 |

文件名是规划，不是不存在正文的链接。正式编写后更新本导航。

## 软硬件关联重点

CPU 配置资源与描述符，硬件执行访问或搬运，再由状态/中断通知软件；具体地址与一致性机制依平台。

## 工程问题入口

C04 MCU 访问不可用 DDR；分别验证映射、供电/初始化、权限、代码与数据位置。

案例定义和建设状态见 [工程案例导航](../10_Engineering_Cases/README.md)。

## 理解检查方向

能解释 Sensor 寄存器地址与 MMIO 地址的区别，并画出一帧图像进入 Buffer 的路径。

## 关联知识与资料

- [硬件接口](../04_Hardware_Interfaces/README.md)
- [Camera](../05_Camera/README.md)
- [嵌入式软件](../08_Embedded_Software/README.md)
- [课程路线](../Roadmap.md)
- [术语速查](../Glossary.md)
- [公开资料索引](../Sources.md)
- 已核对的相关公开资料：[S02 Linux DMA 地址与映射](../Sources.md#s02-linux-dma-地址与映射)。详细实现仍按资料版本和平台核对。
