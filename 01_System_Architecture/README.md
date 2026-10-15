# 智能穿戴系统架构

## 本模块目标

能够识别模块、芯片边界与接口，沿数据/控制/供电/时钟关系推导启动、休眠、唤醒和软件分工。

- 深度：理解架构，作为所有课程的系统参照。
- 前置：无硬性前置；正式分析结合处理器角色、电源域与对应接口。
- 课程位置：S1-01；S5-03、S5-04。
- 状态：仅导航与主题规划；下列详细文档尚未创建。
- 学习掌握情况以 [Progress.md](../Progress.md) 为准。

## 主题与拟建文档

| 拟建文件 | 内容范围 | 建设状态 |
|---|---|---|
| `Smart_Glasses_Overview.md` | Camera、音频、无线、AP/AON 与可选显示的整体分工 | 待创建 |
| `TWS_Overview.md` | 蓝牙音频 SoC、DSP、Mic、播放、双耳、充电盒与检测 | 待创建 |
| `System_Flows_and_Dependencies.md` | 四类关系、资源所有权、启动/低功耗/恢复依赖 | 待创建 |

文件名是规划，不是不存在正文的链接。正式编写后更新本导航。

## 软硬件关联重点

从用户请求标出控制方、数据处理方、完成通知与可访问条件；芯片内功能块不等于独立芯片。

## 工程问题入口

C09 外设休眠后恢复失败；先识别缺失的资源依赖，不能仅归因于驱动。

案例定义和建设状态见 [工程案例导航](../10_Engineering_Cases/README.md)。

## 理解检查方向

能在框图上标出四类连接，说明 AP 与 AON MCU 的职责、所有权及唤醒条件。

## 关联知识与资料

- [处理器与存储](../02_Processor_Memory/README.md)
- [电源与时钟](../03_Power_Clock/README.md)
- [系统设计](../11_System_Design/README.md)
- [课程路线](../Roadmap.md)
- [S1-01：处理器角色与集成关系](../02_Processor_Memory/Processor_Roles.md)
- [术语速查](../Glossary.md)
- [公开资料索引](../Sources.md)




## 典型智能眼镜功能框图

用途：作为课程的全系统位置参照，不是具体产品原理图。
类型：典型教学方案的简化功能框图。假设带 Camera、无线、音频和独立 AON MCU。
[D] 数据；[C] 控制；[K] 时钟；[P] 供电。
DSP/NPU 为可选集成功能；独立 MCU 与 AP 的 SPI 连接只是本例选择。

```mermaid
flowchart TB
    BAT["电池与充电管理"] -->|"[P]" PMIC["PMIC / 稳压器"]
    PMIC -->|"[P] 主域供电"| SOC
    PMIC -->|"[P] AON 域供电"| MCU
    PMIC -->|"[P] AVDD / DVDD / I/O 电源"| SENSOR
    REF["晶体与振荡电路"] -->|"[K] 参考时钟"| SOC

    subgraph SOC["主处理 SoC：简化功能边界"]
        CPU["AP / CPU"]
        CTRL["I2C / I3C / GPIO 控制器"]
        CLK["时钟生成与分配"]
        RX["CSI-2 接收端"]
        ISP["ISP"]
        DMA["DMA / 内存写入通路"]
        PROC["DSP / NPU：可选"]
        CPU -->|"[C] 配置"| CTRL
        CPU -->|"[C] 配置"| RX
        RX -->|"[D] 图像流"| ISP
        ISP -->|"[D] 图像数据"| DMA
    end

    CTRL -->|"[C] I2C 或 I3C；GPIO 复位"| SENSOR["Camera Sensor"]
    CLK -->|"[K] MCLK"| SENSOR
    SENSOR -->|"[D] CSI-2；本例采用 D-PHY"| RX
    DMA -->|"[D] 经内存控制器"| DDR["DDR"]
    CPU <-->|"[D] 经内存控制器"| DDR
    PROC <-->|"[D] 经内存互联"| DDR
    FLASH["Flash / 启动存储"] <-->|"[D] 平台存储接口"| CPU
    MCU["AON MCU / 自有 SRAM"] <-->|"[C/D] 本例采用 SPI"| CPU
    INPUT["按键 / IMU"] -->|"[C/D] GPIO / I2C"| MCU
    MCU -->|"[C] 唤醒请求"| CPU
    MIC["数字 MEMS Mic"] -->|"[D/K] PDM 音频与时钟"| AUDIO["音频接口 / DSP"]
    AUDIO <-->|"[D] 内部数据通路"| CPU
    AUDIO -->|"[D/K] I2S"| DAC["DAC / 功放"]
    DAC -->|"模拟音频"| SPK["扬声器"]
    CPU <-->|"[D/C] Wi-Fi：SDIO；BT HCI：UART"| RADIO["Wi-Fi / BT 芯片"]
    RADIO <-->|"射频连接"| ANT["天线"]
```

边界与省略：
- SoC 内部连线表示功能关系，不是实际电路网表。
- 图中不展开 CPU 到其他处理模块、时钟、DMA 的配置关系。
- DDR、音频、无线、时钟源等模块的供电、时钟、复位连线为可读性省略；不代表它们无需这些资源。
- PDM/I2S 连接汇总数据与时钟关系，箭头不表示每根引脚的真实方向。
- 音频框为聚合功能，不规定其位于 SoC 内还是独立芯片；数字 Mic 在此不经模拟 ADC。
- CSI-2 与物理层不同；本例选择 D-PHY，不推定 lane、速率和时序。
- MCU 未连接图像接收通路；可唤醒 AP 不等于具备低功耗图像采集能力。
- 显示、光学、其他传感器及调试端口按产品任务补图。
- 真实电压、接口归属和启动顺序需核对目标芯片及板级资料。

公开参考：[MIPI CSI-2 介绍](https://www.mipi.org/specifications/csi-2)；范围记录见 [S04](../Sources.md#s04-mipi-csi-2-官方介绍)。

## 围绕框图学习

| 学习主题 | 回到框图的检查 |
|---|---|
| 寄存器与控制器 | CPU、SoC 控制器与 Sensor 寄存器分别在哪里？ |
| 电源、时钟、复位 | 哪些资源是寄存器访问和输出图像的前置？ |
| DMA 与内存 | 图像写入 DDR，谁接管 Buffer，如何完成通知？ |
| 低功耗 | 哪些模块关闭、保留，唤醒后哪些配置要重建？ |
| 系统设计 | 谁拥有外设，如何处理并发、超时和跨域恢复？ |

## TWS 对照架构规划

正式 TWS 框图尚未建立。后续以：
手机 ↔ 蓝牙音频 SoC/处理器 → DSP/音频接口 → DAC/功放 → Speaker，
Mic → 采集/处理，以及双耳同步、检测、充电盒和电源状态为主线。
DSP/Codec 的集成与分工按实际方案说明，不照搬眼镜 AP/DDR/Camera 架构。
