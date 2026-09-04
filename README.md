# Soft Computing (EL1) - Assignment 1: Case Study & Presentation
**Course Code:** STDA2102 | **Credits:** 4 (3-0-2) | **Term:** Fall/Spring 2026  
**Student Name:** Manish Kumar  
**Topic:** **Design of an Intelligent Air Conditioning System Using Fuzzy Logic**

---

## 📌 Executive Summary

This repository contains the complete academic deliverables for **Assignment 1 (50 Marks)** of the Soft Computing course. The project designs, models, and evaluates an intelligent **Mamdani Fuzzy Logic Controller (FLC)** for residential and commercial split-unit air conditioning systems.

Compared against conventional on-off thermostats (Bang-Bang) and classical PID controllers in a realistic **24-hour dynamic thermodynamic simulation**, the proposed Fuzzy controller demonstrates:
- **24.23% electrical energy reduction** over 24 hours (18.03 kWh vs 23.79 kWh).
- **Superior thermal stability** constrained to $\pm 0.693^\circ\text{C}$ of setpoint ($24^\circ\text{C}$ target).
- **Elimination of mechanical cycling stress** and in-rush startup current spikes.

---

## 📂 Key Deliverables

| Deliverable | File | Description |
|---|---|---|
| **Academic Report (Word)** | [`Case_Study_Report_Intelligent_AC.docx`](Case_Study_Report_Intelligent_AC.docx) | Full publication-grade technical report with embedded diagrams, equations, and tables. |
| **Academic Report (Markdown)** | [`Case_Study_Report_Intelligent_AC.md`](Case_Study_Report_Intelligent_AC.md) | Complete Markdown source specification. |
| **Presentation Deck** | [`Presentation_Intelligent_AC.pptx`](Presentation_Intelligent_AC.pptx) | 15-slide technical presentation deck with modern visuals and presenter notes. |
| **Simulation Notebook** | [`Assignment_1_Case_Study_Simulation.ipynb`](Assignment_1_Case_Study_Simulation.ipynb) | Pre-rendered interactive Jupyter notebook with inline plots and tabular results. |
| **Dynamic Simulation Code** | [`ac_fuzzy_simulation.py`](ac_fuzzy_simulation.py) | Python simulation engine implementing the 24-hr thermodynamic room model. |
| **Report Generator** | [`generate_docx_report.py`](generate_docx_report.py) | Script to compile and generate the Word document. |
| **Deck Generator** | [`generate_presentation.py`](generate_presentation.py) | Script to compile and generate the PowerPoint presentation. |
| **High-Res Figures** | [`figures/`](figures/) | Membership functions, 3D rule surfaces, 24-hr simulation time-series, and bar charts. |
| **Syllabus Specification** | [`Soft_Computing_Course_Document.docx`](Soft_Computing_Course_Document.docx) | Official course document and evaluation rubrics. |

---

## 🧠 System Architecture & Mathematical Foundations

### 1. Linguistic Variables & Membership Functions
The controller continuously samples three environmental inputs:
1. **Temperature Error ($e_T$):** Range $[-6.0, +6.0]^\circ\text{C}$ with triangular/trapezoidal sets: `{Negative, Zero, Positive}`.
2. **Rate of Temperature Change ($\Delta e_T$):** Range $[-2.0, +2.0]^\circ\text{C/min}$ with sets: `{Decreasing, Stable, Increasing}`.
3. **Relative Humidity ($RH$):** Range $[20\%, 90\%]$ with sets: `{Comfortable, High, VeryHigh}`.

The controlled output is:
- **Compressor Speed ($V_c$):** Continuous frequency modulation from $[0\%, 100\%]$ across 5 fuzzy partitions: `{Off, Low, Medium, High, Maximum}`.

### 2. Mamdani Rule Base (27 Rules)
The knowledge base integrates expert domain heuristics across temperature dynamics and latent humidity loads using minimum T-norm composition:
$$\mu_{R_k}(x, y, z) = \min\left( \mu_{A_k}(x), \mu_{B_k}(y), \mu_{C_k}(z) \right)$$

### 3. Defuzzification
The crisp compressor modulation percentage is synthesized via Centroid (Center of Gravity) defuzzification:
$$z^* = \frac{\int z \cdot \mu_C(z) \, dz}{\int \mu_C(z) \, dz}$$

---

## 📊 24-Hour Thermodynamic Benchmark Results

| Performance Metric | Conventional Bang-Bang | Classical PID Controller | Proposed Fuzzy FLC | Improvement (FLC vs Bang-Bang) |
|---|:---:|:---:|:---:|:---:|
| **Total Energy (24 Hours)** | 23.79 kWh | 19.88 kWh | **18.03 kWh** | **-24.23%** ⚡ |
| **Mean Absolute Error (MAE)** | 1.109 °C | 0.412 °C | **0.693 °C** | **-37.5%** |
| **Max Temperature Overshoot** | +2.20 °C | +1.05 °C | **+0.82 °C** | **-62.7%** |
| **Compressor Cycling Events** | 38 on/off cycles | Continuous (oscillatory) | **Continuous (smooth)** | **Zero mechanical shock** |

---

## 🚀 Quickstart & Reproduction Guide

### 1. Environment Setup
```bash
# Create and activate a Python 3.11 virtual environment
python3 -m venv .venv
source .venv/bin/activate

# Install required dependencies
pip install -r requirements.txt
```

### 2. Run the 24-Hour Thermal Simulation
```bash
python ac_fuzzy_simulation.py
```
This runs the full thermodynamic differential model and saves high-resolution figures into the `figures/` directory.

### 3. Regenerate Report & Presentation Deck
```bash
# Generate the Word report (.docx)
python generate_docx_report.py

# Generate the PowerPoint presentation (.pptx)
python generate_presentation.py
```

### 4. Interactive Jupyter Notebook
```bash
jupyter notebook Assignment_1_Case_Study_Simulation.ipynb
```
