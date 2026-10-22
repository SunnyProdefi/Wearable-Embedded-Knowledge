# S2-07：I3C、动态地址、CCC 与 IBI

## 课程信息与目标

- 日期：2026-10-22；前置：[S2-06 I2C](I2C.md)。
- 目标：区分动态地址分配方法、普通器件传输与事件通知，并把 Bus Busy 拆成可验证的状态问题。
- 范围：MIPI I3C/I3C Basic v1.1.1 的公开 FAQ v1.1（2022-08-22）及 Linux v6.8 软件概览；FAQ 是说明材料，非完整规范，未逐条取得规范正文。
- 不提供真实地址、CCC 数值、HDR 波形或厂商命令。统一回答 [本轮清单](../Study_Pack_S1-08_S2.md)，状态见 [Progress](../Progress.md)。

## 1. I3C 增加了什么

I3C（Improved Inter-Integrated Circuit）在软件视角引入发现/地址管理、公共命令、带内通知等能力。不能把它理解成“仅提高 I2C 时钟”。
它按传输阶段使用不同电气行为，不能永久按 I2C 开漏模型解释，也不能把混用 I2C 器件当成无条件兼容；电平、时序、滤波、负载和控制器支持都需核对。
本课用 Controller/Target 术语；Linux v6.8 文档仍出现 master/slave，按角色对应理解。[Linux v6.8 I3C 概览](https://www.kernel.org/doc/html/v6.8/driver-api/i3c/protocol.html)

## 2. 静态地址、动态地址与身份不同

| 对象 | 用途 | 不等于什么 |
|---|---|---|
| Static Address | 目标可能具备的预先定义地址，可参与特定兼容或分配流程 | 不保证是当前 I3C 私有传输所用地址 |
| Dynamic Address | Controller 为当前总线管理分配的通信地址 | 不是器件内部寄存器编号或永久身份 |
| PID / BCR / DCR | 协议身份和能力相关字段，参与发现与描述 | 不能与厂商 Chip ID 寄存器值混为一谈 |

PID 在 MIPI 中为 Provisional ID；具体字段和可区分性按器件/规范核对，不凭一个缩写推断任意系统都能无冲突自动发现。
BCR/DCR 在所引 Linux 概览中分别展开为 Bus Characteristic Register、Device Characteristic Register，用于描述总线与设备能力，不是本课虚构的可直接解引用地址。
Controller 软件设备表、Target 当前地址状态、实际总线事务三者必须一致；复位/掉电后不能直接相信旧地址缓存。

## 3. DAA 与两种分配方法

DAA（Dynamic Address Assignment）是动态地址分配过程。CCC（Common Command Code）用于总线公共管理，分为相应广播/直接命令；它与 Target 私有寄存器访问属于不同层次。

| 方法 | 核心作用 | 要确认的前提 |
|---|---|---|
| ENTDAA | 进入待分配目标的发现/仲裁与地址分配流程 | 目标支持该方式，身份可区分，Controller 管理合法可用地址 |
| SETDASA | 利用已知静态地址，为支持它且尚未分配动态地址的目标设置动态地址 | 静态地址已知且可唯一定位，目标支持，动态地址合法且不冲突 |

并非所有 Target 都必须走 ENTDAA，也不能给任意器件无条件使用 SETDASA。这里的支持与条件限定来自 v1.1.1 公开 FAQ；不能跨规范版本自行推定。
SETDASA 不应被当作任意修改已有动态地址的通用命令。[MIPI v1.1.1 FAQ，地址分配章节](https://www.mipi.org/hubfs/FAQs/mipi-I3C-v1-1-1-and-I3C-Basic-v1-1-1-FAQ-v1.1-Public.pdf)

一种教学初始化关系，不是通用命令脚本：确认供电/总线条件 → 按目标能力选择分配方式 → 建立设备身份/地址表 → 配置所需事件 → 执行器件功能访问。
哪些命令、重置和等待需要出现，取决于控制器、目标及当前总线状态。

## 4. IBI 是事件到来，不自动等于厂商任务完成

IBI（In-Band Interrupt）允许 Target 通过同一总线发起通知请求，受协议仲裁、Controller 接收能力与事件配置等条件约束；不是在总线忙时任意抢占当前数据。
通知可能含器件定义的数据，软件仍须核对来源、事件类型、请求代次及错误状态。
Linux I3C 将发现、地址、事件能力组织到软件接口中；具体 Controller 驱动的 IBI 队列、处理上下文及可用性需看目标实现。[Linux I3C 事件概览](https://www.kernel.org/doc/html/v6.8/driver-api/i3c/protocol.html)

厂商 HostCmd、固件邮箱、完成包或寄存器协议不是仅凭名称就能套用的标准 CCC。IBI 到达可以只是“有事件/数据待读”，不能在没有厂商契约时解释为拍照完成。
AP/MCU 谁拥有 Controller、谁处理 IBI、谁向另一核转发，必须在平台架构中明确。

## 5. Bus Busy 至少先分四层

| 层次 | 要问什么 | 证据 |
|---|---|---|
| 软件 | 队列或锁是否被占用，是否在等待旧请求 | 请求/锁/超时与队列记录 |
| 控制器 | FSM、命令队列或错误恢复是否未结束 | 安全的状态快照和最近操作 |
| 电气/连接 | 正确测点的线状态及边沿是否符合预期 | 波形、供电、复位和引脚配置 |
| 协议 | 是否已满足该事件所需总线状态和时序 | 事务起止、事件类型、对应版本的规则 |

MIPI 的 Bus Free、Bus Available、Bus Idle 是有不同条件的协议状态，不能仅凭一次采样“两根线都是高”就当作满足全部状态。此处不引用其数值时限，也不将某控制器 BUSY 位直接等同于其中任一状态。
详细条件与电气能力按规范版本/手册核对。[MIPI FAQ，总线状态章节](https://www.mipi.org/hubfs/FAQs/mipi-I3C-v1-1-1-and-I3C-Basic-v1-1-1-FAQ-v1.1-Public.pdf)

## 6. 模拟问题：Target 重启后旧动态地址不再应答

类型：模拟，无已确认根因。先确认复位范围、动态地址是否保留、Controller 表是否陈旧、目标是否重新具备通信条件，以及其他设备/请求是否仍占用资源。
关联重启代次、地址分配记录、目标身份和实际访问地址；按支持方式恢复地址管理和事件，不盲目重复 SETDASA 或 ENTDAA，不在其他所有者活动时直接清空全总线状态。
若地址正确再查功能就绪和私有命令；没有应答不直接等于 Sensor 损坏。

## 理解检查

1. ENTDAA 与 SETDASA 分别解决什么？为什么选择方式前必须核对目标能力、已有地址状态和已知静态地址条件？
2. IBI 已收到却没有拍照完成、或控制器报告 Bus Busy，你如何区分事件语义、软件/控制器状态与真实总线条件？

## 关联资料

[前课 S2-06](I2C.md) · [下一课 S2-08](SPI_UART.md) · [来源 S40](../Sources.md#s40-mipi-i3c-公开-faq-v111)、[S41](../Sources.md#s41-linux-v68-i3c-软件概览)。本课不声称核对过完整规范条款。
