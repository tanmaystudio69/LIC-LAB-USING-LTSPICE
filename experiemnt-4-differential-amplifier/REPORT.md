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
