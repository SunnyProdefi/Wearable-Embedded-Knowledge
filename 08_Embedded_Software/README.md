# 嵌入式软件架构

## 本模块目标

明确 Boot/BSP/Driver/HAL/OS/Firmware 边界，设计资源所有权、IPC、初始化与异常恢复。

- 深度：深入，重点连接硬件资源与跨处理器协同。
- 前置：S1、至少一个阶段 3 完整子系统；具体依赖见 Roadmap。
- 课程位置：S4-01～S4-07。
- 状态：仅导航与主题规划；下列详细文档尚未创建。
- 学习掌握情况以 [Progress.md](../Progress.md) 为准。

## 主题与拟建文档

| 拟建文件 | 内容范围 | 建设状态 |
|---|---|---|
| `Bootloader_BSP_Driver_HAL.md` | 启动、板级支持、驱动和 HAL 的职责 | 待创建 |
| `OS_Resource_Models.md` | RTOS/Linux/HarmonyOS/OpenHarmony 的资源模型与差异 | 待创建 |
| `Device_Description_and_Initialization.md` | Device Tree 等设备描述、初始化、MMIO、IRQ 与 DMA | 待创建 |
| `IPC_Mailbox_and_Shared_Memory.md` | Mailbox、共享内存、同步、权限与地址 | 待创建 |
| `Firmware_Loading_and_Update.md` | 加载、执行位置、升级、兼容与回退 | 待创建 |
| `State_Machines_and_Recovery.md` | AP/MCU 所有权、命令超时、电源管理与恢复 | 待创建 |

文件名是规划，不是不存在正文的链接。正式编写后更新本导航。

## 软硬件关联重点

同一硬件机制在不同 OS 通过不同抽象管理；API 绑定版本，初始化顺序不代替实际完成条件。

## 工程问题入口

C04 不可用 DDR 访问、C09 恢复失败；追踪 IPC 和资源状态的跨处理器一致性。

案例定义和建设状态见 [工程案例导航](../10_Engineering_Cases/README.md)。

## 理解检查方向

能设计命令成功/超时/重启路径，说明谁访问外设、谁释放资源与如何判定恢复。

## 关联知识与资料

- [执行与存储](../02_Processor_Memory/README.md)
- [资源依赖](../03_Power_Clock/README.md)
- [所有权与恢复](../11_System_Design/README.md)
- [课程路线](../Roadmap.md)
- [术语速查](../Glossary.md)
- [公开资料索引](../Sources.md)
- 已核对的相关公开资料：[S01 Linux Camera PM](../Sources.md#s01-linux-camera-sensor-驱动)、[S05 Zephyr PM](../Sources.md#s05-zephyr-设备电源管理)。详细实现仍按资料版本和平台核对。
