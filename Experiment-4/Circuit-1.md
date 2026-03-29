# Differential Amplifier Analysis  
## Circuit 1 — Resistive Load (MOS Differential Amplifier)

---

## Aim

To design and simulate a MOSFET differential amplifier with resistive load using LTspice and analyze its DC, transient, and AC performance.

---

## Introduction

A differential amplifier amplifies the difference between two input signals while rejecting common-mode signals. It is a fundamental building block in analog circuit design and is widely used in operational amplifiers and signal processing systems.

This experiment focuses on a MOS differential amplifier using resistive loads and evaluates its gain, linearity, and frequency response.

---

## Theory (VVVIMP)

A MOS differential amplifier consists of two matched NMOS transistors (M1 and M2) whose sources are connected together and biased using a constant current source. The drains are connected to resistive loads.

### Differential Input

Vid = Vin1 − Vin2

### Working Principle

- If Vin1 > Vin2 → M1 current increases, M2 decreases  
- If Vin2 > Vin1 → M2 current increases, M1 decreases  

This change in current creates voltage drop across RD, producing output.

---

### Key Equations

ID = (1/2) μnCox (W/L) (VGS − VT)²  
gm = 2ID / Vov  
ro = 1 / (λ ID)  
Av = gm × RD  

---

### Linearity Condition (VERY IMPORTANT)

|Vid| ≤ √2 × Vov ≈ 0.48 V  

- Below → Linear operation  
- Above → Clipping occurs  

---

## Circuit Diagram

![image alt](https://github.com/ShreyasPatil0129/LIC-lab-report/blob/f644ea245f1d9985d3211de5ea4a73ccf2a8c48e/Experiment-4/CIRCUIT%201(0).png)

---

## Given Parameters

| Parameter | Value |
|----------|------|
| VDD | 0.9 V |
| VSS | -0.9 V |
| Power | 2.2 mW |
| μnCox | 236.5 µA/V² |
| Vov | 0.34 V |
| λ | 0.02 V⁻¹ |
| CL | 10 pF |
| L | 540 nm |

---

## Design Calculations

### Tail Current

VDD − VSS = 1.8 V  
ISS = P / (VDD − VSS)  
ISS = 2.2m / 1.8 = 1.222 mA  

---

### Branch Current

ID = ISS / 2 = 0.611 mA  

---

### Drain Resistance

RD = VDD / ID  
RD = 0.9 / 0.611m = 1.47 kΩ  

---

### Transconductance

gm = 2ID / Vov  
gm = 3.59 mS  

---

### Output Resistance

ro = 1 / (λ ID)  
ro = 81.8 kΩ  

Since ro >> RD → Rout ≈ RD  

---

### Gain (Theoretical)

Av = gm × RD  
Av = 5.28 V/V  

Av(dB) = 14.45 dB  

---

### Bandwidth

fp = 1 / (2π RD CL)  
fp = 10.8 MHz  

---

### Slew Rate

SR = ISS / CL  
SR = 122.2 V/µs  

---

### W/L Calculation

W/L = 44.7  
W = 24.1 µm  

---

## DC Analysis

![image alt](https://github.com/ShreyasPatil0129/LIC-lab-report/blob/f644ea245f1d9985d3211de5ea4a73ccf2a8c48e/Experiment-4/CIRCUIT%201(1).png)

### Observed Values

| Parameter | Value |
|----------|------|
| Vout1 | ~0.0033 V |
| Vout2 | ~0.0033 V |
| VS | ~ -0.646 V |
| ID | ~0.61 mA |
| ISS | ~1.22 mA |

✔ Balanced operation  
✔ Proper biasing  


## Transient Analysis

### Case 1: Linear Region

Vin1 = +50mV  
Vin2 = -50mV  
Vid = 100mV < 0.48V  

![image alt](https://github.com/ShreyasPatil0129/LIC-lab-report/blob/f644ea245f1d9985d3211de5ea4a73ccf2a8c48e/Experiment-4/CIRCUIT%201(2)%20LINIAR.png)

Vout(pp) ≈ 0.712 V  
Vin(pp) = 0.1 V  

Av(sim) = 7.12 V/V  
Av(dB) = 17.05 dB  

✔ Output is sinusoidal  
✔ 180° phase shift  



### Case 2: Non-Linear Region

Vin1 = +300mV  
Vin2 = -300mV  
Vid = 600mV > 0.48V  

![image alt](https://github.com/ShreyasPatil0129/LIC-lab-report/blob/f644ea245f1d9985d3211de5ea4a73ccf2a8c48e/Experiment-4/CIRCUIT%201(3)%20NON%20LINIAR.png)


✔ Output clipped (~±0.75V)  
✔ Distortion present  
✔ One transistor cutoff  



## AC Analysis

![image alt](https://github.com/ShreyasPatil0129/LIC-lab-report/blob/f644ea245f1d9985d3211de5ea4a73ccf2a8c48e/Experiment-4/CIRCUIT%201(4).png)

### Results

| Parameter | Value |
|----------|------|
| Gain | ~14–17 dB |
| Bandwidth | ~5–10 MHz |



## Comparison of Results

### Gain Comparison

| Type | Value |
|------|------|
| Theoretical | 5.28 V/V |
| Simulated | 7.12 V/V |

---

### DC Comparison

| Parameter | Theoretical | Simulated |
|----------|------------|----------|
| ID | 0.611 mA | 0.61 mA |
| Vout | 0 V | 0.0033 V |

---

## Complete Comparison of Results — Circuit 1

| Parameter | Theoretical / Designed Value | Simulated / Observed Value | Remark |
|----------|------------------------------:|---------------------------:|--------|
| Supply Voltage \(V_{DD}\) | 0.9 V | 0.9 V | Matched |
| Negative Supply \(V_{SS}\) | -0.9 V | -0.9 V | Matched |
| Total Supply Difference \(V_{DD}-V_{SS}\) | 1.8 V | 1.8 V | Matched |
| Power Budget \(P\) | 2.2 mW | ~2.2 mW | Matched |
| Tail Current \(I_{SS}\) | 1.222 mA | 1.22 mA | Very close |
| Branch Current \(I_{D1}\) | 0.611 mA | 0.61 mA | Very close |
| Branch Current \(I_{D2}\) | 0.611 mA | 0.61 mA | Very close |
| Drain Resistance \(R_D\) | 1.473 kΩ | 1.47 kΩ | Matched |
| Drain Resistance \(R_{D2}\) | 1.473 kΩ | 1.47 kΩ | Matched |
| Output Voltage \(V_{out1}\) at DC | 0 V | 0.0033 V | Very close to zero |
| Output Voltage \(V_{out2}\) at DC | 0 V | 0.0033 V | Very close to zero |
| Source Node Voltage \(V_S\) | -0.14 V | -0.646 V | Differs due to model/actual bias point |
| Overdrive Voltage \(V_{ov}\) | 0.34 V | ~0.34 V (design target) | Used for sizing |
| Transconductance \(g_m\) | 3.595 mS | Not directly shown | Used in theory |
| MOS Output Resistance \(r_o\) | 81.8 kΩ | Not directly shown | Used in theory |
| Effective Output Resistance \(R_{out}\) | 1.473 kΩ | ~1.47 kΩ | Since \(r_o \gg R_D\) |
| Theoretical Gain \(A_v\) | 5.29 V/V | — | From hand calculation |
| Theoretical Gain in dB | 14.46 dB | — | From hand calculation |
| Simulated Gain \(A_v\) from waveform | — | 7.12 V/V | From transient waveform |
| Simulated Gain in dB | — | 17.05 dB | From transient waveform |
| Input Differential Voltage (linear case) | 100 mV | 100 mV | Matched |
| Output Peak-to-Peak (linear case) | ~0.529 V (expected from theory) | ~0.712 V | Simulated is higher |
| Input Differential Voltage (non-linear case) | 600 mV | 600 mV | Matched |
| Output Swing in non-linear case | Clipping expected | ~±0.75 V clipped | Matches behavior |
| Bandwidth \(f_H\) | 10.8 MHz | ~5–10 MHz | Same order, depends on AC plot |
| Gain Bandwidth Product (GBW) | 57.2 MHz | Not directly measured from screenshot | Theoretical |
| Slew Rate \(SR\) | 122.2 V/µs | Not directly shown | Theoretical |
| Channel Length \(L\) | 540 nm | 540 nm | Matched |
| \(W/L\) of M1, M2 | 44.7 | Used in design | Matched by sizing |
| Width of M1, M2 | 24.1 µm | As designed in LTspice | Matched |

---

## Short Comparison Summary

- **DC values** are matching very well:
  - \(I_{SS} \approx 1.22\,mA\)
  - \(I_D \approx 0.61\,mA\)
  - \(V_{out1} \approx V_{out2} \approx 0V\)

- **Gain comparison**:
  - Theoretical gain = **5.29 V/V**
  - Simulated gain = **7.12 V/V**

- **Linear transient case**:
  - Input = **100 mV differential**
  - Output = clean sinusoidal waveform

- **Non-linear transient case**:
  - Input = **600 mV differential**
  - Output = clipped waveform

- **Frequency response**:
  - Theoretical bandwidth = **10.8 MHz**
  - Simulated bandwidth = around **same order**, depending on exact AC plot reading

---

## Reasons for Deviation

- Channel length modulation  
- Mobility degradation  
- Parasitic capacitances  
- LTspice model accuracy  
- Operating point variation  

---

## Inference

- Circuit is properly biased  
- DC matches expected values  
- Linear region shows clean amplification  
- Non-linear region shows clipping  
- Gain slightly higher due to real effects  

---

## Conclusion

The MOS differential amplifier with resistive load was successfully designed and simulated. The circuit shows correct DC biasing, expected gain behavior, and proper transition between linear and non-linear regions.

👉 Key Result:  
Resistive load provides **low gain but high bandwidth** due to low output resistance.

---
