# 📊 Student Performance Analytics Dashboard — Power BI


## 📌 Project Overview

The **Student Performance Analytics Dashboard** is an end-to-end Power BI project that transforms raw academic data into actionable insights. It enables educators and administrators to monitor student scores, attendance trends, behavioral patterns, and subject-wise performance — all through a single interactive report with drill-through, tooltips, and a mobile-optimized layout.

---

## 🗂️ Dataset

Four CSV files power this dashboard:

| File | Fields |
|------|--------|
| `Students.csv` | StudentID, Name, Gender, Class, Section |
| `Scores.csv` | StudentID, Subject, ExamType, Score, MaxScore, Term |
| `Attendance.csv` | StudentID, Date, Status (Present/Absent), Reason |
| `Behavior.csv` | StudentID, Date, BehaviorType, Notes |

---

## 🧩 Data Model

<p align="center">
  <img src="Screenshots/Modelview.png" alt="Data Model" width="80%"/>
</p>

The model uses a **star schema** with `Students` as the central dimension table, connected via one-to-many relationships to three fact tables — `Scores`, `Attendance`, and `Behavior`.

---

## ⚙️ Data Modeling 

### Relationships
- `Students[StudentID]` → `Scores[StudentID]` (1:*)
- `Students[StudentID]` → `Attendance[StudentID]` (1:*)
- `Students[StudentID]` → `Behavior[StudentID]` (1:*)

---

## 📈 Dashboard Pages

### 1. Main Dashboard

<p align="center">
  <img src="Screenshots/Dashboard.png" alt="Main Dashboard" width="100%"/>
</p>

**Visuals included:**
- 📦 **KPI Cards** — Total Students, Average Score, Attendance %, % Score
- 📊 **Bar Chart** — Average Score by Subject and Class
- 📉 **Line Chart** — Performance Trend by Term (Final Exam / Mid Term / Unit Test)
- 📋 **Table** — Student-wise Score Summary with conditional formatting (🟢 green for ≥80%, 🔴 red for <40%)
- 🍩 **Donut Chart** — Behavior Types Distribution
- 🎛️ **Slicers** — Class, Term, Subject, Section

---

### 2. Drillthrough — Student Profile

<p align="center">
  <img src="Screenshots/Drillthrough.png" alt="Drillthrough Page" width="100%"/>
</p>

Right-click any student in the summary table to drill through to their individual profile, which shows:
- Student Name, Attendance %, Section, % Score
- Subject-wise % Score bar chart
- Behavior Details table (BehaviorType, Notes)

---

### 3. Tooltip

<p align="center">
  <img src="Screenshots/Tooltip.png" alt="Tooltip" width="60%"/>
</p>

Hovering over visuals reveals a **custom tooltip page** displaying % Score, Attendance %, and Behavior Count for the hovered context.

---

## 📱 Mobile Layout

The report is fully optimized for the **Power BI mobile app** across all pages.

<p align="center">
  <img src="Screenshots/mobileview1.png" alt="Mobile View 1" width="18%"/>
  <img src="Screenshots/mobileview2.png" alt="Mobile View 2" width="18%"/>
  <img src="Screenshots/mobileview3.png" alt="Mobile View 3" width="18%"/>
  <img src="Screenshots/mobileview4.png" alt="Mobile View 4" width="18%"/>
  <img src="Screenshots/mobileview5.png" alt="Mobile View 5" width="18%"/>
</p>

---

## ✨ Interactivity Features

| Feature | Description |
|--------|-------------|
| **Slicers** | Filter by Class, Section, Subject, Term |
| **Drillthrough** | Navigate to individual student profiles from the summary table |
| **Tooltips** | Mini metric cards appear on hover |
| **Conditional Formatting** | Color-coded score table (green / red) |
| **Mobile Layout** | Responsive design for Power BI mobile app |

---

## 🛠️ Tools & Technologies

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)
![Power Query](https://img.shields.io/badge/Power%20Query-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white)

- **Power BI Desktop** — report authoring
- **Power Query (M)** — data cleaning, null handling, type corrections
- **DAX** — calculated columns and measures
- **Star Schema** — optimized data model

---

## 🚀 Getting Started

1. **Clone the repository**
   ```bash
   git clone https://github.com/HarshalVora86/Student_Performance_Analytics_Dashboard_Power_BI.git
   ```

2. **Open the report**
   - Launch **Power BI Desktop**
   - Open `Student_Performance_Analytics_Dashboard.pbix`

3. **Explore**
   - Use slicers to filter by Class, Term, Subject, or Section
   - Right-click any student row to **drill through** to their profile
   - Hover over charts to see **custom tooltips**

> **Note:** The dataset is embedded within the `.pbix` file — no external data source connection is required.

---

## 👤 Author

**Harshal Vora**

[![GitHub](https://img.shields.io/badge/GitHub-HarshalVora86-181717?style=flat&logo=github)](https://github.com/HarshalVora86)

---

