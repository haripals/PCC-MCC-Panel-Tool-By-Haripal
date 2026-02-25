# ⚡ PCC / MCC Panel Calculation Software

![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python)
![GUI](https://img.shields.io/badge/GUI-Tkinter-green)
![Domain](https://img.shields.io/badge/Domain-Electrical%20Panel%20Design-orange)
![License](https://img.shields.io/badge/License-MIT-yellow)
![Status](https://img.shields.io/badge/Status-Active-success)
![Made By](https://img.shields.io/badge/Developed%20by-Haripal%20Singh-red)

---

## 🏭 Electrical Panel Design Automation Tool

This is an industry-oriented Python GUI application developed to automate calculations used in **PCC / MCC panel design**.

It replicates real EPC workflow for:

- Load list preparation
- Incomer sizing
- Feeder sizing
- Busbar selection
- Cable selection
- APFC capacitor calculation

---

## 🖥 GUI Preview

<img src="pcc_mcc panel tool by_haripal_singh.png" width="800">

---

## 🚀 Key Features

### 🔹 Load Calculation
✔ Total Connected Load  
✔ Maximum Demand using Demand Factor  

### 🔹 Incomer Sizing
✔ Incomer current calculation  
✔ Automatic MCCB selection  

### 🔹 Busbar Sizing
✔ 125% future load consideration  
✔ Copper busbar auto-selection  

### 🔹 Power Factor Correction
✔ Capacitor kVAR calculation  

### 🔹 Feeder-Wise Schedule
✔ Motor FLC calculation  
✔ MCCB selection  
✔ Intelligent cable sizing  

### 🔹 Cable Selection Logic
✔ Copper / Aluminium option  
✔ 125% motor duty  
✔ Automatic parallel runs  

---

## 🧠 Engineering Logic Implemented

- 3Ø FLC = P / (√3 × V × PF × η)
- Demand load calculation
- Standard MCCB selection
- Busbar sizing (125% rule)
- Reactive power compensation
- Motor cable sizing (1.25 × FLC)

---

## ⚙️ Technologies Used

- Python
- Tkinter
- IEC based LT panel design practices

---

## ▶️ How to Run

```bash
git clone https://github.com/your-username/pcc-mcc-panel-calculation-tool.git
cd pcc-mcc-panel-calculation-tool
python main.py
