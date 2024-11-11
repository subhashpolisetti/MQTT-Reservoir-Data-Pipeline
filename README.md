
# California Reservoir Water Monitoring System

This project collects and monitors Water Mark Levels (WML) for California’s state reservoirs. It uses an MQTT-based data aggregation system to gather daily water level readings, generate comprehensive reports, and provide insights to aid the California Department of Water Resources in assessing water availability across the state.

---

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Data Collection and Aggregation](#data-collection-and-aggregation)
- [Repository Structure](#repository-structure)
- [Installation](#installation)
- [Usage](#usage)
- [Data Model](#data-model)
- [Example Reports](#example-reports)
- [Contributing](#contributing)
- [License](#license)

---

## Overview

This system provides a reliable way to monitor water levels in key California reservoirs, including Shasta, Oroville, and Sonoma, by using an MQTT messaging protocol to collect, store, and summarize daily Water Mark Level (WML) data. The project transforms this data from CSV files to JSON format and simulates MQTT subscribers and publishers to create daily summary reports.

## Features

- **Real-Time Water Monitoring**: Collects water levels for California’s major reservoirs.
- **Data Transformation**: Converts CSV files into JSON format for MQTT-compatible publishing.
- **Aggregation and Reporting**: Aggregates daily WML data and generates comprehensive summary reports.
- **Easy to Extend**: Add additional reservoirs or sensors as required by expanding the dataset.

## Data Collection and Aggregation

- **MQTT Protocol**: Utilizes the MQTT messaging protocol, where each reservoir has a specific topic (`{Reservoir_ID}/WML`), allowing the project to act as a scalable data stream.
- **Data Storage**: All data is stored in CSV format initially, then converted to JSON for streamlined data processing.
- **Daily Summaries**: Each day’s data is aggregated to provide total water availability for the selected reservoirs.

---

## Repository Structure

```
.
├── data/                       # Raw CSV data files for each reservoir
├── README.md                   # Project documentation
```

## Installation

1. **Clone the repository**:
   ```bash
   git clone https://github.com/subhashpolisetti/California-Reservoir-WML-Data.git
   cd California-Reservoir-WML-Data
   ```

2. **Install dependencies** (ensure Python 3.6+ is installed):
   ```bash
   pip install pandas
   ```

3. **Upload CSV data**:
   - Upload your `Oroville_WML.csv`, `Shasta_WML.csv`, and `Sonoma_WML.csv` files into the `data` directory or directly to your Colab notebook.

## Usage

1. **Run Data Processing**:
   - Open `notebooks/Reservoir_WML_Data_Aggregation.ipynb` in Google Colab.
   - Upload your CSV files as prompted in the notebook and follow the steps to transform and aggregate data.

2. **Generate Daily Reports**:
   - The notebook provides code cells to convert CSV files into MQTT JSON messages.
   - The aggregation function will produce daily summaries, stored in CSV and JSON formats in the Colab notebook.

3. **Example Output**:
   - Daily report files include aggregated water levels from all reservoirs for each recorded date.

## Data Model

The data follows a `{Reservoir_ID}/WML` schema:
- Each reservoir sends daily WML data as JSON messages to a specific MQTT topic.
- Data format:
  ```json
  {
    "Date": "2024-10-01",
    "TAF": 2000
  }
  ```
- **TAF**: Water levels are measured in Thousands of Acre-Feet (TAF).

---

## Example Reports

Below is an example of the daily water mark level summary report format:

| Date       | Oroville (TAF) | Shasta (TAF) | Sonoma (TAF) | Total_TAF |
|------------|----------------|--------------|--------------|-----------|
| 2024-10-01 | 2001           | 2727         | 193          | 4921      |
| 2024-10-02 | 2000           | 2721         | 192          | 4913      |
| ...        | ...            | ...          | ...          | ...       |

