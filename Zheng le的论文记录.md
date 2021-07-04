# Zheng le的论文记录

### Introduction

what is surveillance channels (SCs) and what is reference channels(RC)?



参考信道的目的：RC is introduced to collect the transmitted signal as a reference for passive detection.
The signal in the RC is regarded as a noisy template to implement an approximate matched filter.

RC不是必须要的，也可以根据received signal and the estimated channel states来解调出信号数据。

下面这句话怎么理解？
As the reflection of targets is usually small, it will cause strong interference for target detection and estimation.

what does delay-Doppler domain mean?

论文指出，通过对完整数据的实例分析，表明当频率间隔大于一定阈值时，凸优化方法可以准确地恢复频率。

### 系统描述