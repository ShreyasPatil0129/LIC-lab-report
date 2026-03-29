# Differential Amplifier Analysis  
## Circuit 3 — Current Mirror with Bias Control (Improved Differential Amplifier)

---

## Aim

To design and simulate a MOS differential amplifier with current mirror load and external bias control, and analyze its DC, transient, and AC performance.

---

## Introduction

In this circuit, the differential amplifier is improved by introducing **explicit bias voltages (VB1 and VB2)** to control:

- Tail current (via M3)
- PMOS current mirror (via M4, M5)

This improves:
✔ Stability  
✔ Bias accuracy  
✔ Gain control  

---

## Theory (VVVIMP)

### Structure

- M1, M2 → NMOS differential pair  
- M3 → Tail current source (controlled by VB1)  
- M4, M5 → PMOS current mirror (controlled by VB2)  

---

### Working Principle

- VB1 sets tail current → controls total current  
- VB2 sets PMOS bias → controls mirror accuracy  

👉 Operation:

- Vin1 > Vin2 → M1 conducts more → Vout1 decreases  
- Vin2 > Vin1 → M2 conducts more → Vout2 decreases  

---

### Key Advantage

✔ Better bias control than Circuit 2  
✔ More stable operating point  
✔ Higher practical gain  

---

### Key Equations

ID = (1/2) μnCox (W/L) (VGS − VT)²  
gm = 2ID / Vov  
ro = 1 / (λ ID)  
Av = gm × (ro || ro)

---

### Linearity Condition

|Vid| ≤ √2 × Vov ≈ 0.48 V  

---

## Circuit Diagram

![image alt](https://github.com/ShreyasPatil0129/LIC-lab-report/blob/d7a974a054bd284fb825cbae6db832046b1d2fb0/Experiment-4/CIRCUIT%203(1).png)

---

## Given Parameters

| Parameter | Value |
|----------|------|
| VDD | 0.9 V |
| VSS | -0.9 V |
| VB1 | -0.25 V |
| VB2 | 0.2 V |
| μnCox | 236.5 µA/V² |
| Vov,n | 0.34 V |
| λ | 0.02 V⁻¹ |
| CL | 10 pF |

---

## Design Calculations

### 1. Tail Current

ISS ≈ 1.23 mA  

---

### 2. Branch Current

ID = ISS / 2  

ID ≈ 0.616 mA  

---

### 3. Transconductance

gm = 2ID / Vov  

gm = 3.62 mS  

---

### 4. Output Resistance

ro = 1 / (λ ID)  

ro ≈ 81 kΩ  

---

### 5. Effective Output Resistance

Rout = ro || ro  

Rout ≈ 40.5 kΩ  

---

### 6. Gain (Theoretical)

Av = gm × Rout  

Av ≈ 147 V/V  

Av(dB) ≈ 43.3 dB  

---

### 7. Bandwidth

fp = 1 / (2π Rout CL)  

fp ≈ 390 kHz  

---

### 8. Slew Rate

SR = ISS / CL  

SR ≈ 123 V/µs  

---

## DC Analysis

![image alt](https://github.com/ShreyasPatil0129/LIC-lab-report/blob/d7a974a054bd284fb825cbae6db832046b1d2fb0/Experiment-4/CIRCUIT%203(2).png)

### Observed Values (From Screenshot)

| Parameter | Value |
|----------|------|
| Vout1 | -0.2719 V |
| Vout2 | -0.2719 V |
| VS | -0.7007 V |
| ID1 | 0.616 mA |
| ID2 | 0.616 mA |
| ISS | 1.233 mA |
| VB1 | -0.25 V |
| VB2 | 0.2 V |

✔ Balanced outputs  
✔ Stable bias achieved  

---

## Transient Analysis

---

### Case 1: Linear Region

Vin1 = +50mV  
Vin2 = -50mV  

Vid = 100mV < 0.48V  

![image alt](https://github.com/ShreyasPatil0129/LIC-lab-report/blob/d7a974a054bd284fb825cbae6db832046b1d2fb0/Experiment-4/CIRCUIT%203(3).png)

### Results

- Output amplitude ≈ ±600 mV  
- Vout(pp) ≈ 1.2 V  

Av(sim) = 1.2 / 0.1 = 12 V/V  

✔ Clean sinusoidal output  
✔ High gain compared to Circuit 2  

---

### Case 2: Non-Linear Region

Vin1 = +300mV  
Vin2 = -300mV  

Vid = 600mV > 0.48V  

![image alt](https://github.com/ShreyasPatil0129/LIC-lab-report/blob/d7a974a054bd284fb825cbae6db832046b1d2fb0/Experiment-4/CIRCUIT%203(4).png)

### Observation

- Output clipped near ±0.85 V  
- Strong distortion  

✔ Saturation occurs  
✔ One transistor cutoff  

---

## AC Analysis

![image alt](https://github.com/ShreyasPatil0129/LIC-lab-report/blob/d7a974a054bd284fb825cbae6db832046b1d2fb0/Experiment-4/CIRCUIT%203(5).png)

### Results (From Graph)

| Parameter | Value |
|----------|------|
| Gain | ~30 dB |
| Gain (linear) | ~31 V/V |
| Bandwidth | ~100 MHz |

---

## Comparison of Results

### Gain Comparison

| Type | Value |
|------|------|
| Theoretical | 147 V/V |
| Simulated (transient) | ~12 V/V |
| Simulated (AC) | ~31 V/V |

---

### DC Comparison

| Parameter | Theoretical | Simulated |
|----------|------------|----------|
| ID | 0.611 mA | 0.616 mA |
| ISS | 1.222 mA | 1.233 mA |
| Vout | 0 V | -0.2719 V |

---

## Complete Comparison of Values

| Parameter | Theoretical | Simulated | Remark |
|----------|------------|----------|--------|
| ISS | 1.222 mA | 1.233 mA | Very close |
| ID | 0.611 mA | 0.616 mA | Matched |
| Vout1 | 0 V | -0.2719 V | Shift due to bias |
| Vout2 | 0 V | -0.2719 V | Balanced |
| VS | -0.14 V | -0.7007 V | Bias controlled |
| Gain (theory) | 147 V/V | — | Ideal |
| Gain (AC) | — | 31 V/V | Practical |
| Gain (transient) | — | 12 V/V | Time-domain |
| Bandwidth | 390 kHz | ~100 MHz | Model dependent |
| Slew Rate | 123 V/µs | — | Theoretical |

---

## Reasons for Deviation

- Bias voltages shift DC point  
- Channel length modulation  
- Non-ideal current mirror  
- Parasitic capacitances  
- Single-ended output measurement  

---

## VERY IMPORTANT NOTE

For actual gain use:

V(vout2) - V(vout1)

---

## Inference

- Bias control improves stability  
- Higher gain than Circuit 2  
- DC operating point well controlled  
- Linear and non-linear behavior clearly observed  

---

## Conclusion

The differential amplifier with current mirror and bias control provides improved performance over previous circuits.

Key Result:  
Bias-controlled current mirror → **better stability + higher practical gain**

---
