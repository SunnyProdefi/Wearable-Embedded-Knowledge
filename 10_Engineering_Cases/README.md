# 真实工程问题与模拟案例

## 本模块目标

从现象建立系统模型，分离事实、假设和待验证项，再用实验形成有边界的结论。

- 深度：以证据驱动分析，贯穿课程。
- 前置：按案例涉及原理动态补齐。
- 课程位置：所有阶段；案例 ID 不是课程掌握状态。
- 状态：仅导航与主题规划；下列详细文档尚未创建。
- 学习掌握情况以 [Progress.md](../Progress.md) 为准。

## 主题与拟建文档

| 拟建文件 | 内容范围 | 建设状态 |
|---|---|---|
| `C01_Camera_DVDD_Failure.md` | Camera DVDD 上电失败 | 待创建 |
| `C02_I3C_Bus_Busy.md` | I3C Bus Busy | 待创建 |
| `C03_Sensor_Chip_ID_Failure.md` | I2C/I3C 读取 Sensor Chip ID 失败 | 待创建 |
| `C04_MCU_DDR_Unavailable.md` | MCU 访问不可用 DDR | 待创建 |
| `C05_Sensor_No_CSI_Data.md` | Sensor 上电但没有 CSI 数据 | 待创建 |
| `C06_Camera_Image_Corruption.md` | 出图异常、格式或 Buffer 问题 | 待创建 |
| `C07_Bluetooth_Audio_Dropouts.md` | 蓝牙音频断续 | 待创建 |
| `C08_WiFi_BT_Coexistence.md` | Wi-Fi 与 BT 共存性能下降 | 待创建 |
| `C09_Peripheral_Resume_Failure.md` | 休眠后外设无法恢复 | 待创建 |

文件名是规划，不是不存在正文的链接。正式编写后更新本导航。

## 软硬件关联重点

案例写出控制链、数据链、完成通知和资源依赖，再逐一实验；不以 API 成功推定物理条件。

## 工程问题入口

当前没有已完成案例。上述名称只规划入口，全部尚待创建，不能声称来自真实产品。

初次教学示例标明模拟；真实公开案例附资料，用户实际案例附授权范围内的证据。

## 理解检查方向

能区分现象、根因候选和已验证根因；提出至少一个可排除主要假设的实验。

## 关联知识与资料

- [调试方法](../09_Debugging_Bringup/README.md)
- [Camera](../05_Camera/README.md)
- [系统方案](../11_System_Design/README.md)
- [课程路线](../Roadmap.md)
- [术语速查](../Glossary.md)
- [公开资料索引](../Sources.md)


## 案例编写与证据规则

使用 [工程案例模板](../Templates/Engineering_Case.md)。
结构：现象 → 系统背景 → 相关原理 → 可能原因 → 验证方法 → 定位过程 → 解决方案 → 经验总结。
每篇列案例类型、调查状态、已知事实、未知条件、假设排序、控制变量、观测点和实测结果。
模拟结果不得包装成真实测量；缺少证据时不宣布根因或修复验证通过。
