# Urban Accessibility Spatial Analyser 🗺️⏱️

An automated data pipeline and spatial visualization tool designed to extract, transform, and map urban mobility metrics (travel times and distances) across localized city grids. 

This prototype maps transit accessibility around **Sector 75, Noida**, utilizing the **MapmyIndia (Mappls) Advanced Routing API** to account for the highly specific nuances of Indian road networks, narrow corridors, and local traffic patterns.

## 🚀 Project Architecture

This project is broken down into three core data engineering phases:

1. **Spatial Data Generation (`generate_nodes.py`):** Mathematically constructs a customized bounding box and coordinate grid around a defined epicenter, generating a structured dataset of destination nodes.
2. **Fault-Tolerant API Extraction (`extract_travel_times.py`):** Handles automated, rate-limited bulk requests to the Mappls Route ADV API to fetch driving durations and distances. Built with enterprise-grade failsafes, including iterative line-by-line saving to protect against data loss during crashes or quota limits.
3. **Spatial Visualization (`map_accessibility.py`):** Transforms the flattened CSV data into an interactive, weighted HTML heatmap. Utilizes `Folium` and `CartoDB` light-mode tiles to overlay transit delay hotspots while keeping the underlying geographic context readable.

## 🛠️ Tech Stack
* **Language:** Python 3.x
* **Data Engineering & ETL:** `pandas`, `numpy`, `requests`
* **Geospatial Visualization:** `folium`, `folium.plugins` (HeatMap)
* **Routing Engine:** MapmyIndia (Mappls) REST API

## ⚙️ How to Run Locally

### 1. Setup & Installation
Clone the repository to your local machine:
```bash
git clone [https://github.com/aryansrivvv/Urban-Accessibility-Spatial-Analyser.git](https://github.com/aryansrivvv/Urban-Accessibility-Spatial-Analyser.git)
cd Urban-Accessibility-Spatial-Analyser

Install the required Python dependencies:

Bash
pip install pandas numpy requests folium
2. Configure API Credentials
To run the extraction, you will need a free REST API Key from the Mappls Developer Portal.

Open extract_travel_times.py.

Replace the placeholder "YOUR_MAPPLS_REST_API_KEY_HERE" with your actual key.

3. Execute the Pipeline
Run the scripts sequentially to build the map from scratch:

Step A: Generate the Grid

Bash
python generate_nodes.py
(Creates noida_nodes.csv with the spatial coordinates).

Step B: Extract Routing Data

Bash
python extract_travel_times.py
(Pings the API with rate-limiting and saves outputs to travel_times_results.csv).

Step C: Generate the Map

Bash
python map_accessibility.py
(Generates the interactive noida_mappls_heatmap_light.html dashboard).

🎯 Context & Use Case
This project was developed as a technical prototype to demonstrate automated pipeline construction, API management, and composite indexing logic for urban transit analytics. It serves as a foundational framework that can be scaled to analyze larger multi-modal transit corridors across different Indian cities.

