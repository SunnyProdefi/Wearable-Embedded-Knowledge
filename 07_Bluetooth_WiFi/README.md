# Bluetooth 与 Wi-Fi

## 本模块目标

理解协议栈与无线芯片分工、Host 连接、音频/数据业务、共存及性能功耗边界。

- 深度：原理与架构；RF/天线侧重软件集成约束。
- 前置：控制器与接口基础；无线音频先了解采集播放。
- 课程位置：S3-08～S3-10；S5-04、S5-06。
- 状态：仅导航与主题规划；下列详细文档尚未创建。
- 学习掌握情况以 [Progress.md](../Progress.md) 为准。

## 主题与拟建文档

| 拟建文件 | 内容范围 | 建设状态 |
|---|---|---|
| `Bluetooth_Host_Controller_and_Profiles.md` | Classic/BLE、HCI/L2CAP/GATT/Profiles、配对与连接 | 待创建 |
| `Classic_and_LE_Audio.md` | A2DP/HFP、LE Audio/LC3 与眼镜/TWS 业务 | 待创建 |
| `WiFi_MAC_PHY_and_Host_Interfaces.md` | MAC/PHY、SDIO/PCIe/UART 等连接位置及数据路径 | 待创建 |
| `RF_Basics_Coexistence_and_Power.md` | RF/天线基础、BT/Wi-Fi 共存、吞吐/延迟/稳定性与功耗 | 待创建 |

文件名是规划，不是不存在正文的链接。正式编写后更新本导航。

## 软硬件关联重点

区分协议栈、Host 接口、Controller 固件、无线调度与射频环境；不把所有断续直接归为 RF。

## 工程问题入口

C07 音频断续、C08 Wi-Fi/BT 共存下降；先建立业务负载、时间关联和排除实验。

案例定义和建设状态见 [工程案例导航](../10_Engineering_Cases/README.md)。

## 理解检查方向

能区分 Host/Controller 与 AP/MCU 分类，并提出无线与本地播放问题的区分实验。

## 关联知识与资料

- [音频](../06_Audio/README.md)
- [Firmware 与 IPC](../08_Embedded_Software/README.md)
- [并发资源](../11_System_Design/README.md)
- [课程路线](../Roadmap.md)
- [术语速查](../Glossary.md)
- [公开资料索引](../Sources.md)
- 已核对的相关公开资料：[S06 Bluetooth SIG LE Audio](../Sources.md#s06-bluetooth-sig-le-audio)。详细实现仍按资料版本和平台核对。
