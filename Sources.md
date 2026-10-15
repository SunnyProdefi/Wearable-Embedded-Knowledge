# 公开资料索引

## 记录规则

本文件记录已用于规划、课程和概念边界核对的公开资料。
查阅日期均为 2026-10-14。未引用公司内部资料，也未指定具体产品和芯片。
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
