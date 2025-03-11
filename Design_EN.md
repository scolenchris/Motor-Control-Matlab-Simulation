![image](https://github.com/user-attachments/assets/f73a3215-59e6-4a66-b499-7629e60450eb)- [中文版](./Design_CN.md)

# I. Research Background

Motor control systems are extensively utilized in various fields such as industry, transportation, and household appliances. With the advancement of technology, advanced control methods like vector control and direct torque control have emerged, imposing new requirements on system design. The course design of motor control involves multiple disciplines including automatic control, electronic technology, and computer applications, which aids students in integrating theoretical knowledge with practical applications, thereby enhancing their ability to comprehensively utilize knowledge. In terms of applications, motor control systems play a pivotal role in modern industrial automation, including CNC machine tools, robotics, and electric vehicles. Designing based on specific application contexts can improve practicality and relevance. Educationally, this serves as a crucial practical component for automation majors. Through course design, students can grasp fundamental principles and design methodologies, cultivate hands-on skills and engineering practice capabilities, and be introduced to preliminary research work, fostering research interest and competence.

# II. Scheme Demonstration (Design Concept)

## 1. Motor Selection and Parameter Calculation

### 1.1 Motor Type Selection

Estimate armature circuit resistance:

${R}_{a}=\left(\frac{1}{2}~\frac{2}{3}\right)\frac{{U}_{N}{I}_{N}-{P}_{N}}{{{I}_{N}}^{2}}=\frac{2}{3}\times \frac{220\times 22.3-4000}{{22.3}^{2}}=1.21\mathrm{\Omega}$

Calculate Ce\*ф_N:

$\mathrm{C}\mathrm{e}{\mathrm{\phi}}_{N}=\frac{{U}_{N}\mathrm\ -{I}_{N}{R}_{a}}{{n}_{N}}=\frac{220-1.21\times 22.3}{1500}=0.1286\mathrm\ \mathrm{V}/(\mathrm{r}\bullet {\mathrm{m}\mathrm{i}\mathrm{n}}^{-1})$

Calculate the no-load speed:

${n}_{0}=\frac{{U}_{N}}{\mathrm{C}\mathrm{e}{\mathrm{\phi}}_{N}}=\frac{220}{0.1286}=1710.73\mathrm\ \mathrm\ \mathrm{r}\bullet {\mathrm{m}\mathrm{i}\mathrm{n}}^{-1}$

Calculate rated torque:

${T}_{N}=9.55\mathrm{C}\mathrm{e}{\mathrm{\phi}}_{N}{I}_{N}=9.55\times 0.1286\times 22.3=27.387\mathrm\ \mathrm{N}\bullet \mathrm{m}$

Estimate armature inductance:

${\mathrm{L}}_{\mathrm{a}}=19.1\times \frac{C{U}_{N}}{2P{n}_{N}{I}_{N}}=19.1\times \frac{0.4\times 220}{2\times 1\times 1500\times 22.3}=0.02512\mathrm\ \mathrm{H}$

Estimate excitation current:

If R_f=20 Ω, then

${I}_{f}=\frac{{U}_{f}}{{R}_{f}}=\frac{220}{20}=11\mathrm{A}$

Estimate the electromotive force constant:

${K}_{E}=\frac{60}{2\pi}\times \mathrm{C}\mathrm{e}{\mathrm{\phi}}_{N}=0.1286\times \frac{60}{2\pi}=1.228$

Estimation of mutual inductance between armature winding and excitation winding:

$\mathrm{L}\mathrm{a}\mathrm{f}=\frac{{K}_{E}}{{I}_{f}}=\frac{1.288}{11}=0.1116\mathrm\ \mathrm{H}$

When selecting a motor, we compared the operational characteristics of separately excited DC motors and three-phase asynchronous motors. By plotting their characteristics on the same coordinate system, it was observed that the three-phase asynchronous motor cannot operate stably at point A3, while the separately excited DC motor exhibits an upward curve due to the demagnetizing effect of armature reaction when the torque exceeds Tl. Additionally, the compensation method for separately excited DC motors is more straightforward and convenient.

**Figure 2.1: Characteristics of Various Motor Types**

![image](https://github.com/user-attachments/assets/2e812cbf-0272-4626-b8b4-a5887b67c942)

In selecting a specific type of DC motor, we compared the mechanical characteristics of various excitation motors. The mechanical characteristic curve of compound-wound series motors is relatively soft, making calculations difficult. This design task requires reverse lowering of objects, which may necessitate reverse braking. However, reverse braking can alter the excitation direction of shunt generators, ultimately failing to change the motor's rotation direction.

Therefore, the separately excited DC generator was ultimately selected.

### 1.2 Detailed Motor Parameter Calculation

According to the requirements: the empty hook weighs 10kg and the maximum load capacity is 1000kg. The reduction ratio of the transmission mechanism is 100:1, and the transmission efficiency is 0.9; The inertia of the flywheel can be ignored. The maximum speed for lifting heavy objects is 1500r/min, and the minimum speed for lowering heavy objects is 300r/min. Raise/lower the height by 25m. The diameter of the drum is 0.4m.

The rated power and load torque of the required motor can be calculated based on the design conditions.

The calculation process is as follows:

Empty hook 10kg, maximum load, 1000kg, g is taken as 10 for calculation, total weight: 1010kg, drum diameter: 0.4m, calculated at maximum speed 1500r/min=25r/s

Torque:

${T}_{F}=\mathrm{m}\mathrm{g}\cdot \mathrm{r}=1010\times 10\times \frac{0.2}{4}=2020\mathrm{N}\cdot \mathrm{m}$

reduction ratio:

${n}_{\mathrm{turn}}=\mathrm\ \frac{{n}_{max}}{100}=\frac{1500}{100}=15\mathrm{r}/\mathrm{m}\mathrm{i}\mathrm{n}$

output power:

${P}_{{F}_{max}}={T}_{F}\cdot {\mathrm{\Omega}}_{max}=2020\times \frac{2\pi \times 15}{60}=3.173\mathrm{k}\mathrm{w}$

Minimum rated power:

$P_{N} = \frac{P_{F_{\text{max}}}}{\text{ŋ}} = \frac{3.173}{0.9} = 3.526\, \mathrm{kW}$

Corresponding to electromagnetic torque:

${T}_{N}=\frac{{P}_{N}}{\frac{2\pi n}{60}}=\frac{3526}{\frac{2\pi \times 1500}{60}}=22.447\mathrm{N}\cdot \mathrm{m}$

Based on the requirements: the empty hook weight is 10 kg, and the maximum load is 1000 kg. The transmission mechanism has a reduction ratio of 100:1 and an efficiency of 0.9; the flywheel inertia can be neglected. The maximum lifting speed is 1500 rpm, and the minimum lowering speed is 300 rpm. The lifting/lowering height is 25 meters, and the drum diameter is 0.4 meters.

Through calculations by team members (calculation process omitted):

A motor with n > 1500 rpm and a rated power PN > 3.526 kW should be selected, ensuring an output power PN·ŋ > 3.173 kW.

After consulting relevant literature, the Z2-42 motor was chosen, with the following rated parameters:

Rated power PN: 4 kW, Rated voltage UN = 220 V, Rated speed nN = 1500 rpm, Rated current IN = 22.3 A.

**Figure 2.2: Simulation Motor Module Parameter Settings**

![image](https://github.com/user-attachments/assets/b222fbf3-3f75-403e-9262-f57e01cb76e3)

Subsequently, motor parameters such as inductance and excitation current were estimated and entered into the Simulink motor parameter settings, as shown in the upper right figure. All subsequent simulations were based on these parameters.

## 2. Startup Scheme Selection

During the selection of the startup scheme, we ultimately decided to adopt a multi-stage series resistance startup method. This choice was primarily based on the following considerations: firstly, the simulation circuit construction is relatively complex but simple to operate and highly reliable; secondly, the multi-stage speed regulation capability is fully demonstrated. Given these advantages, we chose the series resistance startup method.

## 3. Speed Regulation Scheme Selection

The speed regulation scheme selected is series resistance speed regulation. For DC motor speed regulation methods, since the design involves a potential energy load, speed regulation is chosen between the two. Additionally, the braking scheme employs reverse braking, requiring the insertion of a large resistor, hence the series resistance speed regulation is selected. This approach ensures a unified circuit implementation process, making it easier to identify and resolve issues.

## 4. Braking Scheme Selection

In the selection of the speed regulation scheme, we decided to adopt the series resistance speed regulation method. For DC motor speed regulation methods, since the design involves a potential energy load, speed regulation is chosen between the two. Additionally, the braking scheme employs reverse braking, requiring the insertion of a large resistor, hence the series resistance speed regulation is selected. This approach not only ensures a unified circuit implementation process but also facilitates issue identification and resolution, enhancing system reliability and maintainability.

## 5. Parking Scheme Selection

The parking scheme involves cutting off part of the resistance to achieve parking. During the reverse braking process, part of the resistance is short-circuited to reduce the speed to zero.

## 6. Overall Scheme Diagram

**Figure 2.3: Overall Scheme Diagram**

![image](https://github.com/user-attachments/assets/f8cd707e-15cb-42e0-8109-ec39a4838aec)

# III. Process Discussion

## 1. Preparations Before the Overall Task

As the team leader, I initially assigned simulation practice tasks to team members based on the materials I had collected (various books and papers). This was to familiarize them with the functionalities of each module, thereby facilitating problem-solving. I selected examples from several books, some of which focused on speed regulation, others on startup, and some on closed-loop speed regulation, providing a diverse range of content. Issues encountered during the process were discussed collectively and resolved. Subsequently, I allocated specific tasks, allowing each team member to choose a module for in-depth research based on their interests and areas of expertise. To ensure that everyone fully understood and mastered their respective modules, I first had each member conduct preliminary simulation operations, followed by fine-tuning. Any issues were raised and discussed in the group.

Below are the images of the various parts we simulated.

**Figure 3.1: Simulation of Open-Loop Three-Phase Speed Regulation System**

![image](https://github.com/user-attachments/assets/d198e9bd-54ee-43ff-8834-a9c523a37cb1)

**Figure 3.2: Simulation Waveform**

![image](https://github.com/user-attachments/assets/ca1977e5-ff91-4d05-b60f-1b0aaddb2abb)

**Figure 3.3: Simulation of Closed-Loop Three-Phase Speed Regulation System 1**

![image](https://github.com/user-attachments/assets/1e253db7-7c21-4ac4-93a1-5ca542afd454)

**Figure 3.4: Simulation of Closed-Loop Three-Phase Speed Regulation System 2**

![image](https://github.com/user-attachments/assets/206cbe0b-20e7-49dd-b743-85f795566253)

## 2. Simulation Module Construction and Calculation

### 2.1 Initial Model Construction for Energy Consumption Braking Simulation

When energy consumption braking occurs, the power supply is cut off, and the braking resistor is connected to the circuit. At this point, due to the inertia of the motor, it continues to rotate and transforms into a generator. The direction of the armature current is opposite to the original current direction, and the armature generates a braking torque to counteract the torque produced by inertia, thereby rapidly stopping the motor. By adjusting the resistance value of the braking resistor R, the braking time can be regulated. The smaller the resistance value of R, the faster the braking process; conversely, the larger the resistance value, the longer the braking time. The simulation of this process was completed using Simulink.

Calculations were performed for the overall system to determine the resistance value of the energy consumption braking resistor and the minimum resistance value (to avoid excessive current). The calculation process is as follows:

$\mathrm{n}=-\frac{{\mathrm{R}}_{\mathrm{a}}+{\mathrm{R}}_{\mathrm{c}}}{{\mathrm{C}}_{\mathrm{e}}{\mathrm{C}}_{\mathrm{T}}{\mathrm{\phi}}^{2}}$

$\begin{array}{c}{\mathrm{C}}_{\mathrm{e}}\phi=\frac{{U}_{N}-{I}_{N}{R}_{a}}{{n}_{N}}=\frac{220-121\times 22.3}{1500}=0.1286V/r\cdot{min}^{-1}\#\left(\text{3-2}\right)\end{array}$

$\begin{array}{c}n=-\frac{{\mathrm{R}}_{\mathrm{a}}+{\mathrm{R}}_{\mathrm{\Omega}}}{{\mathrm{C}}_{\mathrm{e}}\mathrm{\phi}}{\mathrm{I}}_{\mathrm{N}}=-300r/min\#\left(\text{3-3}\right)\end{array}$

$\begin{array}{c}\therefore {{\mathrm{R}}_{\mathrm{a}}=1.21\mathrm{\Omega},\mathrm{I}}_{\mathrm{N}}=22.3A\#\left(\text{3-4}\right)\end{array}$

$\begin{array}{c}we get:{R}_{\mathrm{\Omega}}=0.52\Omega \#\left(\text{3-5}\right)\end{array}$

$\begin{array}{c}{R}_{\mathrm{\Omega}\mathrm{m}\mathrm{i}\mathrm{n}}=\frac{{E}_{a}}{{I}_{amax}}-{R}_{a}\#\left(\text{3-6}\right)\end{array}$

$\begin{array}{c}but {I}_{amax}=3{I}_{N}=66.9A\#\left(\text{3-7}\right)\end{array}$

$\begin{array}{c}{E}_{a}={\mathrm{C}}_{\mathrm{e}}{\mathrm{\phi}}_{\mathrm{N}}{\mathrm{n}}_{\mathrm{N}}=1000\times 0.1286=128.6V\#\left(\text{3-8}\right)\end{array}$

$\begin{array}{c}{\therefore R}_{\Omega min}=\frac{128.6}{66.9}-1.21=0.7122\Omega \#\left(\text{3-9}\right)\end{array}$

**Figure 3.5: Simulation Diagram of Series Resistance Starting Circuit**

![image](https://github.com/user-attachments/assets/7dae6de4-84e4-488c-9a1e-53a674c10b10)

Firstly, the above figure illustrates the circuit for series resistance starting. The series resistance circuit is relatively complex, so I integrated it and incorporated it as a subsystem into the model. The detailed principles of the starting process are omitted, as shown in the figure below.

**Figure 3.6: Encapsulation of Series Resistance Circuit**

![image](https://github.com/user-attachments/assets/8c4b427b-8cac-43d3-8398-e421ffb99f98)

Next, the energy consumption braking system was simulated and designed as a two-stage braking process. Initially, resistor RΩ is connected, followed by resistor RΩ1. The parallel combination of these resistors significantly reduces the resistance value, thereby achieving braking and stopping. The values set were RΩ = 0.575 Ω and RΩ1 = 0.1 Ω (attempting to achieve stopping). For the breaker module, when a rising edge signal is received, the switch closes, completing the circuit. The resistor below the main switch is set to 10,000 Ω, serving as a grounding resistor to ensure that the voltage applied to the motor remains at 220 V. The motor output signal is fed into the bus selector module, which separates the bus signal into multiple signals for display on the oscilloscope. The speed component uses a gain module to convert the speed unit to rpm.

**Figure 3.7: Energy Consumption Braking Simulation**

![image](https://github.com/user-attachments/assets/d74ad64a-6f2b-4a7b-a7c8-812249daff8c)

The final speed waveform is as follows: energy consumption braking is applied at 11 seconds, reducing the speed to approximately -300 rpm and maintaining it. At 20 seconds, the resistors are connected in parallel, further reducing the resistance. However, the speed cannot approach zero due to the influence of Ra, preventing the slope from decreasing further. Consequently, the characteristic curve cannot intersect the x-axis, making it impossible to meet the stopping requirement. This provides a basis for scheme selection.

**Figure 3.8: Simulation Image—Speed**

![image](https://github.com/user-attachments/assets/c4b78721-61f8-497a-a468-baeeb50e484f)

### 2.2 Simulation Construction of Armature Power Reverse Braking

The process of armature power reverse braking involves first disconnecting the motor's original power supply to halt its normal operation. Then, the polarity of the motor's power supply is reversed, i.e., the positive and negative terminals are swapped. At this point, the motor generates an electromagnetic torque opposite to its original rotation direction, rapidly decelerating the motor until it stops. If the load is small, the motor may even start in the reverse direction.

The calculation process for various parameters is as follows:

$\begin{array}{c}{P}_{N}=4kw,{U}_{N}=220V,{n}_{N}=1500r/min,{I}_{N}=22.3A\#\left(\text{3-10}\right)\end{array}$

$\begin{array}{c}{R}_{a}=4.24\Omega \#\left(\text{3-11}\right)\end{array}$

$\begin{array}{c}{n}_{a}=1000r/min{,E}_{a}={\mathrm{C}}_{\mathrm{e}}{\mathrm{\phi}}_{\mathrm{N}}{\mathrm{n}}_{\mathrm{a}}\#\left(\text{3-12}\right)\end{array}$

$\begin{array}{c}{\mathrm\ \mathrm{C}}_{\mathrm{e}}\phi=\frac{{U}_{N}-{I}_{N}{R}_{a}}{{n}_{N}}=0.1286V/r\cdot {min}^{-1}\#\end{array}$

$\begin{array}{c}\therefore {\mathrm{E}}_{\mathrm{a}}={\mathrm{C}}_{\mathrm{e}}{\mathrm{\phi}}_{\mathrm{N}}{\mathrm{n}}_{\mathrm{a}}=128.6V\#\left(\text{3-1}\text{3}\right)\end{array}$

$\begin{array}{c}{\mathrm{R}}_{\mathrm{b}\mathrm{m}\mathrm{i}\mathrm{n}}=\frac{-\mathrm{U}-{\mathrm{E}}_{\mathrm{a}}}{-{\mathrm{I}}_{\mathrm{a}\mathrm{m}\mathrm{a}\mathrm{x}}}-{\mathrm{R}}_{\mathrm{a}}=\frac{-220-128.6}{-3{\mathrm{I}}_{\mathrm{N}}}-1.21=(5.12-1.21)\Omega =4.00\Omega \#\left(\text{3-1}\text{4}\right)\end{array}$

Below is the simulation circuit I constructed. The startup process is omitted, and the reverse braking process occurs at 9 seconds, when the startup switch is turned off, and the armature power reverse braking switch below is turned on. At this point, reverse voltage is applied to the armature, causing the motor to rapidly undergo reverse braking.

**Figure 3.9: Reverse Braking Simulation**

![image](https://github.com/user-attachments/assets/4f1cacce-29e1-41db-a726-57c5c33d26cf)

The final simulation results were unsatisfactory, as shown in the figure below. Initially, I connected the reverse braking in series with the armature circuit, but in reality, it should be connected in parallel. Under equivalent conditions, reverse braking is in series. Therefore, I modified the circuit to connect it in parallel and substituted the calculated parameter values into the simulation model. However, the resulting image showed that the reversal speed was too fast, and the current was very high.

After further research, I found that reverse braking causes the motor's reverse rotation speed to increase rapidly. Although this method can achieve rapid braking and stopping, the armature current also increases significantly. This high current places a substantial load on the motor and related equipment, posing potential safety hazards and equipment wear issues. Therefore, it is not suitable for deployment in practical applications, providing a basis for scheme selection.

**Figure 3.10: Simulation Image—Speed**

![image](https://github.com/user-attachments/assets/c0b8aa93-1a5c-43d2-9bf5-d6607a05c636)

**Figure 3.11: Simulation Image—Armature Current**

![image](https://github.com/user-attachments/assets/7c2ae02f-0cd5-49ec-8be4-1515ea30ba85)

### 2.3 Final Design of Reverse Braking and Stopping Simulation with Speed Reversal

**Figure 3.12: Encapsulation of Braking and Stopping Module**

![image](https://github.com/user-attachments/assets/ed5e3701-725a-4b44-9f3b-34eee4b9b290)

**Figure 3.13: Encapsulation of Speed Regulation Module**

![image](https://github.com/user-attachments/assets/70ed695f-f1cf-43b0-a8a2-4f2fef78ba3d)

After integrating the speed regulation module and the stopping module, and encapsulating each part as a subsystem, the system interface and structure became clearer. The braking and stopping modules are implemented through reverse braking with speed reversal, replacing the previous energy consumption braking. Practice has shown that this design is superior to the original parallel design, and the final results are very satisfactory.

The above figure divides the resistor into two parts for multi-stage braking, transitioning from the reversal condition to the lowest reversal speed, achieving smooth braking, and then short-circuiting the resistor to achieve stopping. The specific implementation is detailed in the results analysis.

During the integration process, we conducted detailed analysis and optimization of each module, encapsulating them as independent subsystems. This not only simplified the overall design complexity but also improved the system's maintainability and scalability. By using short-circuit resistors to replace the original parallel design, we effectively resolved the issue of excessive current, enhancing the system's stability and safety.

When finally adjusting the reverse braking resistor, it was not possible to fine-tune it to n=0, as detailed in the summary.

## 3. Simulation and Calculation of Series Resistance Starting and Speed Regulation

Starting current:

${I}_{st}=\frac{{U}_{N}}{{R}_{a}+{R}_{st}}=22.3\times 2\mathrm\ \mathrm{A}$

Starting resistor:

${R}_{st}=\frac{220}{22.3\times 2}-1.21=3.723\mathrm{\Omega}$

Total resistance:

${R}_{3}=\frac{{U}_{N}}{{I}_{1}}=\frac{220}{22.3\times 2}=4.933\mathrm{\Omega}$

$$ \beta = \sqrt[3]{\frac{R_3}{R_a}} = \sqrt[3]{\frac{4.933}{1.21}} = 1.597 $$

The segmented resistance is:

${R}_{st1}=\left(\mathrm{\beta}-1\right){R}_{a}=0.597\times 1.21=0.722\mathrm{\Omega}$

${R}_{st2}=\mathrm{\beta}\left(\mathrm{\beta}-1\right){R}_{a}=0.597\times 1.21\times 1.597=1.154\mathrm{\Omega}$

${R}_{st3}={\mathrm{\beta}}^{2}\left(\mathrm{\beta}-1\right){R}_{a}=0.597\times 1.21\times {1.597}^{2}=1.842\mathrm{\Omega}$

At the same time, the corresponding speed control resistance can also be calculated:

$n = \frac{U_N}{\phi C_e} - \frac{R_a + R_c}{(\phi C_e)^2 \times 9.55} \times 23$

${R}_{c}=3.38\mathrm{\Omega}$

Through calculations , the detailed parameters of the series resistance are as follows:

$\begin{array}{c}{R}_{st1}=\left(\mathrm{\beta}-1\right){R}_{a}=0.597\times 1.21=0.722\Omega \#\left(\text{3-1}\text{5}\right)\end{array}$

$\begin{array}{c}{R}_{st2}=\beta \left(\mathrm{\beta}-1\right){R}_{a}=0.597\times 1.21\times 1.597=1.154\Omega \#\left(\text{3-1}\text{6}\right)\end{array}$

$\begin{array}{c}{R}_{st3}={\mathrm{\beta}}^{2}\left(\mathrm{\beta}-1\right){R}_{a}=0.597\times 1.21\times {1.597}^{2}=1.842\Omega \#\left(\text{3-1}\text{7}\right)\end{array}$

Try to adjust the speed to 1000r/min, and adjust the speed resistor according to the characteristic equation

$\begin{array}{c}\mathrm{we}\mathrm{get}{R}_{c}=3.38\Omega \#\left(\text{3-1}\text{8}\right)\end{array}$

The simulation model is as follows, briefly explained.

**Figure 3.14: Simulation of Series Resistance and Speed Regulation**

![image](https://github.com/user-attachments/assets/606bf0d4-b14c-40e2-bd51-68c6894f2286)

## 4. Overall Simulation Design

**Figure 3.15: Overall Simulation Circuit**

![image](https://github.com/user-attachments/assets/d6e513f4-0d71-4d37-a677-2f1b0e78082e)

In the overall design, the speed regulation resistors are divided into multiple stages, with resistors of 4 Ω, 2 Ω, and 1 Ω sequentially connected to the circuit for speed regulation. The calculation process for speed regulation is detailed in Section 3 of Chapter 4. For the overall design, the initial speed of 1500 rpm is first adjusted to 1200 rpm. Through calculations, a series resistance of 2 Ω is determined, which differs slightly from the simulated result of 1176 rpm. Similarly, resistors of 4 Ω, 2 Ω, and 1 Ω are sequentially connected to achieve multi-stage speed reduction. The calculation process is omitted, and the final speed results are discussed in the results analysis.

For braking and stopping, a smooth stopping method is adopted. Initially, the load is lowered at a relatively high speed (-900 rpm), and then part of the reverse resistor is short-circuited to reduce the speed to approximately -300 rpm. Upon reaching the ground, further short-circuiting of the resistor achieves stable stopping. The detailed calculation process is provided in Chapter 4.

# IV. Results Analysis

## 1. Analysis of Overall Simulation Results

**Figure 4.1: Waveform Image of Overall Simulation Data**

![image](https://github.com/user-attachments/assets/8fd41852-090d-4f7a-942d-d446c4e8cf98)

As shown in the simulation results, the speed changes rapidly during the startup and braking processes. The current experiences sudden changes at the moments of startup and braking but does not exceed twice the rated current (IN). Therefore, the armature current remains within a safe range, and the system operates normally.

**Figure 4.2: Mechanical Characteristics Diagram of the Operation Process Processed in Excel**

![image](https://github.com/user-attachments/assets/26deb4f8-795d-4e66-a2b6-553f395e7259)

**Figure 4.3: Waveform Diagram of Overall Operation**

![image](https://github.com/user-attachments/assets/e680dcc2-3204-4688-ba61-9fd2e32d0725)

After processing with Excel, as shown in Figure 4.2, the diagram is compared with the ideal mechanical characteristic curves calculated theoretically in the previous sections. The high degree of matching and correspondence indicates a successful simulation result.

As shown in Figure 4.3, by integrating the speed, the motor's operating condition can be determined. The load begins to descend after reaching 25 meters.

The analysis of Figure 4.3 is as follows:

1. **Smooth Startup Process**: The startup process is smooth, with rapid acceleration and minimal speed fluctuations, showing no obvious traces of multi-stage startup. The entire acceleration process is very stable, achieving the target speed of 25 meters through smooth speed regulation.

2. **Efficient Braking Process**: When the load approaches 25 meters, the system can quickly decelerate and initiate braking, followed by reverse braking. The reverse acceleration is small, making this design very friendly to the transported load and ensuring safety and stability during handling.

3. **Reliable Stopping Process**: As the load approaches the ground, the system gradually decelerates and finally stops. Additionally, since T = TL locks the load at n = 0, the load remains in its initial position. Overall, the acceleration and deceleration settings are reasonable, and the curves are smooth, demonstrating excellent control performance.

## 2. Analysis of Multi-Stage Startup Process

As shown in Figure 4.4, after multi-stage resistor disconnection, the operating state transitions from B -> C -> D -> E -> F, completing a simple and reliable multi-stage startup.

Using MATLAB, the theoretical mechanical characteristic diagram and operating points are plotted based on the characteristic formulas, as shown on the right. The diagram reflects the step-by-step increase in speed, which aligns with the simulation results within the error margin. The analysis of current, voltage, and torque variations is omitted.

**Figure 4.4: Theoretical Analysis Diagram of the Speed Regulation Process**

![image](https://github.com/user-attachments/assets/a9147b8c-de93-4889-a601-c3f73045fa1e)

## 3. Analysis of Speed Regulation Process

Using MATLAB, the diagram on the right is plotted based on the characteristic formulas. Without series resistors, the operating point is at A. After connecting the resistors, the operating point shifts to B and moves downward along the new operating curve to C, achieving a downward adjustment of the base speed. The total series resistance for the speed regulation process is 9.4 Ω, which is relevant to the subsequent stopping and speed regulation resistor calculations. The analysis of current, voltage, and torque variations is omitted.

**Figure 4.5: Theoretical Analysis Diagram of the Speed Regulation Process**

![image](https://github.com/user-attachments/assets/5070fcea-c10c-46ff-9a51-9f9cf656e87e)

## 4. Analysis of Braking and Stopping Process

### 4.1 Reverse Braking Process with Speed Reversal

Using MATLAB, the diagram on the right is plotted based on the characteristic formulas. The calculated resistor value needs to subtract the previously used speed regulation resistors (9.4 Ω). The entire process follows A -> B -> C, where the lowering speed is -400 rpm. At 200 seconds, the braking resistor R3 is connected again, increasing the lowering speed to -900 rpm. This process corresponds to C -> D -> E in the diagram below. The analysis of current, voltage, and torque variations is omitted.

**Figure 4.6: Theoretical Analysis Diagram of Reverse Braking**

![image](https://github.com/user-attachments/assets/161cdde0-1773-4f3d-b933-4c864556b877)

### 4.2 Reliable Stopping Process

The braking process employs speed regulation braking to achieve smoother speed control. Although the calculations are complex, the results are significant, resulting in a more elegant motion trajectory for the load. Specifically, as shown in the diagram below, R2 and R3 are short-circuited, causing the load torque to equal the output torque. When the speed reduces to 0, the acceleration approximates 0, achieving stopping. The analysis of current, voltage, and torque variations is omitted.

**Figure 4.7: Stopping Simulation Circuit Diagram**

![image](https://github.com/user-attachments/assets/4c167521-1e1f-4877-93cb-7877f656642f)
