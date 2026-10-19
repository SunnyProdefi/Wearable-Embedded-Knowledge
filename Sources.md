# 公开资料索引

## 记录规则

本文件记录已用于规划、课程和概念边界核对的公开资料。
S01～S11 首次查阅于 2026-10-14，后续资料按条目记录日期。未引用公司内部资料，也未指定目标产品和芯片。
页面链接可变化；进入详细课程时复核版本、接口与适用条件。
索引不替代正文引用；具体主张在对应文档附近放链接。
规范介绍页不等于已取得和逐条核对规范全文。

## S01 Linux Camera Sensor 驱动

- 类型：公开实现的官方文档。
- 来源：[Writing camera sensor drivers](https://docs.kernel.org/driver-api/media/camera-sensor.html)。
- 版本：查阅时的在线页面，URL 未固定内核版本；具体 API 使用前绑定目标内核版本。
- 支持范围：Linux Camera Sensor 的时钟、regulator/GPIO 资源与 runtime PM 管理。
- 限制：不代表所有 RTOS、OpenHarmony 或厂商 Camera 框架；不能提供具体 Sensor 电压和时序。

## S02 Linux DMA 地址与映射

- 类型：公开实现的官方文档。
- 来源：[Dynamic DMA mapping Guide](https://www.kernel.org/doc/html/v6.8/core-api/dma-api-howto.html)。
- 版本：Linux v6.8 文档。
- 支持范围：CPU 虚拟地址、CPU 物理地址、DMA 地址及映射的区别。
- 限制：不能推定具体平台 IOMMU、一致性或 DMA 能力；具体代码结合目标内核和硬件。
- S1-03 于 2026-10-16 复核地址分类，仅引用概念，不将示例地址用于实际平台。

## S03 Linux I3C 协议概览

- 类型：官方实现文档中的协议概览。
- 来源：[I3C protocol](https://docs.kernel.org/driver-api/i3c/protocol.html)。
- 版本：查阅时的在线页面，未固定规范版本。
- 支持范围：动态地址、DAA、CCC、IBI 与总线概念的软件视角。
- 限制：不是完整 MIPI 规范；文中可能保留旧术语和历史能力描述。
- 详细教学：标注 Controller/Target 与资料中 Master/Slave 的对应；电气和时序核对实际规范版本。

## S04 MIPI CSI-2 官方介绍

- 类型：标准组织官方介绍页。
- 来源：[Camera Serial Interface 2](https://www.mipi.org/specifications/csi-2)。
- 版本：查阅时的官方在线页面；本项目未绑定 CSI-2 规范版本。
- 支持范围：CSI-2 的定位和与物理层的关系。
- 限制：本次未取得规范全文，不声称已核对 lane、速率、时序或规范条款。
- 本库框图仅选用 CSI-2 over D-PHY 作为教学方案。

## S05 Zephyr 设备电源管理

- 类型：公开实现的官方文档。
- 来源：[Device Power Management](https://docs.zephyrproject.org/latest/services/pm/device.html)。
- 版本：latest 在线文档；详细 API 与代码须绑定目标 Zephyr 版本。
- 支持范围：设备运行时电源管理、系统管理设备电源状态及系统依赖的划分。
- 限制：不能直接推广为 Linux 或厂商 PM API 的行为。

## S06 Bluetooth SIG LE Audio

- 类型：标准组织官方介绍页。
- 来源：[LE Audio](https://www.bluetooth.com/learn-about-bluetooth/feature-enhancements/le-audio/)。
- 版本：查阅时的在线介绍；尚未选定 Core、Profile 或 Service 规范版本。
- 支持范围：LE Audio 与 LC3 等基础定位。
- 限制：不证明某芯片支持全部能力，也不能给出实际音频延迟、吞吐或功耗。

## S07 Arm CPU 架构定位

- 类型：处理器 IP 厂商官方介绍。
- 来源：[Arm CPU Architecture](https://www.arm.com/architecture/cpu)。
- 版本：2026-10-14 查阅的在线页，没有绑定具体架构手册版本。
- 支持范围：Cortex-A/Cortex-M 的定位，CPU 内核系列与系统用途的区别。
- 限制：不作为具体核的 MMU、IRQ、功耗和指令能力依据；本课不引用“最新架构版本”判断。

## S08 NXP i.MX 8M Plus 集成实例

- 类型：芯片厂商官方产品页。
- 来源：[i.MX 8M Plus](https://www.nxp.com/products/i.MX8MPLUS)。
- 版本：2026-10-14 查阅的家族介绍，非固定器件料号或参考手册版本。
- 支持范围：应用处理器家族集成 Cortex-A53、Cortex-M7、NPU、ISP 与音频 DSP 的公开例子。
- 限制：不代表智能眼镜选型；不从家族页面推定具体变体、电源域和低功耗能力，不引用本课不需要的数值。

## S09 Arm CMSIS-Ethos-U 软件路径

- 类型：官方软件包说明。
- 来源：[Arm Keil CMSIS-Ethos-U](https://www.keil.arm.com/packs/cmsis-ethos-u-arm/overview/)。
- 版本：2026-10-14 查阅的在线包说明，未绑定目标软件包版本。
- 支持范围：Vela 部署前编译、Cortex-M 应用/推理运行时通过驱动提交命令与模型内存区域。
- 限制：是 Ethos-U 公开实现示例，不是所有 NPU 的统一 ABI/API 或内部结构说明；不提供可直接运行代码。

## S10 TI DSP SoC 与工具

- 类型：芯片厂商官方产品与工具介绍。
- 来源：[Audio & radar DSP SoCs](https://www.ti.com/product-category/microcontrollers-processors/microprocessors-dsp/audio-radar-dsp-socs/overview.html)。
- 版本：2026-10-14 查阅的在线类别页，未绑定具体器件或编译器版本。
- 支持范围：Arm 与 DSP 的集成及 DSP C/C++ 编译工具的公开例子。
- 限制：不是眼镜/TWS 专用方案；不推定 DSP 任务分配、滤波算法或实时性保证。

## S11 ST STM32H7 MCU 集成实例

- 类型：芯片厂商官方产品家族介绍。
- 来源：[STM32H7 Series](https://www.st.com/en/microcontrollers-microprocessors/stm32h7-series.html)。
- 版本：2026-10-14 查阅的家族介绍，未绑定具体料号。
- 支持范围：MCU 含 Cortex-M 内核、存储与外设，家族中存在不同单/双核及存储配置。
- 限制：不将某成员配置推广为所有 MCU；不推定 MCU 必须全片上存储或必须独立封装。

## S12 Micron 运行内存与持久存储

- 类型：存储厂商官方说明；查阅日期：2026-10-16。
- 来源：[Mobile Memory and Storage](https://www.micron.com/markets-industries/mobile)。
- 版本：查阅时在线页，未绑定特定产品版本。
- 支持范围：移动 DRAM/LPDDR 是运行内存，Flash 保存文件及镜像；易失与非易失的区别。
- 限制：不把手机产品配置作为眼镜器件参数，不引用该页面的最新性能宣传。

## S13 Infineon 普通 SRAM

- 类型：存储厂商官方介绍；查阅日期：2026-10-16。
- 来源：[SRAMs](https://www.infineon.com/products/memories/sram-static-ram)。
- 版本：查阅时在线产品类别页。
- 支持范围：普通 SRAM 易失、无需 DRAM 式周期刷新，可用于运行数据与缓冲。
- 限制：不引用营销性能数值；带备份供电或特殊非易失方案另查资料，不推广为普通 SRAM 断电保留。

## S14 Micron 刷新与自刷新条件

- 类型：存储厂商官方 FAQ；查阅日期：2026-10-16。
- 来源：[Micron FAQs](https://www.micron.com/sales-support/sales/faqs)，DRAM refresh 与 DDR self-refresh 相关问答。
- 版本：在线 FAQ，包含不同历史代际的问答，未作为目标器件规范。
- 支持范围：DRAM 内容维持与刷新、自刷新仍依赖保持供电等条件。
- 限制：页面具体电压、引脚和时序不能套到任意 DDR/LPDDR；目标设计必须查数据手册。本课不引用其数值。

## S15 Micron DDR 传输与 DRAM 关系

- 类型：存储厂商官方 FAQ；查阅日期：2026-10-16。
- 来源：[DDR5 DRAM](https://www.micron.com/products/memory/dram-components/ddr5-sdram)。
- 版本：查阅时在线页；只使用基础定义，不绑定本项目内存代际。
- 支持范围：DDR5 系统内存属于 DRAM；DDR 表示相关时钟双沿的数据传输，而非容量翻倍。
- 限制：不推定目标 SoC 支持 DDR5，也不声称应用性能翻倍；LPDDR 另结合 S12。

## S16 ST 加载执行与 XIP

- 类型：芯片厂商官方 Wiki；查阅日期：2026-10-16。
- 来源：[Introduction to External Memory Manager](https://wiki.st.com/stm32mcu/wiki/Introduction_to_External_memory_Manager)。
- 版本：查阅时在线页，页面显示修订标识 oldid=80957；引用可访问的正文入口，不提供具体 API 使用代码。
- 支持范围：XIP 与加载到 RAM 后执行两类流程，以及存储初始化/映射条件的公开实现例子。
- 限制：不是所有 MCU/Flash 的通用功能；没有匹配目标器件、控制器与布局时不能假定支持 XIP。

## S17 NXP Mask ROM 与 Flash 对照

- 类型：厂商应用笔记；查阅日期：2026-10-16。
- 来源：[AN2200](https://www.nxp.com/docs/en/application-note/AN2200.pdf)，第 2.1 节 ROM versus FLASH。
- 版本：文档编号 AN2200，涉及 HC08 系列历史器件；本课不绑定这些器件。
- 支持范围：厂商对出厂 Mask ROM 与可电擦写非易失 Flash 的明确对照。
- 限制：不能将这些器件地址、容量、启动流程推广到当前平台；“BootROM”区域的物理实现仍须单独确认。

## S18 Linux MMIO 设备访问

- 类型：公开实现的官方文档；查阅日期：2026-10-16。
- 来源：[Bus-Independent Device Accesses](https://www.kernel.org/doc/html/v6.8/driver-api/device-io.html)。
- 版本：Linux v6.8 文档。
- 支持范围：内存映射设备的资源映射与访问接口，MMIO 与普通内存语义的区别。
- 限制：不是具体控制器寄存器手册；S1-03 只介绍定位与映射，实际调用和访问顺序后续结合平台。
- S1-04 于 2026-10-17 复核 MMIO、I/O 访问接口与 posted write；只引用定义和边界，不将任意读回当作通用完成机制。

## S19 Linux I2C 目标地址与寄存器参数

- 类型：公开实现的官方文档；查阅日期：2026-10-16。
- 来源：[Implementing I2C device drivers in userspace](https://www.kernel.org/doc/html/v6.8/i2c/dev-interface.html)。
- 版本：Linux v6.8 文档。
- 支持范围：总线实例、目标设备地址、设备寄存器/命令及事务接口的区分。
- 限制：示例的 SMBus 格式不适用于任意 Sensor；I3C 地址管理另查其规范及实现。本课不照抄示例地址作为器件参数。

## S20 Open-CMSIS-SVD 寄存器访问语义

- 类型：公开寄存器描述规范文档；查阅日期：2026-10-17。
- 来源：[registers element](https://open-cmsis-pack.github.io/svd-spec/latest/elem_registers.html)。
- 版本：latest 在线规范描述页，未指定目标芯片 SVD 或硬件版本。
- 支持范围：寄存器/位域、访问类别、oneToClear 和 readAction 等元数据表达的机制。
- 限制：不能据此断定某个实际寄存器采用 W1C 或读清除，也不迁移页面示例地址和位定义；必须核对目标手册。

## S21 Linux volatile 的使用边界

- 类型：公开实现的官方文档；查阅日期：2026-10-17。
- 来源：[Why the volatile type class should not be used](https://www.kernel.org/doc/html/v6.8/process/volatile-considered-harmful.html)。
- 版本：Linux v6.8 文档。
- 支持范围：Linux 中 volatile 不能代替同步与正确访问机制，驱动应使用适当 I/O 接口。
- 限制：不是对所有裸机 SDK 的禁令，也不保证任意语言编译器的设备访问行为；具体平台依其规则。

## S22 Linux 内存屏障与 I/O 顺序

- 类型：公开实现的官方文档；查阅日期：2026-10-17。
- 来源：[Linux kernel memory barriers](https://www.kernel.org/doc/html/v6.8/core-api/wrappers/memory-barriers.html)。
- 版本：Linux v6.8 文档。
- 支持范围：内存/I/O 访问顺序、可见性及访问接口保证需要按其定义理解。
- 限制：不将访问有序等同于外设工作完成；S1-04 不提供通用屏障配方或特定控制器等待代码。

## S23 Linux I2C 软件分层与设备驱动

- 类型：公开实现的官方文档；查阅日期：2026-10-19。
- 来源：[Introduction to I2C and SMBus](https://www.kernel.org/doc/html/v6.8/i2c/summary.html)、[Implementing I2C device drivers](https://www.kernel.org/doc/html/v6.8/i2c/writing-clients.html)。
- 版本：Linux v6.8 文档。
- 支持范围：adapter/client、控制器驱动与设备驱动的分层，以及设备访问参数的组织。
- 限制：文档保留 master/slave 等旧术语；不引用其历史速度概括作为完整 I2C 规范，不照抄示例 SMBus 命令用于任意 Sensor。

## S24 Linux I2C 事务概览

- 类型：公开实现的官方协议说明；查阅日期：2026-10-19。
- 来源：[The I2C Protocol](https://www.kernel.org/doc/html/v6.8/i2c/i2c-protocol.html)。
- 版本：Linux v6.8 文档。
- 支持范围：读写消息、组合事务、起始/停止与 ACK/NACK 在事务中的位置。
- 限制：不是完整电气规范或 Sensor 访问手册；“发送内部编号再读取”是本课器件访问假设，宽度、字节序及 STOP/重复起始要求必须核对实际器件。

## S25 Linux I2C API 返回契约

- 类型：公开实现的官方 API 文档；查阅日期：2026-10-19。
- 来源：[I2C and SMBus Subsystem](https://www.kernel.org/doc/html/v6.8/driver-api/i2c.html)。
- 版本：Linux v6.8 文档。
- 支持范围：`i2c_transfer()` 返回已执行消息数或负错误码，与按字节数返回的接口区分。
- 限制：不将该同步接口语义推广到厂商异步接口；传输完整完成也需另外核对器件数据含义。

## S26 Arm AMBA 连接用途

- 类型：协议制定方官方介绍页；查阅日期：2026-10-19。
- 来源：[AMBA](https://www.arm.com/architecture/system-architectures/amba)。
- 版本：查阅时在线介绍，未绑定具体 AMBA 子协议版本。
- 支持范围：AMBA 连接 SoC 功能模块，AXI/AHB/APB 的基本定位。
- 限制：本次未逐条核对规范全文，不推定目标芯片必用这些协议、桥接结构或拓扑；不把片上用途解释为所有 AMBA 扩展只能片内使用。

## S27 Linux 通用与线程化 IRQ

- 类型：公开实现的官方文档；查阅日期：2026-10-19。
- 来源：[Linux generic IRQ handling](https://www.kernel.org/doc/html/v6.8/core-api/genericirq.html)。
- 版本：Linux v6.8 文档；引用通用分层、IRQ 流程及线程化接口说明，不将历史背景描述当作当前实现状态。
- 支持范围：IRQ 层级、屏蔽/确认/EOI、边沿/电平流程，以及主处理与线程处理的区分。
- 限制：不提供目标芯片 IRQ 编号、路由或状态定义，不假定设备清源与中断控制器确认是同一操作；特殊内核配置按目标实现核对。

## S28 Linux 忙等与睡眠延时

- 类型：公开实现的官方文档；查阅日期：2026-10-19。
- 来源：[delays - Information on the various kernel delay / sleep mechanisms](https://www.kernel.org/doc/html/v6.8/timers/timers-howto.html)。
- 版本：Linux v6.8 文档。
- 支持范围：忙等/睡眠及原子上下文对接口选择的限制。
- 限制：本课不引用页面时间阈值作为通用选型参数；等待时长与 API 需结合目标任务和上下文，固定延时不替代完成判断。

## S29 Linux 工作队列

- 类型：公开实现的官方文档；查阅日期：2026-10-19。
- 来源：[Workqueue](https://www.kernel.org/doc/html/v6.8/core-api/workqueue.html)。
- 版本：Linux v6.8 文档。
- 支持范围：普通工作线程执行排队任务的模型，以及排队与执行完成的区别。
- 限制：不将所有延后执行机制都视为可睡眠；仍需核对具体队列、上下文、所持锁及目标版本。

## S30 Linux Completion 等待与通知

- 类型：公开实现的官方文档；查阅日期：2026-10-19。
- 来源：[Completions - wait for completion barrier APIs](https://www.kernel.org/doc/html/v6.8/scheduler/completion.html)。
- 版本：Linux v6.8 文档。
- 支持范围：先初始化、通知可先于等待、阻塞等待的上下文限制，以及超时/复用/对象生命周期问题。
- 限制：completion 不自动关联硬件请求编号或确认数据有效；本课不提供适用于所有设备的初始化/启动/重置配方。

## 后续需要的器件资料

当前无具体芯片，以下都待用户任务提供或公开查证：
- Sensor Datasheet：电源、时序、寄存器、输出格式与时钟限制。
- SoC Reference Manual：地址映射、控制器、DMA、IRQ、时钟和电源域。
- PMIC/稳压器资料：供电能力、使能、状态与启动条件。
- 音频/无线芯片资料：Host 接口、时钟、固件与能力。
- 板级框图与原理图：仅在用户授权范围内使用，不擅自外传。

## 新来源记录字段

来源 ID、标题、发布机构、直接链接/本地资料路径、版本、查阅日期、支持的结论、适用平台、限制。
没有资料支持的参数标记待验证，并写明需要哪份资料或实验。
