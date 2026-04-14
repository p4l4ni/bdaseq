🧬 BDASeq® RNA-Seq Pipeline Replication & Cross-Disease Biomarker Discovery


📌 Project Overview

This repository presents a Python-based replication and extension of the BDASeq® (Biomarker Discovery Algorithm for RNA-Seq) pipeline for cross-disease biomarker discovery in:

Huntington’s Disease (HD)
Alzheimer’s Disease (AD)

The project reproduces the methodology from Dias Pinto et al. (2025) and validates its reproducibility while extending it to a cross-disease transcriptomic comparison.

🎯 Objectives
Replicate the BDASeq® RNA-Seq pipeline for HD (GSE64810)
Validate FTH1 downregulation as a key biomarker
Implement RMC ensemble differential expression analysis
Perform GO Biological Process enrichment
Extend the pipeline to AD (GSE132903)
Identify shared vs disease-specific druggable targets
🧪 Key Results
✅ 1,236 DEGs identified (788 upregulated, 448 downregulated)
✅ FTH1 significantly downregulated (p = 0.016)
✅ 394 druggable targets extracted
✅ GO enrichment revealed:
Neuroinflammation
Metal ion transport
TGF-β signaling
✅ Cross-disease comparison:
HD targets: 117
AD targets: 360
Shared: 5 (2.1%)
⚙️ Pipeline Architecture

The workflow follows a 3-layer BDASeq® architecture:

1. Data Processing & Quality Control
   ├── GEO Data Acquisition
   ├── Propensity Score Matching (PSM)
   └── UMAP + DBSCAN Outlier Detection

2. RMC Ensemble Differential Expression
   ├── DESeq2
   ├── edgeR
   ├── limma-voom
   └── Majority Voting (RMC)

3. Target Discovery & Analysis
   ├── Feature Selection (Random Forest)
   ├── GO Enrichment (Enrichr)
   └── Cross-Disease Comparison (HD vs AD)
📂 Repository Structure
├── data/
│   ├── GSE64810/              # HD dataset
│   ├── GSE132903/             # AD dataset
│
├── notebooks/
│   └── Bio22MIA1201.ipynb     # Main pipeline notebook
│
├── outputs/
│   ├── rmc_deg_results.csv
│   ├── top_druggable_targets.csv
│   ├── go_enrichment.csv
│   ├── rmc_ad_results.csv
│   ├── figures/
│
├── src/
│   ├── preprocessing.py
│   ├── psm.py
│   ├── dea_rmc.py
│   ├── enrichment.py
│   └── utils.py
│
├── report/
│   └── BDASeq_Final_Report.docx
│
├── requirements.txt
└── README.md
🧰 Tech Stack
Programming & Core Libraries
Python 3.10
pandas, numpy
scipy, statsmodels
Bioinformatics & RNA-Seq
PyDESeq2
edgeR (via rpy2)
limma-voom (via rpy2)
GEOparse
Machine Learning & Analysis
scikit-learn (DBSCAN, Random Forest)
scanpy, umap-learn
gseapy
Visualization
matplotlib
seaborn
📊 Methodology Details
1. Propensity Score Matching (PSM)
1:1 nearest neighbor matching
Covariate: Age
Validation: Kolmogorov-Smirnov test (p > 0.05)
2. Outlier Detection
UMAP dimensionality reduction
DBSCAN clustering
Result: 0 outliers (high-quality dataset)
3. RMC Ensemble DEA

A gene is considered DEG if:

≥2 methods agree (DESeq2, edgeR, limma)
FDR < 0.05
Consistent log2FC direction
4. Feature Selection
Random Forest importance (Gini index)
Combined ranking score
5. GO Enrichment
Database: GO_Biological_Process_2023
Method: Fisher’s Exact Test + BH correction
🧬 Key Biological Insight
FTH1 as a Biomarker
Encodes ferritin heavy chain (iron storage)
Downregulated in HD brain
Linked to ferroptosis & oxidative stress
Potential blood-based biomarker
🔬 Datasets Used
Dataset	Disease	Samples	Platform
GSE64810	Huntington’s Disease	40 (post-PSM)	RNA-Seq
GSE132903	Alzheimer’s Disease	195	Microarray

Source: NCBI GEO

🚀 How to Run
1. Clone Repository
git clone https://github.com/22MIA1201/bdaseq-hd-ad-replication.git
cd bdaseq-hd-ad-replication
2. Install Dependencies
pip install -r requirements.txt
3. Run Pipeline
jupyter notebook notebooks/Bio22MIA1201.ipynb
📈 Outputs
Differential expression results
Druggable targets
GO enrichment results
Visualizations:
Volcano plot
Heatmap
UMAP plots
Boxplots
⚠️ Challenges & Limitations
Reduced RMC (3 methods vs original 8) due to compute limits
Custom PSM implementation in Python
Batch correction differences (pyComBat vs R ComBat-Seq)
No outliers detected (limits demonstration of QC step)
🔍 Future Work
Extend to full 8-method RMC ensemble
Integrate multi-cohort datasets
Add single-cell RNA-Seq analysis
Validate biomarkers in clinical datasets
Explore pan-neurodegeneration targets
📚 References

Key reference:

Dias Pinto et al., Cells (2025) — BDASeq® pipeline

(See full report for complete references)

👨‍💻 Author

Palaniappan M
M.Tech Business Analytics
VIT Chennai

📎 Links
📘 Report: Included in /report
💻 Notebook: Bio22MIA1201.ipynb
📂 Outputs: /outputs
