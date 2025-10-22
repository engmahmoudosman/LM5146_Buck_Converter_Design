# LM5146 Buck Converter PCB Design Documentation   
**Author:** Mahmoud Esameldin Osman  
**Date:** 14.01.2025  
 

---

## Task Description

This laboratory task involves the complete design of a prototype Printed Circuit Board (PCB) of a DC-DC Buck converter evaluation module based on the **LM5146-Q1 controller IC**.  
The task includes schematic and layout design.  

### Design Specifications

| Specification | Description |
|----------------|-------------|
| Input voltage range | 15V – 80V |
| Typical input voltage | 48V |
| Output voltage | 12V |
| Maximum output current | 6A |
| Efficiency | 96% |
| Switching frequency | 400kHz |

---

## Calculations

To correctly implement the schematic, the **Application Circuit 2** from the LM5146-Q1 datasheet was used as a guide. MATLAB was used for the calculations.

### Inductor

**Equation 1:**  
\[
L_F = \frac{V_{OUT}}{V_{IN}} \times \frac{(V_{IN} - V_{OUT})}{f_{sw} \times \Delta I_L}
\]

Given:
- \(V_{IN} = 48V\)
- \(V_{OUT} = 12V\)
- \(f_{sw} = 400kHz\)
- \(I_{MAX} = 6A\)
- \(\Delta I_L = 0.2 \times I_{MAX}\)

\[
L_F = 18µH
\]

---

### Output Capacitor (COUT)

**Equation 2:**  
\[
C_{OUT} = \frac{\Delta I_L}{8 \times f_{sw} \times \sqrt{(\Delta V_{OUT})^2}}
\]

Given:
- \(\Delta V_{OUT} = 0.01 \times V_{OUT}\)

\[
C_{OUT} = 3.12µF
\]

Because ceramic capacitor ESR is negligible, it was ignored.  
To meet the ripple spec (2% of max output current), a higher value was selected:  
**COUT = 3 × 22µF**

---

### Input Capacitor (CIN)

**Equation 3:**  
\[
C_{IN} = \frac{D (1-D) I_{MAX}}{f_{sw} \times \Delta V_{IN}}
\]

Given:
- \(D = 0.5\)
- \(\Delta V_{IN} = 0.01 \times V_{IN}\)

\[
C_{IN} = 7.81µF
\]

Used:
- 4 × 4.7µF  
- 2 × 10nF  
- 2 × 100nF (decoupling capacitors)  
All X7R type for low impedance and high RMS current.

---

### Other Components

Using TI’s **Quickstart Design Calculator**, values of RUV1 and RUV2 were selected.

- **RRT = 24.9kΩ** for 400kHz switching frequency (per datasheet Table 8-1).  
- Added **2.2Ω resistor** in series with the boot capacitor to reduce voltage ringing and peak amplitude at the SW node.

---

## Schematic Design

The schematic uses **EN-60617 standard** circuit symbols.  
Seven test points were added for measurement and debugging.

| Test Point | Net Label |
|-------------|------------|
| TP1 | VIN |
| TP2 | SYNC OUT |
| TP3 | PGOOD |
| TP4 | FB |
| TP5 | VOUT |
| TP6 | SW |
| TP7 | GND |

*(Refer to Figure 3 in the PDF for the full schematic.)*

---

## Layout Design

The PCB layout is based on the LM5146-Q1 datasheet guidelines, using **copper-filled polygon areas** for power routing and **tracks for signals**.

- **Minimum clearance:** 0.6mm for HV nets, 0.15mm for others (per IPC-2221B).  
- **Layer stack-up:** 8 layers (chosen due to lower production cost at Eurocircuits).

### Polygon Pours

| Layer | Polygon Pour Nets |
|--------|------------------|
| 1 | Signals and Power (GND, VIN, VOUT) |
| 2 | Power (GND) |
| 3 | Power (VIN) |
| 4 | Power (GND) |
| 5 | Power (VOUT) |
| 6 | Power (GND) |
| 7 | Power (GND) |
| 8 | Signals and Power (GND) |

*(Refer to Figures 4–14 in the PDF for visual layout and pours.)*

---

## Price Analysis

Using **Eurocircuits PCB manufacturer** pricing tool:  
- **Board size:** 65mm × 40mm  
- **Cost estimate:** €201.70 for one board  

---

## 3D PCB Views

The final PCB was visualized in 3D, showing:
- **Top View**
- **Bottom View**
- **Custom Perspective**

*(Refer to Figures 15–17 in the PDF for 3D renders.)*

---

## References

1. [LM5146 Datasheet](https://www.ti.com/lit/ds/symlink/lm5146.pdf)  
2. [LM5146DESIGN-CALC Tool | TI.com](https://www.ti.com/tool/LM5146DESIGN-CALC)  
3. [Liste der Schaltzeichen (Elektrik/Elektronik) – Wikipedia](https://de.wikipedia.org/wiki/Liste_der_Schaltzeichen_(Elektrik/Elektronik))  
4. [Using an IPC-2221 PCB Clearance Calculator for High Voltage Design – Altium](https://resources.altium.com/p/using-an-ipc-2221-calculator-for-high-voltage-design)  
5. [Eurocircuits PCB Manufacturer](https://www.eurocircuits.com)  
