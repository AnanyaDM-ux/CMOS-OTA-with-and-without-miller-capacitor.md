# CMOS-OTA-with-and-without-miller-capacitor.md
# CMOS Operational Transconductance Amplifier (OTA) with and without Miller Capacitor

This project presents a comparative analysis of two two-stage CMOS Operational Transconductance Amplifier (OTA) designs—one employing traditional **Miller compensation** and the other using a novel **non-Miller compensation** approach. Both designs were implemented in **180 nm CMOS technology** using **LTspice** simulations.

---

## 📌 Abstract

This report presents a comparative analysis of two OTA designs: one with traditional Miller compensation and the other without a Miller capacitor. The Miller OTA features a two-stage differential amplifier using a 2 pF capacitor for frequency compensation. The non-Miller OTA introduces a Class A-AB architecture using dual nMOS and pMOS input pairs and a MOSFET-based RC compensation network.

Simulation results show:
- **Miller OTA**: Higher gain (77.2 dB), higher power (450 µW)
- **Non-Miller OTA**: Better phase margin (up to 142.8°), higher slew rate (142.6 V/µs), lower power (103.5 µW)

---

## 🧠 Introduction

Operational Transconductance Amplifiers (OTAs) are core components in analog and mixed-signal systems, including filters, ADCs, and sensor interfaces. This work addresses the performance trade-offs between conventional Miller-compensated OTAs and novel non-Miller compensated OTAs for high-speed, low-power applications.

---

## 🏗️ Circuit Architecture

### 1. Miller Compensated OTA

- Differential input using NMOS (M1, M2) with PMOS loads (M3, M4)
- Gain stage with common-source amplifier (M7) and load (M6)
- Miller compensation using a capacitor from M7's output to its gate

![Image](https://github.com/user-attachments/assets/a7ed26f4-8cc2-44f4-b0e3-65ebd5f7e895)\
Miller Compensated Circuit

---

### 2. Non-Miller OTA (Class A-AB)

- Dual differential input pairs (nMOS + pMOS)
- RC compensation using MOSFET-based transmission gates and capacitive elements
- Dominant pole placed at output to avoid RHP zero

![Image](https://github.com/user-attachments/assets/32cf4dcb-3f61-47b3-b2da-846e24e75e2f)\
Without Miller Compensated Circuit

---

## 🔧 Design Methodology

### Common Design Details:
- **Technology**: TSMC 180 nm CMOS
- **Supply Voltage**: 1.8 V
- **Bias Current**: 250 µA

### Key Parameters:
| Parameter          | Value            |
|--------------------|------------------|
| W/L (typical)      | Various (µm/0.18 µm) |
| Compensation Cap   | 2 pF (Miller OTA) |
| RC Network         | MOSFET-based (Non-Miller OTA) |

---

## 🧮 Equations Used

### Miller Compensation OTA Gain:
\[
A_v = g_{m1} \cdot r_{o1} \cdot g_{m2} \cdot r_{o2}
\]

### Bandwidth and UGB:
\[
\text{UGB} = \frac{g_m}{2\pi C_c}
\]

---

## 📈 Simulation Results

### A. Miller OTA
| Metric             | Value            |
|--------------------|------------------|
| DC Gain            | 77.2 dB          |
| Phase Margin       | > 60°            |
| GBW                | 8.6 MHz          |
| Power              | 450 µW           |

### B. Non-Miller OTA

#### For different load capacitances (CL):

| Parameter         | CL = 1pF | CL = 10pF | CL = 70pF |
|------------------|----------|-----------|-----------|
| DC Gain (dB)     | 67.8     | 67.8      | 67.8      |
| Phase Margin (°) | 132.76   | 142.82    | 120.04    |
| Slew Rate (V/µs) | 549.8    | 142.6     | 28.2      |
| GBW (MHz)        | 9.32     | 4.318     | 1.042     |
| Power (µW)       | 103.5    | 103.5     | 103.5     |

---

## 🧪 Observed Issues & Fixes (Miller OTA)

- **Incorrect biasing**: Fixed by ensuring M8 delivers ~250 µA.
- **Transistors in triode region**: Adjusted W/L to maintain saturation.
- **Improper capacitor connection**: Reconnected between gate and drain of M7.

---

## ✅ Conclusion

### With Miller Compensation:
- Achieves high gain and decent bandwidth
- Suitable for front-end analog interfaces
- Higher power consumption

### Without Miller Compensation:
- Excellent slew rate and phase margin
- Lower power and complexity
- Better suited for high-speed, power-sensitive applications like LCD drivers and analog buffers

---

## 🙏 Acknowledgments

Special thanks to **Dr. Remya Jayachandran** for valuable guidance and mentorship during this project.

---

## 📚 References

1. B. Razavi, *Design of Analog CMOS Integrated Circuits*, McGraw-Hill, 2001.  
2. P. E. Allen & D. R. Holberg, *CMOS Analog Circuit Design*, Oxford University Press, 2012.  
3. LTspice Simulator, Analog Devices.  
4. TSMC 0.18 µm CMOS Process Design Kit (PDK).  
5. Gangineni, M., et al. (2023), *Electronics Letters*, 59, e13005.

---

## 📂 File Structure

