# 电源与时钟系统

## 本模块目标

理解电源、时钟、复位与状态依赖，将软件资源管理关联到引脚和电源域的实际条件。

- 深度：深入，直接服务 Sensor 启停和整机低功耗。
- 前置：S1-04；电压/电流知识在本模块补齐。
- 课程位置：S2-01～S2-04；S4-07；S5-05。
- 状态：S2-01～S2-04 正文已建立，列入 [本轮连贯阅读](../Study_Pack_S1-08_S2.md)；休眠保留详细内容仍为规划。
- 学习掌握情况以 [Progress.md](../Progress.md) 为准。

## 主题与拟建文档

| 拟建文件 | 内容范围 | 建设状态 |
|---|---|---|
| [Electrical_Basics_and_Regulators.md](Electrical_Basics_and_Regulators.md) | S2-01：电压/电流/功率/能量/纹波/压降，LDO/BUCK/DC-DC | 正文已建立 |
| [Power_Rails_and_Domains.md](Power_Rails_and_Domains.md) | S2-02：PMIC/PMU、电源轨与域、AVDD/DVDD/DOVDD/VDDIO | 正文已建立 |
| [Power_Reset_Sequences.md](Power_Reset_Sequences.md) | S2-03：上电、掉电、复位及可访问条件 | 正文已建立 |
| [Clock_Tree_and_Gating.md](Clock_Tree_and_Gating.md) | S2-04：Crystal/Oscillator/PLL、MCLK/PCLK、Clock/Power Gating | 正文已建立 |
| `Sleep_Wakeup_and_Retention.md` | Sleep/Standby/Deep Sleep 的平台语义、AON、保留与恢复 | 待创建 |

文件名是规划，不是不存在正文的链接。正式编写后更新本导航。

## 软硬件关联重点

驱动请求电源/时钟、配置复位并等待条件；API 返回和物理条件满足要分别验证。

## 工程问题入口

C01 Camera DVDD 未建立、C09 外设恢复失败；观测使能、输出电压、复位、时钟和状态。

案例定义和建设状态见 [工程案例导航](../10_Engineering_Cases/README.md)。

## 理解检查方向

能按器件资料画出启动依赖，并解释电源轨、电源域和驱动状态为何不同。

## 关联知识与资料

- [硬件接口](../04_Hardware_Interfaces/README.md)
- [Camera](../05_Camera/README.md)
- [电源管理软件](../08_Embedded_Software/README.md)
- [课程路线](../Roadmap.md)
- [术语速查](../Glossary.md)
- [公开资料索引](../Sources.md)
- 已核对的相关公开资料：[S01 Camera 资源管理](../Sources.md#s01-linux-camera-sensor-驱动)、[S05 Zephyr PM](../Sources.md#s05-zephyr-设备电源管理)。详细实现仍按资料版本和平台核对。
