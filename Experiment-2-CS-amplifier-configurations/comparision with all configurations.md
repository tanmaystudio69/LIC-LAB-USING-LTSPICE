# Comparative Study of Common Source Amplifier Configurations

---

# Objective of the Comparison

In Experiments 2A, 2B, and 2C, three different implementations of a **Common Source (CS) MOS amplifier** were designed and analyzed using TSMC 180 nm technology under identical supply and load conditions:

$$
V_{DD}=1.8V
$$

$$
C_L=10pF
$$

$$
P \le 1mW
$$

Although all three circuits perform voltage amplification, each configuration differs in:

- load structure
- biasing mechanism
- degeneration technique
- achievable gain
- bandwidth
- operating-point stability

This section compares their electrical performance and practical usefulness in analog CMOS design.

---

# Overview of the Three Configurations

| Configuration | Load Type | Biasing Method | Degeneration Present | Design Objective |
|--------------|-----------|----------------|----------------------|------------------|
| Config A | Active load with source degeneration resistor | Resistive degeneration bias | Yes | Improved linearity and stability |
| Config B | PMOS active load + NMOS current source | Current mirror style biasing | Moderate | High output resistance and gain |
| Config C | PMOS active load + diode-connected NMOS | Self-biasing degeneration | Strong | Stable bias with controlled gain |

Each configuration represents a different trade-off between gain, bandwidth, stability, and circuit complexity.

---

# Theoretical Gain Comparison

For a Common Source amplifier without degeneration:

$$
A_v=-g_m R_{out}
$$

However, degeneration modifies the gain expression.

### Configuration A

Source resistor introduces degeneration:

$$
A_v=\frac{-g_m R_{out}}{1+g_m R_S}
$$

This improves linearity but reduces gain.

---

### Configuration B

Current source load increases effective output resistance:

$$
A_v=-g_m (r_{o1}\parallel r_{o2}\parallel r_{o3})
$$

Thus Config B produces higher gain than Config A.

---

### Configuration C

Diode-connected NMOS introduces controlled degeneration:

$$
A_v=\frac{-g_m(r_{o1}\parallel r_{o2})}{1+\frac{g_m}{g_{m3}}}
$$

This reduces gain compared to an ideal CS amplifier but improves bias stability.

---

# Comparison of Theoretical Voltage Gain

| Configuration | Theoretical Gain Expression | Relative Gain Level |
|--------------|-----------------------------|---------------------|
| Config A | $\frac{-g_mR_{out}}{1+g_mR_S}$ | Moderate |
| Config B | $-g_m(r_{o1}\parallel r_{o2}\parallel r_{o3})$ | Highest |
| Config C | $\frac{-g_m(r_{o1}\parallel r_{o2})}{1+g_m/g_{m3}}$ | Moderate–High |

Thus:

$$
A_v(\text{Config B}) > A_v(\text{Config C}) > A_v(\text{Config A})
$$

---

# Simulated Gain Comparison

| Configuration | Simulated Gain (V/V) | Gain (dB) |
|--------------|---------------------|-----------|
| Config A | 2.23 | 6.96 dB |
| Config B | 0.026 | −31.67 dB |
| Config C | 25.05 | 27.97 dB |

Config C demonstrates significantly higher practical gain than Config B due to reduced degeneration compared with current-source loading limitations.

---

# Output Resistance Comparison

Output resistance determines achievable gain:

$$
R_{out}=r_{o1}\parallel r_{o2}
$$

Comparison:

| Configuration | Output Resistance | Effect on Gain |
|--------------|------------------|---------------|
| Config A | Reduced by source resistor | Lower gain |
| Config B | Increased by current source | Higher gain |
| Config C | Moderately high | Balanced gain |

Thus Config B achieves the highest theoretical output resistance.

---

# Bandwidth Comparison

Bandwidth depends on dominant pole location:

$$
f_H=\frac{1}{2\pi R_{out}C_L}
$$

| Configuration | Bandwidth Behaviour |
|--------------|--------------------|
| Config A | Highest bandwidth due to reduced gain |
| Config B | Moderate bandwidth |
| Config C | Balanced gain–bandwidth trade-off |

Higher gain generally reduces bandwidth because:

$$
BW \propto \frac{1}{R_{out}}
$$

---

# Unity Gain Bandwidth Comparison

Unity gain bandwidth:

$$
UGB=A_v \times f_H
$$

Comparison:

| Configuration | Unity Gain Bandwidth |
|--------------|----------------------|
| Config A | Moderate |
| Config B | Lower |
| Config C | Highest |

Config C achieves the best gain-bandwidth balance among the three.

---

# Bias Stability Comparison

Bias stability improves with degeneration.

| Configuration | Stability Level | Reason |
|--------------|----------------|-------|
| Config A | High | Source resistor feedback |
| Config B | Moderate | Current source stabilization |
| Config C | Highest | Diode-connected local feedback |

Thus Config C provides the most reliable operating-point control.

---

# Linearity Comparison

Linearity improves when degeneration is present:

$$
r_d\approx\frac{1}{g_m}
$$

| Configuration | Linearity |
|--------------|-----------|
| Config A | High |
| Config B | Moderate |
| Config C | Very high |

Diode-connected degeneration improves small-signal linear response significantly.

---

# Power Efficiency Comparison

Power consumption:

$$
P=V_{DD}I_D
$$

Since all configurations operate at:

$$
I_D=200\mu A
$$

their power dissipation remains approximately:

$$
P=0.36mW
$$

Thus efficiency differences arise mainly from gain utilization rather than current consumption.

---

# Silicon Area Considerations

Integrated circuit area is influenced by load implementation.

| Configuration | Area Requirement |
|--------------|------------------|
| Config A | Larger (resistive degeneration) |
| Config B | Moderate |
| Config C | Compact |

Active-load implementations reduce chip area significantly compared to resistor-based structures.

---

# Frequency Response Behaviour

Frequency response depends on parasitic capacitances and output resistance.

| Configuration | Frequency Behaviour |
|--------------|--------------------|
| Config A | Wide bandwidth |
| Config B | Moderate bandwidth |
| Config C | Optimized gain–bandwidth balance |

Dominant pole appears at output node due to:

$$
C_L=10pF
$$

---

# Practical Application Suitability

| Configuration | Typical Application |
|--------------|--------------------|
| Config A | Linear analog front-end stages |
| Config B | High-gain intermediate amplifier stages |
| Config C | Stable voltage amplification blocks |

Config C provides the best compromise between gain, bandwidth, and stability.

---

# Overall Performance Comparison

| Parameter | Config A | Config B | Config C |
|----------|----------|----------|----------|
| Gain | Moderate | Very high (ideal) | High (practical) |
| Bandwidth | High | Moderate | High |
| Stability | High | Moderate | Very high |
| Linearity | High | Moderate | Very high |
| Complexity | Low | Moderate | Moderate |
| Area Efficiency | Low | High | High |

---

# Final Comparative Conclusion

The three Common Source amplifier configurations investigated in this experiment demonstrate different trade-offs between gain, bandwidth, linearity, and bias stability.

Configuration A improves linearity through resistive degeneration but limits achievable voltage gain due to reduced effective transconductance.

Configuration B increases gain by using a current-source load that enhances output resistance, making it suitable for intermediate amplification stages where higher gain is required.

Configuration C introduces diode-connected source degeneration that stabilizes the operating point while maintaining strong voltage gain and wide bandwidth. This configuration achieves the most balanced performance among the three circuits.

Therefore, Configuration C represents the most practical solution for CMOS voltage amplification when both gain and stability are important design requirements.
