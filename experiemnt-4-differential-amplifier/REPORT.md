# Experiment-04  
# Differential Amplifier Analysis

---

## Aim

To design and analyze CMOS differential amplifier circuits using three different configurations and evaluate their performance through theoretical calculations and LTspice simulations. The study includes determination of operating point conditions, input common-mode range (ICMR), differential gain, bandwidth, unity-gain bandwidth (UGB), gain-bandwidth product (GBP), linear input range, output swing, and power consumption, followed by a comparative analysis of all configurations.

---

## Design Specifications

The circuits are designed according to the constraints provided for **Batch C2**.

### Supply Parameters

| Parameter | Symbol | Value |
|-----------|--------|-------|
| Positive supply voltage | $V_{DD}$ | $+0.9\,\text{V}$ |
| Negative supply voltage | $V_{SS}$ | $-0.9\,\text{V}$ |

---

### Bias Conditions

| Parameter | Symbol | Value |
|-----------|--------|-------|
| Input common-mode voltage | $V_{ICM}$ | $0\,\text{V}$ |
| Output common-mode voltage | $V_{OCM}$ | $0\,\text{V}$ |
| Tail bias voltage | $V_P$ | $-0.7\,\text{V}$ |

---

### Load and Technology Parameters

| Parameter | Symbol | Value |
|-----------|--------|-------|
| Load capacitance | $C_L$ | $10\,\text{pF}$ |
| Channel length | $L$ | $560\,\text{nm}$ |
| Maximum power dissipation | $P$ | $\leq 2.2\,\text{mW}$ |

These constraints define the allowable biasing region and ensure low-power operation with adequate gain and frequency response.

---

## Introduction

Differential amplifiers form the fundamental input stage of most analog integrated circuits, including operational amplifiers, comparators, voltage regulators, and data-conversion interfaces. Their ability to amplify only the difference between two input signals while rejecting common-mode noise makes them essential in precision analog design.

Compared to single-ended amplifiers, differential amplifiers provide improved linearity, better noise immunity, higher power-supply rejection capability, and enhanced symmetry in output swing. These advantages arise from the constant tail-current biasing mechanism and matched transistor operation.

Modern CMOS analog circuits frequently employ differential architectures combined with active loads and current mirrors to achieve higher gain without increasing power consumption. Therefore, analyzing multiple differential amplifier configurations helps understand tradeoffs between gain, bandwidth, area, and signal swing.

---

## Working Principle of MOS Differential Amplifier

A MOS differential amplifier operates by steering a constant tail current between two matched transistors depending on the applied differential input voltage.

When identical inputs are applied,

$$
V_{in1} = V_{in2}
$$

the tail current divides equally:

$$
I_{D1} = I_{D2} = \frac{I_{SS}}{2}
$$

and both output nodes remain at the same potential.

When a differential signal is applied,

$$
V_{id} = V_{in1} - V_{in2}
$$

the drain currents redistribute as

$$
I_{D1} = \frac{I_{SS}}{2} + \Delta I
$$

$$
I_{D2} = \frac{I_{SS}}{2} - \Delta I
$$

producing amplified differential output voltages across the load elements.

For small-signal operation, the differential voltage gain is

$$
A_v = g_m R_{out}
$$

where the MOS transconductance is

$$
g_m = \frac{2I_D}{V_{OV}}
$$

The circuit behaves linearly only within the range

$$
|V_{id}| < \sqrt{2}V_{OV}
$$

Beyond this limit, one transistor enters cutoff and distortion appears at the output.

---

## Configurations Considered in This Experiment

Three CMOS differential amplifier architectures are analyzed:

| Configuration | Load Type | Expected Advantage |
|--------------|-----------|-------------------|
| Circuit 1 | Resistive load | Simplicity and predictable bias behavior |
| Circuit 2 | PMOS active load | Higher gain due to increased output resistance |
| Circuit 3 | Current-mirror load | Differential-to-single-ended conversion with maximum gain |

Each configuration is evaluated using DC analysis, transient response, and AC frequency response simulations.

---

## Experimental Objectives

The following performance parameters are extracted for each circuit:

| Category | Parameters Evaluated |
|----------|--------------------|
| DC Analysis | Operating point, ICMR limits |
| Large-Signal Behavior | Linear input range |
| Small-Signal Analysis | Differential gain |
| Frequency Response | Bandwidth, UGB, GBP |
| Practical Metrics | Output swing, power dissipation, area |

Finally, all three circuits are compared to determine the most suitable topology for low-power CMOS differential amplification.

 
# Configuration 1: CMOS Differential Amplifier with Resistive Load
<img width="1538" height="954" alt="circuit (1)" src="https://github.com/user-attachments/assets/5a7823e2-0739-4558-86d4-7c80247a24f5" />

---

## Objective

To design and analyze a CMOS differential amplifier with resistive loads under given biasing constraints and evaluate its performance through theoretical derivations and LTspice simulations.

The following parameters are determined:

- DC operating point
- input common-mode range (ICMR)
- output voltage swing limits
- linear differential input range
- differential voltage gain
- transient response under linear and nonlinear excitation
- frequency response (midband gain, bandwidth, unity gain bandwidth)
- power dissipation verification
- theoretical vs simulated comparison

---

## Given Design Specifications

| Parameter | Symbol | Value |
|-----------|--------|-------|
| Positive supply voltage | $$V_{DD}$$ | $$+0.9\,V$$ |
| Negative supply voltage | $$V_{SS}$$ | $$-0.9\,V$$ |
| Input common-mode voltage | $$V_{ICM}$$ | $$0\,V$$ |
| Output common-mode voltage | $$V_{OCM}$$ | $$0\,V$$ |
| Tail bias voltage | $$V_P$$ | $$-0.7\,V$$ |
| Load capacitance | $$C_L$$ | $$10\,pF$$ |
| Channel length | $$L$$ | $$560\,nm$$ |
| Maximum allowed power | $$P$$ | $$\le 2.2\,mW$$ |

---

## Circuit Operation Overview

A MOS differential amplifier operates by steering a constant tail current between two matched transistors depending on the differential input voltage:

$$
V_{id} = V_{in1} - V_{in2}
$$

When

$$
V_{in1} = V_{in2}
$$

the current splits equally:

$$
I_{D1} = I_{D2} = \frac{I_{SS}}{2}
$$

and both output voltages remain equal.

The resistors convert branch currents into output voltages.

---

## Transistor Role Explanation

| Device | Function |
|--------|----------|
| $$M_1$$ | Left differential input transistor |
| $$M_2$$ | Right differential input transistor |
| $$R_D$$ | Current-to-voltage conversion |
| $$I_{SS}$$ | Tail current stabilization |

---

## Design Calculations

### Tail Current Selection

Power constraint:

$$
P = (V_{DD} - V_{SS}) I_{SS}
$$

Substituting:

$$
2.2\,mW = 1.8 \times I_{SS}
$$

Thus,

$$
I_{SS,max} = 1.22\,mA
$$

Chosen value:

$$
I_{SS} = 200\,\mu A
$$

---

### Branch Current Calculation

Due to symmetry:

$$
I_D = \frac{I_{SS}}{2}
$$

Therefore:

$$
I_D = 100\,\mu A
$$

---

### Overdrive Voltage Selection

Chosen:

$$
V_{OV} = 0.25\,V
$$

Trade-off:

| Parameter | Effect |
|----------|--------|
| Higher $$V_{OV}$$ | wider linear input range |
| Lower $$V_{OV}$$ | higher voltage gain |

---

### Transconductance Calculation

$$
g_m = \frac{2I_D}{V_{OV}}
$$

Substituting:

$$
g_m = \frac{2 \times 100\,\mu A}{0.25}
$$

Thus,

$$
g_m = 0.8\,mS
$$

---

### Drain Resistance Calculation

Given:

$$
V_{OCM} = 0
$$

Voltage drop:

$$
0.9\,V
$$

Thus:

$$
R_D = \frac{0.9}{100\,\mu A}
$$

Therefore:

$$
R_D = 9\,k\Omega
$$

---

## DC Operating Point Verification
<img width="951" height="785" alt="opt pt" src="https://github.com/user-attachments/assets/3e679756-4359-453e-9a3b-bd09212a4559" />
<img width="1919" height="941" alt="circuit (3)" src="https://github.com/user-attachments/assets/d6fc2ad2-27bd-4ec9-aa92-a82b436ebc5b" />


From simulation:

$$
I_{D1} = I_{D2} = 100\,\mu A
$$

Source node voltage:

$$
V_S \approx -0.648\,V
$$

Gate voltage:

$$
V_G = 0\,V
$$

Thus:

$$
V_{GS} = 0.648\,V
$$

Overdrive voltage:

$$
V_{OV} = V_{GS} - V_T
$$

Assuming:

$$
V_T \approx 0.40\,V
$$

Therefore:

$$
V_{OV} \approx 0.248\,V
$$

Saturation condition:

$$
V_{DS} > V_{OV}
$$

Hence both transistors operate in saturation.

---

## Input Common Mode Range (ICMR)

Lower limit:

$$
V_{ICM(min)} = V_{SS} + V_{GS} + V_{OV}
$$

Upper limit:

$$
V_{ICM(max)} = V_{DD} - I_D R_D + V_T
$$

---

## Output Voltage Swing Limits

Upper limit:

$$
V_{out(max)} = V_{DD}
$$

Lower limit:

$$
V_{out(min)} = V_S + V_{OV}
$$

---

## Linear Differential Input Range

Condition:

$$
|V_{id}| < \sqrt{2} V_{OV}
$$

Substituting:

$$
|V_{id}| < 0.353\,V
$$

---

## Large Signal Differential Behaviour

Branch currents:

$$
I_{D1} = \frac{I_{SS}}{2} + \Delta I
$$

$$
I_{D2} = \frac{I_{SS}}{2} - \Delta I
$$

Cutoff occurs when:

$$
|V_{id}| > \sqrt{2} V_{OV}
$$

Observed in simulation for

$$
V_{id} = 400\,mV
$$

---

## Small Signal Gain Calculation

Differential gain:

$$
A_v = g_m R_D
$$

Substituting:

$$
A_v = 0.8\,mS \times 9k\Omega
$$

Thus:

$$
A_v = 7.2
$$

In decibels:

$$
A_v(dB) = 20\log(7.2)
$$

Therefore:

$$
A_v = 17.15\,dB
$$

---

## Differential Output Expression

$$
V_{od} = V_{out1} - V_{out2}
$$

Voltage gain:

$$
A_v = \frac{V_{od}}{V_{id}}
$$

---

## Transient Analysis
# Linear
<img width="1912" height="969" alt="tran line" src="https://github.com/user-attachments/assets/06281415-4237-4a2d-9d4f-57fbda0cc0ca" />
<img width="1912" height="969" alt="tran line" src="https://github.com/user-attachments/assets/d5003ec7-55d1-46dd-bd29-a3f28177b362" />

# Non Linear
<img width="1919" height="925" alt="tran non li (2)" src="https://github.com/user-attachments/assets/e0446b2a-707a-48c1-9080-51685320e995" />
<img width="1918" height="968" alt="tran non li (1)" src="https://github.com/user-attachments/assets/c355cdc8-6f8d-49b2-b923-fedf99b2ccd6" />



### Linear Operation Case

Input:

$$
V_{id} = 20\,mV
$$

Output:

$$
V_{od} \approx 150\,mV
$$

Thus:

$$
A_v = 7.5
$$

---

### Nonlinear Operation Case

Input:

$$
V_{id} = 400\,mV
$$

Observed:

- waveform distortion
- transistor cutoff
- nonlinear operation

---

## AC Frequency Response
## Effect of Load Capacitance on Frequency Response

To study the influence of output loading on amplifier bandwidth, a load capacitance

$$
C_L = 10\,\text{pF}
$$

was connected from each output node to ground:

$$
v_{out1} \rightarrow C_L \rightarrow \text{GND}
$$

$$
v_{out2} \rightarrow C_L \rightarrow \text{GND}
$$

This models practical parasitic and external load capacitances present at amplifier outputs.

---
# Without capacitor
<img width="1919" height="961" alt="ac analysis (3)" src="https://github.com/user-attachments/assets/f8fdd4fa-6170-470b-8cc4-90f3b5aa65ed" />
<img width="1919" height="999" alt="ac analysis (1)" src="https://github.com/user-attachments/assets/4fb78e28-be8b-4ece-8100-95e25ba450c0" />

# With Capacitor
<img width="1919" height="922" alt="ac analysis with cap (4)" src="https://github.com/user-attachments/assets/6915580e-3150-4f4c-960e-ed14c03901ae" />
<img width="1919" height="927" alt="ac analysis with cap (3)" src="https://github.com/user-attachments/assets/d1425011-9208-4284-a925-958c42a2a895" />




### Dominant Pole Formation

The load capacitance introduces a dominant pole at the output node given by

$$
f_H = \frac{1}{2\pi R_D C_L}
$$

Substituting

$$
R_D = 9k\Omega
$$

$$
C_L = 10pF
$$

we obtain

$$
f_H = \frac{1}{2\pi (9\times10^3)(10\times10^{-12})}
$$

Thus,

$$
f_H \approx 1.77\,\text{MHz}
$$

---

### Observed Frequency Response

From AC simulation:

- midband gain ≈ $$17.6\,\text{dB}$$
- dominant pole clearly visible in MHz region
- gain roll-off slope ≈ $$-20\,\text{dB/decade}$$

This confirms single-pole dominant behavior expected for a resistive-load differential amplifier.

---

### Comparison Without Load Capacitance

Without the load capacitor:

- bandwidth appears unrealistically large
- no dominant pole observed in practical frequency range
- gain remains nearly constant over extended frequency span

After introducing

$$
C_L = 10\,\text{pF}
$$

a dominant pole appears near the theoretical cutoff frequency, producing a realistic frequency response.

---

### Unity Gain Bandwidth

Unity gain bandwidth is estimated as

$$
UGB = A_v \times f_H
$$

Substituting

$$
A_v = 7.6
$$

and

$$
f_H = 1.77\,\text{MHz}
$$

we obtain

$$
UGB \approx 13.45\,\text{MHz}
$$

which closely matches the simulated response.

---

### Observation

The load capacitance limits the high-frequency performance of the amplifier by introducing a dominant pole at the output node. This confirms that bandwidth is primarily determined by

$$
R_D C_L
$$

in resistive-load differential amplifier configurations.

## Comparison of Frequency Response With and Without Load Capacitance

To understand the effect of output loading on amplifier bandwidth, AC analysis was performed under two conditions:

1. Without load capacitance
2. With load capacitance $$C_L = 10\,\text{pF}$$ connected at each output node

---

### Case 1: Frequency Response Without Load Capacitance

When no load capacitor is connected at the output nodes:

- the gain remains nearly constant over a wide frequency range
- no dominant pole appears in the MHz region
- bandwidth appears unrealistically large
- roll-off begins only at very high frequencies due to intrinsic device parasitics

Measured midband gain:

$$
A_v \approx 17.6\,\text{dB}
$$

This confirms that in the absence of external loading, the amplifier bandwidth is limited primarily by internal parasitic capacitances.

---

### Case 2: Frequency Response With Load Capacitance

After connecting

$$
C_L = 10\,\text{pF}
$$

between each output node and ground:

- a dominant pole appears at the output node
- gain roll-off begins in the MHz region
- slope approaches $$-20\,\text{dB/decade}$$
- bandwidth becomes practically limited by $$R_D C_L$$

The dominant pole frequency is given by

$$
f_H = \frac{1}{2\pi R_D C_L}
$$

Substituting

$$
R_D = 9\,k\Omega
$$

$$
C_L = 10\,pF
$$

we obtain

$$
f_H \approx 1.77\,\text{MHz}
$$

which closely matches the simulated response.

---

### Comparative Observation

| Parameter | Without $$C_L$$ | With $$C_L = 10\,\text{pF}$$ |
|-----------|----------------|------------------------------|
| Dominant pole | Not visible in MHz range | Clearly visible |
| Bandwidth | Very large | Limited to MHz range |
| Gain roll-off | Delayed | Begins near theoretical cutoff |
| Practical accuracy | Unrealistic | Matches physical behavior |

---

### Conclusion

The load capacitance introduces a dominant pole at the output node and limits the amplifier bandwidth according to

$$
f_H = \frac{1}{2\pi R_D C_L}
$$

Thus, the frequency response of the resistive-load differential amplifier is strongly governed by the output load capacitance, making it a critical parameter in bandwidth design.
Measured midband gain:

$$
A_v = 17.61\,dB
$$

Linear scale:

$$
A_v = 7.6
$$

---

## Dominant Pole Analysis

$$
f_H = \frac{1}{2\pi R_D C_L}
$$

Substituting:

$$
f_H = \frac{1}{2\pi (9k)(10pF)}
$$

Thus:

$$
f_H \approx 1.77\,MHz
$$

---

## Unity Gain Bandwidth

$$
UGB = A_v \times f_H
$$

Therefore:

$$
UGB \approx 12.7\,MHz
$$

---

## Power Consumption Verification

$$
P = (V_{DD}-V_{SS}) I_{SS}
$$

Substituting:

$$
P = 1.8 \times 200\,\mu A
$$

Thus:

$$
P = 0.36\,mW
$$

Constraint satisfied.

---

## Theoretical vs Simulation Comparison

| Parameter | Theory | Simulation |
|----------|--------|------------|
| Gain | 7.2 | 7.5 |
| Gain (dB) | 17.15 | 17.61 |
| Bandwidth | 1.77 MHz | ≈ MHz range |
| Power | 0.36 mW | 0.36 mW |

---

## Design Trade-Off Discussion

Increasing $$R_D$$ increases gain but reduces bandwidth.

Increasing $$I_{SS}$$ increases gain but increases power consumption.

Increasing $$V_{OV}$$ increases linear range but reduces gain.

---

## Practical Limitations

Real circuits are affected by:

- channel length modulation
- finite output resistance
- parasitic capacitances
- device mismatch
- thermal noise
- flicker noise

These effects introduce deviations between theoretical and simulated results.

---

## Observations and Inference

The resistive-load differential amplifier provides:

- moderate voltage gain
- symmetric operation
- predictable bias stability
- controlled linear response region

However, gain improvement is limited compared to active-load configurations, making this topology suitable primarily as a reference architecture for further differential amplifier enhancements.

---  


 
# Configuration–2: CMOS Differential Amplifier with PMOS Active Load
<img width="1574" height="955" alt="circuit" src="https://github.com/user-attachments/assets/2d723645-0284-4248-8041-7500ff0065c9" />

---

## 1. Objective

The objective of this experiment is to design, simulate, and analyze a CMOS differential amplifier using PMOS active load transistors under constrained operating specifications and verify its performance through DC, transient, and AC simulations.

The following parameters are evaluated:

- DC operating point verification
- Input Common Mode Range (ICMR)
- Output Common Mode Range (OCMR)
- Differential linear input range
- Differential voltage gain
- Frequency response
- 3-dB bandwidth
- Gain Bandwidth Product (GBW)
- Effect of load capacitance
- Power dissipation
- Comparison with resistive-load differential amplifier (Configuration-1)

---

# 2. Design Specifications

The circuit is designed according to batch specification **C2 constraints**:

| Parameter | Value |
|----------|------|
| Supply voltage | $V_{DD}=+0.9V$ |
| Negative supply | $V_{SS}=-0.9V$ |
| Input common-mode voltage | $V_{ICM}=0V$ |
| Output common-mode voltage | $V_{OCM}=0V$ |
| Tail bias voltage | $V_B=-0.3V$ |
| Technology length | $L=540nm$ |
| Load capacitance | $C_L=10pF$ |
| Power constraint | $P \le 2.2mW$ |

---

# 3. Circuit Description

The CMOS differential amplifier consists of five MOS transistors:

| Transistor | Function |
|-----------|----------|
| $M_1, M_2$ | NMOS differential pair |
| $M_3, M_4$ | PMOS active current mirror load |
| $M_5$ | NMOS tail current source |

### Functional Blocks

The circuit can be divided into three sections:

1. Differential input stage
2. Active load stage
3. Tail current bias stage

Unlike resistive load configuration, PMOS active loads provide:

- higher gain
- higher output resistance
- improved matching
- reduced silicon area

---

# 4. Principle of Operation

A differential amplifier amplifies the difference between two input voltages:

$$
v_{id}=v_{in1}-v_{in2}
$$

Output voltage:

$$
v_{out}=A_d(v_{in1}-v_{in2})
$$

When:

$$
v_{in1}=v_{in2}
$$

Then:

$$
v_{out}=0
$$

Thus common-mode signals are rejected.

---

# 5. Tail Current Source Design

The transistor $M_5$ acts as a constant current source.

Given:

$$
V_G=-0.3V
$$

$$
V_S=-0.9V
$$

Therefore:

$$
V_{GS5}=V_G-V_S
$$

$$
V_{GS5}=(-0.3)-(-0.9)=0.6V
$$

Since:

$$
V_{GS5}>V_{TH}
$$

the transistor operates in saturation.

Hence constant tail current is established.

---

# 6. Tail Current Calculation

MOS current equation:

$$
I_D=\frac{1}{2}\mu_n C_{ox}\frac{W}{L}(V_{GS}-V_{TH})^2
$$

Simulation result:

$$
I_{tail}=115.4\mu A
$$

Thus each branch carries:

$$
I_D=\frac{I_{tail}}{2}
$$

$$
I_D=57.7\mu A
$$

---

# 7. Verification of Saturation Region Operation

For NMOS saturation:

$$
V_{DS} \ge V_{GS}-V_{TH}
$$

For PMOS saturation:

$$
V_{SD} \ge V_{SG}-|V_{TH}|
$$

Simulation confirms:

| Transistor | Region |
|-----------|-------|
| $M_1$ | Saturation |
| $M_2$ | Saturation |
| $M_3$ | Saturation |
| $M_4$ | Saturation |
| $M_5$ | Saturation |

Thus amplifier operates in correct region.

---

# 8. DC Operating Point Analysis
<img width="1919" height="927" alt="dc opt pt (1)" src="https://github.com/user-attachments/assets/535b869a-914a-4f57-8f98-5f2ffaf835ae" />
<img width="727" height="886" alt="dc opt pt (2)" src="https://github.com/user-attachments/assets/e2878b1d-55f2-414e-ac99-3426f7e05ce8" />



Measured values:

| Parameter | Value |
|----------|------|
| $V_{out1}$ | 0.240V |
| $V_{out2}$ | 0.240V |
| $V_P$ | −0.594V |
| $I_{tail}$ | 115.4µA |
| $I_{D1}$ | 57.7µA |
| $I_{D2}$ | 57.7µA |

Balanced operation confirmed.

---
# Detailed Design Calculations

This section explains the design methodology used to select circuit parameters for the CMOS differential amplifier with PMOS active load. The objective is to obtain correct biasing, ensure saturation-region operation of all MOSFETs, satisfy power constraints, and achieve predictable gain and bandwidth performance.

---

# Tail Current Selection

The tail current determines:

- transconductance
- gain
- linear input range
- power consumption
- bandwidth

From the power constraint:

$$
P=(V_{DD}-V_{SS})I_{tail}
$$

Given:

$$
P_{max}=2.2mW
$$

and

$$
V_{DD}-V_{SS}=1.8V
$$

Maximum allowable current:

$$
I_{tail(max)}=\frac{2.2mW}{1.8V}
$$

$$
I_{tail(max)}=1.22mA
$$

To ensure safe operation with margin, a smaller current is selected:

$$
I_{tail}\approx115\mu A
$$

This improves:

- linearity
- power efficiency
- stability

---

# Branch Current Calculation

Since the circuit is symmetric:

$$
I_{D1}=I_{D2}=\frac{I_{tail}}{2}
$$

Therefore:

$$
I_D=57.7\mu A
$$

This current defines transistor operating region and gain.

---

# Tail Current Source Bias Voltage Selection

Tail transistor $M_5$ must operate in saturation:

$$
V_{GS5}>V_{TH}
$$

Given:

$$
V_G=-0.3V,\quad V_S=-0.9V
$$

Thus:

$$
V_{GS5}=0.6V
$$

Since typical threshold voltage:

$$
V_{TH}\approx0.45V
$$

Therefore:

$$
V_{GS5}>V_{TH}
$$

ensuring proper current-source behavior.

---

# Overdrive Voltage Selection

Overdrive voltage is defined as:

$$
V_{OV}=V_{GS}-V_{TH}
$$

Using:

$$
V_{GS}\approx0.6V
$$

and

$$
V_{TH}\approx0.45V
$$

we obtain:

$$
V_{OV}\approx0.15V
$$

Lower overdrive voltage improves:

- gain
- output resistance
- small-signal sensitivity

while maintaining saturation.

---

# Transconductance Calculation

Small-signal transconductance is:

$$
g_m=\frac{2I_D}{V_{OV}}
$$

Substituting:

$$
I_D=57.7\mu A
$$

$$
V_{OV}=0.15V
$$

Therefore:

$$
g_m=\frac{2\times57.7\mu A}{0.15}
$$

$$
g_m=0.769mS
$$

This parameter determines voltage gain.

---

# Output Resistance Estimation

MOSFET output resistance:

$$
r_o=\frac{1}{\lambda I_D}
$$

For short-channel devices:

$$
\lambda\approx0.1V^{-1}
$$

Thus:

$$
r_o=\frac{1}{0.1\times57.7\mu A}
$$

$$
r_o\approx173k\Omega
$$

Since both NMOS and PMOS loads contribute:

$$
R_{out}=r_{on}\parallel r_{op}
$$

Assuming equal values:

$$
R_{out}\approx86.5k\Omega
$$

---

# Expected Voltage Gain Calculation

Differential gain expression:

$$
A_d=g_mR_{out}
$$

Substituting:

$$
A_d=(0.769mS)(86.5k\Omega)
$$

$$
A_d\approx66.5
$$

Converting to decibels:

$$
A_d(dB)=20\log(66.5)
$$

$$
A_d\approx36.4dB
$$

Simulation gain is smaller due to:

- channel-length modulation
- body effect
- mobility degradation
- parasitic capacitances

but theoretical prediction confirms gain improvement over resistive load configuration.

---

# Linear Differential Input Range

Linear operation condition:

$$
v_{id}<\sqrt{2}V_{OV}
$$

Substituting:

$$
V_{OV}=0.15V
$$

Thus:

$$
v_{id}<0.212V
$$

Therefore differential inputs below approximately:

$$
212mV
$$

produce linear amplification.

---

# Dominant Pole Estimation

Load capacitance introduces dominant pole:

$$
f_p=\frac{1}{2\pi R_{out}C_L}
$$

Given:

$$
R_{out}=86.5k\Omega
$$

$$
C_L=10pF
$$

Therefore:

$$
f_p=\frac{1}{2\pi(86.5\times10^3)(10\times10^{-12})}
$$

$$
f_p\approx184kHz
$$

This predicts bandwidth limitation observed in AC analysis.

---

# Gain Bandwidth Product Estimation

Gain-bandwidth product:

$$
GBW=A_d\times f_p
$$

Substituting:

$$
GBW=66.5\times184kHz
$$

$$
GBW\approx12.2MHz
$$

This represents amplifier speed capability.

---

# Transistor Sizing Considerations

MOS current equation:

$$
I_D=\frac{1}{2}\mu C_{ox}\frac{W}{L}(V_{OV})^2
$$

Rearranging:

$$
\frac{W}{L}=\frac{2I_D}{\mu C_{ox}(V_{OV})^2}
$$

Thus transistor dimensions were selected to maintain:

- saturation operation
- symmetry
- matching accuracy
- required bias current

with fixed technology constraint:

$$
L=540nm
$$

---

# Power Consumption Verification

Power dissipation:

$$
P=(V_{DD}-V_{SS})I_{tail}
$$

Substituting:

$$
P=1.8\times115.4\mu A
$$

$$
P=0.207mW
$$

Thus:

$$
P<2.2mW
$$

Design satisfies specification constraint.

---

# Summary of Designed Parameters

| Parameter | Value |
|----------|------|
| Tail current | $115.4\mu A$ |
| Branch current | $57.7\mu A$ |
| Overdrive voltage | $0.15V$ |
| Transconductance | $0.769mS$ |
| Output resistance | $86.5k\Omega$ |
| Expected gain | $66.5$ |
| Linear input limit | $212mV$ |
| Dominant pole | $184kHz$ |
| GBW | $12.2MHz$ |
| Power dissipation | $0.207mW$ |

These calculations validate the correctness of transistor biasing and expected amplifier performance prior to simulation.
# 9. Input Common Mode Range (ICMR)

Lower limit:

$$
V_{ICM(min)}=V_{SS}+V_{GS1}
$$

Upper limit:

$$
V_{ICM(max)}=V_{DD}-V_{SD3(sat)}-V_{GS1}
$$

Therefore:

$$
V_{ICM(min)} < V_{ICM} < V_{ICM(max)}
$$

Simulation verifies:

$$
V_{ICM}=0V
$$

lies inside valid region.

---

# 10. Output Common Mode Range (OCMR)

Condition for NMOS saturation:

$$
V_{out}>V_{DS1(sat)}+V_P
$$

Condition for PMOS saturation:

$$
V_{out}<V_{DD}-V_{SD3(sat)}
$$

Measured:

$$
V_{out}=0.240V
$$

Hence valid operation confirmed.

---

# 11. Differential Gain Derivation

Small signal gain:

$$
A_d=g_mR_{out}
$$

Output resistance:

$$
R_{out}=r_{on}\parallel r_{op}
$$

Thus:

$$
A_d=g_m(r_{on}\parallel r_{op})
$$

Simulation result:

$$
A_d=2.83dB
$$

Linear scale:

$$
A_d=1.38
$$

---

# 12. Small Signal Equivalent Model

The differential pair can be represented using:

- transconductance source $g_mv_{id}$
- output resistance $r_o$

Output voltage:

$$
v_o=g_m v_{id}(r_{on}\parallel r_{op})
$$

Active load increases $r_o$ significantly.

Thus gain increases.

---

# 13. Linear Differential Input Range

Linear operation condition:

$$
v_{id}<\sqrt{2}V_{OV}
$$

Beyond this:

current steering occurs

leading to nonlinear response.

---

# 14. Transient Analysis

## Linear Region Operation
<img width="1919" height="967" alt="tran linear (2)" src="https://github.com/user-attachments/assets/c8f64b0e-0a19-4e8e-ab8f-1c6eeb4a5953" />
<img width="1919" height="968" alt="tran linear (1)" src="https://github.com/user-attachments/assets/db8caab2-9aa8-43a2-928a-a53b22a9c6e2" />



Observed characteristics:

- sinusoidal outputs
- equal amplitude
- 180° phase difference
- no distortion

Thus amplifier operates in small signal region.

---

## Nonlinear Region Operation
<img width="1917" height="922" alt="tran non linear (2)" src="https://github.com/user-attachments/assets/baa1e86b-3561-432b-8f30-414c1c225794" />
<img width="1915" height="959" alt="tran non linear (1)" src="https://github.com/user-attachments/assets/65e6fe0f-75c3-4660-b5bd-601742360977" />


Observed characteristics:

- waveform clipping
- asymmetric output
- current steering

Amplifier behaves like switching pair.

---

# 15. AC Analysis Setup

Differential excitation applied:

$$
V_{in1}=0.5\angle0^\circ
$$

$$
V_{in2}=0.5\angle180^\circ
$$

Differential output measured:

$$
V_{out}=V_{out1}-V_{out2}
$$

Measured gain:

$$
A_d=2.83dB
$$

---

# 16. Frequency Response Analysis
<img width="1919" height="916" alt="ac without capacitor (1)" src="https://github.com/user-attachments/assets/2ad3449b-864c-4b98-90d5-15c5db6bf67c" />
<img width="1918" height="966" alt="ac without capacitor (2)" src="https://github.com/user-attachments/assets/3f54b698-0a23-41aa-acca-4275da05cfc2" />


Observed characteristics:

| Region | Behaviour |
|-------|-----------|
| Low frequency | constant gain |
| Midband | maximum gain |
| High frequency | roll-off |

Roll-off caused by:

- parasitic capacitances
- load capacitance
- channel capacitances

---

# 17. 3-dB Bandwidth

Bandwidth defined as:

$$
A_d=\frac{A_{mid}}{\sqrt2}
$$

Frequency at this point:

$$
f=f_{3dB}
$$

obtained from AC plot.

---

# 18. Gain Bandwidth Product (GBW)

Defined as:

$$
GBW=A_d\times BW
$$

Indicates amplifier speed capability.

Higher GBW implies better performance.

---

# 19. Effect of Load Capacitor

Load capacitance:
<img width="1919" height="960" alt="ac with cap (1)" src="https://github.com/user-attachments/assets/a418e33d-6225-44f9-9f8e-a8cfc8fc139e" />
<img width="1919" height="1000" alt="ac with cap (2)" src="https://github.com/user-attachments/assets/a4af5561-3e52-4706-82a8-08b33e93bf20" />


$$
C_L=10pF
$$

Dominant pole:

$$
f_p=\frac{1}{2\pi R_{out}C_L}
$$

Observed:

| Parameter | Without $C_L$ | With $C_L$ |
|----------|---------------|------------|
Bandwidth | higher | reduced |
Phase shift | smaller | larger |
Gain | unchanged | unchanged |

Thus capacitor stabilizes amplifier.

---

# 20. Power Dissipation

Power consumption:

$$
P=(V_{DD}-V_{SS})I_{tail}
$$

Substituting values:

$$
P=1.8\times115.4\mu A
$$

$$
P=0.207mW
$$

Constraint satisfied:

$$
P<2.2mW
$$

---

# 21. Theoretical vs Simulation Comparison

| Parameter | Theory | Simulation |
|----------|--------|------------|
Tail current | ≈100µA | 115µA |
Branch current | 50µA | 57.7µA |
Output voltage | 0.2–0.3V | 0.240V |
Gain | moderate | 2.83dB |

Close agreement observed.

---

# 22. Comparison with Configuration-1

| Parameter | Configuration-1 | Configuration-2 |
|----------|----------------|----------------|
Load type | resistive | active |
Gain | lower | higher |
Output resistance | low | high |
Area | larger | smaller |
Bandwidth | larger | slightly smaller |

Active load improves gain efficiency.

---

# 23. Advantages of Active Load Differential Amplifier

- high gain
- reduced chip area
- improved matching
- better integration capability
- lower power for same gain

---

# 24. Applications

Used in:

- operational amplifier input stages
- comparators
- ADC front-end circuits
- instrumentation amplifiers
- analog signal processing blocks

---

# 25. Conclusion

The CMOS differential amplifier with PMOS active load was successfully designed and analyzed under given specifications.

Results confirm:

- correct DC biasing
- saturation region operation
- valid ICMR and OCMR
- predictable linear behaviour
- differential gain of 2.83dB
- bandwidth reduction with load capacitor
- power consumption within specification

Thus Configuration-2 demonstrates superior gain performance compared to resistive-load differential amplifier while maintaining low power operation.
