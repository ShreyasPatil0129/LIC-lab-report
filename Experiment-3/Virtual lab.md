# Experiment 3 — Characteristic Parameters of Op-Amp IC-741

| | |
|---|---|
| **Institute** | The National Institute of Engineering, Mysuru |
| **Department** | Electronics & Communication Engineering |
| **Course** | Linear Integrated Circuits Lab |
| **Experiment No.** | 03 |
| **IC Used** | IC-741 Op-Amp |
| **Supply Voltage** | ±15 V DC |

---

## 1. Aim

To study and measure the characteristic parameters of an Operational Amplifier **(IC-741)**:

- **(a)** Input Bias Current at the Inverting Terminal — $I_{B2}$
- **(b)** Input Bias Current at the Non-Inverting Terminal — $I_{B1}$
- **(c)** Input Offset Current — $I_{io}$
- **(d)** Input Offset Voltage — $V_{io}$
- **(e)** Slew Rate — $S.R.$

---

## 2. Components & Equipment Required

| Sl. No. | Component / Equipment | Specification | Quantity |
|:-------:|----------------------|:-------------:|:--------:|
| 1 | Op-Amp IC | IC-741 | 1 |
| 2 | Resistors | 470 kΩ, 10 kΩ, 100 Ω | As required |
| 3 | Capacitors | 1000 pF | 2 |
| 4 | Dual Power Supply | ±15 V DC | 1 |
| 5 | Digital Multimeter | — | 1 |
| 6 | A.F. Oscillator | Variable frequency | 1 |
| 7 | CRO (Oscilloscope) | Dual channel | 1 |
| 8 | Breadboard & Connecting Wires | — | 1 set |

---

## 3. Theory

An **Operational Amplifier (Op-Amp)** is a direct-coupled, high-gain differential amplifier available as a single IC package. Originally designed for mathematical operations (addition, subtraction, integration), modern op-amps are widely used in signal amplification, active filters, oscillators, comparators, and regulators.

The **IC-741** is a general-purpose op-amp with a BJT differential input stage, operating from a dual supply of ±15 V. Practical (non-ideal) op-amps deviate from ideal behaviour due to internal transistor mismatches, which manifest as the parameters below.

### 3.1 Input Bias Current ( $I_B$ )

The two input terminals of the op-amp draw small dc currents due to the base currents of the input BJT pair. The **input bias current** is the average of the two:

$$I_B = \frac{I_{B1} + I_{B2}}{2}$$

> **IC-741C spec:** $I_B$ (max) = 500 nA

### 3.2 Input Offset Current ( $I_{io}$ )

Due to transistor mismatch, $I_{B1} \neq I_{B2}$. The **input offset current** is their algebraic difference:

$$I_{io} = |I_{B1} - I_{B2}|$$

> **IC-741C spec:** $I_{io}$ (max) = 200 nA

### 3.3 Input Offset Voltage ( $V_{io}$ )

The differential dc voltage that must be applied at the inputs to force the output to zero. Measured using a high closed-loop gain circuit:

$$V_{io} = \frac{V_o - I_{io} \cdot R_f}{1 + \dfrac{R_f}{R_i}}$$

> **IC-741C spec:** $V_{io}$ (max) = 6 mV

### 3.4 Slew Rate ( $S.R.$ )

The **maximum rate of change** of the output voltage in response to a large-signal step input:

$$S.R. = \frac{2\pi \cdot f_{max} \cdot V_m}{10^6} \quad \text{V/µs}$$

where $f_{max}$ is the frequency at which the output just begins to turn triangular, and $V_m$ = 3 V is the input signal amplitude.

> **IC-741C spec:** $S.R.$ = 0.5 V/µs (typical)

---

## 4. Circuit Diagrams, Procedure & Observations

---

### 4(a) — Inverting Bias Current ( $I_{B2}$ )

**Circuit Configuration:**
- Non-inverting input (Pin 3) → GND
- Feedback resistor $R_f$ = 470 kΩ connected from output (Pin 6) to inverting input (Pin 2)
- Decoupling capacitor $C_1$ = 1000 pF across supply
- Output voltage $V_o$ measured on DMM

**Formula:**

$$I_{B2} = \frac{V_o}{R_f}$$

**Simulation:**

![image alt](https://github.com/ShreyasPatil0129/LIC-lab-report/blob/86c18dd46a197c64e7af375a4ba0b03017eb4fa2/1-INVERTING%20BIAS%20CURRENT.png)

*Fig. 1 — Inverting Bias Current measurement circuit (DMM reads 0.024 V)*

**Observation & Calculation:**

| $V_o$ (V) | $R_f$ (kΩ) | $I_{B2}$ (µA) |
|:---------:|:----------:|:-------------:|
| 0.024 | 470 | **0.0510** |

$$I_{B2} = \frac{0.024}{470 \times 10^3} = 0.0510 \ \mu\text{A}$$

> ✅ **Result: $I_{B2}$ = 0.0510 µA**

---

### 4(b) — Non-Inverting Bias Current ( $I_{B1}$ )

**Circuit Configuration:**
- Inverting input (Pin 2) → GND
- Resistor $R_1$ = 470 kΩ from non-inverting input (Pin 3) to GND
- Decoupling capacitor $C_1$ = 1000 pF across supply
- Output voltage $V_o$ measured on DMM

**Formula:**

$$I_{B1} = \frac{V_o}{R_1}$$

**Simulation:**

![image alt](https://github.com/ShreyasPatil0129/LIC-lab-report/blob/86c18dd46a197c64e7af375a4ba0b03017eb4fa2/2-NON-INVERTING%20BIAS%20CURRENT.png)

*Fig. 2 — Non-Inverting Bias Current measurement circuit (DMM reads −0.020 V)*

**Observation & Calculation:**

| $V_o$ (V) | $R_1$ (kΩ) | $I_{B1}$ (µA) |
|:---------:|:----------:|:-------------:|
| −0.020 | 470 | **−0.0425** |

$$I_{B1} = \frac{-0.020}{470 \times 10^3} = -0.0425 \ \mu\text{A}$$

**Average Input Bias Current:**

$$I_B = \frac{I_{B1} + I_{B2}}{2} = \frac{-0.0425 + 0.0510}{2} = 0.00425 \ \mu\text{A}$$

> ✅ **Result: $I_{B1}$ = −0.0425 µA &nbsp;|&nbsp; $I_B$ (average) = 0.00425 µA**

---

### 4(c) — Input Offset Current ( $I_{io}$ )

**Circuit Configuration:**
- $R_f$ = 470 kΩ from output (Pin 6) to inverting input (Pin 2)
- $R_1$ = 470 kΩ from non-inverting input (Pin 3) to GND
- $C_1$, $C_2$ = 1000 pF decoupling capacitors
- Output voltage $V_o$ measured on DMM

**Formula:**

$$I_{io} = \frac{V_o}{R_f}$$

**Simulation:**

![image alt](https://github.com/ShreyasPatil0129/LIC-lab-report/blob/86c18dd46a197c64e7af375a4ba0b03017eb4fa2/3-INPUT%20OFFSET%20CURRENT.png)

*Fig. 3 — Input Offset Current measurement circuit (DMM reads 0.003 V)*

**Observation & Calculation:**

| $V_o$ (V) | $R_f$ (kΩ) | $I_{io}$ (µA) |
|:---------:|:----------:|:-------------:|
| 0.003 | 470 | **0.0063** |

$$I_{io} = \frac{0.003}{470 \times 10^3} = 0.0063 \ \mu\text{A}$$

> ✅ **Result: $I_{io}$ = 0.0063 µA**

---

### 4(d) — Input Offset Voltage ( $V_{io}$ )

**Circuit Configuration:**
- Both inputs grounded through $R_1$ = $R_2$ = 100 Ω
- Feedback resistor $R_f$ = 10 kΩ (output to inverting input)
- $C_1$ = 1000 pF decoupling capacitor
- Output voltage $V_o$ measured on DMM

**Formula:**

$$V_{io} = \frac{V_o - I_{io} \cdot R_f}{1 + \dfrac{R_f}{R_i}}$$

**Simulation:**

![image alt](https://github.com/ShreyasPatil0129/LIC-lab-report/blob/86c18dd46a197c64e7af375a4ba0b03017eb4fa2/4-INPUT%20OFFSET%20VOLTAGE.png)

*Fig. 4 — Input Offset Voltage measurement circuit (DMM reads 0.106 V)*

**Observation & Calculation:**

| $V_o$ (V) | $R_f$ (kΩ) | $R_i$ (Ω) | $I_{io}$ (µA) | $V_{io}$ (mV) |
|:---------:|:----------:|:---------:|:-------------:|:-------------:|
| 0.106 | 10 | 100 | 0.0063 | **1.048** |

$$V_{io} = \frac{0.106 - (0.0063 \times 10^{-6} \times 10{,}000)}{1 + \dfrac{10{,}000}{100}} = \frac{0.106 - 0.000063}{101} \approx 1.048 \ \text{mV}$$

> ✅ **Result: $V_{io}$ = 1.048 mV**

---

### 4(e) — Slew Rate ( $S.R.$ )

**Circuit Configuration:**
- Voltage follower (unity gain, non-inverting configuration)
- Load resistor $R_1$ = 10 kΩ
- Input: sinusoidal signal from A.F. Oscillator, $V_m$ = 3 V
- Output monitored on CRO (CH2); input on CRO (CH1)
- Frequency increased until output just becomes triangular → this is $f_{max}$

**Formula:**

$$S.R. = \frac{2\pi \cdot f_{max} \cdot V_m}{10^6} \quad \text{V/µs}$$

**Simulation:**

![image alt](https://github.com/ShreyasPatil0129/LIC-lab-report/blob/86c18dd46a197c64e7af375a4ba0b03017eb4fa2/5-SLEW%20RATE.png)

*Fig. 5 — Slew Rate measurement: CRO showing triangular distortion at $f_{max}$*

**Observation & Calculation:**

| $V_m$ (V) | $f_{max}$ | Calculated $S.R.$ |
|:---------:|:---------:|:-----------------:|
| 3 | (from CRO at triangular output) | **0.471 V/µs** |

$$S.R. = 2\pi \times f_{max} \times 3 \ / \ 10^6 = 0.471 \ \text{V/µs}$$

> ✅ **Result: $S.R.$ = 0.471 V/µs**

---

## 5. Consolidated Observation Table

| Parameter | Symbol | Formula | Measured Value | IC-741C Datasheet Limit |
|-----------|:------:|---------|:--------------:|:-----------------------:|
| Inverting Bias Current | $I_{B2}$ | $V_o / R_f$ | 0.0510 µA | ≤ 500 nA |
| Non-Inverting Bias Current | $I_{B1}$ | $V_o / R_1$ | −0.0425 µA | ≤ 500 nA |
| Average Bias Current | $I_B$ | $(I_{B1}+I_{B2})/2$ | 0.00425 µA | ≤ 500 nA |
| Input Offset Current | $I_{io}$ | $V_o / R_f$ | 0.0063 µA | ≤ 200 nA |
| Input Offset Voltage | $V_{io}$ | $(V_o - I_{io}R_f)/(1+R_f/R_i)$ | 1.048 mV | ≤ 6 mV |
| Slew Rate | $S.R.$ | $2\pi f_{max} V_m / 10^6$ | 0.471 V/µs | ≥ 0.5 V/µs |

---

## 6. Calculations Summary

```
(a)  IB2 = Vo / Rf
         = 0.024 / 470,000
         = 0.0510 µA

(b)  IB1 = Vo / R1
         = -0.020 / 470,000
         = -0.0425 µA

     IB  = (IB1 + IB2) / 2
         = (-0.0425 + 0.0510) / 2
         = 0.00425 µA

(c)  Iio = Vo / Rf
         = 0.003 / 470,000
         = 0.0063 µA

(d)  Vio = (Vo - Iio × Rf) / (1 + Rf/Ri)
         = (0.106 - 0.0063e-6 × 10,000) / (1 + 10,000/100)
         = (0.106 - 0.000063) / 101
         = 1.048 mV

(e)  S.R. = 2π × fmax × Vm / 10^6
          = 0.471 V/µs
```

---

## 7. Results

1. **Input Bias Current (Inverting), $I_{B2}$** = **0.0510 µA**
2. **Input Bias Current (Non-Inverting), $I_{B1}$** = **−0.0425 µA**
3. **Average Input Bias Current, $I_B$** = **0.00425 µA**
4. **Input Offset Current, $I_{io}$** = **0.0063 µA**
5. **Input Offset Voltage, $V_{io}$** = **1.048 mV**
6. **Slew Rate, $S.R.$** = **0.471 V/µs**

---

## 8. Conclusion

All five characteristic parameters of IC-741 Op-Amp were successfully measured and found to be within the datasheet specifications for IC-741C:

- The **input bias currents** ($I_{B1}$, $I_{B2}$) are in the nanoampere range, confirming the high input impedance of the BJT differential pair at the input stage.
- The **input offset current** (0.0063 µA) and **input offset voltage** (1.048 mV) are small values, indicating good internal transistor matching within the differential amplifier stage — well within the 200 nA and 6 mV limits respectively.
- The measured **slew rate of 0.471 V/µs** is in close agreement with the IC-741C standard value of 0.5 V/µs, confirming the limited high-frequency response of this op-amp. This low slew rate makes IC-741 unsuitable for high-frequency applications such as fast oscillators and wideband filters.

This experiment demonstrates practical techniques for measuring non-ideal op-amp parameters and reinforces the understanding of how internal imperfections affect real circuit behaviour.

---

*NIE Mysuru — Linear Integrated Circuits Lab*
