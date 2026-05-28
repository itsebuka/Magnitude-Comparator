# 🔲 4-Bit Magnitude Comparator & Display — PCB Design

> A hardware PCB module that compares two 4-bit binary numbers and visually indicates the result via three dedicated LED outputs. Built as part of the **EEE 312 (Digital Electronics) Capstone Project** at Pan Atlantic University.

---

## 📌 Overview

This module receives two 4-bit binary numbers (**A** and **B**) from an external register block, compares them using a **74LS85 TTL Magnitude Comparator IC**, and drives one of three LEDs to indicate the result:

| LED | Condition |
|-----|-----------|
| 🔴 LED 1 | A > B |
| 🟡 LED 2 | A = B |
| 🟢 LED 3 | A < B |

> ⚠️ By design, only **one LED is active at any given time** — the outputs are mutually exclusive.

This is a standalone comparator block intended to integrate into a larger multi-block digital logic system. Inputs A0–A3 and B0–B3 are brought in via an 8-pin header connector (J1), making it modular and system-compatible.

---

## 🧰 Bill of Materials (BOM)

| Ref | Component | Value / Part No. | Notes |
|-----|-----------|-----------------|-------|
| U1 | 4-bit TTL Magnitude Comparator | 74LS85 | DIP-16 package |
| D1, D2, D3 | LEDs | Standard 5mm | A>B, A=B, A<B indicators |
| R4, R5, R6 | Current-limiting resistors | 330Ω | One per LED |
| C1 | Decoupling capacitor | 100nF ceramic | Across VCC/GND, noise filtering |
| J1 | Input connector | 8-pin 2.54mm pitch header | A0–A3, B0–B3 inputs |
| — | Power supply | 5V TTL-compatible | — |

---

## 🔌 Pinout — J1 Input Connector

| Pin | Signal |
|-----|--------|
| 1 | A0 (LSB) |
| 2 | A1 |
| 3 | A2 |
| 4 | A3 (MSB) |
| 5 | B0 (LSB) |
| 6 | B1 |
| 7 | B2 |
| 8 | B3 (MSB) |

---

## 🛠 Tools Used

| Tool | Purpose |
|------|---------|
| **KiCAD 10.0** | Schematic capture & PCB layout |
| **GitHub Desktop** | Version control |

---

## 📁 Repository Structure

```
Magnitude-Comparator-main/
│
├── Comparator project.kicad_sch          # Main schematic file
├── Comparator project.kicad_pcb          # PCB layout file
├── Comparator project.kicad_pro          # KiCAD project file
│
├── Comparator project MAIN.kicad_sch     # Main (alternate) schematic
├── Comparator project PCB Schematic.kicad_pcb   # PCB schematic
├── Comparator project PCB Schematic.kicad_pro   # PCB project file
│
├── Comparator project-backups/           # Auto-saved KiCAD backups
│
├── report.txt                            # KiCAD symbol update log
└── README.md
```

---

## ⚙️ How to Open

1. Install [KiCAD 10.0](https://www.kicad.org/download/) or later.
2. Clone or download this repository.
3. Open `Comparator project.kicad_pro` in KiCAD.
4. The schematic and PCB layout will load automatically from within the project.

---

## 🔁 How It Works

The **74LS85** is a 4-bit magnitude comparator IC that takes two 4-bit inputs (A3–A0 and B3–B0) and three cascading inputs (A=B, A>B, A<B — tied to their respective logic levels for standalone use), and produces three active-high outputs:

- **OA>B** → HIGH when A is numerically greater than B
- **OA=B** → HIGH when A equals B  
- **OA<B** → HIGH when A is numerically less than B

Each output drives one LED through a 330Ω current-limiting resistor. The 100nF decoupling capacitor on the power rail suppresses switching noise from the TTL logic.

---

## 📝 Design Notes

- Power supply must be **5V TTL-compatible**. The 74LS85 operates between 4.75V and 5.25V.
- The cascading inputs (pins 2, 3, 4) are wired for **standalone operation**. For cascading multiple comparators to handle wider bit-widths, these need to be connected to the outputs of the lower-order comparator stage.
- This PCB is a **first revision** — trace routing and component placement may not be fully optimized. Improvements are planned in future iterations.

---

## 🔭 Future Improvements

- [ ] Add silkscreen labels for LED indicators (A>B, A=B, A<B) directly on the PCB
- [ ] Cascade to 8-bit comparison using two 74LS85 stages
- [ ] Add onboard power regulation (e.g. 7805) to accept a wider input voltage range
- [ ] Export Gerber files for PCB fabrication
- [ ] Add a ground plane pour for improved noise immunity

---

## 👤 Author

**Eleogu Chukwuebuka Joseph (Ebuka)**  
Electrical/Electronics Engineering Student  
Pan Atlantic University  
GitHub: [@itsebuka](https://github.com/itsebuka)  
Email: eleogujoseph007@gmail.com

---

> *"This marks my first real personal milestone project that I have ever done from scratch by myself. It's not perfect, but it is undoubtedly a step in the right direction."*
