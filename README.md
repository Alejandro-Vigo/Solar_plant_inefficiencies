# ☀️ Detection of Solar Plant Inefficiencies

## 📋 Project Overview
This project focuses on the **predictive maintenance** and **performance analysis** of two solar power plants. By analyzing generation and weather sensor data, the goal is to identify:
- **Inefficient Inverters**: Underperforming components that require maintenance.
- **Sensor Faults**: Data consistency issues indicating broken or miscalibrated sensors.
- **Production Loss**: Quantification of lost energy due to inefficiencies.

> **⚠️ Critical Finding**: The efficiency analysis revealed a likely **unit scaling error** in the raw data. Inverter efficiency (`AC Power / DC Power`) consistently averages **~10%**, whereas industry standard is **>95%**. This suggests DC Power and AC Power are recorded in different units (e.g., Watts vs Kilowatts).

## 📂 Repository Structure
```
├── 00_Project_design.ipynb       # Project scoped: Objective, Levers, KPIs
├── 01_Data_quality.ipynb         # Data cleaning: Nulls, duplicates, consistency checks
├── 02_Data_transformation.ipynb  # Feature engineering: Creating the efficiency KPI
├── 03_Analysis_insights.ipynb    # Statistical analysis & visualization
├── Solar_plant.pptx              # Original presentation (Spanish)
├── Solar_plant_translated.pptx   # Updated presentation (English)
├── README.md                     # Project documentation
└── requirements.txt              # Python dependencies
```

## 📊 Data Dictionary
The dataset consists of two main types of files for each plant (Plant 1 & Plant 2).

### Generation Data
| Column | Description |
|--------|-------------|
| `DATE_TIME` | Date and time of the reading (15-min intervals) |
| `PLANT_ID` | Unique identifier for the solar plant |
| `SOURCE_KEY` | Unique identifier for the Inverter |
| `DC_POWER` | Direct Current power generated (kW - *to be verified*) |
| `AC_POWER` | Alternating Current power generated (kW - *to be verified*) |
| `DAILY_YIELD` | Cumulative energy generated for the day |
| `TOTAL_YIELD` | Cumulative energy generated since installation |

### Weather Sensor Data
| Column | Description |
|--------|-------------|
| `DATE_TIME` | Date and time of the reading |
| `PLANT_ID` | Unique identifier for the solar plant |
| `SOURCE_KEY` | Unique identifier for the Sensor |
| `AMBIENT_TEMPERATURE` | Temperature of the air (°C) |
| `MODULE_TEMPERATURE` | Temperature of the solar panel (°C) |
| `IRRADIATION` | Solar irradiation falling on the panel |

## 🚀 How to Run
### Prerequisites
Ensure you have Python 3.8+ installed.

1. **Clone the repository**:
   ```bash
   git clone <repository-url>
   ```
2. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```
3. **Execute Notebooks**:
   Run the notebooks in sequential order (`00` -> `03`) to reproduce the analysis.

## 🔍 Key Insights
1. **Inverter Performance**:
   - Plant 1 has specific inverters (`1BY6WEcLGh8j5v7` and others) showing consistently lower DC generation compared to the plant average for the same irradiation.
2. **Thermal Efficiency**:
   - Module temperature follows irradiation closely. However, peak efficiency is observed before the maximum daily temperature is reached, confirming that excessive heat can marginally reduce panel efficiency.
3. **Data Gaps**:
   - Several days show zero irradiation readings during daylight hours while power generation is non-zero, indicating sensor dropouts.
