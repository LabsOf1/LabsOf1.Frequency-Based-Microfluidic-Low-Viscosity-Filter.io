# LabsOf1.Frequency Based Microfluidic Low Viscosity Filter.io

### PROJECT 2 Frequency Based Microfluidic Low Viscosity Filter

**Summary:**  
A microfluidic filtration system that uses dynamic fluid vibrations to control flow based on frequency stability, enabling selective filtering of particles or compounds in low-viscosity fluids.

**Problem Solved:**  
Traditional microfluidic systems rely on pressure, valves, or material chemistry. This project introduces a novel approach: use frequency tuning to allow or block fluid flow, minimizing complexity and increasing selectivity.

**Key Features / Innovations:**
- Piezoelectric pump emits controlled wave pulses (A·exp(it))
- System measures stability over time (2t) using 3 cantilever sensors
- Fluid is only allowed to flow if frequency stabilizes near desired range (f ≈ f_desired)
- Precision filtering achieved with minimal moving parts

**Technical Overview:**
- MP6 piezoelectric micro-pump controlled by Arduino Uno
- 3 fluidic cantilever sensors: C1, C2, C3
- RC low-pass filter to remove high-frequency noise
- Flow control via frequency logic, not mechanical valves
- Operating range: 85–270 Vpp, 25–226 Hz

**Outcomes / Results:**
- Demonstrated filtration based on frequency tuning
- Showed system stability feedback can regulate fluid flow dynamically
- Proved feasibility for integration in future bio-MEMS systems

**Next Steps / Potential Applications:**
- Lab-on-a-chip diagnostics
- Biomedical separation of compounds (DNA, proteins)
- Adaptive, non-mechanical flow regulation in micro-robotics

**Diagrams / Schematics and Technical Document:**
<img width="980" height="490" alt="image" src="https://github.com/user-attachments/assets/b9b2a9f0-37e5-4fc3-bb8b-d0075068a827" />

**Fig 0. Frequency – Based Filtration**

The idea is to create a filtration system using fluid vibrations that can be used in microfluidic applications. The setup consists of a piezoelectric pump that 
generates waves of a given amplitude A along the chip, 3 fluidic cantilever beams responsible for determining when the fluid stabilizes at a particular frequency, 
and a valve that allows the fluid when tuned at the correct frequency to enter another chip containing the filtered elements of the fluid. For this system we 
will avoid using fluids of high viscosity. 

<img width="980" height="448" alt="image" src="https://github.com/user-attachments/assets/3af0f909-4d79-43a0-b34d-5516c4b84d6d" />

**Fig 1. Frequency – Based Filtration Control Logic**

Piezoelectric pump will send a short pulse signal for a small period of time T and then will stop for a period of time 2t (with T << 2t) which is proportional 
to at least twice the length of the microfluidic chip to ensure frequency stability after 2t. After that time the signal will still have irregularities b of the form A*exp(bit) 
representing that the frequency of the fluid won’t be entirely stable. The sensors C1, C2, C3 are activated near the end of period 2t. Sensors C1, C3 are first activated to measure 
if the frequency of each end of the chip is more or less consistent. Sensor C2 captures the final measured frequency f and compares it to f_desired. If f < f_desired the piezoelectric
pump is activated once more and the entire process repeats until f is somewhere within the range of f_desired. Similarly, if f > f_desired then we wait for period t for the frequency 
to reduce. When the fluid frequency f is within f_desired the valve can be activated to allow filtered content.

<img width="980" height="574" alt="image" src="https://github.com/user-attachments/assets/8074e8a8-c6d1-4054-a85e-1ce371e87692" />

**Fig 2. Micropump MP6 Connector Interface**

The piezoelectric pump is programmed through an Arduino Uno board with the help of a micropump mp6 connector which operates at 5V. Port 11 will represent the amplitude 
of the wave at which the pump will impose on the fluid. Additionally, an RC low pass filter is placed to remove unnecessary high frequency noise. To implement this filtration system, we will 
be controlling fluid flow with respect to the amplitude port 4 and clock port 2. The amplitude range and frequency range for this connector will be 85 – 270 Vpp and 25 – 226 Hz respectively. 
Since our application is a microfluidic filter, we only need a single amplitude and some small variations of some small frequency. The goal is to keep amplitude A as constant as possible while
varying frequency f in order to achieve frequency - based filtration.


<img width="979" height="257" alt="image" src="https://github.com/user-attachments/assets/92247d3f-3826-456c-9df7-b826fa77efee" />
<img width="979" height="379" alt="image" src="https://github.com/user-attachments/assets/c700d187-1bf1-428e-8b29-429a4c76ea87" />
<img width="979" height="210" alt="image" src="https://github.com/user-attachments/assets/161439f4-6580-4403-a64c-bc07321a6f63" />

**Fig 3. Filtration Control Logic Pseudocode**

This pseudocode summarizes the control logic. While filtration may not be perfect and amplitude may not stay completely constant over
time it is important to understand that in order to obtain more accurate amplitude and frequency selection, we must find the correct wait time 2t. In order to construct accurate 
amplitude frequency selection, we need to find efficient algorithms that allow us to compute wait time with respect to fluid density and rate of fluid flow.



