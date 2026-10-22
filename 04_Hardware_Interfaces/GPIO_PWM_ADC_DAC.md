# S2-05：GPIO、PWM、ADC 与 DAC

## 课程信息与目标

- 日期：2026-10-22；前置：[MMIO](../02_Processor_Memory/Registers_and_MMIO.md)、[电气基础](../03_Power_Clock/Electrical_Basics_and_Regulators.md)。
- 目标：从软件参数判断引脚行为与测量含义，区分逻辑状态、物理电平、周期波形及模拟量转换。
- 通用机制与 Linux v6.8 例子；不指定实际引脚、电压阈值或转换器参数。学完统一回答 [本轮清单](../Study_Pack_S1-08_S2.md)，状态见 [Progress](../Progress.md)。

## 1. GPIO 值不是完整引脚配置

GPIO（General-Purpose Input/Output）可提供数字输入/输出。实际行为还取决于 pin mux（引脚复用）、方向、I/O 供电、上下拉、输出类型、驱动能力和外部负载。
当引脚已复用为 I2C 或时钟输出时，写 GPIO 数据位不保证它按 GPIO 驱动；输入悬空也不能假定读值稳定。

| 概念 | 含义 | 调试时应问 |
|---|---|---|
| Push-pull，推挽 | 主动驱动高、低电平 | 电平兼容、负载与两端是否冲突 |
| Open-drain，开漏 | 主动拉低，另一状态通常释放为高阻 | 由谁上拉、上拉到哪路电源、上升时间如何 |
| Pull-up/down | 给未被强驱动的网络提供偏置 | 内外部电阻、漏电、容限和掉电条件 |
| VIH/VIL | 接收端识别高/低的输入条件 | 必须查接收器与 I/O 电压，不能只看发送端“输出 1” |

逻辑 1 不代表所有芯片固定输出同一电压。开漏释放不等于输出级主动驱动高电平，也不保证没有上拉时实际为高。

## 2. Active-low：逻辑有效与物理电平

Linux GPIO descriptor 的逻辑接口会处理 active-low 属性：逻辑 1 表示有效，逻辑 0 表示无效。若该描述符配置为 active-low，则逻辑 1 对应物理低，逻辑 0 对应物理高。
因此“设置 reset=1”可能是在断言复位，不能仅凭数字判断已经释放。raw 接口与逻辑接口语义不同，不能混用。[Linux v6.8 GPIO consumer](https://www.kernel.org/doc/html/v6.8/driver-api/gpio/consumer.html)
外置 GPIO 扩展器经 I2C/SPI 访问时可能需要睡眠，相应操作不能直接放硬中断路径；先检查控制器与 API 上下文。

## 3. PWM 不是任意模拟电压

PWM（Pulse Width Modulation，脉宽调制）用周期 T 和有效时长 Ton 描述波形，`f=1/T`、占空比 `D=Ton/T`。还要说明有效极性和启停状态。
它可用于 LED、马达或其他接受脉冲控制的负载。理想波形经适当滤波并满足负载条件时，平均值与占空比有关；不能将任意 PWM 引脚直接视为高精度 DAC。
Linux PWM 对周期、占空比、极性和使能有状态接口；所选控制器能否准确实现以及调用是否睡眠依实际能力。[Linux v6.8 PWM](https://www.kernel.org/doc/html/v6.8/driver-api/pwm.html)

## 4. ADC 与 DAC：数字码不等于精度

ADC（Analog-to-Digital Converter）将模拟输入采样并量化为数字码；DAC（Digital-to-Analog Converter）按数字码产生模拟输出。
对理想 N 位转换器有 `2^N` 个数字码；在规定满量程模型下，量化步长约为 `满量程/2^N`。实际传输函数、偏置、增益和端点定义依器件，不能用位数替代准确度。

| 维度 | 要检查什么 |
|---|---|
| 参考与输入范围 | 参考电压、前端分压/放大、输入阻抗、是否超范围 |
| 采样 | 采样率、建立时间、带宽及抗混叠条件；并非采样越快就一定更准 |
| 误差 | 偏置、增益、非线性、噪声、温漂及校准 |
| 输出解释 | 原始码、符号、比例/偏移和单位，避免把 raw code 直接当伏特 |

ADI 对理想量化噪声的说明强调模型条件，不能把理想 N 位公式直接当实际系统性能。[ADI MT-001 Rev.A](https://www.analog.com/media/en/training-seminars/tutorials/MT-001.pdf)
Linux IIO 是 ADC/DAC/传感器等设备的一种接口组织方式，不定义所有芯片统一的原始码转换公式。[Linux v6.8 IIO 简介](https://raw.githubusercontent.com/torvalds/linux/v6.8/Documentation/driver-api/iio/intro.rst)
DAC 输出也不代表可直接驱动扬声器或大电流负载；缓冲、功放与模拟前端是另外的能力边界。

## 5. 模拟问题：软件显示 reset 已释放，引脚却仍为低

类型：模拟，无已确认根因。先核对“释放”在 API 中的逻辑含义、active-low 配置和引脚复用，再查输出类型、上拉、I/O 供电、外部驱动与测点。
日志、描述符配置和示波器共同关联；不直接将低电平判为引脚损坏。若为开漏，释放后仍低可能来自缺少上拉或其他器件拉低，需按板级连接验证。
候选修正是修正绑定/极性/复用或电气条件，而非盲目把所有逻辑值反转。

## 理解检查

1. active-low 的 Linux GPIO 逻辑接口写 1，物理引脚是什么状态？开漏“释放”为什么也不保证实际测到高？
2. 为什么 PWM 的占空比、ADC 的位数都不能直接当作精确模拟电压或测量精度？还应核对哪些条件？

## 关联资料

[前课 S2-04](../03_Power_Clock/Clock_Tree_and_Gating.md) · [下一课 S2-06](I2C.md) · [来源 S38](../Sources.md#s38-linux-gpio-pwm-与-iio)、[S43](../Sources.md#s43-adi-转换器理想量化模型)。
