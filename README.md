# 📊 Student Performance  — Power BI



## 📌 Project Overview

The **Student Performance Analytics Dashboard** is an end-to-end Power BI project that transforms raw academic data into actionable insights. It enables educators and administrators to monitor student scores, attendance trends, behavioral patterns, and subject-wise performance — all through a single interactive report with drill-through, custom tooltips, bookmark navigation, and a fully mobile-optimized layout.

This project was built as part of the **Power BI — Data Analysis & Data Science** practical exam at Red & White Skill Education, covering data modeling, DAX calculations, interactive visualizations, and storytelling.

---

## 🗂️ Dataset

Four CSV files power this dashboard:

| File | Fields | Description |
|------|--------|-------------|
| `Students.csv` | StudentID, Name, Gender, Class, Section | 120 students across Classes 9–12 and Sections A–D |
| `Scores.csv` | StudentID, Subject, ExamType, Score, MaxScore, Term | 6,480 rows — all subjects × exam types × 3 terms |
| `Attendance.csv` | StudentID, Date, Status (Present/Absent), Reason | 21,600 rows with daily attendance records |
| `Behavior.csv` | StudentID, Date, BehaviorType, Notes | 885 behavior records — Positive, Negative, Neutral |

> **Note:** The dataset is embedded within the `.pbix` file — no external data source connection is required after opening.

---

## 🧩 Data Model

The model uses a **star schema** with `Students` as the central dimension table, connected via one-to-many relationships to three fact tables — `Scores`, `Attendance`, and `Behavior`.

```
Students[StudentID]  ──1:M──►  Scores[StudentID]
Students[StudentID]  ──1:M──►  Attendance[StudentID]
Students[StudentID]  ──1:M──►  Behavior[StudentID]
```

- **Filter direction:** Single (Students → child tables)
- **Cross-filter:** Single direction only
- **Date Table:** CALENDAR() table created and marked as Date Table for time-intelligence support

---

## ⚙️ Data Modeling & Cleaning

### Power Query Steps
- Loaded all 4 CSVs via **Get Data → Text/CSV**
- Renamed columns (removed spaces and special characters)
- Corrected data types — Date columns → `Date`; Score/MaxScore → `Decimal Number`; Status, Gender, Class → `Text`
- Replaced nulls in the `Reason` column with `"N/A"`

### Calculated Column — Performance Category (on Scores table)

```dax
Performance Category =
VAR Pct = DIVIDE(Scores[Score], Scores[MaxScore], 0)
RETURN
SWITCH(
    TRUE(),
    Pct >= 0.80, "High",
    Pct >= 0.40, "Medium",
    "Low"
)
```

### Behavior Category Column (on Behavior table)

```dax
Behavior Category =
IF(
    SEARCH("Positive", Behavior[BehaviorType], 1, 0) > 0, "Positive",
    IF(SEARCH("Negative", Behavior[BehaviorType], 1, 0) > 0, "Negative", "Neutral")
)
```

---

## 📐 DAX Measures

| Measure | Formula | Used In |
|---------|---------|---------|
| `% Score` | `AVERAGEX(Scores, DIVIDE(Scores[Score], Scores[MaxScore], 0))` | KPI Card, Line Chart |
| `Attendance %` | `DIVIDE(Present days, Total days)` | KPI Card, Drillthrough |
| `Total Students` | `DISTINCTCOUNT(Students[StudentID])` | KPI Card |
| `Avg Score by Subject` | `AVERAGEX(Scores, Scores[Score])` | Bar Chart |
| `Behavior Count` | `COUNTROWS(Behavior)` | Donut Chart |
| `Positive Behaviors` | `CALCULATE(COUNTROWS(Behavior), SEARCH("Positive",…))` | KPI / Drillthrough |
| `Negative Behaviors` | `CALCULATE(COUNTROWS(Behavior), SEARCH("Negative",…))` | KPI / Drillthrough |
| `Score Color` | `SWITCH(TRUE(), Pct>=0.80, "#27AE60", Pct<0.40, "#E74C3C", "#F39C12")` | Conditional Formatting |

### Full Attendance % DAX

```dax
Attendance % =
VAR TotalDays   = COUNTROWS(Attendance)
VAR PresentDays = CALCULATE(COUNTROWS(Attendance), Attendance[Status] = "Present")
RETURN DIVIDE(PresentDays, TotalDays, 0)
```

---

## 📈 Dashboard Pages

### 1. Main Dashboard

**Visuals included:**
- 📦 **KPI Cards** — Total Students, Average Score, Attendance %, % Score
- 📊 **Bar Chart** — Average Score by Subject and Class
- 📉 **Line Chart** — Performance Trend by Term (Final Exam / Mid Term / Unit Test)
- 📋 **Table** — Student-wise Score Summary with conditional formatting  
  - 🟢 Green for ≥ 80%  
  - 🟠 Orange for 40–79%  
  - 🔴 Red for < 40%
- 🍩 **Donut Chart** — Behavior Types Distribution (Positive / Negative / Neutral)
- 🎛️ **Slicers** — Class, Term, Subject, Section

---

### 2. Drillthrough — Student Profile

Right-click any student in the summary table → **Drillthrough → Student Profile**

The individual profile page shows:
- Student Name, Attendance %, Section, % Score (KPI Cards)
- Subject-wise % Score bar chart
- Behavior Details table (BehaviorType, Notes)
- Back button to return to the main dashboard

---

### 3. Tooltip Page

Hovering over visuals reveals a **custom tooltip page** displaying:
- % Score
- Attendance %
- Behavior Count

for the hovered student or context.

---

### 4. Bookmark Navigation

Two bookmark buttons switch between views without changing pages:

| Bookmark | Shows | Hides |
|----------|-------|-------|
| 📚 Academic View | Score charts, KPIs, Bar Chart, Line Chart | Behavior visuals |
| 🎭 Behavioral View | Donut Chart, Behavior table | Score visuals |

---

## 📱 Mobile Layout

The report is fully optimized for the **Power BI Mobile App** across all pages.

- All 3 report pages have dedicated mobile layouts
- Visuals are stacked vertically in single-column format
- KPI cards appear at the top for quick at-a-glance metrics
- Charts and tables follow in priority order for mobile readability

---

## ✨ Interactivity Features

| Feature | Description |
|---------|-------------|
| **Slicers** | Filter entire report by Class, Section, Subject, Term |
| **Drillthrough** | Navigate to individual student profiles from the summary table |
| **Custom Tooltips** | Mini metric cards appear on hover over any visual |
| **Conditional Formatting** | Color-coded score table (green ≥80% / orange 40–79% / red <40%) |
| **Bookmark Navigation** | One-click toggle between Academic and Behavioral views |
| **Mobile Layout** | Responsive design optimized for the Power BI Mobile app |

---

## 📊 Evaluation Criteria

| Component | Marks |
|-----------|-------|
| Data Modeling & Cleaning | 10 |
| DAX Calculations | 10 |
| Visualizations & Storytelling | 15 |
| Slicers, Filters & Drillthrough | 10 |
| Optional Features (Mobile Layout) | 5 |
| **Total** | **50** |

---

## 🛠️ Tools & Technologies

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)
![Power Query](https://img.shields.io/badge/Power%20Query-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white)

- **Power BI Desktop** — report authoring and publishing
- **Power Query (M)** — data cleaning, null handling, type corrections
- **DAX** — calculated columns, measures, conditional formatting
- **Star Schema** — optimized relational data model

---

## 🚀 Getting Started

1. **Clone the repository**
   ```bash
   git clone https://github.com/HarshalVora86/Student_Performance_Analytics_Dashboard_Power_BI.git
   ```

2. **Open the report**
   - Launch **Power BI Desktop**
   - Open `Student_Performance_Analytics_Dashboard.pbix`

3. **Explore the dashboard**
   - Use slicers to filter by Class, Term, Subject, or Section
   - Right-click any student row to **drill through** to their individual profile
   - Hover over charts to see **custom tooltips**
   - Click the Academic / Behavioral **bookmark buttons** to switch views
   - Open in the **Power BI Mobile app** for the mobile-optimized layout

> **Note:** The dataset is fully embedded within the `.pbix` file — no external data source or database connection is required.

---

## 📁 Repository Structure

```
Student_Performance_Analytics_Dashboard_Power_BI/
│
├── Student_Performance_Analytics_Dashboard.pbix   ← Main Power BI report file
│
├── Data/
│   ├── Students.csv         ← 120 students (StudentID, Name, Gender, Class, Section)
│   ├── Scores.csv           ← 6,480 exam score records
│   ├── Attendance.csv       ← 21,600 daily attendance records
│   └── Behavior.csv         ← 885 behavior incident records
│
├── Screenshots/
│   ├── Modelview.png        ← Data model (star schema) screenshot
│   ├── mobileview1.png      ← Mobile layout screenshots
│   ├── mobileview2.png
│   ├── mobileview3.png
│   ├── mobileview4.png
│   └── mobileview5.png
│
└── README.md                ← This file
```

---

## 👤 Author

**Dhruv Prajapati**

