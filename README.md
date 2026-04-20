# COVID-19 Single-Cell RNA-seq Analysis

## Dataset
- **Source:** GSE145926 (Liao et al. 2020, Nature Medicine)
- **Sample Type:** Bronchoalveolar lavage fluid (BALF)
- **Technology:** 10x Genomics single-cell RNA-seq
- **Patients:** 12 total (3 Healthy, 6 Moderate COVID-19, 3 Severe COVID-19)

## Analysis Summary

### Dataset Statistics
- **Total cells (raw):** 108,230
- **Total cells (filtered):** 82,319 (76.1% retention)
- **Total genes:** 24,899
- **Highly variable genes:** 1,589
- **Clusters identified:** 17
- **Cell types annotated:** 15

### Cell Type Distribution
1. Alveolar Macrophages: 22,335 cells (27.1%)
2. Inflammatory Macrophages: 17,652 cells (21.4%)
3. T cells: 14,483 cells (17.6%)
4. Activated Macrophages: 6,370 cells (7.7%)
5. Other cell types: 21,479 cells (26.1%)

### Key Findings

**1. Disease-Specific Cellular Remodeling**
- Healthy lungs: Dominated by alveolar macrophages
- COVID-19 lungs: Shift to inflammatory macrophages
- 15 distinct cell types identified in BALF

**2. Strong Interferon Response**
- 1,494 genes significantly upregulated in COVID-19 T cells
- Top genes: ISG15, IFITM3, IFITM1, MX1, IFIT1, IFIT3, RSAD2
- Universal type I interferon signature across cell types

**3. Cell Type-Specific Responses**
- T cells: Robust interferon-stimulated gene expression
- Macrophages: Activation and inflammatory signatures
- Epithelial cells: Present in both conditions

## Files Generated

### Figures
- `01_patient_distribution.png` - Cell counts per patient
- `02_qc_metrics_prefilter.png` - Quality control metrics
- `04_umap_overview.png` - UMAP visualizations
- `05_cell_type_annotation.png` - Cell type identification
- `06_interferon_genes.png` - Interferon response genes
- `07_figure_complete_analysis.png` - Complete overview

### Results
- `summary_statistics.csv` - Overall dataset statistics
- `cell_type_distribution.csv` - Cell type counts and percentages
- `DE_tcells_covid_vs_healthy.csv` - Differential expression results
- `covid_analysis_complete.h5ad` - Processed AnnData object

## Analysis Pipeline

### Stage 1-2: Data Loading and QC
- Loaded 12 H5 files from GEO
- Quality control filtering:
  - Min genes per cell: 200
  - Max genes per cell: 5,000
  - Max mitochondrial %: 20%
  - Min cells per gene: 3

### Stage 3-4: Normalization
- Normalized to 10,000 counts per cell
- Log transformation
- Identified 1,589 highly variable genes
- Scaled data for downstream analysis

### Stage 5: Dimensionality Reduction
- PCA: 50 components
- UMAP: 2D embedding
- Neighbor graph: k=15, using 30 PCs

### Stage 6: Clustering
- Leiden algorithm (resolution=0.5)
- 17 clusters identified
- Merged into 15 cell types based on marker genes

### Stage 7: Cell Type Annotation
- Marker gene identification (t-test)
- Manual annotation using canonical markers
- Cell types: Macrophages, T cells, NK cells, Plasma cells, Epithelial cells

### Stage 8: Differential Expression
- Compared COVID-19 vs Healthy within cell types
- Method: Wilcoxon rank-sum test
- Focus: T cells (14,387 COVID vs 96 Healthy)
- Result: 1,494 significant genes (p<0.01, |logFC|>2)

## Software and Versions
- Python 3.x
- scanpy
- pandas
- numpy
- matplotlib
- seaborn

## Author
Aysha Khenza U

## Date
April 2026

## Reference
Liao M, Liu Y, Yuan J, et al. Single-cell landscape of bronchoalveolar immune cells in patients with COVID-19. Nat Med. 2020;26(6):842-844.
