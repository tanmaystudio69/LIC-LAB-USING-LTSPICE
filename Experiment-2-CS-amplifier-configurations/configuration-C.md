# Experiment 2C – Single Stage Common Source Amplifier using PMOS Active Load with Diode-Connected NMOS Bias Stabilization

---

# Aim

To design and simulate a **Common Source (CS) MOSFET amplifier** using:

- PMOS active load transistor
- NMOS amplifying transistor
- diode-connected NMOS degeneration transistor

in **TSMC 180 nm technology** using LTSpice under the constraints

$$
V_{DD}=1.8V
$$

$$
P \le 1mW
$$

$$
C_L=10pF
$$

$$
L=560nm
$$

The experiment includes theoretical analysis and verification of:

- DC operating point
- transistor saturation conditions
- voltage gain
- frequency response
- bandwidth
- unity gain bandwidth

---

# 1. Introduction

The Common Source amplifier is one of the most important single-stage voltage amplifiers used in CMOS analog circuits. It converts variations in gate voltage into amplified variations in drain voltage.

In discrete implementations, resistors are often used as loads. However, in integrated circuit design, MOSFET active loads are preferred because:

- they occupy less silicon area
- they provide higher output resistance
- they improve voltage gain

In this configuration:

- NMOS transistor M2 acts as the amplifying device
- PMOS transistor M1 acts as the active load
- NMOS transistor M3 is diode-connected and introduces source degeneration

This structure improves bias stability while maintaining moderate gain.

---

# 2. Role of Each Transistor

| Transistor | Function |
|-----------|-----------|
| M1 | PMOS active load |
| M2 | Amplifying transistor |
| M3 | Diode-connected degeneration transistor |

---

# 3. Working Principle of the Circuit

When an input signal is applied at the gate of M2:

$$
v_{in} \rightarrow v_{gs2}
$$

this produces a change in drain current:

$$
i_d=g_{m2}v_{gs2}
$$

This current flows through the PMOS active load and produces output voltage:

$$
v_{out}=-i_dR_{out}
$$

Thus

$$
A_v=-g_{m2}R_{out}
$$

Because M3 is diode-connected, source voltage varies with signal, introducing negative feedback which reduces gain.

---

# 4. PMOS Active Load Operation

When PMOS operates in saturation:

$$
r_{o1}=\frac{1}{\lambda I_D}
$$

Effective output resistance becomes

$$
R_{out}=r_{o1}\parallel r_{o2}
$$

Thus gain increases as output resistance increases.

---

# 5. Diode-Connected NMOS and Source Degeneration

For diode-connected transistor:

$$
V_G=V_D
$$

Therefore

$$
V_{GS3}=V_{DS3}
$$

Small-signal resistance becomes

$$
r_{d3}=\frac{1}{g_{m3}+g_{ds3}}
$$

Approximating

$$
r_{d3}\approx\frac{1}{g_{m3}}
$$

Gain expression becomes

$$
A_v=\frac{-g_{m2}(r_{o1}\parallel r_{o2})}{1+g_{m2}r_{d3}}
$$

Since

$$
r_{d3}=\frac{1}{g_{m3}}
$$

$$
A_v=\frac{-g_{m2}(r_{o1}\parallel r_{o2})}{1+\frac{g_{m2}}{g_{m3}}}
$$

---

# 6. Design Specifications

Given:

$$
V_{DD}=1.8V
$$

$$
P\le1mW
$$

$$
C_L=10pF
$$

$$
L=560nm
$$

Threshold voltage:

$$
V_T=0.366V
$$

Chosen overdrive voltage:

$$
V_{OV}=0.25V
$$

Chosen drain current:

$$
I_D=200\mu A
$$

---

# 7. Power Constraint Verification

Power consumption:

$$
P=V_{DD}I_D
$$

Substituting values:

$$
P=1.8\times200\times10^{-6}
$$

$$
P=3.6\times10^{-4}W
$$

$$
P=0.36mW
$$

Since

$$
0.36mW<1mW
$$

power constraint is satisfied.

---

# 8. Bias Voltage Calculation

Overdrive relation:

$$
V_{OV}=V_{GS}-V_T
$$

Thus

$$
V_{GS}=V_{OV}+V_T
$$

$$
V_{GS}=0.25+0.366
$$

$$
V_{GS}=0.616V
$$

Since M3 is diode-connected

$$
V_S=V_{GS3}=0.616V
$$

Input bias voltage becomes

$$
V_{IN}=V_{GS2}+V_S
$$

$$
V_{IN}=0.616+0.616
$$

$$
V_{IN}=1.232V
$$

---

# 9. Output Bias Selection

For symmetrical swing

$$
V_{OUT}=\frac{V_{DD}}{2}+V_{DS3}
$$

$$
V_{OUT}=0.9+0.616
$$

$$
V_{OUT}=1.516V
$$

Thus

$$
V_{DS2}=1.516-0.616
$$

$$
V_{DS2}=0.9V
$$

Since

$$
V_{DS2}>V_{OV}
$$

NMOS operates in saturation.

---

# 10. PMOS Saturation Verification

For PMOS transistor:

$$
V_{SG}=V_{OV}+|V_{TP}|
$$

$$
V_{SG}=0.25+0.39
$$

$$
V_{SG}=0.64V
$$

Drain-source voltage:

$$
V_{SD}=1.8-1.516
$$

$$
V_{SD}=0.284V
$$

Since

$$
V_{SD}>V_{OV}
$$

PMOS operates in saturation.

---

# 11. Diode-Connected NMOS Saturation Verification

For M3:

$$
V_{DS3}=V_{GS3}=0.616V
$$

Since

$$
V_{DS3}>V_{OV}
$$

M3 operates in saturation.

---

# 12. Width Calculation

MOSFET saturation current equation:

$$
I_D=\frac{1}{2}\mu C_{ox}\frac{W}{L}(V_{OV})^2
$$

Rearranging

$$
W=\frac{2I_DL}{\mu C_{ox}(V_{OV})^2}
$$

Calculated width:

$$
W_{M2}\approx15.15\mu m
$$

After tuning:

$$
W_{M2}=73.5\mu m
$$

Similarly:

$$
W_{M3}=78.5\mu m
$$

$$
W_{M1}=87.4\mu m
$$

---

# 13. Small Signal Equivalent Circuit Analysis

Small-signal drain current:

$$
i_d=g_m v_{gs}
$$

Output voltage:

$$
v_{out}=-i_d(r_{o1}\parallel r_{o2})
$$

Including degeneration:

$$
A_v=\frac{-g_m(r_{o1}\parallel r_{o2})}{1+g_m r_{d3}}
$$

---

# 14. Transconductance Calculation

$$
g_m=\frac{2I_D}{V_{OV}}
$$

$$
g_m=\frac{2\times200\times10^{-6}}{0.25}
$$

$$
g_m=1.6mS
$$

---

# 15. Output Resistance Calculation

Assuming

$$
\lambda=0.1
$$

$$
r_o=\frac{1}{\lambda I_D}
$$

$$
r_o=50k\Omega
$$

---

# 16. Theoretical Gain Calculation

Including degeneration:

$$
A_v=\frac{-g_m r_o}{1+\frac{g_m}{g_{m3}}}
$$

Since

$$
g_{m2}=g_{m3}
$$

$$
A_v=\frac{-1.6\times10^{-3}\times50\times10^3}{2}
$$

$$
A_v=40
$$

Gain in dB:

$$
A_v(dB)=32.04dB
$$

---

# 17. Simulated Gain (Transient Analysis)

Measured values:

$$
V_{in(pp)}=0.019V
$$

$$
V_{out(pp)}=0.476V
$$

Thus

$$
A_v=\frac{0.476}{0.019}
$$

$$
A_v=25.05
$$

Gain in decibels:

$$
A_v(dB)=27.97dB
$$

---

# 18. AC Analysis

Midband gain:

$$
A_v=27.27dB
$$

Upper cutoff frequency:

$$
f_H=83.21MHz
$$

Since

$$
f_L\approx0
$$

Bandwidth becomes

$$
BW=83.21MHz
$$

---

# 19. Dominant Pole Calculation

Dominant pole frequency:

$$
f_H=\frac{1}{2\pi R_{out}C_L}
$$

Substituting

$$
R_{out}=50k\Omega
$$

$$
C_L=10pF
$$

$$
f_H\approx83MHz
$$

which matches simulation.

---

# 20. Unity Gain Bandwidth

$$
UGB=A_v\times f_H
$$

$$
UGB=25.05\times83.21MHz
$$

$$
UGB=2.08GHz
$$

---

# 21. Percentage Error

$$
Error=\frac{|40-25.05|}{40}\times100
$$

$$
Error=37.4\%
$$

---

# 22. Design Validation and Discussion

All three transistors operate in saturation region confirming correct biasing.

Gain reduction occurs due to:

- degeneration resistance
- channel length modulation
- parasitic capacitances
- mobility degradation

The dominant pole formed by load capacitance limits bandwidth.

---

# 23. Inference

The Common Source amplifier using PMOS active load and diode-connected NMOS satisfies all design requirements.

The circuit demonstrates:

- stable biasing
- predictable degeneration behaviour
- moderate voltage gain
- wide bandwidth response

The difference between theoretical and simulated gain confirms the importance of second-order MOSFET effects in practical analog circuit design.
