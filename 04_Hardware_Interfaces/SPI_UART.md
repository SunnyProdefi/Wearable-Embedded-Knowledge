# S2-08：SPI、UART 与高速接口的系统位置

## 课程信息与目标

- 日期：2026-10-22；前置：[控制器与总线](../02_Processor_Memory/Controllers_and_Buses.md)、[时钟](../03_Power_Clock/Clock_Tree_and_Gating.md)、[GPIO](GPIO_PWM_ADC_DAC.md)。
- 目标：按控制、数据、时钟和协议层次识别接口，解释“链路上有数据”为什么不等于设备功能完成。
- 范围：SPI/UART 基本机制、Linux v6.8 分层与其他接口位置概览；不展开高速 PHY、布线或标准版本性能参数。
- 这是本轮最后一课，之后可统一回答 [18 题清单](../Study_Pack_S1-08_S2.md)；状态见 [Progress](../Progress.md)。

## 1. SPI：时钟和片选把字节送到目标

SPI（Serial Peripheral Interface）是常见同步串行接口，典型线包括 SCK、片选 CS、控制器输出/输入数据线（常见名称 MOSI/MISO，亦有其他命名）。半双工、多线等变体按器件核对。
Controller 提供时钟并组织片选及传输；两端要匹配模式、位序、字宽、最大允许速率和片选要求。

| 参数 | 回答什么问题 |
|---|---|
| CPOL，Clock Polarity，时钟极性 | 空闲时钟电平是什么 |
| CPHA，Clock Phase，时钟相位 | 相对于规定边沿，在什么时机采样/移位 |
| CS 极性与保持 | 哪个目标被选中，一组命令是否要求连续片选 |
| 位序/字宽 | 字节或字的位如何解释 |

不能只凭模式编号口头判断采样边沿，按双方时序图核对。读操作也需要控制器提供时钟，发送的占位或命令内容依目标协议。
SPI 没有可无条件套用的 I2C 地址 ACK 机制；电气层收发了字节，不证明目标解析成功。[Linux v6.8 SPI 概览](https://www.kernel.org/doc/html/v6.8/spi/spi-summary.html)
智能眼镜 AP/MCU 可能用 SPI 传消息，但帧格式、长度、校验、重试和请求完成语义属于约定的上层协议。

## 2. UART：两端按约定时间解释异步串行位

UART（Universal Asynchronous Receiver/Transmitter）以约定波特率和帧格式收发数据。常见异步连接使用 TX/RX，另可有 RTS/CTS 流控；需要正确连接、参考地、电平和两端配置。
双方独立时钟决定采样，须匹配数据位、校验和停止位等。UART TTL/CMOS 电平与 RS-232 等电气标准不是同义词，不能只凭接口名字连接。
FIFO、DMA 或中断可帮助传输，但上层还要处理分包、超时、缓冲、流控和错误。写接口返回可能仅表示送入软件/硬件队列，要按具体 API 判断是否真正发完。
Linux serial core 与底层 UART 驱动分工，不把某个控制器寄存器行为推广到所有 UART。[Linux v6.8 Serial API](https://www.kernel.org/doc/html/v6.8/driver-api/serial/driver.html)

## 3. 放回智能眼镜/TWS 全系统

以下为典型用途，不是目标板接口清单：

| 接口 | 典型位置 | 不能混淆的层次 |
|---|---|---|
| I2C/I3C | Sensor/小外设控制及部分事件 | 寄存器控制与图像流不是同一路 |
| SPI | MCU、存储或外设数据/命令 | 位传输与私有消息协议 |
| UART | 调试、模块控制，某些 BT HCI 传输 | UART 是传输，HCI 是另一个协议层 |
| CSI-2 | Sensor 到接收端的图像数据 | CSI-2 协议与 D-PHY/C-PHY 等物理层 |
| DSI | 主处理/显示控制到显示设备 | 显示接口不是把 Camera 线倒接即可使用 |
| USB | Host 与设备的数据和控制 | 角色、枚举、端点/传输与设备功能 |
| SDIO | Host 与 I/O 功能，常见无线模块连接之一 | 不是仅指 SD 存储卡，也不自动等于 Wi-Fi 协议 |
| PCIe | Root/Endpoint 的高速互联 | 链路、枚举/资源、DMA 与设备服务是不同阶段 |

CSI-2 定位见 [MIPI CSI-2](https://www.mipi.org/specifications/csi-2)，DSI 定位见 [MIPI DSI](https://www.mipi.org/specifications/dsi)。未取得规范全文，不据介绍页推定 lane、速率、时序或具体芯片支持。
USB、SDIO、PCIe 的分层例子见 [Linux USB](https://www.kernel.org/doc/html/v6.8/driver-api/usb/usb.html)、[SD Association SDIO](https://www.sdcard.org/developers/sd-standard-overview/sdio-isdio/)、[Linux PCI](https://www.kernel.org/doc/html/v6.8/PCI/pci.html)。

## 4. 控制路径成功不等于数据路径成功

Camera 读 ID 成功后，还需完成模式配置、Sensor 输出、物理连接/接收配置、数据格式、Buffer 与通知交接；具体过程在第三阶段深入。
无线模块 UART 有日志，只证明该日志路径运行；不保证固件功能、HCI 协议、射频或音频链已经可用。
HCI（Host Controller Interface）是蓝牙 Host/Controller 间的接口层名称；UART 可承担其传输，不能将两者等同。
同一个名为 Controller 的模块可能属于 SPI、USB 或蓝牙协议内部不同层次，要先确认上下文，不凭名称画同一框图。

## 5. 模拟问题：SPI 波形存在，但 MCU 没返回有效结果

类型：模拟，无实测根因。先检查电平与选中目标，再对齐 CPOL/CPHA、字宽/位序、CS 边界；之后核对完整字节、长度、上层消息、固件就绪及完成返回契约。
观察原始发送/接收记录和时序，不因 MISO 全固定值就直接认定 MCU 损坏。若通信涉及共享 Buffer，还要回到 [S1-07](../02_Processor_Memory/Cache_MMU_and_DMA_Mapping.md) 的生命周期与同步条件。
修正只依据确认的分支，不能把切换模式或不断降速当作已定位原因。

## 理解检查

1. SPI 有时钟波形、UART 能输出日志，分别为什么仍不能证明目标命令已完成？你会检查哪些协议和配置边界？
2. Sensor ID 已读通但无图像，你如何区分控制接口、CSI-2/物理层、接收/内存通路和软件通知？DSI、USB、SDIO、PCIe 又分别位于什么类型的系统连接？

## 关联资料

[前课 S2-07](I3C.md) · [Camera 后续模块](../05_Camera/README.md) · [来源 S42](../Sources.md#s42-linux-spi-与-uart)、[S44](../Sources.md#s44-高速接口的官方定位)。本轮不自动开始第三阶段，先按统一答题反馈更新进度。
