# **DESIGN AND ANALYSIS OF PMOS COMMON SOURCE (CS) AMPLIFIER**

**Technology:** TSMC 180nm  
**Tool Used:** LTspice  
**Supply Voltage (VDD):** 2V  

---

# **AIM**

To design and analyze a **PMOS Common Source (CS) amplifier** using TSMC 180nm technology and study its:

- DC operating point  
- DC sweep characteristics  
- Transient response  
- AC frequency response  
- Voltage gain and bandwidth  

---

# **INTRODUCTION**

The PMOS transistor is widely used in analog integrated circuits due to its:

- High input impedance  
- Low power consumption  
- Good voltage amplification capability  

In a Common Source amplifier:

- Input is applied at the gate terminal  
- Output is taken from the drain terminal  
- Source is connected to the supply voltage  

This configuration provides:

- Significant voltage gain  
- 180° phase inversion  
- Good small-signal amplification  

For proper amplifier operation, the transistor must operate in the **saturation region**.

---

# **WORKING PRINCIPLE**

Saturation condition for PMOS transistor:

<div align="center">

**VSD ≥ VSG − |VT|**

</div>

When input voltage increases:

- VSG increases  
- Drain current increases  
- Voltage drop across RD increases  
- Output voltage decreases  

Thus, the output is amplified and inverted.

Voltage gain:

<div align="center">

**Av = − gm RD**

</div>

---

# **DESIGN SPECIFICATIONS**

Given parameters:

<div align="center">

**VDD = 2V**  
**P ≤ 1.5mW**  
**CL = 1pF**  
**L = 560nm**

</div>

---

# **CIRCUIT DIAGRAM**

<img width="959" height="478" alt="Screenshot 2026-02-26 131005" src="https://github.com/user-attachments/assets/74c19fc7-be21-45e9-b092-71f6faa50707" />


---

# **DESIGN CALCULATIONS**

## **Drain Current Calculation**

Power relation:

<div align="center">

**ID = P / VDD**

</div>

<div align="center">

**ID = 1.5mW / 2V**

</div>

<div align="center">

**ID = 0.75mA**

</div>

Chosen safe value:

<div align="center">

**ID = 0.5mA**

</div>

Power consumed:

<div align="center">

**P = 1mW**

</div>

---

## **Output Voltage**

<div align="center">

**Vout = VDD / 2 = 1V**

</div>

---

## **Drain Resistance**

<div align="center">

**RD = (VDD − Vout) / ID**

</div>

<div align="center">

**RD = 2kΩ**

</div>

---

## **Threshold Voltage from TSMC Model**

<div align="center">

**VT = 0.3906V**

</div>

---

## **Gate Source Voltage**

<div align="center">

**VSG = Vov + VT**

</div>

<div align="center">

**VSG = 0.6V**

</div>

---

## **Width Calculation**

Using:

<div align="center">

**ID = (1/2) kp (W/L) Vov²**

</div>

Result:

<div align="center">

**W = 144µm**

</div>

---

# **DC OPERATING POINT ANALYSIS (.op)**

<img width="364" height="258" alt="Screenshot 2026-02-26 131041" src="https://github.com/user-attachments/assets/931228ea-00c1-4f08-b6f7-6f3b0b0357b7" />
<img width="959" height="461" alt="Screenshot 2026-02-26 131128" src="https://github.com/user-attachments/assets/a640b179-2c83-4b8c-abf2-8b230fbc652c" />



From LTspice simulation:

- Supply voltage = 2V  
- Gate voltage = 1.409V  
- Output voltage = 1.461V  
- Drain current = 0.7305mA  

Observations:

- The output voltage is close to the designed bias point  
- The drain current is within the power constraint  

Power dissipation:

<div align="center">

**P = VDD × ID**

</div>

<div align="center">

**P = 2 × 0.7305mA**

</div>

<div align="center">

**P = 1.461mW**

</div>

This satisfies the design constraint.

The transistor is operating in saturation region since:

<div align="center">

**VSD ≥ VSG − VT**

</div>

Thus, proper amplifier biasing is achieved.



---

# **DC SWEEP ANALYSIS (.dc)**
<img width="959" height="470" alt="Screenshot 2026-02-26 131249" src="https://github.com/user-attachments/assets/3461f64c-9d50-43d6-9d04-a568a5dd3c78" />


The DC sweep analysis shows variation of output voltage with input voltage.

Observations:

- At low input voltage, transistor operates in cutoff region  
- Output voltage remains close to supply voltage  
- As input increases, transistor enters saturation region  
- Output voltage decreases linearly  

This confirms proper amplifier behavior.

The middle region represents the active region where amplification occurs.



---

# **TRANSIENT ANALYSIS (.tran)**
<img width="959" height="474" alt="Screenshot 2026-02-26 131811" src="https://github.com/user-attachments/assets/ef6b8033-69f8-411d-8c50-649522f1eec7" />


Input signal applied:

<div align="center">

**Vin = 1.409 + 10mV sin(2π × 1000t)**

</div>

From simulation:

Input peak-to-peak voltage:

<div align="center">

**Vin(pp) ≈ 20mV**

</div>

Output peak-to-peak voltage:

<div align="center">

**Vout(pp) ≈ 240mV**

</div>

Voltage gain:

<div align="center">

**Av = Vout / Vin**

</div>

<div align="center">

**Av = 240mV / 20mV**

</div>

<div align="center">

**Av = 12 V/V**

</div>

Gain in dB:

<div align="center">

**Av = 21.6 dB**

</div>

Observations:

- Output signal is amplified  
- Output signal is inverted (180° phase shift)  
- Amplifier operates in linear region  

This confirms correct amplifier operation.



---

# **AC ANALYSIS (.ac)**
<img width="959" height="484" alt="Screenshot 2026-02-26 132203" src="https://github.com/user-attachments/assets/edd9fe19-feef-4f3b-b33b-cb0e308412b4" />
<img width="959" height="471" alt="Screenshot 2026-02-26 132133" src="https://github.com/user-attachments/assets/13efee18-4e98-454b-b642-a5d646d9b030" />



From AC analysis plot:

Midband gain:

<div align="center">

**Av ≈ 22 dB**

</div>

Upper cutoff frequency:

<div align="center">

**fH ≈ 80 MHz**

</div>

Bandwidth:

<div align="center">

**BW ≈ 80 MHz**

</div>

Observations:

- Gain remains constant in midband region  
- Gain decreases at higher frequencies  
- Load capacitor introduces dominant pole  



---

# **GAIN CALCULATION**

Theoretical gain:

<div align="center">

**Av = gm RD**

</div>

<div align="center">

**Av ≈ 10 V/V**

</div>

Simulated gain:

<div align="center">

**Av ≈ 12 V/V**

</div>

The difference occurs due to:

- Channel length modulation  
- Finite output resistance  
- Model non-idealities  

Actual gain:

<div align="center">

**Av = −gm (RD || ro)**

</div>

---

# **BANDWIDTH**

From AC analysis:

<div align="center">

**Bandwidth = 80 MHz**

</div>

---
---

# **COMPARISON OF THEORETICAL AND SIMULATED RESULTS**

| Parameter | Theoretical Value | Simulated Value | Observation |
|----------|------------------|-----------------|-------------|
| Supply Voltage (VDD) | 2 V | 2 V | Matches design specification |
| Drain Current (ID) | 0.5 mA | 0.7305 mA | Slightly higher due to real TSMC model effects |
| Output Voltage (Vout) | 1 V | 1.461 V | Close to expected bias region |
| Drain Resistance (RD) | 2 kΩ | 2 kΩ | Matches design value |
| Transconductance (gm) | 5 mS | ≈ 6.1 mS | Higher due to increased drain current |
| Voltage Gain (Av) | 10 V/V | 12 V/V | Close agreement |
| Gain (dB) | 20 dB | 22 dB | Matches expected amplification |
| Bandwidth | 79.6 MHz | ≈ 80 MHz | Matches theoretical prediction |
| Power Dissipation | 1 mW | 1.461 mW | Within allowed limit (≤ 1.5 mW) |
| Region of Operation | Saturation | Saturation | Proper amplifier operation |

---

# **DISCUSSION**

The theoretical and simulated results show close agreement. Small differences occur due to:

- Channel length modulation  
- Finite output resistance (ro)  
- Mobility degradation  
- Non-ideal behavior of TSMC 180nm transistor model  

The simulated gain is slightly higher due to higher drain current, which increases transconductance.

The bandwidth closely matches theoretical prediction, confirming correct frequency response.

Overall, the amplifier behaves as expected.

---
# **CONCLUSION**

The PMOS Common Source amplifier was successfully designed using TSMC 180nm technology.

Results obtained:

- Proper DC bias achieved  
- Drain current within power limit  
- Gain ≈ 12 V/V  
- Gain ≈ 22 dB  
- Bandwidth ≈ 80 MHz  

The simulated results match theoretical expectations.

The amplifier operates correctly and satisfies all design specifications.

---
