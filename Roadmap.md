# 学习路线

## 适用范围

对象：具备 Camera 软件开发经验、希望补齐硬件与系统协同能力的工程师。
目录分类不等于课程顺序；每课使用稳定 ID，允许按前置依赖交叉学习。
课程按学习逐步建立；[S1-01](02_Processor_Memory/Processor_Roles.md)、[S1-02](02_Processor_Memory/Memory_and_Address_Spaces.md)、[S1-03](02_Processor_Memory/Address_Spaces_and_Mapping.md)、[S1-04](02_Processor_Memory/Registers_and_MMIO.md)、[S1-05](02_Processor_Memory/Controllers_and_Buses.md)、[S1-06](02_Processor_Memory/Interrupts_and_Polling.md)、[S1-07](02_Processor_Memory/Cache_MMU_and_DMA_Mapping.md) 正文已建立，其余正文待创建。实际进度见 [Progress.md](Progress.md)。

## 开课前导览与评估

先用 [智能眼镜简化框图](01_System_Architecture/README.md#典型智能眼镜功能框图) 识别四类连接。
结合用户反馈检查：寄存器访问、Sensor 启动、Buffer、故障定位是否已有完整模型。
已有经验只作为调整难度的线索，不自动标记掌握。

## 五阶段总览

| 阶段 | 目标 | 核心前置 | 验收产出 |
|---|---|---|---|
| 1 底层计算与存储 | 理解处理器、地址、寄存器、中断、DMA 与运行前提 | C/C++ 基础 | 区分寄存器控制链与图像数据链 |
| 2 电源、时钟与接口 | 理解硬件可访问条件和接口行为 | S1-03～S1-06 | Sensor 启动依赖图、Chip ID 验证方案 |
| 3 主要子系统 | Camera 深入，音频无线建立完整链路 | 对应接口与电源知识 | 图像和音频链路，控制/数据/通知标注 |
| 4 软硬件协同 | 资源管理、IPC、固件与恢复 | 一个完整子系统及基础运行前提 | AP/MCU 命令、超时、所有权与恢复方案 |
| 5 系统设计与实践 | 联合分析功耗、性能、并发与异常 | 所涉及模块的阶段检查 | 低功耗 Camera 架构评审与跨模块案例 |

## 第一阶段：底层计算与存储

每课建议 30–45 分钟，按反馈拆分。S1-07 较复杂，可分两次完成。
前置列表示必需依赖，不表示必须按日历顺序学习。

| ID | 课程与目标 | 前置 | 工程锚点 | 理解检查 |
|---|---|---|---|---|
| S1-01 | CPU/MCU/AP/SoC/DSP/NPU：区分角色与集成关系 | 无 | 标出眼镜运算、图像处理、常开控制 | AP、MCU、SoC 是否互斥？ |
| S1-02 | SRAM、DRAM/DDR、Flash、ROM：区分存储用途与易失性 | S1-01 | 固件、运行数据、图像 Buffer 存放位置 | 断电后哪些内容需恢复？ |
| S1-03 | 地址空间与 Memory Mapping：理解地址的上下文 | S1-02 | RAM、控制器寄存器与 Sensor 寄存器 | 相同数值的地址是否同一对象？ |
| S1-04 | 寄存器与 MMIO：说明 CPU 控制硬件的机制 | S1-03 | SoC 寄存器与外部 Sensor 寄存器访问 | 两类写寄存器有何不同？ |
| S1-05 | 控制器、片上互联与外部总线：建立请求链 | S1-04 | 一次 Chip ID 读取，不深入完整波形 | CPU 与控制器分别做什么？ |
| S1-06 | 中断与轮询：理解事件通知与处理上下文 | S1-04 | 帧完成到软件处理 | 状态置位却无回调，检查哪些层？ |
| S1-07 | DMA、Cache、MMU/IOMMU 入门：建立 Buffer 使用条件 | S1-02、S1-03、S1-06 | 接收端写内存、CPU 接管与读取 | DMA 完成后数据为何仍可能异常？ |
| S1-08 | Boot、Firmware、异构执行概览：整合运行前提 | S1-01～S1-07 | MCU 访问不可用 DDR 的模拟问题 | 执行代码与访问数据依赖什么？ |

第一阶段验收：
1. 画 CPU → 驱动/控制器 → 外部总线 → Sensor 的读取逻辑链。
2. 画 Sensor → 接收/处理 → DMA → 内存 → 软件 Buffer 的数据链。
3. 对模拟故障列出事实、假设、实验及观测点。
4. 区分通用机制与特定平台的地址、API 和控制器行为。

阶段 1 的 Boot 与电源仅建立运行前提；详细启动时序在阶段 2/4 学习。

## 第二阶段：电源、时钟与硬件接口

| ID | 课程主题 | 前置 |
|---|---|---|
| S2-01 | 电压、电流、功率、纹波、压降；LDO/BUCK | S1-01 |
| S2-02 | Power Rail/Domain、PMIC/PMU、Camera 电源命名 | S2-01、S1-04 |
| S2-03 | 上电、复位、掉电顺序与可访问条件 | S2-02、S1-05 |
| S2-04 | Crystal/Oscillator/PLL、Clock Tree、MCLK 与门控 | S1-04、S2-01 |
| S2-05 | GPIO/PWM/ADC/DAC、输入输出、电平与测量基础 | S1-04、S2-01 |
| S2-06 | I2C：电气、事务、控制器、ACK/NACK 与错误 | S1-05、S2-05、S2-03、S2-04 |
| S2-07 | I3C：DAA/CCC/IBI、ENTDAA/SETDASA 与实现边界 | S2-06 |
| S2-08 | SPI/UART；CSI-2/DSI、USB/SDIO/PCIe 位置概览 | S1-05、S2-04、S2-05 |

验收：按实际器件资料画启动依赖；为 Chip ID 失败提出电源、复位、时钟、地址及事务验证实验。
案例入口：C01、C02、C03。案例均尚待创建，首次教学示例默认标明模拟。

## 第三阶段：智能穿戴子系统

| ID | 课程主题 | 前置 |
|---|---|---|
| S3-01 | CMOS Sensor、RAW/Bayer、曝光、增益与帧时序 | S2-03、S2-04、S2-06 |
| S3-02 | Sensor 控制与开流；寄存器配置和启动依赖 | S3-01、S2-07（I3C 平台） |
| S3-03 | CSI-2、物理层与接收配置；无 RAW 排查 | S3-02、S2-08 |
| S3-04 | ISP Pipeline、格式、Buffer、带宽与丢帧 | S3-03、S1-07 |
| S3-05 | Camera Driver/HAL/Framework、采集状态机 | S3-04、S1-06 |
| S3-06 | Mic/Codec/DSP、PDM/I2S/PCM/TDM 与采集播放 | S2-04、S2-05、S1-07 |
| S3-07 | ANC/ENC/AEC、同步、延迟与音频功耗 | S3-06 |
| S3-08 | BT Host/Controller、HCI、L2CAP、GATT、配对和 Profiles | S1-05、S2-08 |
| S3-09 | A2DP/HFP、LE Audio；软硬件 Codec 语义区分 | S3-06、S3-08 |
| S3-10 | Wi-Fi MAC/PHY、Host 接口、RF 基础与 BT 共存 | S3-08、S2-08 |

验收：跟踪一帧图像、一段音频及无线传输，标出数据、控制、时钟、存储与完成通知。
案例入口：C05、C06、C07、C08。音频和无线保留眼镜与 TWS 两套系统对照。

## 第四阶段：软硬件协同

| ID | 课程主题 | 前置 |
|---|---|---|
| S4-01 | Bootloader/BSP/Driver/HAL；固件执行和加载边界 | S1-08、S3-05 |
| S4-02 | RTOS/Linux/OpenHarmony 资源模型及设备描述 | S4-01 |
| S4-03 | 驱动初始化、MMIO、中断/DMA 的平台实现 | S4-02、S1-07 |
| S4-04 | IPC/Mailbox/Shared Memory、地址、一致性和协议 | S4-03 |
| S4-05 | AP/MCU 资源所有权、命令完成与超时恢复 | S4-04、S2-07（涉及 IBI 时） |
| S4-06 | Firmware 加载、升级、兼容性与失败回退 | S4-01、S4-05 |
| S4-07 | Runtime PM、Suspend/Resume、保留状态与恢复 | S4-05、S2-02～S2-04、S3-05 |

验收：设计一项 AP/MCU 协作事务，说明成功、超时、重复请求、处理器重启和外设掉电。
案例入口：C04、C09。公开平台 API 分开讲，不将 Linux 机制直接套到 RTOS 或厂商平台。

## 第五阶段：系统设计与工程实践

| ID | 课程主题 | 前置 |
|---|---|---|
| S5-01 | Datasheet/Reference Manual/Schematic 与 Bring-up 检查 | S2、S4 对应知识 |
| S5-02 | 日志、寄存器、波形、功耗与性能的时间关联 | S5-01、S1-06、S1-07 |
| S5-03 | 智能眼镜整机架构评审 | S3、S4 对应知识 |
| S5-04 | TWS 双耳、充电盒、音频同步与功耗评审 | S3-06～S3-10、S4-07 |
| S5-05 | AON Camera 与低功耗启动方案；完整硬件路径验证 | S5-03、S4-07 |
| S5-06 | Camera/音频/无线并发、资源预算与跨模块恢复 | S5-02～S5-05 |

验收：完成一个有条件、有预算、有替代方案、有证据要求的系统方案评审。
无器件或实测数据时标明假设，不虚构性能和能耗数字。

## 关键依赖链

- MMIO → 控制器 → I2C/I3C → Sensor 控制与 Chip ID。
- 地址空间 → DMA/Cache/映射 → Camera Buffer → 带宽与共享内存。
- 电源轨/电源域 + 时钟/复位 → 可访问条件 → 电源管理 → 休眠/恢复。
- 中断/事务完成 → IPC 协议 → 所有权与异常恢复 → 系统低功耗。
- 单子系统模型 → 多子系统资源争用 → 系统预算与架构权衡。

Bring-up 与故障分析贯穿所有阶段，并非到阶段 5 才开始。
