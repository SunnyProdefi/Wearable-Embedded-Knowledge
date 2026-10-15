# 音频系统

## 本模块目标

识别拾音、处理、播放的硬件与软件分工，理解时钟、同步、延迟及功耗约束。

- 深度：理解原理与完整架构，按调试任务深入。
- 前置：S1-07、S2-04、S2-05；对应音频接口可同步学习。
- 课程位置：S3-06、S3-07、S3-09；S5-04。
- 状态：仅导航与主题规划；下列详细文档尚未创建。
- 学习掌握情况以 [Progress.md](../Progress.md) 为准。

## 主题与拟建文档

| 拟建文件 | 内容范围 | 建设状态 |
|---|---|---|
| `Mic_Codec_DSP_Speaker.md` | MEMS Mic、模拟/数字链路、ADC/DAC、DSP、功放与 Speaker | 待创建 |
| `Capture_and_Playback.md` | PDM/I2S/PCM/TDM、采集播放、Buffer 和时钟关系 | 待创建 |
| `ANC_ENC_AEC_Sync_and_Latency.md` | 降噪与回声处理目的、同步、延迟、功耗及眼镜/TWS 对照 | 待创建 |

文件名是规划，不是不存在正文的链接。正式编写后更新本导航。

## 软硬件关联重点

从音频任务、驱动、接口、DSP 和 Buffer 追踪采集与播放；硬件 Audio Codec 与压缩编解码器分开解释。

## 工程问题入口

C07 蓝牙音频断续；分辨无线到达、解码、Buffer、时钟、调度与播放问题。

案例定义和建设状态见 [工程案例导航](../10_Engineering_Cases/README.md)。

## 理解检查方向

能画一段语音的采集与播放路径，并标出时钟、缓冲和延迟来源。

## 关联知识与资料

- [音频接口](../04_Hardware_Interfaces/README.md)
- [无线音频](../07_Bluetooth_WiFi/README.md)
- [资源预算](../11_System_Design/README.md)
- [课程路线](../Roadmap.md)
- [术语速查](../Glossary.md)
- [公开资料索引](../Sources.md)
