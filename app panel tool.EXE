# =========================================================
#  PCC / MCC PANEL CALCULATION SOFTWARE
#  Developed by: Haripal Singh
#  Unauthorized use without credit is prohibited
# =========================================================

import tkinter as tk
from tkinter import ttk, messagebox
import math

DEVELOPER = "Developed by Haripal Singh"

# ---------------- FUNCTIONS ---------------- #

def flc(power_kw, voltage=415, pf=0.85, eff=0.9):
    return (power_kw * 1000) / (math.sqrt(3) * voltage * pf * eff)

def select_mccb(current):
    ratings = [63, 100, 160, 250, 400, 630, 800, 1000, 1250, 1600, 2000, 2500, 3200]
    for r in ratings:
        if current <= r:
            return r
    return "Above 3200A"

# ---------------- BUSBAR SELECTION ---------------- #

def select_busbar(current):
    busbar_table = {
        "25x3": 200,
        "25x5": 300,
        "32x5": 400,
        "40x5": 500,
        "50x5": 630,
        "50x10": 1000,
        "75x10": 1600
    }

    for size, amp in busbar_table.items():
        if current <= amp:
            return size

    return "Use multiple busbars"


# ---------------- CABLE SELECTION ---------------- #

def select_cable(current, material):

    current = current * 1.25   # motor duty

    if material == "Copper":
        cable_table = {
            4: 28, 6: 36, 10: 50, 16: 68, 25: 89, 35: 110,
            50: 140, 70: 175, 95: 215, 120: 250,
            150: 285, 185: 320, 240: 380, 300: 430
        }
    else:
        cable_table = {
            10: 35, 16: 45, 25: 60, 35: 75, 50: 95,
            70: 120, 95: 145, 120: 170, 150: 195,
            185: 225, 240: 260, 300: 300, 400: 350
        }

    for size, amp in cable_table.items():
        if current <= amp:
            return f"1 Run × {size} sqmm {material}"

    max_size = max(cable_table, key=cable_table.get)
    max_amp = cable_table[max_size]

    runs = math.ceil(current / max_amp)

    return f"{runs} Runs × {max_size} sqmm {material}"

    

def capacitor_kvar(p_kw, pf1, pf2):
    return p_kw * (
        math.sqrt((1 / pf1**2) - 1) -
        math.sqrt((1 / pf2**2) - 1)
    )

# ---------------- CALCULATE ---------------- #

def calculate():
    try:
        loads = [float(e.get()) for e in motor_entries if e.get() != ""]

        connected_load = sum(loads)
        demand = connected_load * float(demand_factor.get())

        incomer_current = flc(demand, float(voltage.get()))
        bus_current = incomer_current * 1.25

        cap = capacitor_kvar(demand, float(pf1.get()), float(pf2.get()))

        busbar_size = select_busbar(bus_current)

        result_text.set(
           f"Connected Load = {connected_load:.2f} kW\n"
           f"Max Demand = {demand:.2f} kW\n"
           f"Incomer Current = {incomer_current:.2f} A\n"
           f"Select Incomer MCCB = {select_mccb(incomer_current)} A\n"
           f"Busbar Current = {bus_current:.2f} A\n"
           f"Recommended Busbar = {busbar_size} Cu\n"
           f"Capacitor Bank = {cap:.2f} kVAR"
      )

        feeder_box.delete(*feeder_box.get_children())

        for i, kw in enumerate(loads):
            current = flc(kw, float(voltage.get()))

            cable = select_cable(current, cable_material.get())
            feeder_box.insert("", "end", values=(
                f"Feeder {i+1}",
                f"{kw}",
                f"{current:.2f}",
                select_mccb(current)
                , cable
            ))

    except:
        result_text.set("Enter valid data")


# ---------------- ABOUT POPUP ---------------- #

def show_about():
    messagebox.showinfo("About", 
    "PCC / MCC Panel Calculation Software\n\n"
    "Developer: Haripal Singh\n"
    "For Panel Design Engineering Use")

# ---------------- GUI ---------------- #

root = tk.Tk()
root.title("PCC / MCC PANEL TOOL  |  Developer: Haripal Singh")
root.geometry("900x800")

# INPUT FRAME
input_frame = tk.Frame(root)
input_frame.pack(pady=10)

tk.Label(input_frame, text="Voltage").grid(row=0, column=0)
voltage = tk.Entry(input_frame)
voltage.insert(0, "415")
voltage.grid(row=0, column=1)

tk.Label(input_frame, text="Demand Factor").grid(row=1, column=0)
demand_factor = tk.Entry(input_frame)
demand_factor.insert(0, "0.8")
demand_factor.grid(row=1, column=1)

tk.Label(input_frame, text="Existing PF").grid(row=2, column=0)
pf1 = tk.Entry(input_frame)
pf1.insert(0, "0.8")
pf1.grid(row=2, column=1)

tk.Label(input_frame, text="Target PF").grid(row=3, column=0)
pf2 = tk.Entry(input_frame)
pf2.insert(0, "0.95")
pf2.grid(row=3, column=1)

tk.Label(input_frame, text="Cable Material").grid(row=4, column=0)

cable_material = ttk.Combobox(input_frame, values=["Copper", "Aluminium"], width=17)
cable_material.current(0)
cable_material.grid(row=4, column=1)

# MOTOR LOAD INPUT
motor_frame = tk.Frame(root)
motor_frame.pack()

tk.Label(motor_frame, text="Motor Loads (kW)").pack()

motor_entries = []
for i in range(10):
    e = tk.Entry(motor_frame, width=10)
    e.pack(pady=2)
    motor_entries.append(e)

# BUTTON
tk.Button(root, text="CALCULATE", command=calculate, bg="green", fg="white").pack(pady=10)

# RESULT
result_text = tk.StringVar()
tk.Label(root, textvariable=result_text, font=("Arial", 12), justify="left").pack()

# FEEDER TABLE
columns = ("Feeder", "kW", "Current (A)", "MCCB (A)","Cable")
feeder_box = ttk.Treeview(root, columns=columns, show="headings")


for col in columns:
    feeder_box.heading(col, text=col)

feeder_box.pack(fill="both", expand=True, pady=10)

# FOOTER CREDIT
tk.Label(root, text=DEVELOPER, fg="blue", font=("Arial", 10, "bold")).pack(side="bottom", pady=5)

# MENU
menu = tk.Menu(root)
root.config(menu=menu)
menu.add_command(label="About Developer", command=show_about)

root.mainloop()
