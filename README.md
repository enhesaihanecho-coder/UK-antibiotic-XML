# UK Antibiotic Prescribing Patterns: Clustering & Explainable AI Analysis

A data-driven exploration of regional antibiotic prescribing heterogeneity across 106 UK Sub-ICBs, combining unsupervised learning with explainable AI to uncover socio-economic and clinical determinants.

## 📋 Project Overview

This project analyzes antibiotic prescribing patterns at the Sub-ICB level in England (2024-2025 data) to identify distinct regional "prescribing archetypes" and understand what drives them. Rather than treating all regions uniformly, this analysis reveals that different regions face fundamentally different challenges requiring tailored stewardship strategies.

### Key Questions Addressed:
- What distinct prescribing patterns exist across UK regions?
- Which socio-economic and clinical factors drive high antibiotic use?
- Do these drivers operate differently across regional different patterns?

## 🔍 Methodology

### 1. Data Collection & Integration
- **Antibiotic data**: Extracted via UKHSA Fingertips API (106 Sub-ICBs)
- **Socio-economic determinants**: 
  - GP workforce density (NHS Digital)
  - Population age structure (NHS Digital)
  - Index of Multiple Deprivation (Fingertips API)
  - COPD prevalence (Fingertips API)
  - Ethnic minority percentage (Nomis)

### 2. Feature Engineering
Created 4 dimensions to characterize prescribing behavior:
- **Intensity**: Antibiotic items per 1,000 registered patients
- **Quality**: Proportion of broad-spectrum antibiotics (%)
- **Seasonality**: Winter-to-summer prescribing ratio
- **Trend**: Year-over-year volume change (%)

### 3. Unsupervised Learning (K-Means Clustering)
Applied K-Means clustering to identify natural groupings in the 4D feature space, revealing **4 distinct prescribing archetypes**.

### 4. Dimensionality Reduction (PCA)
Used Principal Component Analysis for visualization:
- **PC1 (horizontal)**: Prescribing quality & seasonality
- **PC2 (vertical)**: Prescribing intensity

### 5. Explainable AI (Random Forest + SHAP)
- Trained Random Forest model (R² ≈ 0.94) to predict prescribing intensity
- Applied SHAP (SHapley Additive exPlanations) for feature attribution
- Conducted both national-level and cluster-specific analyses

## 📊 Key Findings

### Four Prescribing Archetypes

**Cluster 0: High Demand, Well-Managed (26 regions)**
- High prescribing volume but targeted (low broad-spectrum use)
- Driven primarily by aging population (>65%)
- COPD prevalence as secondary driver

**Cluster 1: Low Intensity, Inefficient (24 regions)**
- Young population, low overall prescribing
- High broad-spectrum use and seasonal fluctuation
- "Young but inefficient" - opportunity for quality improvement

**Cluster 2: Low Intensity, Targeted (29 regions)**
- Benchmark group with stable, refined prescribing
- **Hidden concern**: High deprivation paradoxically associated with *lower* antibiotic use, raising accessibility questions

**Cluster 3: The Double Burden (27 regions)**
- High prescribing volume AND high broad-spectrum use
- Driven by aging population + social complexity
- **Critical insight**: GP workforce shortage significantly amplifies prescribing intensity in these regions

### National vs. Cluster-Specific Drivers

At the national level, elderly population dominates. However, cluster-specific analysis reveals:
- **GP workforce density** becomes critical specifically in high-burden regions (Cluster 3)
- **Deprivation (IMD)** shows complex, non-linear effects varying by cluster
- Simple national-level policies would miss these regional nuances

## 🗂️ Repository Structure

```
.
├── UK_antibiotic_drivers.ipynb              # main analysis notebook
├── data/
│   ├── raw/                                 # Source data files
│   │   ├── antibiotics_raw_data.csv
│   │   ├── 94240_Deprivation_score_IMD_2025.csv
│   │   ├── 93468_GP_populations_by_age.csv
│   │   ├── 253_COPD_QOF_prevalence.csv
│   │   └── Ethnic_group_by_religion.xlsx
│   └── processed/                           # Cleaned datasets
│       ├── clustering_input.csv
│       └── merged_drivers_data.csv
├── requirements.txt
└── README.md
```

## 🛠️ Technologies Used

- **Python 3.11**
- **Data Processing**: pandas, numpy
- **Machine Learning**: scikit-learn (K-Means, Random Forest, PCA)
- **Explainable AI**: SHAP
- **Visualization**: matplotlib, seaborn
- **API Access**: requests

## 🚀 Getting Started

### Prerequisites
```bash
python >= 3.11
```

### Installation
```bash
# Clone the repository
git clone https://github.com/yourusername/uk-antibiotic-clustering.git
cd uk-antibiotic-clustering

# Install dependencies
pip install -r requirements.txt

# Launch Jupyter
jupyter notebook
```

### Running the Analysis
Execute notebooks in order (01 → 05):
1. Fetch data from Fingertips API
2. Engineer prescribing features
3. Perform clustering analysis
4. Integrate socio-economic determinants
5. Run explainable ML analysis

## 💡 Implications

This analysis demonstrates that:
1. **Regional heterogeneity matters**: One-size-fits-all stewardship policies overlook critical local contexts
2. **Workforce is infrastructure**: GP density emerges as a key lever in high-burden areas
3. **Quality vs. Quantity trade-offs**: Some regions need volume reduction, others need prescribing refinement
4. **Hidden accessibility gaps**: Low prescribing in deprived areas may signal under-treatment

## 📈 Future Directions

- Extend to practice-level  analysis for real-time monitoring
- Explore links to health economic perspectives, such as indicative budget impact or resource utilisation implications, to provide contextual insights relevant for healthcare planning.

## 📧 Contact

**Author**: Enhe Saihan 
**Email**: enhesaihanecho@gmail.com
**Affiliation**: Self-directed research project

---
