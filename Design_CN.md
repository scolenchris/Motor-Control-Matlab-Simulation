- [English Version](./Design_EN.md)
- **由于 GitHub 对 latex 糟糕的支持，请下载后使用 typora 查看**
- 为了更好的阅读体验，可以直接点击进入我的 blog 进行阅读（公式能够显示正常）
- [blog 文章链接](https://scolenchris.top/posts/69002990.html)

# 一、选题背景

电机控制系统广泛应用于工业、交通和家电等领域，随着科技进步，先进控制方法如矢量控制和直接转矩控制不断涌现，对系统设计提出了新要求，而电机控制的课程设计涉及自动控制、电子技术和计算机应用等多个学科，有助于学生将理论知识与实际应用相结合，提升综合运用知识的能力。在应用方面，电机控制系统在数控机床、机器人和电动汽车等现代工业自动化中占据重要地位，基于具体应用背景进行设计可以提高实用性和针对性。教育上，这是自动化专业的重要实践环节，通过课程设计，我们能够掌握基本原理和设计方法，培养动手能力和工程实践能力，还能引导我们学生初步接触科研工作，培养科研兴趣和能力。

## 目录

- [一、选题背景](#一选题背景)
  - [目录](#目录)
- [二、方案论证(设计理念)](#二方案论证设计理念)
  - [1.电机选型与相关参数计算](#1电机选型与相关参数计算)
    - [1.1 电机类型选择](#11-电机类型选择)
    - [1.2 电机详细参数计算](#12-电机详细参数计算)
    - [2.启动方案选择](#2启动方案选择)
    - [3.调速方案选择](#3调速方案选择)
    - [4.制动方案选择](#4制动方案选择)
    - [5.停车方案选择](#5停车方案选择)
    - [6.整体方案图](#6整体方案图)
- [三、过程论述](#三过程论述)
  - [1.整体任务前准备](#1整体任务前准备)
  - [2.仿真模块搭建与计算](#2仿真模块搭建与计算)
    - [2.1 能耗制动仿真初期模型搭建](#21-能耗制动仿真初期模型搭建)
    - [2.2 电枢电源反接制动仿真搭建](#22-电枢电源反接制动仿真搭建)
    - [2.3 转速反向的反接制动与停车仿真最终设计](#23-转速反向的反接制动与停车仿真最终设计)
  - [3.串电阻启动与调速仿真与计算](#3串电阻启动与调速仿真与计算)
  - [4.整体仿真设计](#4整体仿真设计)
- [四、结果分析](#四结果分析)
  - [1.仿真整体结果分析](#1仿真整体结果分析)
  - [2.分级启动环节分析](#2分级启动环节分析)
  - [3.调速过程分析](#3调速过程分析)
  - [4.制动与停车过程分析](#4制动与停车过程分析)
    - [4.1 转速方向的反接制动过程](#41-转速方向的反接制动过程)
    - [4.2 可靠停车过程](#42-可靠停车过程)

# 二、方案论证(设计理念)

## 1.电机选型与相关参数计算

### 1.1 电机类型选择

估算电枢回路电阻:

${R}_{a}=\left(\frac{1}{2}~\frac{2}{3}\right)\frac{{U}_{N}{I}_{N}-{P}_{N}}{{{I}_{N}}^{2}}=\frac{2}{3}\times \frac{220\times 22.3-4000}{{22.3}^{2}}=1.21\mathrm{\Omega}$

计算 CeФ_N:

$\mathrm{C}\mathrm{e}{\mathrm{\phi}}_{N}=\frac{{U}_{N}\mathrm\ -{I}_{N}{R}_{a}}{{n}_{N}}=\frac{220-1.21\times 22.3}{1500}=0.1286\mathrm\ \mathrm{V}/(\mathrm{r}\bullet {\mathrm{m}\mathrm{i}\mathrm{n}}^{-1})$

计算空载转速:

${n}_{0}=\frac{{U}_{N}}{\mathrm{C}\mathrm{e}{\mathrm{\phi}}_{N}}=\frac{220}{0.1286}=1710.73\mathrm\ \mathrm\ \mathrm{r}\bullet {\mathrm{m}\mathrm{i}\mathrm{n}}^{-1}$

计算额定转矩：

${T}_{N}=9.55\mathrm{C}\mathrm{e}{\mathrm{\phi}}_{N}{I}_{N}=9.55\times 0.1286\times 22.3=27.387\mathrm\ \mathrm{N}\bullet \mathrm{m}$

估算电枢电感：

${\mathrm{L}}_{\mathrm{a}}=19.1\times \frac{C{U}_{N}}{2P{n}_{N}{I}_{N}}=19.1\times \frac{0.4\times 220}{2\times 1\times 1500\times 22.3}=0.02512\mathrm\ \mathrm{H}$

估算励磁电流：
设 R\*f=20Ω 则

${I}*{f}=\frac{{U}_{f}}{{R}_{f}}=\frac{220}{20}=11\mathrm{A}$

估算电动势常数:

${K}_{E}=\frac{60}{2\pi}\times \mathrm{C}\mathrm{e}{\mathrm{\phi}}_{N}=0.1286\times \frac{60}{2\pi}=1.228$

估算电枢绕组和励磁绕组互感:

$\mathrm{L}\mathrm{a}\mathrm{f}=\frac{{K}_{E}}{{I}_{f}}=\frac{1.288}{11}=0.1116\mathrm\ \mathrm{H}$

在选择电机时，我们比较了他励直流电动机和三相异步电动机的工作特性。通过将二者的特性并绘制在同一坐标系中，可以看出，三相异步电机在 A3 处无法稳定运行，而他励直流电动机在力矩大于 Tl 后由于电枢反应的去磁作用产生了上翘的现象，且他励直流电机的补偿方式更为方便简洁。

**图 2.1 各类电机特性图**

![image](https://github.com/user-attachments/assets/2e812cbf-0272-4626-b8b4-a5887b67c942)

在选择具体类型的直流电机时，我们比较了各种励磁电机的机械特性。复励串励电动机的机械特性曲线较软，不易于计算。本设计任务中需要反向下放物体，可能需要反接制动，而反接制动会导致并励发电机的励磁方向发生改变，最终导致电机转动方向未发生改变。
因此，最终选择了他励直流发电机。

### 1.2 电机详细参数计算

转矩：

${T}_{F}=\mathrm{m}\mathrm{g}\cdot \mathrm{r}=1010\times 10\times \frac{0.2}{4}=2020\mathrm{N}\cdot \mathrm{m}$

减速比：

${n}_{\mathrm{turn}}=\mathrm\ \frac{{n}_{max}}{100}=\frac{1500}{100}=15\mathrm{r}/\mathrm{m}\mathrm{i}\mathrm{n}$

输出功率：

${P}_{{F}_{max}}={T}_{F}\cdot {\mathrm{\Omega}}_{max}=2020\times \frac{2\pi \times 15}{60}=3.173\mathrm{k}\mathrm{w}$

故最小额定功率:

$P_{N} = \frac{P_{F_{\text{max}}}}{\text{ŋ}} = \frac{3.173}{0.9} = 3.526\, \mathrm{kW}$

对应电磁转矩：

${T}_{N}=\frac{{P}_{N}}{\frac{2\pi n}{60}}=\frac{3526}{\frac{2\pi \times 1500}{60}}=22.447\mathrm{N}\cdot \mathrm{m}$

根据需求：空勾重量为 10 公斤，最大载重为 1000 公斤。传动机构的减速比为 100:1，传动效率为 0.9；飞轮惯量可以忽略不计。提升重物的最高转速为 1500 转/分钟，下放重物的最低转速为 300 转/分钟。提升/下降的高度为 25 米，卷筒的直径为 0.4 米。
组内成员计算可得出，计算过程略：
应选取 n>1500r/min,额定功率 P_N>3.526kw 的电机，同时保证输出功率 P_N·ŋ>3.173kw。
经过查阅资料，选择了 Z2-42 的电机，电机额定参数为：
额定功率 PN:4kW，额定电压 UN=220V ，额定转速 nN=1500r/min，额定电流 IN=22.3 A。

**图 2.2 仿真电机模块参数设置**

![image](https://github.com/user-attachments/assets/b222fbf3-3f75-403e-9262-f57e01cb76e3)

然后对电机参数估算得到电感，励磁电流等参数，将其填入 simulink 电机的参数设置中，如右上图，之后的仿真都以这个参数为基准进行。

### 2.启动方案选择

在启动方案的选择过程中，我们最终决定采用多级串电阻启动方式。此选择主要基于以下几个方面的考虑：首先，仿真电路的搭建相对复杂，但操作简单且可靠性高；其次，多级调速能力得到了充分的体现。基于这些优点，我们最终选择了串电阻启动方式。

### 3.调速方案选择

调速方案选择串电阻调速，对于直流电动机的调速方式，由于本设计中的吊重物为位能性负载，选择在前两者中调速。同时，制动方案采用反接制动，需要串入大电阻，因此调速方案选用串电阻调速，电路实现的过程比较统一，容易发现问题。

### 4.制动方案选择

在调速方案的选择中，我们决定采用串电阻调速方式。对于直流电动机的调速方式，由于本设计中的吊重物为位能性负载，我们选择在前两者中进行调速。同时，制动方案采用反接制动，需要串入大电阻，因此调速方案选用串电阻调速。这种方式不仅使电路实现过程更加统一，还便于发现和解决问题，提高了系统的可靠性和可维护性。

### 5.停车方案选择

停车方案选择切除部分电阻实现停车，在转速反向的制动过程中短路部分电阻，让转速下降为 0。

### 6.整体方案图

**图 2.3 整体方案图**

![image](https://github.com/user-attachments/assets/f8cd707e-15cb-42e0-8109-ec39a4838aec)

# 三、过程论述

## 1.整体任务前准备

作为组长，先根据我收集到的材料（各类书籍和论文），给组员们布置仿真练手任务，熟悉各个模块的功能，便于解决问题，我选用了几本书的例子，有些是关于调速的，有启动的，还有闭环调速的，内容比较多样，途中出现的问题也让大家说出来，然后一块解决了；接下来，我开始分配具体任务，每个组员根据自己的兴趣和擅长的领域选择一个模块进行深入研究。为了确保每个人都能充分理解并掌握所负责的模块，我先让大家先各自进行初步的仿真操作，然后在进行细调，有问题在群里提出来。
下面则是我们模拟的各个部分图片。

**图 3.1 开环三相调速系统仿真**

![image](https://github.com/user-attachments/assets/d198e9bd-54ee-43ff-8834-a9c523a37cb1)

**图 3.2 仿真波形**

![image](https://github.com/user-attachments/assets/ca1977e5-ff91-4d05-b60f-1b0aaddb2abb)

**图 3.3 闭环三相调速系统仿真 1**

![image](https://github.com/user-attachments/assets/1e253db7-7c21-4ac4-93a1-5ca542afd454)

**图 3.4 闭环三相调速系统仿真 2**

![image](https://github.com/user-attachments/assets/206cbe0b-20e7-49dd-b743-85f795566253)

## 2.仿真模块搭建与计算

### 2.1 能耗制动仿真初期模型搭建

当能耗制动发生时，电源被切断，制动电阻被接入电路。此时，由于电动机的惯性，电动机继续旋转，并转变为发电机。电枢电流的方向与原来的电流方向相反，电枢产生制动转矩，以抵抗由于惯性所产生的力矩，从而使电动机迅速停止旋转。通过调整制动电阻 R 的阻值，可以调节制动时间。制动电阻 R 的阻值越小，制动过程越迅速；而 R 的阻值越大，制动时间则越长。使用 simulink 完成对上述过程的仿真。
对整体系统进行计算，计算出能耗制动电阻的阻值和最小电阻值（避免电流过大），计算过程如下：

$\mathrm{n}=-\frac{{\mathrm{R}}_{\mathrm{a}}+{\mathrm{R}}_{\mathrm{c}}}{{\mathrm{C}}_{\mathrm{e}}{\mathrm{C}}_{\mathrm{T}}{\mathrm{\phi}}^{2}}$

$\begin{array}{c}{\mathrm{C}}_{\mathrm{e}}\phi=\frac{{U}_{N}-{I}_{N}{R}_{a}}{{n}_{N}}=\frac{220-121\times 22.3}{1500}=0.1286V/r\cdot{min}^{-1}\#\left(\text{3-2}\right)\end{array}$

$\begin{array}{c}n=-\frac{{\mathrm{R}}_{\mathrm{a}}+{\mathrm{R}}_{\mathrm{\Omega}}}{{\mathrm{C}}_{\mathrm{e}}\mathrm{\phi}}{\mathrm{I}}_{\mathrm{N}}=-300r/min\#\left(\text{3-3}\right)\end{array}$

$\begin{array}{c}\therefore {{\mathrm{R}}_{\mathrm{a}}=1.21\mathrm{\Omega},\mathrm{I}}_{\mathrm{N}}=22.3A\#\left(\text{3-4}\right)\end{array}$

$\begin{array}{c}we get:{R}_{\mathrm{\Omega}}=0.52\Omega \#\left(\text{3-5}\right)\end{array}$

$\begin{array}{c}{R}_{\mathrm{\Omega}\mathrm{m}\mathrm{i}\mathrm{n}}=\frac{{E}_{a}}{{I}_{amax}}-{R}_{a}\#\left(\text{3-6}\right)\end{array}$

$\begin{array}{c}but {I}_{amax}=3{I}_{N}=66.9A\#\left(\text{3-7}\right)\end{array}$

$\begin{array}{c}{E}_{a}={\mathrm{C}}_{\mathrm{e}}{\mathrm{\phi}}_{\mathrm{N}}{\mathrm{n}}_{\mathrm{N}}=1000\times 0.1286=128.6V\#\left(\text{3-8}\right)\end{array}$

$\begin{array}{c}{\therefore R}_{\Omega min}=\frac{128.6}{66.9}-1.21=0.7122\Omega \#\left(\text{3-9}\right)\end{array}$

**图 3.5 串电阻启动电路仿真图**

![image](https://github.com/user-attachments/assets/7dae6de4-84e4-488c-9a1e-53a674c10b10)

首先，上图为串电阻启动的电路，串电阻的电路比较复杂，因此我对此进行了整合，将其作为子系统加入到模型当中，其启动详细原理略过，如下图所示。

**图 3.6 串电阻电路封装**

![image](https://github.com/user-attachments/assets/8c4b427b-8cac-43d3-8398-e421ffb99f98)

然后，对能耗制动系统进行仿真设计，设计为两阶段的制动过程。首先接入电阻 RΩ，随后接入电阻 RΩ1。并联后的电阻值将显著减小，从而实现制动停车，设置的 RΩ=0.575Ω，RΩ1=0.1Ω（尝试实现停车），对于 breaker 模块，当上升沿信号到来时，开关将闭合，接通电路；中间总开关下方的电阻设定为 10000Ω，作为接地电阻，以确保施加到电机的电压维持在 220V；电机输出信号会进入到 bus selector 模块，它能将总线信号分为多个信号并在示波器中显示，转速部分使用 gain 模块将转速单位转为 r/min。

**图 3.7 能耗制动仿真**

![image](https://github.com/user-attachments/assets/d74ad64a-6f2b-4a7b-a7c8-812249daff8c)

最终的转速波形如下，在 11s 时候进行能耗制动，转速降为-300r/min 左右并保持，在 20s 时候并联电阻，电阻进一步降低，但是无法接近 0 的转速，由于 Ra 的原因，斜率无法进一步降低，其特性曲线也就无法和 x 轴产生交点，因此无法到达停车的要求，为方案选择提供了依据。

**图 3.8 仿真图像——转速**

![image](https://github.com/user-attachments/assets/c4b78721-61f8-497a-a468-baeeb50e484f)

### 2.2 电枢电源反接制动仿真搭建

电枢电源反接制动的过程是先断开电动机的原电源，停止电动机的正常运行。然后，将电动机的电源极性反接，即将电源的正负极对调。此时电动机会产生一个与原来转动方向相反的电磁力矩，迅速减慢电动机的转速，直至停止，若负载较小，则可能会反向启动。
各类参数计算过程如下：

$\begin{array}{c}{P}_{N}=4kw,{U}_{N}=220V,{n}_{N}=1500r/min,{I}_{N}=22.3A\#\left(\text{3-10}\right)\end{array}$

$\begin{array}{c}{R}_{a}=4.24\Omega \#\left(\text{3-11}\right)\end{array}$

$\begin{array}{c}{n}_{a}=1000r/min{,E}_{a}={\mathrm{C}}_{\mathrm{e}}{\mathrm{\phi}}_{\mathrm{N}}{\mathrm{n}}_{\mathrm{a}}\#\left(\text{3-12}\right)\end{array}$

$\begin{array}{c}{\mathrm\ \mathrm{C}}_{\mathrm{e}}\phi=\frac{{U}_{N}-{I}_{N}{R}_{a}}{{n}_{N}}=0.1286V/r\cdot {min}^{-1}\#\end{array}$

$\begin{array}{c}\therefore {\mathrm{E}}_{\mathrm{a}}={\mathrm{C}}_{\mathrm{e}}{\mathrm{\phi}}_{\mathrm{N}}{\mathrm{n}}_{\mathrm{a}}=128.6V\#\left(\text{3-1}\text{3}\right)\end{array}$

$\begin{array}{c}{\mathrm{R}}_{\mathrm{b}\mathrm{m}\mathrm{i}\mathrm{n}}=\frac{-\mathrm{U}-{\mathrm{E}}_{\mathrm{a}}}{-{\mathrm{I}}_{\mathrm{a}\mathrm{m}\mathrm{a}\mathrm{x}}}-{\mathrm{R}}_{\mathrm{a}}=\frac{-220-128.6}{-3{\mathrm{I}}_{\mathrm{N}}}-1.21=(5.12-1.21)\Omega =4.00\Omega \#\left(\text{3-1}\text{4}\right)\end{array}$

下面展示的是我搭建的仿真电路。启动过程略过，反接制动过程发生在 9 秒时，此时启动开关关闭，而下方的电枢电源反接制动开关打开。这时，反向电压被接入电枢，导致电机快速进行反向制动。

**图 3.9 反接制动仿真**

![image](https://github.com/user-attachments/assets/4f1cacce-29e1-41db-a726-57c5c33d26cf)

最终仿真的效果不佳，如下图所示。最初，我将反接制动以串联的形式接入电枢回路，但实际上应为并联连接。在等效条件下，反接制动是串联的。因此，我对电路进行了修改，将其并联接入，并将计算所得的参数值代入仿真模型。然而，得出的图像显示反转速度过快，电流很大。
经过进一步查阅资料后发现，反接制动会导致电机反向运转速度迅速增加。尽管这种方法能够实现快速制动停车，但其电枢电流也会显著增大。这种高电流对电机及相关设备的负载较大，存在潜在的安全隐患和设备损耗问题，因此不适合在实际应用中部署，也为方案选择提供了依据。

**图 3.10 仿真图像——转速**

![image](https://github.com/user-attachments/assets/c0b8aa93-1a5c-43d2-9bf5-d6607a05c636)

**图 3.11 仿真图——电枢电流**

![image](https://github.com/user-attachments/assets/7c2ae02f-0cd5-49ec-8be4-1515ea30ba85)

### 2.3 转速反向的反接制动与停车仿真最终设计

**图 3.12 制动与停车模块封装**

![image](https://github.com/user-attachments/assets/ed5e3701-725a-4b44-9f3b-34eee4b9b290)

**图 3.13 调速模块封装**

![image](https://github.com/user-attachments/assets/70ed695f-f1cf-43b0-a8a2-4f2fef78ba3d)

将调速模块和停车模块整合后，并将各个部分封装为子系统后，系统界面和结构更加清晰。制动和停车模块通过转速反向的反接制动实现，代替先前的能耗制动。实践证明，这种设计比原来的并联设计更为优越，最终效果也非常理想。
上图将电阻分为了两个作为多级的制动，从反转情况转变为最低的转速反转转速，实现平稳刹车，然后再对电阻进行短路，实现停车，具体实现见结果分析。
在整合过程中，我们对各个模块进行了详细的分析和优化，将其封装为独立的子系统，不仅简化了整体设计的复杂度，还提高了系统的可维护性和扩展性。通过使用短路电阻替代原有的并联设计，我们有效地解决了此前存在的电流过大问题，提升了系统的稳定性和安全性。
在最后调节反接制动的电阻时，无法细调至 n=0，详细在小结阐述。

## 3.串电阻启动与调速仿真与计算

启动电流：

${I}_{st}=\frac{{U}_{N}}{{R}_{a}+{R}_{st}}=22.3\times 2\mathrm\ \mathrm{A}$

启动电阻：

${R}_{st}=\frac{220}{22.3\times 2}-1.21=3.723\mathrm{\Omega}$

总电阻：

${R}_{3}=\frac{{U}_{N}}{{I}_{1}}=\frac{220}{22.3\times 2}=4.933\mathrm{\Omega}$

$$ \beta = \sqrt[3]{\frac{R_3}{R_a}} = \sqrt[3]{\frac{4.933}{1.21}} = 1.597 $$

分段电阻为:

${R}_{st1}=\left(\mathrm{\beta}-1\right){R}_{a}=0.597\times 1.21=0.722\mathrm{\Omega}$

${R}_{st2}=\mathrm{\beta}\left(\mathrm{\beta}-1\right){R}_{a}=0.597\times 1.21\times 1.597=1.154\mathrm{\Omega}$

${R}_{st3}={\mathrm{\beta}}^{2}\left(\mathrm{\beta}-1\right){R}_{a}=0.597\times 1.21\times {1.597}^{2}=1.842\mathrm{\Omega}$

同时也可算出对应的调速电阻:

$n = \frac{U_N}{\phi C_e} - \frac{R_a + R_c}{(\phi C_e)^2 \times 9.55} \times 23$

${R}_{c}=3.38\mathrm{\Omega}$

通过计算，串电阻详细参数如下:

$\begin{array}{c}{R}_{st1}=\left(\mathrm{\beta}-1\right){R}_{a}=0.597\times 1.21=0.722\Omega \#\left(\text{3-1}\text{5}\right)\end{array}$

$\begin{array}{c}{R}_{st2}=\beta \left(\mathrm{\beta}-1\right){R}_{a}=0.597\times 1.21\times 1.597=1.154\Omega \#\left(\text{3-1}\text{6}\right)\end{array}$

$\begin{array}{c}{R}_{st3}={\mathrm{\beta}}^{2}\left(\mathrm{\beta}-1\right){R}_{a}=0.597\times 1.21\times {1.597}^{2}=1.842\Omega \#\left(\text{3-1}\text{7}\right)\end{array}$

$\begin{array}{c}\mathrm{we}\mathrm{get}{R}_{c}=3.38\Omega \#\left(\text{3-1}\text{8}\right)\end{array}$

**图 3.14 串电阻与调速仿真**

![image](https://github.com/user-attachments/assets/606bf0d4-b14c-40e2-bd51-68c6894f2286)

## 4.整体仿真设计

**图 3.15 整体仿真电路**

![image](https://github.com/user-attachments/assets/d6e513f4-0d71-4d37-a677-2f1b0e78082e)

在整体设计中，我们将调速电阻分为多级，将大小为 4Ω，2Ω，1Ω 的电阻陆续接入电路中进行调速，调速的计算过程如章节四的第 3 节；对于整体的设计，首先设计将 1500r/min 的初始转速调整为 1200r/min，通过计算，得出串电阻为 2Ω，与仿真的 1176r/min 有一定区别，因此同理，在继续串入 4Ω，2Ω，1Ω 的电阻进行调速，实现多级的降速，计算过程省略，最终的转速情况可见结果分析。
对于制动与停车，则也采用平稳停车的方式，先以比较高的速度(-900r/min)进行下放，然后短接部分反转电阻进行减速至-300r/min 左右，然后到地面后，再继续短接部分电阻进行制动，实现稳定停车，详细的计算过程见第四章节。

# 四、结果分析

## 1.仿真整体结果分析

**图 4.1 整体仿真数据波形图像**

![image](https://github.com/user-attachments/assets/8fd41852-090d-4f7a-942d-d446c4e8cf98)

由仿真结果图可见，转速在启动和制动过程中变化较快，启动和制动瞬间电流突变，但未超过两倍的额定电流（IN），因此电枢电流在安全范围内，系统能正常运行。

**图 4.2 excel 处理的运行过程机械特性图**

![image](https://github.com/user-attachments/assets/26deb4f8-795d-4e66-a2b6-553f395e7259)

**图 4.3 整体运行情况波形图**

![image](https://github.com/user-attachments/assets/e680dcc2-3204-4688-ba61-9fd2e32d0725)

通过 excel 处理后，如图 4.2，将该图与前文的理论值计算绘制的各个部分的机械特性理想曲线相比对，匹配程度高，对应性高，仿真结果较为成功。
如图 4.3 通过对转速的积分，可得出电机运行情况，到 25m 后开始下下放物块。
对图 4.3 的图线分析解释如下：
（1）启动过程平滑且启动增速迅速，速度变化不明显，呈现出多级启动痕迹不明显的特征。整个升速过程十分平稳，通过平滑的调速能稳定地达到 25 米的目标速度。
（2）制动过程迅速且高效，当重物接近 25 米时，系统能够迅速减速并进行制动，随后进行反向制动操作。反向加速度较小，这种设计对搬运的重物非常友好，确保了重物在搬运过程中的安全性和稳定性。
（3）停车过程可靠且稳定，当重物接近地面时，系统能够缓缓减速并最终停车。同时，由于在 n=0 时 T=TL 锁住物体，确保了物体最终保持在初始位置不变。总体来看，整个过程的加减速设置合理，曲线优美，展示了良好的控制性能。

## 2.分级启动环节分析

如图 4.4 所示，在多级切断电阻后，运行状态从 B->C->D->E->F，完成简单可靠的分级启动。
根据特性公式使用 matlab 画出理论机械特性图与运行点分析如右图所示，体现了转速逐级向上的变化，在误差范围内符合仿真的情况，电流、电压、转矩的变化规律分析略。

**图 4.4 调速过程理论分析图**

![image](https://github.com/user-attachments/assets/a9147b8c-de93-4889-a601-c3f73045fa1e)

## 3.调速过程分析

使用 matlab 根据特性公式画出右图。未串入电阻时，工作点为 A 点。串入电阻后，工作点向右平移至 B，沿新的工作曲线向下运动至 C 点，实现基速向下调，调速过程串入的总电阻为 9.4Ω，对后面停车调速电阻计算有关。
电流、电压、转矩的变化规律分析略。

**图 4.5 调速过程理论分析**

![image](https://github.com/user-attachments/assets/5070fcea-c10c-46ff-9a51-9f9cf656e87e)

## 4.制动与停车过程分析

### 4.1 转速方向的反接制动过程

使用 matlab 根据特性公式画出右图。通过计算得出的电阻需要减去前面调速的电阻（9.4Ω），整个过程先是为图的 A-> B->C,此时下放速度为-400r/min，200 秒时，再次接入制动电阻 R3，使下放速度加快至-900r/min。此过程为下图的 C-> D-> E。
电流、电压、转矩的变化规律分析略。

**图 4.6 反接理论分析图**

![image](https://github.com/user-attachments/assets/161cdde0-1773-4f3d-b933-4c864556b877)

### 4.2 可靠停车过程

制动中采用了调速制动的方式使调速更加平滑，虽然计算比较繁琐，但是效果显著，重物的运动轨迹更加的漂亮；具体制动表现在下图中 R2 与 R3 被短路，导致负载力矩等于输出力矩，速度减为 0 后，使加速度近似为 0，实现停车。
电流、电压、转矩的变化规律分析略。

**图 4.7 停车仿真电路图**

![image](https://github.com/user-attachments/assets/4c167521-1e1f-4877-93cb-7877f656642f)
