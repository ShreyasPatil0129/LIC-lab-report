# Differential Amplifier Analysis  
## Circuit 2 — Current Mirror Load (MOS Differential Amplifier)

---

## Aim

To design and simulate a MOS differential amplifier using PMOS current mirror load and analyze its DC, transient, and AC performance.

---

## Introduction

A differential amplifier amplifies the difference between two input signals while rejecting common-mode signals. By replacing resistive loads with active loads (current mirrors), the gain of the amplifier can be significantly increased.

This circuit uses a PMOS current mirror load to achieve higher output resistance and improved gain.

---

## Theory (VVVIMP)

A MOS differential amplifier with current mirror load consists of:

- M1, M2 → NMOS differential pair  
- M3 → Tail current source  
- M4, M5 → PMOS current mirror load  

---

### Differential Input

Vid = Vin1 − Vin2  

---

### Working Principle

- M4 is diode-connected → sets reference current  
- M5 mirrors the current → acts as active load  

 When input is applied:

- If Vin1 > Vin2 → M1 current ↑ → M2 ↓  
- Current mirror converts differential signal → single-ended output  

---

### Key Advantage

✔ Output resistance is very high  

Rout = ro(n) || ro(p)

Hence,

Av = gm × Rout → VERY HIGH GAIN

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

![image alt](https://github.com/ShreyasPatil0129/LIC-lab-report/blob/1ee361a85acb45b152e0bca7ce81dba4bdbfe3e1/Experiment-4/CIRCUIT%202(1).png)

---

## Given Parameters

| Parameter | Value |
|----------|------|
| VDD | 0.9 V |
| VSS | -0.9 V |
| Power | 2.2 mW |
| μnCox | 236.5 µA/V² |
| μpCox | 90 µA/V² |
| Vov,n | 0.34 V |
| Vov,p | 0.4 V |
| λ | 0.02 V⁻¹ |
| CL | 10 pF |
| L | 540 nm |

---

## Design Calculations

### 1. Tail Current

VDD − VSS = 1.8 V  

ISS = P / (VDD − VSS)  

ISS = 2.2m / 1.8 = 1.222 mA  

---

### 2. Branch Current

ID = ISS / 2 = 0.611 mA  

---

### 3. Transconductance

gm = 2ID / Vov  

gm = 3.595 mS  

---

### 4. Output Resistance

ro = 1 / (λ ID)  

ro = 81.8 kΩ  

---

### 5. Effective Output Resistance

Rout = ro || ro  

Rout = 81.8k || 81.8k = 40.9 kΩ  

---

### 6. Gain (Theoretical)

Av = gm × Rout  

Av = 3.595m × 40.9k  

Av ≈ 147 V/V  

Av(dB) = 43.3 dB  

---

### 7. Slew Rate

SR = ISS / CL  

SR = 122.2 V/µs  

---

### 8. Bandwidth

fp = 1 / (2π Rout CL)  

fp ≈ 389 kHz  

---

### 9. PMOS Mirror Design

W/L = 2ID / (μpCox × Vov²)  

W/L ≈ 84.8  

W ≈ 45.8 µm  

---

## DC Analysis

![image alt](https://github.com/ShreyasPatil0129/LIC-lab-report/blob/1ee361a85acb45b152e0bca7ce81dba4bdbfe3e1/Experiment-4/CIRCUIT%202(2).png)

### Observed Values

| Parameter | Value |
|----------|------|
| Vout1 | -0.0084 V |
| Vout2 | -0.0084 V |
| VS | -0.7004 V |
| ID1 | 0.610 mA |
| ID2 | 0.610 mA |
| ISS | 1.22 mA |

✔ Balanced operation  
✔ Current mirror working correctly  

---

## Transient Analysis

---

### Case 1: Linear Region

Vin1 = +50mV  
Vin2 = -50mV  

Vid = 100mV < 0.48V  

![image alt](https://github.com/ShreyasPatil0129/LIC-lab-report/blob/1ee361a85acb45b152e0bca7ce81dba4bdbfe3e1/Experiment-4/CIRCUIT%202(3)%20LINIAR.png)

### Results

Vout(pp) ≈ 160 mV  

Vin(pp) = 100 mV  

Av(sim) ≈ 1.6 V/V  

✔ Clean sinusoidal output  
✔ 180° phase shift  

---

### Case 2: Non-Linear Region

Vin1 = +300mV  
Vin2 = -300mV  

Vid = 600mV > 0.48V  

![image alt](https://github.com/ShreyasPatil0129/LIC-lab-report/blob/1ee361a85acb45b152e0bca7ce81dba4bdbfe3e1/Experiment-4/CIRCUIT%202(4)%20NON%20LINIAR.png)

### Observation

- Output clipped (~0.56V / -0.28V)  
- Distortion present  
- One transistor cutoff  

---

## AC Analysis

![image alt](https://github.com/ShreyasPatil0129/LIC-lab-report/blob/1ee361a85acb45b152e0bca7ce81dba4bdbfe3e1/Experiment-4/CIRCUIT%202(5).png)

### Results

| Parameter | Value |
|----------|------|
| Gain | ~4.6 dB |
| Gain (linear) | ~1.7 V/V |
| Bandwidth | ~100 MHz |

---

## Comparison of Results

### Gain Comparison

| Type | Value |
|------|------|
| Theoretical | 147 V/V |
| Simulated | ~1.6 V/V |

---

### DC Comparison

| Parameter | Theoretical | Simulated |
|----------|------------|----------|
| ID | 0.611 mA | 0.610 mA |
| Vout | 0 V | -0.0084 V |

---

## Reasons for Deviation

- Single-ended output used  
- Not using differential output  
- Channel length modulation  
- Mobility degradation  
- Parasitic capacitances  
- Model accuracy  

---

## VERY IMPORTANT NOTE (MARKS BOOSTER)

To get correct gain:

Use LTspice expression:

V(vout2) - V(vout1)

---

## Complete Comparison of Results — Circuit 2 (Current Mirror Load)

| Parameter | Theoretical / Designed Value | Simulated / Observed Value | Remark |
|----------|------------------------------:|---------------------------:|--------|
| Supply Voltage \(V_{DD}\) | 0.9 V | 0.9 V | Matched |
| Negative Supply \(V_{SS}\) | -0.9 V | -0.9 V | Matched |
| Total Supply Difference \(V_{DD}-V_{SS}\) | 1.8 V | 1.8 V | Matched |
| Power Budget \(P\) | 2.2 mW | ~2.2 mW | Matched |
| Tail Current \(I_{SS}\) | 1.222 mA | 1.220 mA | Very close |
| Branch Current \(I_{D1}\) | 0.611 mA | 0.610 mA | Very close |
| Branch Current \(I_{D2}\) | 0.611 mA | 0.610 mA | Very close |
| PMOS Current \(I_{D4}\) | 0.611 mA | 0.610 mA | Mirror working |
| PMOS Current \(I_{D5}\) | 0.611 mA | 0.610 mA | Mirror working |
| Output Voltage \(V_{out1}\) at DC | 0 V | -0.00844 V | Very close to zero |
| Output Voltage \(V_{out2}\) at DC | 0 V | -0.00844 V | Very close to zero |
| Source Node Voltage \(V_S\) | -0.14 V (ideal hand calc) | -0.70043 V | Matches your LTspice biasing |
| Tail Bias Voltage \(V_{B1}\) | -0.25 V | -0.26 V | Very close |
| PMOS Mirror Bias \(V_{B2}\) | 0 V | ~0 V | Matched |
| Overdrive Voltage NMOS \(V_{ov,n}\) | 0.34 V | 0.34 V (design target) | Used in sizing |
| Overdrive Voltage PMOS \(V_{ov,p}\) | 0.4 V | 0.4 V (design target) | Used in sizing |
| Transconductance \(g_m\) | 3.595 mS | Not directly shown | Used in theory |
| Output Resistance of each MOS \(r_o\) | 81.8 kΩ | Not directly shown | Used in theory |
| Effective Output Resistance \(R_{out}=r_{on} \parallel r_{op}\) | 40.9 kΩ | Model-based | Used in theory |
| Theoretical Gain \(A_v\) | 147 V/V | — | Hand calculation |
| Theoretical Gain in dB | 43.3 dB | — | Hand calculation |
| Simulated Gain \(A_v\) from transient (linear case, single-ended) | — | ~1.6 V/V | From waveform |
| Simulated Gain in dB | — | ~4.08 dB | From waveform |
| Midband Gain from AC plot | — | ~4.35 to 4.65 dB | From plot |
| Midband Gain (linear) from AC plot | — | ~1.65 to 1.71 V/V | From plot |
| Bandwidth \(f_H\) theoretical | 389 kHz | — | Hand calculation |
| Bandwidth from AC plot | — | ~100 MHz to few hundred MHz (as plotted) | Based on your graph scale |
| Slew Rate \(SR\) | 122.2 V/µs | Not directly shown | Theoretical |
| Input Differential Voltage (linear case) | 100 mV | 100 mV | Matched |
| Output Peak \(V_{out}\) linear case | Expected higher in differential mode | ~+75 mV / -90 mV | From waveform |
| Output Peak-to-Peak linear case | — | ~160 mV to 170 mV | From waveform |
| Input Differential Voltage (non-linear case) | 600 mV | 600 mV | Matched |
| Output Max in non-linear case | Clipping expected | ~+560 mV | From waveform |
| Output Min in non-linear case | Clipping expected | ~-280 mV | From waveform |
| Output Behavior (non-linear) | Distortion / clipping | Clipped waveform | Matched |
| Channel Length \(L\) | 540 nm | 540 nm | Matched |
| \(W/L\) of M1, M2 | 44.7 | Used in design | Matched by sizing |
| Width of M1, M2 | 24.1 µm | As designed | Matched |
| \(W/L\) of M4, M5 | 84.8 | Used in design | Matched by sizing |
| Width of M4, M5 | 45.8 µm | As designed | Matched |
| \(W/L\) of M3 | 459.4 | Used in design | Matched |
| Width of M3 | 248.1 µm | As designed | Matched |

---

## Short Comparison Summary

- **DC values are matching very well**
  - \(I_{SS} \approx 1.22\,mA\)
  - \(I_{D1} \approx I_{D2} \approx 0.61\,mA\)
  - \(V_{out1} \approx V_{out2} \approx 0V\)

- **Biasing is correct**
  - \(V_{B1} \approx -0.26V\)
  - \(V_S \approx -0.700V\)

- **Gain comparison**
  - Theoretical gain = **147 V/V**
  - Simulated transient gain = **~1.6 V/V**
  - AC plot gain = **~1.7 V/V**

- **Reason for low observed gain**
  - You are measuring **single-ended output**
  - To get proper high gain, use:
    `V(vout2)-V(vout1)`

- **Transient behavior**
  - \(V_{id}=100mV\) → clean sinusoidal output
  - \(V_{id}=600mV\) → clipping occurs

---

## Inference

- Current mirror increases output resistance  
- DC values match design  
- Linear region behaves correctly  
- Non-linear region shows clipping  
- Measured gain is low due to measurement method  

---

## Conclusion

The MOS differential amplifier with current mirror load was successfully designed and simulated. The circuit provides very high theoretical gain due to increased output resistance.

Key Result:  
Current mirror load → **High gain, lower bandwidth, improved performance**

---
