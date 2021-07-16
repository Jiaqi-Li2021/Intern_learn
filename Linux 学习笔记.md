# Linux 学习笔记

[TOC]

## 0. 计算机概论

![](_static/linux0.png)

电脑由几个单元组成：输入单元，输出单元，CPU 内部的控制单元，算术逻辑单元，内存 (main memory, RAM)。

### 0.1 电脑

**CPU 架构**

- 精简指令集 (RISC Reduced Instruction Set Computer)

  例如 SPARC，Power Architecture，ARM CPU

- 复杂指令集 (CISC Complex Instruction Set Computer)

  例如 AMD，Intel，VIA 等 x86 架构的 CPU

### 0.2 电脑架构

早期芯片通常分为两个**桥接器**来控制各元件的沟通

- **北桥**：负责连接速度较快的 CPU 、内存与显卡接口等元件。大多将北桥内存控制器整合到 CPU 封装中
- **南桥**：负责连接速度较慢的设备接口，包括硬盘、USB、网卡等

**CPU 的频率**表示每秒可以进行的工作次数，每次工作都可以进行少数的指令运行。由于每颗 CPU 的微指令集不同，所以不能单纯以 CPU 频率来判断运算性能

**前段总线** (Front Side Bud FSB)：内存控制芯片与内存间的传输

![](_static/linux0.2.png)

**内存** (DRAM) 根据技术的更新又分为好几代，使用较广泛的是 SDRAM 与 DDR SDRAM (Double Data Rate)

**第二层高速缓存** (L2 cache) 在 CPU 内部，由静态随即存取内存 (Static Random Access Memory SRAM) 组成，速度同 CPU 内部频率，DRAM 无法达到这个频率

**只读存储器** (Read Only Memory ROM) 非挥发性的内存

**显卡** (Video Graphics Array VGA) 图形影像的显示重点在于分辨率与色彩深度，显卡上内存用于图像显示，显卡嵌入 3D 加速的芯片用于 3D 运算，称为 GPU。常用插槽：PCI / PCIe。PCIe 数据传输的带宽远大于 PCI。PCIe 最多支持 16 信道，信道越多带宽越大。多信道卡（如 x8 的卡）也可安装在少信道插槽（如 x4 的插槽）中

**硬盘**常用接口：SATA / SAS (Serial Attached SCSI) / USB

**固态硬盘** (Solid State Disk SSD) 没有传统硬盘的磁头与盘片，

