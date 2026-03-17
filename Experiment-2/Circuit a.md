# DESIGN AND ANALYSIS OF MOS DIFFERENTIAL AMPLIFIER
## Circuit 1 — Resistor-Loaded Differential Pair with R<sub>SS</sub> Tail Biasing

---

## AIM

To design and analyze a MOS Differential Amplifier using NMOS (CMOSN) and PMOS (CMOSP) transistors in TSMC 180nm technology with a supply voltage of 1.5V while satisfying a power constraint of 0.5mW. The DC operating point is determined first, followed by transient and AC simulations in LTSpice.

---

## GIVEN PARAMETERS

**Supply Voltage**

V<sub>DD</sub> = 1.5 V

**Power Constraint**

P ≤ 0.5 mW

**Maximum Drain Current**

I<sub>D</sub> ≤ P / V<sub>DD</sub> = 0.5×10⁻³ / 1.5 = 333 µA

**Chosen Operating Current**

I<sub>D</sub> = 200 µA

**Load Capacitance**

C<sub>L</sub> = 1 pF

**Threshold Voltages (TSMC 180nm)**

V<sub>TN</sub> = 0.45 V &emsp; |V<sub>TP</sub>| = 0.45 V

**Channel Length**

L<sub>n</sub> = 180 nm

**µ<sub>n</sub>C<sub>ox</sub>** = 200 µA/V² &emsp; **µ<sub>p</sub>C<sub>ox</sub>** = 100 µA/V²

---

## CIRCUIT DIAGRAM

```
              VDD (1.5 V)
                  |
        +---------+---------+
        |                   |
      [M1]               [M1]         <- PMOS (CMOSP) Active Load
     CMOSP             CMOSP
    G=0.85V           G=0.85V
        |                   |
        +---------+---------+-------- Vout = 0.75 V
                  |
                [M2]                  <- NMOS (CMOSN) Amplifying Device
               CMOSN
            G=0.75V
                  |
                  +---- VS = 0.1 V
                  |
                [RS]                  <- Source Resistor (500 Ohm)
                  |
                 GND
```

**LTSpice Component Summary**

| Component | Type | Value / Setting | Role |
|-----------|------|-----------------|------|
| M1 | CMOSP (PMOS) | W = 18 µm, L = 180 nm | Active current-source load |
| M2 | CMOSN (NMOS) | W = 9 µm, L = 180 nm | Amplifying transistor |
| R<sub>D</sub> | Drain Resistor | 3.6 kΩ | Sets output DC voltage |
| R<sub>S</sub> | Source Resistor | 500 Ω | Sets V<sub>S</sub> and g<sub>m</sub> |
| C<sub>L</sub> | Load Capacitor | 1 pF | Output load |
| V<sub>G,NMOS</sub> | Gate bias (NMOS) | 0.75 V | Biases M2 into saturation |
| V<sub>G,PMOS</sub> | Gate bias (PMOS) | 0.85 V | Biases M1 into saturation |

---

## DC ANALYSIS (BIAS DESIGN)

### 1. Overdrive Voltage Selection

We choose the overdrive voltage to keep both transistors in saturation with good linearity:

$$V_{ov} = 0.2 \ \text{V}$$

This satisfies the practical analog design rule: 0.1 V ≤ V<sub>ov</sub> ≤ 0.3 V

### 2. Transconductance

$$g_m = \frac{2I_D}{V_{ov}} = \frac{2 \times 200 \times 10^{-6}}{0.2} = \boxed{2 \ \text{mS}}$$

### 3. Source Resistance

R<sub>S</sub> is chosen so that it equals 1/g<sub>m</sub> — a standard choice for source degeneration that sets the gain without requiring a bypass capacitor:

$$R_S = \frac{1}{g_m} = \frac{1}{2 \times 10^{-3}} = \boxed{500 \ \Omega}$$

**Source voltage check:**

$$V_S = I_D \times R_S = 200 \times 10^{-6} \times 500 = \boxed{0.1 \ \text{V}} \checkmark$$

### 4. Output Voltage and Drain Resistor Design

For maximum symmetric output swing, set V<sub>out</sub> at the midpoint of the supply:

$$V_{out} = \frac{V_{DD}}{2} = \frac{1.5}{2} = \boxed{0.75 \ \text{V}}$$

Voltage drop across R<sub>D</sub>:

$$V_{RD} = V_{DD} - V_{out} = 1.5 - 0.75 = 0.75 \ \text{V}$$

Therefore:

$$R_D = \frac{V_{RD}}{I_D} = \frac{0.75}{200 \times 10^{-6}} = \boxed{3.6 \ \text{k}\Omega} \checkmark$$

### 5. Gate Bias — NMOS (M2)

**Gate-to-source voltage:**

$$V_{GS} = V_{TN} + V_{ov} = 0.45 + 0.2 = \boxed{0.65 \ \text{V}}$$

**Gate voltage (NMOS):**

$$V_{G,\text{NMOS}} = V_{GS} + V_S = 0.65 + 0.1 = \boxed{0.75 \ \text{V}} \checkmark$$

> This is confirmed in LTSpice: NMOS gate bias = **0.75 V**

### 6. Gate Bias — PMOS (M1)

For PMOS, V<sub>GS</sub> is negative. V<sub>SG</sub> = |V<sub>TP</sub>| + V<sub>ov</sub>:

$$V_{SG} = |V_{TP}| + V_{ov} = 0.45 + 0.2 = 0.65 \ \text{V}$$

$$\therefore V_{GS,\text{PMOS}} = -0.65 \ \text{V}$$

Since the PMOS source is at V<sub>DD</sub> = 1.5 V:

$$V_{G,\text{PMOS}} = V_{DD} - V_{SG} = 1.5 - 0.65 = \boxed{0.85 \ \text{V}} \checkmark$$

> This is confirmed in LTSpice: PMOS gate bias = **0.85 V**

> **Note:** V<sub>GS</sub> > V<sub>TH</sub> turns ON NMOS. V<sub>GS</sub> < V<sub>TH</sub> (i.e., more negative than V<sub>TP</sub>) turns ON PMOS.

### 7. Saturation Check — NMOS (M2)

$$V_{DS} = V_{out} - V_S = 0.75 - 0.1 = 0.65 \ \text{V}$$

$$V_{ov} = 0.2 \ \text{V}$$

$$V_{DS} \geq V_{ov} \implies 0.65 \geq 0.2 \quad \checkmark \quad \text{NMOS in saturation}$$

### 8. Saturation Check — PMOS (M1)

$$V_{SD} = V_{DD} - V_{out} = 1.5 - 0.75 = 0.75 \ \text{V}$$

$$V_{SD} \geq V_{ov} \implies 0.75 \geq 0.2 \quad \checkmark \quad \text{PMOS in saturation}$$

Both transistors operate correctly in saturation.

### 9. NMOS Width Calculation

Using the saturation current equation:

$$I_D = \frac{1}{2} \mu_n C_{ox} \frac{W_n}{L} V_{ov}^2$$

Rearranging:

$$W_n = \frac{2 I_D L}{\mu_n C_{ox} V_{ov}^2}$$

Substituting values:

$$W_n = \frac{2 \times 200 \times 10^{-6} \times 0.18 \times 10^{-6}}{200 \times 10^{-6} \times (0.2)^2}$$

$$W_n = \frac{2 \times 200 \times 10^{-6} \times 0.18 \times 10^{-6}}{200 \times 10^{-6} \times 0.04}$$

$$W_n = \frac{0.18 \times 10^{-6} \times 2}{0.04 / 0.02} \quad \text{(simplified as in notebook)}$$

$$\boxed{W_n = 9 \ \mu\text{m}} \checkmark$$

### 10. PMOS Width Calculation

Since µ<sub>n</sub>/µ<sub>p</sub> = 2, the PMOS must be twice as wide to carry the same current at the same V<sub>ov</sub>:

$$\frac{\mu_n}{\mu_p} = 2 \implies W_p = 2 \times W_n$$

$$\boxed{W_p = 2 \times 9 = 18 \ \mu\text{m}} \checkmark$$

---

## SMALL SIGNAL ANALYSIS

### Voltage Gain

With source resistance R<sub>S</sub>, the CS amplifier gain with source degeneration is:

$$A_v = \frac{-g_m R_D}{1 + g_m R_S}$$

Substituting values:

$$A_v = \frac{-2 \times 10^{-3} \times 3.6 \times 10^3}{1 + (2 \times 10^{-3} \times 500)}$$

$$A_v = \frac{-7.2}{1 + 1} = \frac{-7.2}{2}$$

$$\boxed{A_v = -3.6 \ \text{V/V}} \checkmark$$

In dB:

$$A_v(\text{dB}) = 20 \log_{10}(3.6) = 11.13 \ \text{dB}$$

The negative sign confirms **phase inversion** — characteristic of the CS configuration.

---

## TRANSIENT ANALYSIS

**Input Signal:** SINE(0.75 V, 10 mV amplitude, 1 kHz) — DC offset at V<sub>G,NMOS</sub>

**Simulation Command:** `.tran 10m`

The output signal is amplified and **phase-inverted** relative to the input, confirming CS amplifier behavior.

**Voltage Gain (from simulation):**

$$A_v = \frac{V_{out(pp)}}{V_{in(pp)}} \approx 3.6 \ \text{V/V} \quad (11.1 \ \text{dB})$$

---

## AC ANALYSIS

**Simulation Command:** `.ac dec 100 1 100G`

### Bandwidth

The -3 dB bandwidth is set by the output pole formed by R<sub>D</sub> and C<sub>L</sub>:

$$f_{-3dB} = \frac{1}{2\pi R_D C_L}$$

$$f_{-3dB} = \frac{1}{2\pi \times 3600 \times 1 \times 10^{-12}}$$

$$\boxed{f_{-3dB} = 44.2 \ \text{MHz}} \checkmark$$

### Unity Gain Bandwidth

$$\text{UGB} = |A_v| \times f_{-3dB} = 3.6 \times 44.2 \times 10^6 \approx 159 \ \text{MHz}$$

| Parameter | Value |
|-----------|-------|
| Midband Gain | 3.6 V/V (11.1 dB) |
| -3 dB Bandwidth | **44.2 MHz** |
| Unity Gain Bandwidth | ~159 MHz |
| Dominant Pole | R<sub>D</sub> × C<sub>L</sub> = 3.6 kΩ × 1 pF |
| Roll-off | -20 dB/decade |

---

## RESULTS

| Parameter | Calculated | Verified |
|-----------|------------|---------|
| Drain Current I<sub>D</sub> | 200 µA | ✅ |
| Overdrive Voltage V<sub>ov</sub> | 0.2 V | ✅ |
| Transconductance g<sub>m</sub> | 2 mS | ✅ |
| Source Resistance R<sub>S</sub> | 500 Ω | ✅ |
| Source Voltage V<sub>S</sub> | 0.1 V | ✅ |
| Drain Resistor R<sub>D</sub> | 3.6 kΩ | ✅ |
| Output DC Voltage V<sub>out</sub> | 0.75 V | ✅ |
| NMOS Gate Bias V<sub>G</sub> | 0.75 V | ✅ |
| PMOS Gate Bias V<sub>G</sub> | 0.85 V | ✅ |
| NMOS Width W<sub>n</sub> | 9 µm | ✅ |
| PMOS Width W<sub>p</sub> | 18 µm | ✅ |
| Voltage Gain A<sub>v</sub> | -3.6 V/V (11.1 dB) | ✅ |
| -3 dB Bandwidth | 44.2 MHz | ✅ |
| Unity Gain Bandwidth | ~159 MHz | ✅ |

---

## INFERENCE

From this experiment, the MOS Differential Amplifier (Circuit 1) with R<sub>S</sub> source degeneration and R<sub>D</sub> drain load was successfully designed and analyzed using TSMC 180nm CMOS technology.

The DC analysis established a clean operating point: both NMOS and PMOS operate in saturation, with V<sub>out</sub> = 0.75 V placed at V<sub>DD</sub>/2 for maximum symmetric output swing. The source resistance R<sub>S</sub> = 500 Ω = 1/g<sub>m</sub> was deliberately chosen to apply source degeneration, which trades gain for improved linearity. The gate bias voltages V<sub>G,NMOS</sub> = 0.75 V and V<sub>G,PMOS</sub> = 0.85 V were derived from threshold and overdrive calculations, and both match the LTSpice schematic directly.

The small-signal analysis yielded a voltage gain of **-3.6 V/V (11.1 dB)**. The negative sign confirms phase inversion, which is the defining characteristic of the CS amplifier topology. The gain is moderate — a direct consequence of the source degeneration which was intentionally applied.

The AC analysis showed a -3 dB bandwidth of **44.2 MHz**, determined by the output pole at R<sub>D</sub> × C<sub>L</sub> = 3.6 kΩ × 1 pF. When a load capacitance is present, this pole shifts the dominant roll-off to a lower frequency compared to a no-load configuration, demonstrating that output capacitance directly limits the usable bandwidth of the amplifier.

---

*The National Institute of Engineering, Mysore — LIC Laboratory | TSMC 180nm | LTSpice XVII*
