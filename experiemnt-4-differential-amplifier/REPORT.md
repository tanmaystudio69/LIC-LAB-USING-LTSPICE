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
