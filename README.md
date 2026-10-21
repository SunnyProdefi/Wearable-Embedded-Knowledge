# Wearable Embedded Knowledge

智能穿戴底层软硬件知识体系，面向 Camera 底层软件工程师，重点覆盖智能眼镜，并与 TWS 耳机架构对照。

目标：从局部 Camera 软件开发，扩展到整机软硬件理解、联调、故障分析与架构设计。

## 当前状态

- 2026-10-14：用户确认初始化方案，完成基础目录与导航。
- 第一阶段 [S1-01](02_Processor_Memory/Processor_Roles.md)、[S1-02](02_Processor_Memory/Memory_and_Address_Spaces.md)、[S1-03](02_Processor_Memory/Address_Spaces_and_Mapping.md)、[S1-04](02_Processor_Memory/Registers_and_MMIO.md)、[S1-05](02_Processor_Memory/Controllers_and_Buses.md)、[S1-06](02_Processor_Memory/Interrupts_and_Polling.md)、[S1-07](02_Processor_Memory/Cache_MMU_and_DMA_Mapping.md) 已建立，其余详细课程与独立工程案例随学习逐步补齐。
- 实际学习状态见 [Progress.md](Progress.md)，文档存在和阅读不等同于已掌握。
- 2026-10-15：按用户要求将现有知识库通过 GitHub 公开维护；本地 Markdown 仍是编辑入口。
- 公开仓库：[SunnyProdefi/Wearable-Embedded-Knowledge](https://github.com/SunnyProdefi/Wearable-Embedded-Knowledge)。

## 如何使用

可直接在 GitHub 浏览 Markdown、相对链接和 Mermaid 图，也可克隆到本地阅读与维护：

```sh
git clone https://github.com/SunnyProdefi/Wearable-Embedded-Knowledge.git
cd Wearable-Embedded-Knowledge
```

- 系统学习：说“开始 S1-01”或“继续第一阶段”；按前置依赖学习，结束做简短检查。
- 术语速查：直接问“PMIC 与 PMU 有什么区别？”；简答后关联已有知识。
- 工程分析：提供现象、平台、发生条件、已确认事实和观测结果；按假设与实验定位。
- 架构分析：提供可授权使用的框图或通用描述；分析接口、资源依赖、状态和权衡。

工作规范见 [AGENTS.md](AGENTS.md)。在 Codex 中继续使用时，建议打开本项目目录，使项目规则直接适用。

## 知识地图

所有模块共用结构、行为、软件交互、调试证据四个视角。

| 模块 | 核心问题 | 学习深度 |
|---|---|---|
| [01 系统架构](01_System_Architecture/README.md) | 模块在哪里，谁控制谁，依赖谁？ | 架构理解 |
| [02 处理器与存储](02_Processor_Memory/README.md) | 代码如何执行，地址、数据与事件如何流动？ | 深入 |
| [03 电源与时钟](03_Power_Clock/README.md) | 硬件何时可访问，启停如何协调？ | 深入 |
| [04 硬件接口](04_Hardware_Interfaces/README.md) | 软件请求如何转为引脚行为？ | 重点接口深入 |
| [05 Camera](05_Camera/README.md) | 从 Sensor 到应用，一帧如何产生和交付？ | 最深入 |
| [06 音频](06_Audio/README.md) | 拾音、处理、播放如何协作？ | 原理与架构 |
| [07 蓝牙与 Wi-Fi](07_Bluetooth_WiFi/README.md) | 协议、芯片连接和无线资源如何协作？ | 原理与架构 |
| [08 嵌入式软件](08_Embedded_Software/README.md) | 系统资源、固件与异构处理如何管理？ | 深入 |
| [09 调试与 Bring-up](09_Debugging_Bringup/README.md) | 用什么证据验证系统模型？ | 深入 |
| [10 工程案例](10_Engineering_Cases/README.md) | 如何从现象形成可验证的根因分析？ | 实践 |
| [11 系统设计](11_System_Design/README.md) | 如何划边界、做预算、选方案并恢复异常？ | 综合 |

眼镜主线：采集 → 处理 → 存储/传输 → 唤醒与功耗管理。
TWS 主线：拾音 → 音频处理 → 播放/无线同步 → 充电与待机。
每个主题回到完整系统中，训练架构阅读、软硬件关联与工程定位。

## Camera 学习优先级

先连接电源/时钟/复位、I2C/I3C 控制、CSI 接收、DMA/DDR/Cache、驱动状态机和 AP/MCU 低功耗协同。
初期建议约六成学习投入这些直接依赖，比例按实际反馈调整。
RF、PCB 和模拟电路以软件与集成约束为边界。

## 项目导航

| 文件 | 职责 |
|---|---|
| [Roadmap.md](Roadmap.md) | 五阶段课程、稳定 ID、前置依赖和验收 |
| [Progress.md](Progress.md) | 学习状态、检查证据、疑问与复习 |
| [Glossary.md](Glossary.md) | 首批术语与课程新增概念，共 65 个条目，含关联入口 |
| [Sources.md](Sources.md) | 公开来源、版本、查阅日期与适用边界 |
| [ChangeLog.md](ChangeLog.md) | 结构和知识的重要修订 |
| [课程模板](Templates/Lesson.md) | 正式知识点的编写骨架 |
| [案例模板](Templates/Engineering_Case.md) | 事实、假设、实验与定位证据 |
| [架构评审模板](Templates/Architecture_Review.md) | 边界、流、预算、权衡与恢复 |

## 知识与进度的区别

术语速查和系统课程共享知识条目。新增可靠知识先查重，再补主文档、索引及术语链接。
未验证信息标记待验证，闲聊和一次性信息不机械沉淀。

文档建设情况记录在导航与 ChangeLog；个人掌握情况只记在 Progress。
文档存在、阅读结束、答案已发送，都不能自动推出已掌握。

## 维护边界

2026-10-19 起，按用户授权，每次课程与学习进展更新完成后检查相关改动，并自动提交、推送到上述公开 GitHub 仓库；具体授权范围见 [AGENTS.md](AGENTS.md)。
内部资料留在用户授权范围，不擅自发往外部服务。
通用原理、平台实现、典型方案与假设分开标注。
规划中的文件名仅作主题说明；正文建立后才添加对应链接。
