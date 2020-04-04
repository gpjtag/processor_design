# Processor Design - (1)
Some memo about processor design

## Introduction
处理器按照设计的目标，或者用途，可以简单的划分为：General Processor（偏重于软硬件生态）、Application Processor（偏重于功能优化和指令自定义）。

**通用处理器**
Intel的X86、X86_64、ARM Cortex、TI TMS320、MIPS、Sparc等。

**专用处理器**
比特币挖矿芯片（针对SHA计算）、Google TPU（针对矩阵乘加法）、Codec集成的DSP（针对滤波器）、nVIDIA显卡（针对多边形的浮点计算、通用浮点计算）、ARM/高通的NPU（针对图像的CNN）、各种通信控制器。

按照指令中Field的Encoding方式，可以分为：CISC、RISC

按照并行指令Encoding方式，可以分为：SIMD、MIMD（VLIW）

按照指令的执行式，可以分为：标量（单发射）、超标量（多发射）

按照数据存取方式：Acc-based（x86、8051）、Stack-based、LoadStore Register-based（ARM）

最常见的VLIW设备是GPU，不过最新的AMD和nVIDIA的显卡已经是SIMD风格了。而定制性比较好的是MIPS32/MIPS64和Cadence/Tensilica Xtensa。这两种处理器常见的实现是：RISC + SIMD + 标量/超标量 + 可扩展EU。

## RISC-V

RISC-V指令集相较于其它常见指令集的优势有这么几点：

- 指令集开放
- 无需授权
- 免费
- 基础工具链完整
    
劣势也很明显：

- 不同Vendor的实现都有自己的特色、导致兼容性问题
- 指令集容易出现碎片化
- 缺少稳定的软件生态
- 缺少编译器开发人员做持续优化

## Free?

需要说明的是RISC-V免费，并不代表RISC-V IP是免费的，这样导致一个问题。
如果我们面向产品开发，自行设计IP难度大、耗时长、收益少、高风险，
如果从Vendor买IP，因为现在还是蓝海，远未到洗牌的阶段，所以各家的IP都很难充分验证，
都或多或少的有bug……所以如果流片的量不是很大，或者利润不高，还是老老实实用ARM吧。


## RISC-V vs ARM?

在RISC-V的生态没有完全建立起来之前，直接的竞争对手应该是Xtensa，而不是ARM。
ARM现在的优势是稳定、稳定、稳定，可以直接用，重要的事说3遍:)

就目前的情况看，RISC-V的优势是可以自定义指令扩展，
调度效率会比挂外设或者协处理器的实现方式要好不少，
软件开发也相对友好，不需要频繁的切换工具链。

如果产品有一些自己的算法，想用指令扩展的方式来做，
RISC-V比较合适，这么一来就又回到了是造轮子，还是买IP的问题。
尽可能选一个合适的，扩展方式清晰的RISC-V IP吧，
最后不要忽略了Compiler，这个是和Processor一样重要的。









