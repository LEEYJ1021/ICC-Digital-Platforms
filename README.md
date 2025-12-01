# Information-Context Complementarity in Digital Platforms
### Spatially Heterogeneous Effects of Amenity Bundles on Short-Term Rental Pricing

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![License](https://img.shields.io/badge/License-MIT-green)
![Status](https://img.shields.io/badge/Status-Research%20Complete-orange)

This repository contains the data and analytical code for the research study titled: **"Information-Context Complementarity in Digital Platforms: Spatially Heterogeneous Effects of Amenity Bundles on Short-Term Rental Pricing."**

The project investigates how the economic value of information bundles (e.g., groups of amenities) on digital platforms like Airbnb is contingent on the local geographic context. It proposes and tests a theory of **Information-Context Complementarity (ICC)** using a dataset of short-term rental listings in Hong Kong.

---

## 📝 Abstract

Digital platforms utilize standardized information architectures, yet their economic outcomes often vary across local contexts. This study examines the theory of Information-Context Complementarity (ICC), which posits that the performance association of platform-disclosed information bundles depends on their alignment with local context. 

Using a dataset of approximately 2,900 short-term rental listings in Hong Kong, we find associational evidence supporting ICC. Our analytical pipeline first identifies coherent amenity bundles (e.g., “Family/Business,” “Leisure”) through network analysis. Next, Multiscale Geographically Weighted Regression (MGWR) models the spatial variation in their price associations. The results indicate that these associations differ in magnitude and direction across neighborhoods and operate at multiple spatial scales. For example, business-oriented bundles are associated with price premia in central business districts but are discounted elsewhere. A supplementary XGBoost-SHAP analysis suggests that linear spatial models (MGWR) and non-linear machine learning provide complementary insights. 

This study contributes by: 
1. Developing the ICC framework, integrating information systems and spatial economics.
2. Presenting an analytical pipeline for deriving spatial insights from platform data.
3. Offering design implications for geo-contingent platform governance. 

Finally, we outline a research agenda for extending the ICC theory.

**Keywords:** Information-Context Complementarity (ICC); Digital Platforms; Spatial Heterogeneity; Amenity Bundles; Short-Term Rental Markets; Geographically Weighted Regression (MGWR)

---

## 🧠 Conceptual Framework

This research is grounded in the theory of **Information-Context Complementarity (ICC)**. The core idea is that the value of standardized information provided on a platform (like an amenity list) is not absolute but is moderated by the local, real-world context in which a transaction occurs. For example, a "Business-Ready" amenity bundle is more valuable in a financial district than in a remote, scenic area.

Our model posits that platform architecture (information) and neighborhood characteristics (context) interact to determine economic outcomes like price and ratings.

![Conceptual Model Figure](PLACEHOLDER_FOR_YOUR_IMAGE_URL_HERE)
*(Figure 1: Conceptual Model of ICC)*

---

## 📂 Repository Structure

The repository is organized to mirror the analytical pipeline of the research. Raw data, intermediate outputs, and final results are separated into distinct directories.

```text
ICC in Digital Platforms/
├── Code.ipynb                       # Main analysis notebook
├── STAGE 1&2_outputs/               # Outputs from Amenity Analysis & Clustering
│   ├── amenity_communities.csv
│   ├── amenity_frequencies.csv
│   ├── cluster_profiles.csv
│   ├── clustering_bootstrap_ari.csv
│   ├── clustering_model_comparison.csv
│   ├── fig_amenity_network.png
│   ├── fig_clustering_results.png
│   ├── icc_comprehensive_report.txt
│   ├── icc_log.txt
│   ├── stage1_amenity_features.csv
├── STAGE 3&4_outputs/               # Outputs from Spatial Analysis & ML Validation
│   ├── ESDA_Hotspots.png
│   ├── ESDA_KDE_Heatmaps.png
│   ├── Interactive_Map_Accessibility.html
│   ├── Interactive_Map_Bathroom_Personal.html
│   ├── Interactive_Map_Bedding_Comfort.html
│   ├── Interactive_Map_Business_Work.html
│   ├── Interactive_Map_Climate_Control.html
│   ├── Interactive_Map_Essential_Tech.html
│   ├── Interactive_Map_Kitchen_Dining.html
│   ├── Interactive_Map_Outdoor_Recreation.html
│   ├── Interactive_Map_Safety_Security.html
│   ├── Interactive_Map_Transportation.html
│   ├── Interactive_Map_log_price.html
│   ├── Interactive_Map_review_scores_rating.html
│   ├── MGWR_Coeffs_Price_Model.png
│   ├── MGWR_Coeffs_Rating_Model.png
│   ├── SHAP_Importance_log_price.png
│   ├── SHAP_Summary_log_price.png
├── calendar.csv.gz                  # Raw Data
├── listings.csv                     # Raw Data
├── listings_Add_Amenity.xlsx        # Pre-processed Data
├── neighbourhoods.csv               # Neighborhood list
├── neighbourhoods.geojson           # Spatial boundary files
└── reviews.csv                      # Raw Data
````

-----

## ⚙️ Methodological Pipeline

The analysis is conducted in a single Jupyter Notebook, `Code.ipynb`, which is divided into four main stages corresponding to the research methodology.

### `Code.ipynb` Structure

  * **Part 1: Stages 1 & 2** - Focuses on feature engineering and market segmentation.
  * **Part 2: Stages 3 & 4** - Focuses on spatial analysis and machine learning validation.

### Stage 1: Amenity Analysis & Feature Engineering

  * **Goal:** To transform raw amenity text into meaningful "information bundles."
  * **Method:** Social Network Analysis (SNA) models amenity co-occurrence. Amenities are nodes, and their co-presence in a listing creates a weighted edge. The Louvain community detection algorithm identifies densely connected clusters (bundles).
  * **Implementation:** `ICCAnalysisPipeline` class (`stage1_amenity_analysis` method) using `networkx`.

### Stage 2: Listing Clustering

  * **Goal:** To segment listings into distinct typologies based on their amenity profiles.
  * **Method:** A multi-stage clustering protocol (K-Means and Agglomerative Clustering) evaluated using internal validation metrics (Silhouette, Calinski-Harabasz, Davies-Bouldin). Stability is verified using bootstrap analysis and Adjusted Rand Index (ARI).
  * **Implementation:** `stage2_clustering_analysis` method using `sklearn`.

### Stage 3: Spatial Analysis (ESDA & MGWR)

  * **Goal:** To test for spatial heterogeneity (H2) and contextual alignment (H3).
  * **Method:** \* *Exploratory Spatial Data Analysis (ESDA):* Kernel Density Estimation (KDE) and Getis-Ord Gi\* hotspot analysis.
      * *Multiscale Geographically Weighted Regression (MGWR):* Models how price association coefficients of amenity bundles vary across the city at unique spatial scales.
  * **Implementation:** `HongKongSpatialAnalysis` class (`run_esda_analysis`, `run_spatial_modeling`) using `esda`, `libpysal`, and `mgwr`.

### Stage 4: ML Validation (XGBoost & SHAP)

  * **Goal:** To triangulate MGWR findings and test for methodological complementarity (H4).
  * **Method:** An XGBoost model predicts `log_price`. SHapley Additive exPlanations (SHAP) provide global feature importance and local feature contributions, which are compared to MGWR coefficients.
  * **Implementation:** `run_ml_validation` method using `xgboost` and `shap`.

-----

## 📄 File Descriptions

### Input Data

  * `listings.csv`: Primary raw dataset from Inside Airbnb (price, location, amenities).
  * `reviews.csv`: Raw guest reviews.
  * `calendar.csv.gz`: Raw pricing and availability data.
  * `neighbourhoods.csv`: List of Hong Kong neighbourhoods.
  * `neighbourhoods.geojson`: Boundary polygons for spatial joins and mapping.
  * `listings_Add_Amenity.xlsx`: Pre-processed `listings.csv` with parsed amenity categories (primary input for Stages 3 & 4).

### STAGE 1&2\_outputs/ (Generated by ICCAnalysisPipeline)

  * `amenity_frequencies.csv`: Unique amenities and frequencies.
  * `amenity_communities.csv`: Mapping of amenities to Louvain community IDs.
  * `stage1_amenity_features.csv`: **Primary Output** - Listing dataset with counts of amenities per category.
  * `clustering_model_comparison.csv`: Performance metrics for different clustering algorithms/K values.
  * `clustering_bootstrap_ari.csv`: ARI scores from bootstrap stability testing.
  * `cluster_profiles.csv`: Descriptive statistics (size, market share, feature means) for final clusters.
  * `fig_amenity_network.png`: Visualization of the amenity co-occurrence network.
  * `fig_clustering_results.png`: Composite plot of clustering results (PCA, sizes, heatmaps).
  * `icc_log.txt` & `icc_comprehensive_report.txt`: Logs and summary reports.

### STAGE 3&4\_outputs/ (Generated by HongKongSpatialAnalysis)

  * `ESDA_KDE_Heatmaps.png`: Spatial concentration heatmaps.
  * `ESDA_Hotspots.png`: Getis-Ord Gi\* hotspot/coldspot maps.
  * `Interactive_Map_*.html`: Folium interactive maps for exploring hotspots/coldspots.
  * `MGWR_Coeffs_Price_Model.png` & `_Rating_Model.png`: Maps visualizing spatially varying MGWR coefficients.
  * `SHAP_Summary_log_price.png`: Beeswarm plot of feature impact on XGBoost predictions.
  * `SHAP_Importance_log_price.png`: Bar plot of global feature importance.

-----

## 🚀 How to Run the Analysis

### 1\. Clone the Repository

```bash
git clone [https://github.com/your-username/ICC-in-Digital-Platforms.git](https://github.com/your-username/ICC-in-Digital-Platforms.git)
cd ICC-in-Digital-Platforms
```

### 2\. Set up the Environment

It is recommended to use a virtual environment (e.g., conda or venv). Install the required Python packages:

```bash
pip install pandas numpy geopandas matplotlib seaborn networkx python-louvain scikit-learn chardet esda libpysal mgwr xgboost shap folium openpyxl
```

*Note: `python-louvain` is for community detection. Spatial libraries (`esda`, `libpysal`, `mgwr`) may have complex dependencies; refer to their official documentation if issues arise.*

### 3\. Update File Paths

Open `Code.ipynb`. In the first and second code cells, update the file paths in the `files` dictionary and `CONFIG` dictionary to match the location of the data on your local machine.

### 4\. Execute the Notebook

Run the cells in `Code.ipynb` sequentially.

1.  **Cell 1:** Executes Stages 1 and 2 (Generates `STAGE 1&2_outputs/`).
2.  **Cell 2:** Executes Stages 3 and 4 (Generates `STAGE 3&4_outputs/`).

> **⚠️ Warning:** The MGWR analysis in Stage 3 is computationally intensive and may take a significant amount of time to run (potentially several hours) depending on your hardware.

-----

## 📊 Hypotheses and Key Findings

This study tested four primary hypotheses:

  * **H1 (Associational Disclosure Efficacy): Supported.**
      * On average, providing more amenities within coherent bundles is positively associated with `log_price`.
  * **H2 (Spatial Heterogeneity): Supported.**
      * MGWR results show that the associations between amenity bundles and `log_price` are not constant; they vary significantly in both magnitude and sign across different neighborhoods in Hong Kong.
  * **H3 (Contextual Alignment): Supported.**
      * The nature of the spatial variation aligns with local context. For example, the `Business_Work` bundle has a stronger positive price association in central business districts compared to residential or tourist areas.
  * **H4 (Methodological Complementarity): Supported.**
      * The linear spatial model (MGWR) and the non-linear ML model (XGBoost-SHAP) provide complementary insights. While there is partial positive alignment on the most important features, the models capture different facets of heterogeneity, confirming that ICC is a robust phenomenon not tied to a single analytical method.
