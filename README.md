# PCC-MCC-Panel-Tool-By-Haripal
Python GUI tool for PCC/MCC panel design that automates load calculation, incomer sizing, busbar selection, feeder MCCB and intelligent cable sizing with parallel run logic.

# ⚡ PCC / MCC Panel Calculation Software

### 🏭 Electrical Panel Design Automation Tool  
**Developed by: Haripal Singh**

This project is an industry-oriented GUI application developed using Python to automate electrical calculations required for PCC and MCC panel design.

It replicates the real workflow used in EPC companies and switchgear manufacturing for load list preparation, feeder sizing, incomer selection, and cable & busbar sizing.

---

## 🚀 Key Features

### 🔹 Load Calculation
- Total Connected Load
- Maximum Demand using Demand Factor

### 🔹 Incomer Sizing
- Incomer current calculation
- Automatic MCCB selection (next higher standard rating)

### 🔹 Busbar Sizing
- Busbar current with 125% future expansion
- Automatic copper busbar size selection

### 🔹 Power Factor Correction
- Capacitor kVAR calculation for PF improvement

### 🔹 Feeder-Wise Schedule Generation
For each motor feeder:
- Full Load Current calculation
- MCCB selection
- Cable size selection

### 🔹 Intelligent Cable Selection
- Copper / Aluminium option
- 125% motor duty consideration
- Automatic parallel run logic
- Output in practical format:
