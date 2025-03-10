# I. Research Background

Motor control systems are extensively utilized in various fields such as industry, transportation, and household appliances. With the advancement of technology, advanced control methods like vector control and direct torque control have emerged, imposing new requirements on system design. The course design of motor control involves multiple disciplines including automatic control, electronic technology, and computer applications, which aids students in integrating theoretical knowledge with practical applications, thereby enhancing their ability to comprehensively utilize knowledge. In terms of applications, motor control systems play a pivotal role in modern industrial automation, including CNC machine tools, robotics, and electric vehicles. Designing based on specific application contexts can improve practicality and relevance. Educationally, this serves as a crucial practical component for automation majors. Through course design, students can grasp fundamental principles and design methodologies, cultivate hands-on skills and engineering practice capabilities, and be introduced to preliminary research work, fostering research interest and competence.

# II. Scheme Demonstration (Design Concept)

## 1. Motor Selection and Parameter Calculation

### 1.1 Motor Type Selection

When selecting a motor, we compared the operational characteristics of separately excited DC motors and three-phase asynchronous motors. By plotting their characteristics on the same coordinate system, it was observed that the three-phase asynchronous motor cannot operate stably at point A3, while the separately excited DC motor exhibits an upward curve due to the demagnetizing effect of armature reaction when the torque exceeds Tl. Additionally, the compensation method for separately excited DC motors is more straightforward and convenient.
**Figure 2.1: Characteristics of Various Motor Types**
In selecting a specific type of DC motor, we compared the mechanical characteristics of various excitation motors. The mechanical characteristic curve of compound-wound series motors is relatively soft, making calculations difficult. This design task requires reverse lowering of objects, which may necessitate reverse braking. However, reverse braking can alter the excitation direction of shunt generators, ultimately failing to change the motor's rotation direction.
Therefore, the separately excited DC generator was ultimately selected.

### 1.2 Detailed Motor Parameter Calculation

Based on the requirements: the empty hook weight is 10 kg, and the maximum load is 1000 kg. The transmission mechanism has a reduction ratio of 100:1 and an efficiency of 0.9; the flywheel inertia can be neglected. The maximum lifting speed is 1500 rpm, and the minimum lowering speed is 300 rpm. The lifting/lowering height is 25 meters, and the drum diameter is 0.4 meters.
Through calculations by team members (calculation process omitted):
A motor with n > 1500 rpm and a rated power PN > 3.526 kW should be selected, ensuring an output power PN·ŋ > 3.173 kW.
After consulting relevant literature, the Z2-42 motor was chosen, with the following rated parameters:
Rated power PN: 4 kW, Rated voltage UN = 220 V, Rated speed nN = 1500 rpm, Rated current IN = 22.3 A.
**Figure 2.2: Simulation Motor Module Parameter Settings**
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

# III. Process Discussion

## 1. Preparations Before the Overall Task

As the team leader, I initially assigned simulation practice tasks to team members based on the materials I had collected (various books and papers). This was to familiarize them with the functionalities of each module, thereby facilitating problem-solving. I selected examples from several books, some of which focused on speed regulation, others on startup, and some on closed-loop speed regulation, providing a diverse range of content. Issues encountered during the process were discussed collectively and resolved. Subsequently, I allocated specific tasks, allowing each team member to choose a module for in-depth research based on their interests and areas of expertise. To ensure that everyone fully understood and mastered their respective modules, I first had each member conduct preliminary simulation operations, followed by fine-tuning. Any issues were raised and discussed in the group.
Below are the images of the various parts we simulated.
**Figure 3.1: Simulation of Open-Loop Three-Phase Speed Regulation System**
**Figure 3.2: Simulation Waveform**
**Figure 3.3: Simulation of Closed-Loop Three-Phase Speed Regulation System 1**
**Figure 3.4: Simulation of Closed-Loop Three-Phase Speed Regulation System 2**

## 2. Simulation Module Construction and Calculation

### 2.1 Initial Model Construction for Energy Consumption Braking Simulation

When energy consumption braking occurs, the power supply is cut off, and the braking resistor is connected to the circuit. At this point, due to the inertia of the motor, it continues to rotate and transforms into a generator. The direction of the armature current is opposite to the original current direction, and the armature generates a braking torque to counteract the torque produced by inertia, thereby rapidly stopping the motor. By adjusting the resistance value of the braking resistor R, the braking time can be regulated. The smaller the resistance value of R, the faster the braking process; conversely, the larger the resistance value, the longer the braking time. The simulation of this process was completed using Simulink.
Calculations were performed for the overall system to determine the resistance value of the energy consumption braking resistor and the minimum resistance value (to avoid excessive current). The calculation process is as follows:

$\mathrm{n}=-\frac{{\mathrm{R}}_{\mathrm{a}}+{\mathrm{R}}_{\mathrm{c}}}{{\mathrm{C}}_{\mathrm{e}}{\mathrm{C}}_{\mathrm{T}}{\mathrm{\phi}}^{2}}$

$\begin{array}{c}{\mathrm{C}}_{\mathrm{e}}\phi=\frac{{U}_{N}-{I}_{N}{R}_{a}}{{n}_{N}}=\frac{220-121\times 22.3}{1500}=0.1286V/r\cdot{min}^{-1}\#\left(\text{3-2}\right)\end{array}$

$\begin{array}{c}n=-\frac{{\mathrm{R}}_{\mathrm{a}}+{\mathrm{R}}_{\mathrm{\Omega}}}{{\mathrm{C}}_{\mathrm{e}}\mathrm{\phi}}{\mathrm{I}}_{\mathrm{N}}=-300r/min\#\left(\text{3-3}\right)\end{array}$

$\begin{array}{c}\therefore {{\mathrm{R}}_{\mathrm{a}}=1.21\mathrm{\Omega},\mathrm{I}}_{\mathrm{N}}=22.3A\#\left(\text{3-4}\right)\end{array}$

$\begin{array}{c}解得:{R}_{\mathrm{\Omega}}=0.52\Omega \#\left(\text{3-5}\right)\end{array}$

$\begin{array}{c}{R}_{\mathrm{\Omega}\mathrm{m}\mathrm{i}\mathrm{n}}=\frac{{E}_{a}}{{I}_{amax}}-{R}_{a}\#\left(\text{3-6}\right)\end{array}$

$\begin{array}{c}而 {I}_{amax}=3{I}_{N}=66.9A\#\left(\text{3-7}\right)\end{array}$

$\begin{array}{c}{E}_{a}={\mathrm{C}}_{\mathrm{e}}{\mathrm{\phi}}_{\mathrm{N}}{\mathrm{n}}_{\mathrm{N}}=1000\times 0.1286=128.6V\#\left(\text{3-8}\right)\end{array}$

$\begin{array}{c}{\therefore R}_{\Omega min}=\frac{128.6}{66.9}-1.21=0.7122\Omega \#\left(\text{3-9}\right)\end{array}$
