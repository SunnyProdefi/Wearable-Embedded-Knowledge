# 术语速查

## 使用说明

首批 30 个术语，加上 S1-01～S1-06 的关联条目，共 59 个，面向 Camera 底层软件工作；这是通用概念速查，不是器件参数表。
关联链接指向已存在的模块导航或课程正文；正式讲解后更新相关入口。
术语存在不代表用户已学习或掌握。

| 序号 | 缩写/术语 | 英文全称/名称 | 中文名称 | 简要说明 | 关联文档 |
|---|---|---|---|---|---|
| 1 | CPU | Central Processing Unit | 中央处理器 | 执行指令；需结合其可访问资源理解行为。 | [S1-01](02_Processor_Memory/Processor_Roles.md) |
| 2 | MCU | Microcontroller Unit | 微控制器 | 通常集成处理器、存储与外设，角色和能力取决于芯片。 | [S1-01](02_Processor_Memory/Processor_Roles.md) |
| 3 | AP | Application Processor | 应用处理器 | 承担应用和较复杂系统任务的处理器角色，常指整颗主处理芯片。 | [S1-01](02_Processor_Memory/Processor_Roles.md) |
| 4 | SoC | System on Chip | 片上系统 | 集成多类处理、存储接口和外设模块；与 AP/MCU 不是互斥分类。 | [S1-01](02_Processor_Memory/Processor_Roles.md) |
| 5 | SRAM | Static Random-Access Memory | 静态随机存储器 | 普通 SRAM 易失；静态表示不需要 DRAM 式周期刷新，不代表断电保留。 | [S1-02](02_Processor_Memory/Memory_and_Address_Spaces.md) |
| 6 | DRAM / DDR | Dynamic RAM / Double Data Rate | 动态随机存储器 / 双倍数据率 | DRAM 需要供电与刷新；本课 DDR SDRAM 属于 DRAM，DDR 描述传输特性。 | [S1-02](02_Processor_Memory/Memory_and_Address_Spaces.md) |
| 7 | Flash | Flash Memory | 闪存 | 非易失、可电擦写，常存固件和文件；镜像存放位置与执行位置可以不同。 | [S1-02](02_Processor_Memory/Memory_and_Address_Spaces.md) |
| 8 | Cache | Cache Memory | 缓存 | 减少访问较慢存储的开销；与 DMA 共享数据要考虑一致性。 | [模块入口](02_Processor_Memory/README.md) |
| 9 | MMU | Memory Management Unit | 内存管理单元 | 提供地址转换和访问权限等机制，具体功能依架构。 | [模块入口](02_Processor_Memory/README.md) |
| 10 | Register | Register | 寄存器 | 外设暴露的配置、状态或数据访问接口；读写可能有副作用，本课不同于 CPU 通用寄存器。 | [S1-04](02_Processor_Memory/Registers_and_MMIO.md) |
| 11 | MMIO | Memory-Mapped I/O | 内存映射 I/O | 把 CPU 地址空间的一部分用于设备访问；映射、宽度、接口和寄存器语义需匹配。 | [S1-04](02_Processor_Memory/Registers_and_MMIO.md) |
| 12 | DMA | Direct Memory Access | 直接内存访问 | 硬件搬运数据，减少 CPU 逐项搬运；仍需配置、同步及完成处理。 | [模块入口](02_Processor_Memory/README.md) |
| 13 | IRQ | Interrupt Request | 中断请求 | 通知处理器发生事件；实际触发、屏蔽和处理链依平台，不代表上层回调已执行。 | [S1-06](02_Processor_Memory/Interrupts_and_Polling.md) |
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
| 33 | ROM | Read-Only Memory | 只读存储器 | 本课为非易失启动存储语境；Mask ROM 出厂固化，具体 ROM 区域实现需查芯片。 | [S1-02](02_Processor_Memory/Memory_and_Address_Spaces.md) |
| 34 | RAM | Random-Access Memory | 随机存取存储器 | 本课主要指 SRAM/DRAM 等运行内存；随机存取不表示随机写入。 | [S1-02](02_Processor_Memory/Memory_and_Address_Spaces.md) |
| 35 | LPDDR | Low-Power Double Data Rate | 低功耗双倍数据率内存 | 低功耗 DRAM 家族；仍要满足供电、刷新与访问条件。 | [S1-02](02_Processor_Memory/Memory_and_Address_Spaces.md) |
| 36 | Buffer | Buffer | 缓冲区 | 内存的一种用途，不是独立存储技术；可位于 DDR 或 SRAM，依容量和可达性。 | [S1-02](02_Processor_Memory/Memory_and_Address_Spaces.md) |
| 37 | XIP | Execute In Place | 就地执行 | 从支持直接取指的存储映射执行代码，需要器件、控制器与系统支持。 | [S1-02](02_Processor_Memory/Memory_and_Address_Spaces.md) |
| 38 | Address Space | Address Space | 地址空间 | 某访问主体在指定上下文中使用的一套地址；相同数值不保证相同对象。 | [S1-03](02_Processor_Memory/Address_Spaces_and_Mapping.md) |
| 39 | Memory Map / Mapping | Memory Map / Memory Mapping | 地址分布图 / 地址映射 | 前者记录区域分配，后者表示地址与资源的对应；建立映射不等于复制内容。 | [S1-03](02_Processor_Memory/Address_Spaces_and_Mapping.md) |
| 40 | VA | Virtual Address | 虚拟地址 | 依赖当前地址转换上下文；不能仅凭数值当作物理地址或跨处理器地址。 | [S1-03](02_Processor_Memory/Address_Spaces_and_Mapping.md) |
| 41 | PA | Physical Address | 物理地址 | CPU 地址转换后所用硬件视图中的地址；仍需说明访问者和平台地址图。 | [S1-03](02_Processor_Memory/Address_Spaces_and_Mapping.md) |
| 42 | Base / Offset | Base Address / Offset | 基址 / 偏移 | 在同一视图及手册规定单位下，用区域基址与偏移定位；不能混用 CPU、总线和器件内部编号。 | [S1-03](02_Processor_Memory/Address_Spaces_and_Mapping.md) |
| 43 | Bit Field / Mask | Bit Field / Bit Mask | 位域 / 位掩码 | 用一个或多个位表达功能，掩码选择目标位；不改变寄存器本身的访问语义。 | [S1-04](02_Processor_Memory/Registers_and_MMIO.md) |
| 44 | RO / RW / WO | Read-Only / Read-Write / Write-Only | 只读 / 读写 / 只写 | 描述访问类别，仍需核对各位副作用、生效和保留位规则。 | [S1-04](02_Processor_Memory/Registers_and_MMIO.md) |
| 45 | W1C | Write One to Clear | 写 1 清零 | 对目标位写 1 触发清除，写 0 不清；不能照搬普通 RW 读改写。 | [S1-04](02_Processor_Memory/Registers_and_MMIO.md) |
| 46 | Read-to-clear | Read-to-clear | 读后清除 | 读取会清除指定状态，调试和日志也可能改变事件可见性。 | [S1-04](02_Processor_Memory/Registers_and_MMIO.md) |
| 47 | RMW | Read-Modify-Write | 读改写 | 读取、修改目标字段、写回；仅在语义允许且并发等条件妥当时使用，不是通用原子操作。 | [S1-04](02_Processor_Memory/Registers_and_MMIO.md) |
| 48 | Controller | Controller | 控制器 | 执行特定接口操作的硬件模块；其寄存器接口与外部协议接口各有规则。 | [S1-05](02_Processor_Memory/Controllers_and_Buses.md) |
| 49 | Interconnect | On-chip Interconnect | 片上互联 | 连接芯片内部功能模块并传递访问请求与响应，具体拓扑依平台。 | [S1-05](02_Processor_Memory/Controllers_and_Buses.md) |
| 50 | AMBA | Advanced Microcontroller Bus Architecture | Arm 片上互联协议体系 | 包含 AXI/AHB/APB 等，不能凭名称推定具体 SoC 的连接与版本。 | [S1-05](02_Processor_Memory/Controllers_and_Buses.md) |
| 51 | Adapter / Client | I2C Adapter / I2C Client | I2C 适配器 / 客户设备 | Linux I2C 的软件对象及分层术语；逻辑 adapter 不一定一一对应物理控制器。 | [S1-05](02_Processor_Memory/Controllers_and_Buses.md) |
| 52 | ACK / NACK | Acknowledge / Not Acknowledge | 应答 / 非应答 | I2C 中需结合阶段和发送方解释；应答不证明器件身份或图像完成，读末尾 NACK 可为正常结束。 | [S1-05](02_Processor_Memory/Controllers_and_Buses.md) |
| 53 | Transaction | Bus Transaction | 总线事务 | 按接口协议组织的一次通信过程；器件寄存器读取可由多个消息组合完成。 | [S1-05](02_Processor_Memory/Controllers_and_Buses.md) |
| 54 | Polling | Polling | 轮询 | 软件再次检查状态，可忙等或间隔查询；需核对读取副作用、事件保持与超时。 | [S1-06](02_Processor_Memory/Interrupts_and_Polling.md) |
| 55 | ISR | Interrupt Service Routine | 中断服务例程 | 识别并处理事件的程序；允许执行的操作取决于处理上下文。 | [S1-06](02_Processor_Memory/Interrupts_and_Polling.md) |
| 56 | Interrupt Controller | Interrupt Controller | 中断控制器 | 管理中断的屏蔽、路由与分派等，具体能力依平台；不同于执行 I2C 事务的控制器。 | [S1-06](02_Processor_Memory/Interrupts_and_Polling.md) |
| 57 | Execution Context | Execution Context | 执行/处理上下文 | 决定代码能否睡眠、阻塞及使用哪些接口；硬中断与线程上下文分别核对。 | [S1-06](02_Processor_Memory/Interrupts_and_Polling.md) |
| 58 | Mask / Unmask | Interrupt Mask / Unmask | 中断屏蔽 / 解除屏蔽 | 控制指定层级的中断通知，不自动等于清状态或停止硬件任务。 | [S1-06](02_Processor_Memory/Interrupts_and_Polling.md) |
| 59 | Edge / Level | Edge-triggered / Level-triggered | 边沿 / 电平触发 | 分别关注规定方向的变化或有效电平；锁存、重送与清源规则依平台。 | [S1-06](02_Processor_Memory/Interrupts_and_Polling.md) |

## 相关公开依据与边界

- DMA 地址、CPU 地址及映射：见 [S02：Linux DMA 指南](Sources.md#s02-linux-dma-地址与映射)。
- Camera 时钟、电源和软件资源管理的公开实现：见 [S01：Linux Camera Sensor](Sources.md#s01-linux-camera-sensor-驱动)。
- I3C 动态地址、CCC 与 IBI 概览：见 [S03：Linux I3C](Sources.md#s03-linux-i3c-协议概览)。
- 存储类型、DDR、ROM/Flash 和执行位置：见 [S1-02 正文及对应来源](02_Processor_Memory/Memory_and_Address_Spaces.md)。
- 地址空间、映射和器件内部编号：见 [S1-03 正文及对应来源](02_Processor_Memory/Address_Spaces_and_Mapping.md)。
- 寄存器位域、读写副作用与 MMIO 完成语义：见 [S1-04 正文及对应来源](02_Processor_Memory/Registers_and_MMIO.md)。
- 控制器分工、片上互联、I2C 请求与返回契约：见 [S1-05 正文及对应来源](02_Processor_Memory/Controllers_and_Buses.md)。
- 中断、轮询、处理上下文与等待通知：见 [S1-06 正文及对应来源](02_Processor_Memory/Interrupts_and_Polling.md)。
- AON、电源域、电源引脚名称及复位语义要查目标平台/器件资料；本库尚未指定芯片，未核对任何具体电压或时序。
- PMIC/PMU、AP/MCU 等是功能与集成边界相关概念，不凭缩写推定实际芯片拓扑。

## 下一批术语

规划：ISP、CSI-2、D-PHY、PDM、I2S、Codec、HCI、DAA、CCC、ENTDAA、SETDASA、IBI、BootROM、IOMMU、Runtime PM。
这些尚未作为正式速查条目建立；随课程或会议问题查证后补入。

## 速查回答约定

一句话解释 → 核心原理 → 穿戴系统作用 → 与软件的关系 → 关联知识。
总线 ACK 与设备命令完成通知分开解释；厂商 HostCmd 协议没有资料时标记待验证。
