# Experiment 2A – Common Source Amplifier with PMOS Active Load

---

# Aim

To design and simulate a **Common Source (CS) amplifier** using an NMOS transistor with PMOS active load in **TSMC 180nm technology** using **LTSpice**, satisfying the following design constraints:

- Supply voltage: $V_{DD} = 1.8\,V$
- Power constraint: $P \le 1\,mW$
- Channel length: $L_n = 560\,nm$
- Load capacitance: $C_L = 10\,pF$

The circuit is analyzed using:

- DC operating point analysis  
- Transient analysis  
- AC frequency response analysis  

---

# 1. Introduction

The **Common Source (CS) amplifier** is one of the most fundamental MOSFET amplifier configurations used in analog integrated circuits.

In this configuration:

- Input signal → applied at the **gate**
- Output signal → taken from the **drain**
- Source → acts as the **common reference node**

Key properties of CS amplifiers:

- High voltage gain  
- 180° phase inversion  
- Widely used in analog CMOS circuits  

In integrated circuits, a **PMOS transistor is used as an active load instead of a resistor** because it provides higher output resistance and occupies less chip area.

---

# 2. Working Principle (What the Circuit Does)

The NMOS transistor acts as the **main amplifying device**. When a small input signal $v_{in}$ is applied at the gate, it produces a small variation in the gate-source voltage $V_{GS}$.

The drain current of the MOSFET changes according to the transconductance relation:

$$
i_d = g_m v_{gs}
$$

This variation in drain current flows through the PMOS load, producing a voltage variation at the output node:

$$
v_{out} = -i_d R_{out}
$$

The negative sign indicates that the output signal is **inverted (180° phase shift)** relative to the input signal.

---

# 3. PMOS Active Load

Instead of using a physical resistor as the load, a **PMOS transistor is used as an active load**.

Advantages:

- Higher output resistance  
- Higher voltage gain  
- Better compatibility with CMOS technology  

Voltage gain of a CS amplifier is approximately:

$$
A_v \approx - g_m R_{out}
$$

Where

$$
R_{out} \approx r_{o,n} \parallel r_{o,p}
$$

Since the PMOS transistor provides large output resistance, the gain of the amplifier increases.

---

# 4. Source Degeneration

A resistor $R_S$ is placed at the source terminal of the NMOS transistor. This technique is called **source degeneration**.

The gain of the amplifier becomes:

$$
A_v = \frac{-g_m (r_{o1} || r_{o2})}{1 + g_m R_S}
$$

Effects of source degeneration:

- Improves linearity  
- Stabilizes the bias point  
- Reduces distortion  
- Increases input dynamic range  

However, the gain reduces slightly due to the factor $(1 + g_m R_S)$.

---

# Circuit Diagram
<img src="https://github.com/tanmaystudio69/LIC-LAB-USING-LTSPICE/blob/8fa757e555762a61000c84fd8b2f48193c6ffa17/Experiment-2-CS-amplifier-configurations/results-from-LTspice/Screenshot%202026-03-15%20235116.png" alt="Alt text" width="800" height="800">



---

# 5. Design Calculations

## Given Parameters

Technology: **TSMC 180nm**

Supply voltage:

$$
V_{DD} = 1.8V
$$

Power constraint:

$$
P \le 1mW
$$

Channel length:

$$
L_n = 560nm
$$

Load capacitance:

$$
C_L = 10pF
$$

Threshold voltages from model file:

$$
V_{TN} \approx 0.366V
$$

$$
|V_{TP}| \approx 0.39V
$$

Electron mobility:

$$
\mu_n = 273.8 \times 10^{-4} \, m^2/Vs
$$

---

# 5.1 Power Constraint (Drain Current Calculation)

Total power consumed:

$$
P = V_{DD} I_D
$$

Maximum allowable current:

$$
I_D \le \frac{P}{V_{DD}}
$$

Substitute values:

$$
I_D \le \frac{1 \times 10^{-3}}{1.8}
$$

$$
I_D \le 555.5\mu A
$$

Choose safe current:

$$
I_D = 200\mu A
$$

Power consumed:

$$
P = V_{DD} \times I_D
$$

$$
P = 1.8 \times 200\times10^{-6}
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

# 5.2 Overdrive Voltage

Assume overdrive voltage:

$$
V_{OV} = 0.25V
$$

MOSFET relation:

$$
V_{OV} = V_{GS} - V_T
$$

Therefore

$$
V_{GS} = V_{OV} + V_T
$$

Substitute values:

$$
V_{GS} = 0.25 + 0.366
$$

$$
V_{GS} = 0.616V
$$

---

# 5.3 Output Bias Point

For symmetrical signal swing:

$$
V_{OUT} \approx \frac{V_{DD}}{2} + V_{RS}
$$

Assume

$$
V_{RS} = 0.2V
$$

Then

$$
V_{OUT} = \frac{1.8}{2} + 0.2
$$

$$
V_{OUT} = 0.9 + 0.2
$$

$$
V_{OUT} = 1.1V
$$

---

# 5.4 Source Resistor

Using Ohm's law:

$$
V_{RS} = I_D R_S
$$

Substitute values:

$$
0.2 = 200\times10^{-6} \times R_S
$$

Solve:

$$
R_S = \frac{0.2}{200\times10^{-6}}
$$

$$
R_S = 1000\Omega
$$

$$
R_S = 1k\Omega
$$

---

# 5.5 NMOS Width Calculation

Drain current in saturation region:

$$
I_D = \frac{1}{2}\mu_n C_{ox} \frac{W}{L}(V_{OV})^2
$$

Rearranging:

$$
W = \frac{2 I_D L}{\mu_n C_{ox} (V_{OV})^2}
$$

Using extracted technology parameters:

$$
W_n \approx 15\mu m
$$

After simulation adjustments to maintain $I_D = 200\mu A$:

$$
W_n \approx 56.8\mu m
$$

---

# 5.6 PMOS Width Calculation

Using same drain current equation:

$$
I_D = \frac{1}{2}\mu_p C_{ox}\frac{W}{L}(V_{OV})^2
$$

Solving:

$$
W_p \approx 35\mu m
$$

After adjusting to match simulation current:

$$
W_p \approx 83\mu m
$$

---

# 5.7 PMOS Gate Bias Voltage

For PMOS:

$$
V_{OVp} = V_{SG} - |V_{TP}|
$$

Rearranging:

$$
V_{SG} = V_{OVp} + |V_{TP}|
$$

Substitute values:

$$
V_{SG} = 0.25 + 0.39
$$

$$
V_{SG} = 0.64V
$$

Since

$$
V_{SG} = V_S - V_G
$$

and

$$
V_S = V_{DD}
$$

Therefore

$$
V_G = V_{DD} - V_{SG}
$$

$$
V_G = 1.8 - 0.64
$$

$$
V_G = 1.16V
$$

---

# 6. DC Analysis
![image alt](https://github.com/tanmaystudio69/LIC-LAB-USING-LTSPICE/blob/5951024eecd451d264ec85c70884a0a21e3d542a/Experiment-2-CS-amplifier-configurations/results-from-LTspice/Screenshot%202026-03-16%20114532.png)
<img src="https://github.com/tanmaystudio69/LIC-LAB-USING-LTSPICE/blob/5951024eecd451d264ec85c70884a0a21e3d542a/Experiment-2-CS-amplifier-configurations/results-from-LTspice/Screenshot%202026-03-15%20235256.png" alt="Alt text" width="800" height="700">





The DC operating point confirms that the MOSFETs operate in **saturation region**, which is required for linear amplification.

---

# 7. Transient Analysis
<img src="https://github.com/tanmaystudio69/LIC-LAB-USING-LTSPICE/blob/5951024eecd451d264ec85c70884a0a21e3d542a/Experiment-2-CS-amplifier-configurations/results-from-LTspice/Screenshot%202026-03-15%20235943.png" alt="Alt text" width="800" height="700">
<img src="https://github.com/tanmaystudio69/LIC-LAB-USING-LTSPICE/blob/5951024eecd451d264ec85c70884a0a21e3d542a/Experiment-2-CS-amplifier-configurations/results-from-LTspice/Screenshot%202026-03-15%20235952.png" alt="Alt text" width="900" height="800">




Input signal:

- Frequency = 1kHz  
- Amplitude = 10mV  
- Offset = 0.81V  

---

# Simulated Gain

Input peak-to-peak voltage:

$$
V_{in(pp)} = 819.956mV - 800.212mV
$$

$$
V_{in(pp)} = 19.744mV
$$

Output peak-to-peak voltage:

$$
V_{out(pp)} = 0.834V - 0.790V
$$

$$
V_{out(pp)} = 44mV
$$

Voltage gain:

$$
A_v = \frac{V_{out(pp)}}{V_{in(pp)}}
$$

$$
A_v = \frac{0.044}{0.019744}
$$

$$
A_v = 2.23
$$

---

# Gain in dB

$$
A_v(dB) = 20\log_{10}(A_v)
$$

$$
A_v(dB) = 20\log_{10}(2.23)
$$

$$
A_v(dB) = 6.96dB
$$

The output waveform is inverted relative to the input confirming **CS amplifier behavior**.

---

# 8. AC Analysis
<img src="https://github.com/tanmaystudio69/LIC-LAB-USING-LTSPICE/blob/5951024eecd451d264ec85c70884a0a21e3d542a/Experiment-2-CS-amplifier-configurations/results-from-LTspice/Screenshot%202026-03-16%20000324.png" alt="Alt text" width="900" height="700">
<img src="https://github.com/tanmaystudio69/LIC-LAB-USING-LTSPICE/blob/5951024eecd451d264ec85c70884a0a21e3d542a/Experiment-2-CS-amplifier-configurations/results-from-LTspice/Screenshot%202026-03-16%20000316.png" alt="Alt text" width="900" height="700">
<img src="https://github.com/tanmaystudio69/LIC-LAB-USING-LTSPICE/blob/5951024eecd451d264ec85c70884a0a21e3d542a/Experiment-2-CS-amplifier-configurations/results-from-LTspice/Screenshot%202026-03-16%20000444.png" alt="Alt text" width="700" height="600">





The AC analysis provides the **frequency response** of the amplifier.

---

# Midband Gain

From the flat region of the Bode plot:

$$
A_v = -15.84dB
$$

---

# Bandwidth Calculation

Bandwidth is defined as the frequency range between the lower and upper cutoff frequencies.

Lower cutoff frequency:

$$
f_L \approx 0Hz
$$

Upper cutoff frequency:

$$
f_H \approx 80MHz
$$

Therefore bandwidth:

$$
BW = f_H - f_L
$$

$$
BW = 80MHz
$$

---

# 9. Conclusion

The **Common Source amplifier with PMOS active load and source degeneration** was successfully designed using **TSMC 180nm technology** while satisfying the design constraints.

The circuit meets the specifications:

- $V_{DD} = 1.8V$
- $P \le 1mW$
- $C_L = 10pF$

Simulation results confirm:

- Proper **DC biasing**
- Expected **voltage amplification**
- **180° phase inversion**
- Correct **frequency response**

Thus the amplifier demonstrates correct **CMOS analog amplifier operation** and validates the design methodology.
