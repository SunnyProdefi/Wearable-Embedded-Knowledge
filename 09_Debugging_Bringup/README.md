# 硬件调试与 Bring-up

## 本模块目标

使用系统模型、资料和测量形成可复核证据，将软件时间线关联到硬件行为。

- 深度：深入，所有阶段贯穿。
- 前置：按问题涉及的模块补齐；不需要等待第五阶段才使用。
- 课程位置：所有课程的工程检查；S5-01、S5-02。
- 状态：仅导航与主题规划；下列详细文档尚未创建。
- 学习掌握情况以 [Progress.md](../Progress.md) 为准。

## 主题与拟建文档

| 拟建文件 | 内容范围 | 建设状态 |
|---|---|---|
| `Reading_Hardware_Documents.md` | Datasheet/Reference Manual/Schematic/Block Diagram 的职责与阅读 | 待创建 |
| `Instruments_and_Observation_Points.md` | 万用表/示波器/逻辑分析仪、测点、触发、采样及局限 | 待创建 |
| `Bringup_Checklist.md` | 供电/时钟/复位/Chip ID/事务/中断/数据链分层验证 | 待创建 |
| `Correlating_Logs_Registers_and_Signals.md` | Boot、DMA、内存、功耗、性能与统一事件时间线 | 待创建 |

文件名是规划，不是不存在正文的链接。正式编写后更新本导航。

## 软硬件关联重点

每个软件成功条件配一个硬件或状态观测；错误码、时间戳、测点和采样条件保留语境。

## 工程问题入口

所有 C01～C09；本模块提供方法，案例保存具体事实和实验。

案例定义和建设状态见 [工程案例导航](../10_Engineering_Cases/README.md)。

## 理解检查方向

能为一个假设设计控制变量实验，并说明支持结果、排除结果和证据局限。

## 关联知识与资料

- [供电与时钟](../03_Power_Clock/README.md)
- [总线](../04_Hardware_Interfaces/README.md)
- [工程案例](../10_Engineering_Cases/README.md)
- [课程路线](../Roadmap.md)
- [术语速查](../Glossary.md)
- [公开资料索引](../Sources.md)
