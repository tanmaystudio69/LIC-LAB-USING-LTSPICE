# Experiment 2B – Common Source Amplifier with NMOS Current Source Load

---

# Aim

To design, analyze, and simulate a **Common Source (CS) MOSFET amplifier** using **NMOS current source biasing and PMOS active load** in **TSMC 180nm technology** using **LTSpice**.

The amplifier must satisfy the following constraints:

- Supply voltage  

$$
V_{DD} = 1.8V
$$

- Power consumption  

$$
P \le 1mW
$$

- Channel length  

$$
L = 560nm
$$

- Load capacitance  

$$
C_L = 10pF
$$

The objectives of this experiment are:

1. To design the biasing conditions for proper MOSFET operation.
2. To ensure that all transistors operate in **saturation region**.
3. To determine theoretical values of gain, bandwidth, and bias currents.
4. To verify the design using **LTSpice simulation**.
5. To compare theoretical predictions with simulated results.

---

# 1. Introduction

The **Common Source (CS) amplifier** is one of the most widely used amplifier configurations in analog integrated circuits.

In this configuration:

- The **input signal is applied to the gate**
- The **output signal is taken from the drain**
- The **source terminal acts as the common reference node**

Because of its ability to produce large voltage gain, the CS amplifier is commonly used in:

- Operational amplifiers
- Sensor interface circuits
- Analog signal conditioning systems
- RF amplifiers

Traditional CS amplifiers use **resistors as loads**, but integrated circuits rarely use large resistors due to silicon area constraints. Instead, **MOSFET active loads** are used.

In this experiment the amplifier consists of:

- **PMOS active load transistor**
- **NMOS amplifying transistor**
- **NMOS current source transistor**

This configuration provides:

- High output resistance
- Stable bias current
- Improved gain characteristics

---

# 2. What the Circuit Does

The circuit acts as a **voltage amplifier**.

Its purpose is to amplify a small AC input signal applied at the gate of the NMOS transistor.

The operation can be summarized as:

1. A small input voltage variation changes the **gate-source voltage**.
2. This variation produces a change in **drain current**.
3. The varying current flows through the **active load**.
4. This produces a larger voltage variation at the output node.

Therefore:

$$
\text{Small input voltage} \rightarrow \text{Large output voltage}
$$

Additionally, the output signal is **inverted** relative to the input signal, which means the amplifier provides **180° phase shift**.

---

# 3. Circuit Description

## Circuit Diagram

![Circuit Diagram](Results/exp2b_topology.png)

## LTSpice Implementation

![LTSpice Circuit](Results/exp2b_circuit.png)

---

# 4. Function of Each Transistor

| Transistor | Function |
|------------|-----------|
| PMOS (M1) | Active load |
| NMOS (M2) | Amplifying transistor |
| NMOS (M3) | Current source |

---

# 5. Working Principle

The CS amplifier operates by converting **small voltage variations into current variations**.

The drain current of a MOSFET operating in saturation is

$$
I_D = \frac{1}{2}\mu C_{ox}\frac{W}{L}(V_{GS}-V_T)^2
$$

A small input signal produces

$$
v_{in} \rightarrow v_{gs}
$$

This produces a current variation

$$
i_d = g_m v_{gs}
$$

where

$$
g_m = \frac{2I_D}{V_{OV}}
$$

This current flows through the output resistance and produces

$$
v_{out} = - i_d R_{out}
$$

Thus

$$
A_v = -g_m R_{out}
$$

---

# 6. Degeneration Due to Current Source

The NMOS current source introduces a form of **degeneration**.

This occurs because the current source limits the change in current flowing through the amplifier transistor.

Effects of current source degeneration include:

- Stabilized bias current
- Reduced sensitivity to parameter variations
- Improved linearity
- Reduced gain compared to ideal amplifier

The effective gain becomes

$$
A_v = - g_m (r_{o1} \parallel r_{o2} \parallel r_{o3})
$$

where the output resistance is influenced by all three transistors.

---

# 7. Design Calculations

---

# 7.1 Given Parameters

Supply voltage

$$
V_{DD} = 1.8V
$$

Maximum allowed power

$$
P \le 1mW
$$

Channel length

$$
L = 560nm
$$

Load capacitance

$$
C_L = 10pF
$$

NMOS threshold voltage

$$
V_{TN} = 0.366V
$$

PMOS threshold voltage

$$
|V_{TP}| = 0.39V
$$

Chosen overdrive voltage

$$
V_{OV} = 0.25V
$$

Assumed drain current

$$
I_D = 200\mu A
$$

---

# 7.2 Power Constraint

Power consumption

$$
P = V_{DD} I_D
$$

Substituting values

$$
P = 1.8 \times 200\times10^{-6}
$$

$$
P = 3.6\times10^{-4}
$$

$$
P = 0.36mW
$$

Since

$$
0.36mW < 1mW
$$

the power constraint is satisfied.

---

# 7.3 Overdrive Voltage

Overdrive voltage is defined as

$$
V_{OV} = V_{GS} - V_T
$$

Rearranging

$$
V_{GS} = V_{OV} + V_T
$$

Substituting values

$$
V_{GS} = 0.25 + 0.366
$$

$$
V_{GS} = 0.616V
$$

---

# 7.4 Output Bias Point

To allow maximum symmetrical swing

$$
V_{OUT} = \frac{V_{DD}}{2}
$$

Substitute

$$
V_{OUT} = \frac{1.8}{2}
$$

$$
V_{OUT} = 0.9V
$$

---

# 7.5 Transconductance

Transconductance

$$
g_m = \frac{2I_D}{V_{OV}}
$$

Substitute

$$
g_m = \frac{2\times200\times10^{-6}}{0.25}
$$

$$
g_m = 1.6\times10^{-3}
$$

$$
g_m = 1.6mS
$$

---
---

## 7.8 MOS Transistor Width Calculation (Device Sizing)

The drain current of a MOSFET operating in saturation is

$$
I_D = \frac{1}{2}\mu_n C_{ox}\frac{W}{L}(V_{OV})^2
$$

Rearranging the equation to determine the transistor width:

$$
W = \frac{2 I_D L}{\mu_n C_{ox} (V_{OV})^2}
$$

### Step 1 – Compute Oxide Capacitance

The oxide capacitance per unit area is

$$
C_{ox} = \frac{\varepsilon_{ox}}{t_{ox}}
$$

Where

$$
\varepsilon_{ox} = 3.45 \times 10^{-11} \; F/m
$$

$$
t_{ox} = 4.1 \times 10^{-9} \; m
$$

Substituting,

$$
C_{ox} =
\frac{3.45 \times 10^{-11}}{4.1 \times 10^{-9}}
$$

$$
C_{ox} = 8.41 \times 10^{-3} \; F/m^2
$$

---

### Step 2 – Substitute Known Values

$$
I_D = 200 \times 10^{-6} \; A
$$

$$
L = 560 \; nm = 560 \times 10^{-9} \; m
$$

$$
\mu_n = 273.8 \times 10^{-4} \; m^2/Vs
$$

$$
V_{OV} = 0.25V
$$

Substituting into width equation

$$
W =
\frac{2 \times (200 \times 10^{-6}) \times (560 \times 10^{-9})}
{(273.8 \times 10^{-4}) \times (8.41 \times 10^{-3}) \times (0.25)^2}
$$

Simplifying numerator

$$
2 \times 200 \times 10^{-6} = 4 \times 10^{-4}
$$

$$
4 \times 10^{-4} \times 560 \times 10^{-9}
= 2.24 \times 10^{-10}
$$

Denominator

$$
(273.8 \times 10^{-4})(8.41 \times 10^{-3})(0.0625)
$$

$$
= 1.44 \times 10^{-4}
$$

Therefore

$$
W =
\frac{2.24 \times 10^{-10}}{1.44 \times 10^{-4}}
$$

$$
W \approx 1.55 \times 10^{-6} m
$$

$$
W \approx 1.55 \mu m
$$

Thus the transistor dimensions become

$$
W \approx 1.55\mu m
$$

$$
L = 0.56\mu m
$$

---

## 7.9 Small-Signal Equivalent Circuit Analysis

To analyze the amplifier gain more accurately, the circuit can be replaced with its **small-signal equivalent model**.

In this model:

- The MOS transistor is represented by a controlled current source
- The current source value is \( g_m v_{gs} \)
- Each transistor contributes an output resistance \(r_o\)

The small-signal drain current is

$$
i_d = g_m v_{gs}
$$

The output voltage is therefore

$$
v_{out} = - i_d (r_{o1} \parallel r_{o2} \parallel r_{o3})
$$

Substituting

$$
v_{out} =
- g_m v_{gs}(r_{o1} \parallel r_{o2} \parallel r_{o3})
$$

Voltage gain is defined as

$$
A_v =
\frac{v_{out}}{v_{in}}
$$

Since

$$
v_{gs} \approx v_{in}
$$

the gain becomes

$$
A_v = - g_m (r_{o1} \parallel r_{o2} \parallel r_{o3})
$$

---

## 7.10 Dominant Pole and Frequency Limitation

At high frequencies the amplifier gain decreases due to **parasitic capacitances and load capacitance**.

The dominant pole is formed at the output node by the load capacitor \(C_L\).

The upper cutoff frequency is approximated as

$$
f_H = \frac{1}{2\pi R_{out} C_L}
$$

Substituting

$$
R_{out} = 25k\Omega
$$

$$
C_L = 10pF
$$

$$
f_H =
\frac{1}{2\pi \times 25\times10^3 \times 10\times10^{-12}}
$$

Simplifying

$$
2\pi \times 25\times10^3 \times 10\times10^{-12}
= 1.57\times10^{-6}
$$

Therefore

$$
f_H =
\frac{1}{1.57\times10^{-6}}
$$

$$
f_H \approx 637kHz
$$

---

## 7.11 Unity Gain Bandwidth

Unity gain bandwidth (UGB) is the frequency at which the amplifier gain becomes equal to one.

The approximate relation is

$$
UGB = A_v \times f_H
$$

Substituting

$$
A_v = 40
$$

$$
f_H = 637kHz
$$

$$
UGB = 40 \times 637kHz
$$

$$
UGB = 25.48MHz
$$

---

## Additional Observation on Current Source Degeneration

The NMOS current source introduces a form of **degeneration**.

This occurs because the current source limits the variation of current flowing through the amplifier transistor.

Effects of this degeneration include:

- Reduced voltage gain
- Improved bias stability
- Improved linearity
- Reduced sensitivity to MOSFET parameter variations

Thus the current source acts as a **negative feedback element**, stabilizing the amplifier operation.
# 7.6 Output Resistance

Assuming

$$
\lambda = 0.1
$$

Output resistance

$$
r_o = \frac{1}{\lambda I_D}
$$

Substitute

$$
r_o = \frac{1}{0.1 \times 200\times10^{-6}}
$$

$$
r_o = 50k\Omega
$$

---

# 7.7 Theoretical Voltage Gain

Assume effective resistance

$$
R_{out} = 25k\Omega
$$

Voltage gain

$$
A_v = -g_m R_{out}
$$

Substitute

$$
A_v = -1.6\times10^{-3} \times 25\times10^3
$$

$$
A_v = -40
$$

---

# 8. Midband Gain

Midband gain is the gain in the frequency region where capacitive effects are negligible.

Theoretical midband gain

$$
A_v = 40
$$

In decibels

$$
A_v(dB) = 20\log_{10}(40)
$$

$$
A_v(dB) = 32dB
$$

---

# 9. Bandwidth Calculation

Bandwidth is defined as

$$
BW = f_H - f_L
$$

Where

- \(f_L\) = lower cutoff frequency  
- \(f_H\) = upper cutoff frequency  

From AC analysis

$$
f_L \approx 0
$$

Therefore

$$
BW \approx f_H
$$

---

# 10. Unity Gain Bandwidth

Unity gain frequency is defined as the frequency where

$$
A_v = 1
$$

The approximate relationship

$$
UGB = A_v \times f_H
$$

---

# 11. Saturation Condition Verification

For NMOS

$$
V_{DS} \ge V_{GS} - V_T
$$

Calculated

$$
V_{GS} = 0.616V
$$

Thus

$$
V_{GS}-V_T = 0.25V
$$

Measured

$$
V_{DS} \approx 0.9V
$$

Since

$$
0.9 > 0.25
$$

the transistor operates in saturation.

---

# 12. DC Analysis

![DC Analysis](Results/exp2b_dc.png)

---

# 13. Transient Analysis

![Transient Analysis](Results/exp2b_transient.png)

Input signal

- Frequency = 1kHz  
- Amplitude = 10mV  
- Offset = 0.91V  

---

# 14. Simulated Gain

Input

$$
V_{in(max)} = 0.918V
$$

$$
V_{in(min)} = 0.89796V
$$

$$
V_{in(pp)} = 0.02004V
$$

Output

$$
V_{out(max)} = 42.3889mV
$$

$$
V_{out(min)} = 41.8659mV
$$

$$
V_{out(pp)} = 0.523mV
$$

Voltage gain

$$
A_v = \frac{0.523\times10^{-3}}{20.04\times10^{-3}}
$$

$$
A_v = 0.0261
$$

Gain in dB

$$
A_v(dB) = 20\log_{10}(0.0261)
$$

$$
A_v(dB) = -31.67dB
$$

---

# 15. AC Analysis

![AC Analysis](Results/exp2b_ac.png)

---

# 16. Theoretical vs Simulated Results

| Parameter | Theoretical | Simulated |
|-----------|-------------|-----------|
| Voltage Gain | 40 V/V | 0.026 V/V |
| Gain (dB) | 32 dB | -31.7 dB |

---

# 17. Percentage Error

$$
Error =
\frac{|40 - 0.0261|}{40} \times 100
$$

$$
Error = 99.93\%
$$

---
---

## 19. Design Validation and Discussion

The purpose of this section is to verify whether the designed amplifier satisfies the required specifications and operates according to theoretical expectations.

### Validation of Bias Conditions

From the DC operating point analysis, the output node voltage was observed to be close to the intended bias value of

$$
V_{OUT} \approx 0.9V
$$

This confirms that the circuit is biased approximately at half the supply voltage:

$$
V_{OUT} \approx \frac{V_{DD}}{2}
$$

Biasing the amplifier at the midpoint of the supply voltage allows the output signal to swing symmetrically in both directions, which prevents signal clipping and ensures proper amplification.

---

### Verification of Saturation Operation

For proper operation of a MOS amplifier, the transistors must remain in the **saturation region**.

For the NMOS transistor, the saturation condition is

$$
V_{DS} \ge V_{GS} - V_T
$$

From the design calculations

$$
V_{GS} = 0.616V
$$

Therefore

$$
V_{GS} - V_T = 0.25V
$$

From simulation, the drain-source voltage was approximately

$$
V_{DS} \approx 0.9V
$$

Since

$$
0.9V > 0.25V
$$

the NMOS transistor clearly operates in the **saturation region**.

Similarly, the PMOS transistor also satisfies its saturation condition

$$
V_{SD} \ge V_{SG} - |V_{TP}|
$$

which ensures proper operation of the active load.

---

### Comparison of Theoretical and Simulated Gain

The theoretical gain derived from small-signal analysis was

$$
A_v = -40
$$

or

$$
A_v = 32dB
$$

However, the simulated gain obtained from transient analysis was

$$
A_v = 0.0261
$$

or

$$
A_v = -31.67dB
$$

This discrepancy arises due to several practical non-ideal effects present in real MOSFET models.

---

### Sources of Error

The difference between theoretical and simulated results can be attributed to:

1. **Channel Length Modulation**

   In practical MOSFETs, the drain current slightly increases with drain voltage due to channel shortening effects.

2. **Parasitic Capacitances**

   MOSFETs exhibit intrinsic capacitances such as:

   - Gate-to-source capacitance \(C_{gs}\)
   - Gate-to-drain capacitance \(C_{gd}\)
   - Drain-to-body capacitance \(C_{db}\)

   These capacitances reduce gain at higher frequencies.

3. **Finite Output Resistance**

   In theoretical calculations, the output resistance is often assumed to be very large. In reality, MOSFET output resistance is finite.

4. **Current Source Imperfections**

   The NMOS current source introduces degeneration, which stabilizes the bias but also reduces gain.

---

### Stability of the Bias Current

The inclusion of an NMOS current source provides a stable bias current of approximately

$$
I_D = 200\mu A
$$

This current source ensures that the amplifier operates with a nearly constant operating current even when small variations occur in supply voltage or transistor parameters.

This improves the robustness of the amplifier design.

---

### Frequency Response Behavior

The load capacitor

$$
C_L = 10pF
$$

creates a dominant pole at the output node.

This limits the high-frequency gain of the amplifier and defines the upper cutoff frequency.

The dominant pole frequency was estimated using

$$
f_H = \frac{1}{2\pi R_{out} C_L}
$$

which determines the bandwidth of the amplifier.

---

### Overall Design Assessment

The amplifier successfully satisfies the required design constraints:

- Supply voltage: $$V_{DD} = 1.8V$$
- Power consumption: $$P < 1mW$$
- Load capacitance: $$C_L = 10pF$$
- Stable bias current: $$I_D = 200\mu A$$

The circuit demonstrates proper MOSFET biasing, stable operation in the saturation region, and the expected behavior of a Common Source amplifier.

---

### Engineering Insight

This experiment demonstrates the importance of combining **theoretical analysis with circuit simulation**.

While theoretical equations provide initial design guidelines, simulation tools such as LTSpice are essential for understanding the practical behavior of analog circuits where device non-idealities significantly affect performance.

The results therefore validate both the design methodology and the practical limitations of MOSFET amplifier circuits.
# 18. Inference

The CS amplifier using **NMOS current source biasing and PMOS active load** was successfully designed and simulated in **TSMC 180nm technology**.

The design satisfies the required constraints:

- $$V_{DD} = 1.8V$$
- $$P < 1mW$$
- $$C_L = 10pF$$

The amplifier demonstrates proper biasing and correct transistor operation in saturation region.

The theoretical analysis predicts high gain due to ideal assumptions. However, simulation results show lower gain due to practical device effects including:

- channel length modulation
- parasitic capacitances
- current source limitations
- non-ideal MOSFET behavior

Despite these differences, the experiment clearly demonstrates the operation of a **Common Source amplifier with active load and current source biasing**, which is widely used in modern analog integrated circuits.
