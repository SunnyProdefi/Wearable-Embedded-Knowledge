# 系统设计与架构能力

## 本模块目标

结合眼镜与 TWS 全系统，设计模块边界、所有权、状态依赖和恢复，权衡功耗/性能/成本/复杂度。

- 深度：综合，围绕可验证的边界、预算和权衡。
- 前置：掌握所涉及子系统、资源管理与故障分析；并非必须先完成全部课程。
- 课程位置：S5-03～S5-06；S4-05、S4-07。
- 状态：仅导航与主题规划；下列详细文档尚未创建。
- 学习掌握情况以 [Progress.md](../Progress.md) 为准。

## 主题与拟建文档

| 拟建文件 | 内容范围 | 建设状态 |
|---|---|---|
| `Smart_Glasses_Architecture_Review.md` | 眼镜完整系统分工与数据/控制/电源/时钟 | 待创建 |
| `TWS_Architecture_Review.md` | 耳机、双耳、充电盒及音频无线协同 | 待创建 |
| `Low_Power_Camera_Startup.md` | AON Camera、采集完整路径、触发与唤醒延迟 | 待创建 |
| `AP_MCU_Ownership_and_Recovery.md` | 接口、资源归属、重启、超时和恢复 | 待创建 |
| `Resource_Budgets_and_Tradeoffs.md` | Camera/音频/无线并发，内存/带宽/功耗/延迟预算 | 待创建 |

文件名是规划，不是不存在正文的链接。正式编写后更新本导航。

## 软硬件关联重点

从需求到状态机和资源预算，再到可观察完成判据；典型方案写明条件，实测不足时保留假设。

## 工程问题入口

整合 C01/C04/C07/C08/C09，分析局部修复是否破坏其他模块状态或整机预算。

案例定义和建设状态见 [工程案例导航](../10_Engineering_Cases/README.md)。

## 理解检查方向

能比较有意义的备选方案，说明收益、代价、适用条件以及验证计划。

## 关联知识与资料

- [系统架构](../01_System_Architecture/README.md)
- [协同机制](../08_Embedded_Software/README.md)
- [验证方法](../09_Debugging_Bringup/README.md)
- [课程路线](../Roadmap.md)
- [术语速查](../Glossary.md)
- [公开资料索引](../Sources.md)



## 设计评审入口

使用 [架构评审模板](../Templates/Architecture_Review.md)。
方案记录适用条件、资源所有权、启动/休眠/唤醒/恢复、资源预算、备选方案与验证要求。
缺少产品参数时使用明确假设；不虚构功耗、吞吐、延迟或硬件能力。
