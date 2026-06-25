# Curvature-Based Financial Network Analysis

[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## 📌 Overview

This repository contains the implementation of a curvature-based financial network analysis framework, developed for my accepted paper at The 10th International conference on Interdisciplinary research on Computer Science Psychology and Education (ICICPE) 2026 titled "Forman–Ricci Curvature Reveals Structural Fragility in Financial Correlation Networks". The code analyzes the topological structure of financial markets using **Forman-Ricci curvature** to identify systemic risk and vulnerability across different market regimes.

### Key Features

- **Forman-Ricci Curvature Computation**: Implementation of edge and node-level curvature for weighted undirected financial networks
- **Multi-Regime Analysis**: Analysis across Pre-crisis (2005-2007), Crisis (2008-2009), and Post-crisis (2010-2015) periods
- **Systemic Risk Identification**: Curvature-based fragility scores for identifying systemically important nodes and edges
- **Shock Propagation Modeling**: Curvature-adjusted propagation framework for contagion analysis
- **Statistical Validation**: Comprehensive statistical tests including Mann-Whitney U, bootstrap confidence intervals, and permutation tests
- **Robustness Analysis**: Threshold sensitivity, null model testing, and random shock validation

## 📊 Dataset

The analysis uses monthly stock return data for 401 stocks from the S&P 500 index, spanning from 2005 to 2015. The dataset is divided into three market regimes:

| Regime | Period | Description |
|--------|--------|-------------|
| Pre-crisis | 2005-2007 | Pre-financial crisis period |
| Crisis | 2008-2009 | Global Financial Crisis |
| Post-crisis | 2010-2015 | Post-crisis recovery period |

## 🏗️ Methodology

### Network Construction
- Correlation-based networks using Pearson correlation of stock returns
- Threshold-based edge filtering (threshold = 0.4)
- Weighted undirected graph representation

### Forman-Ricci Curvature
For each edge `(u, v)` with weight `w_e`, the Forman-Ricci curvature is computed as:

```
F_e = w_e × (w_u/w_e + w_v/w_e - Σ_u - Σ_v)
```

where:
- `w_u`, `w_v` are node weights
- `Σ_u = Σ_{e∼u, e≠e'} 1/√(w_e × w_e')` (sum over adjacent edges)
- Node curvature is the average of incident edge curvatures

### Systemic Risk Metrics
- **Curvature Fragility Score**: Negative curvature magnitude (higher = more fragile)
- **Systemic Risk Score**: Composite of degree centrality, eigenvector centrality, and curvature fragility

### Shock Propagation
- Markov-chain based propagation with curvature adjustment
- Negative curvature amplifies contagion; positive curvature dampens it

## 📁 Repository Structure

```
forman-ricci-financial-networks/
├── Notebook 
│   └── ICICPE_2026.ipynb       # Main Jupyter notebook with complete analysis
├── data/
│   └── returns_2005_2015.csv  # Stock returns dataset
├── requirements.txt           # Python dependencies
├── README.md                  # This file
└── LICENSE                    # MIT License
```

## 🚀 Getting Started

### Prerequisites

- Python 3.8 or higher
- Jupyter Notebook / JupyterLab

### Installation

1. Clone the repository:
```bash
git clone https://github.com/sowole-aims/forman-ricci-financial-networks.git
cd forman-ricci-financial-networks
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

3. Launch Jupyter Notebook:
```bash
jupyter notebook ICICPE_2026.ipynb
```


## 📈 Usage

### Running the Analysis

The notebook is organized into the following sections:

1. **Data Loading & Preprocessing**: Load stock return data and define market regimes
2. **Network Construction**: Build correlation networks for each regime
3. **Curvature Computation**: Calculate Forman-Ricci curvature for edges and nodes
4. **Systemic Risk Analysis**: Identify fragile nodes and edges
5. **Shock Propagation**: Run baseline and curvature-adjusted propagation models
6. **Statistical Validation**: Perform statistical tests and robustness checks
7. **Visualization**: Generate figures for publication

### Key Functions

```python
# Build correlation network
G, corr = build_corr_network(data, threshold=0.4)

# Compute Forman-Ricci curvature
frc = FormanRicci(G)
G_curved = frc.compute_ricci_curvature()

# Identify systemic nodes
systemic_nodes = systemic_node_table(G_curved, top_n=20)

# Run shock propagation
result = propagate_shock(
    G_curved,
    shocked_node='GS',
    shock_size=0.5,
    gamma=0.95,
    max_steps=25,
    curvature_adjusted=True,
    alpha=0.5
)
```

## 📊 Results

### Key Findings

1. **Curvature and Systemic Risk**: Crisis periods exhibit significantly more negative Forman-Ricci curvature, indicating higher financial network fragility.

2. **Sectoral Patterns**: Financial sector stocks (GS, IVZ, BEN) consistently appear among the most systemically important nodes across all regimes.

3. **Curvature-Adjusted Propagation**: Incorporating curvature into shock propagation models reveals:
   - Amplified contagion through negatively curved edges during crises
   - Dampened propagation through positive curvature edges during stable periods

4. **Statistical Significance**: Mann-Whitney U tests confirm statistically significant differences in curvature distributions across regimes (p < 0.001).

### Figures

| Figure | Description |
|--------|-------------|
| `regime_curvature_distribution.png` | Box plots of curvature distributions across regimes |
| `density_vs_curvature.png` | Relationship between network density and mean curvature |
| `null_model_comparison.png` | Null model validation using edge weight permutation |
| `curvature_vs_density.png` | Regression analysis of curvature vs. density |

## 🔬 Statistical Validation

The code includes comprehensive statistical validation:

- **Mann-Whitney U Tests**: Compare curvature distributions across regimes
- **Bootstrap Confidence Intervals**: 95% confidence intervals for mean curvature
- **Permutation Tests**: Null model significance testing
- **Threshold Sensitivity**: Analysis across correlation thresholds (0.3-0.6)
- **Random Shock Validation**: Robustness of propagation results
- **Rank Correlation Analysis**: Spearman correlations with centrality measures

## 📝 Citation

If you use this code in your research, please cite:

```bibtex
@inproceedings{author2026curvature,
  title={Forman–Ricci Curvature Reveals Structural Fragility in Financial Correlation Networks},
  author={Oladimeji Samuel Sowole},
  booktitle={The 10th International conference on Interdisciplinary research on Computer Science Psychology and Education (ICICPE)},
  year={2026}
}
```

## 📄 License

Distributed under the MIT License. See `LICENSE` for more information.

## 📧 Contact

Oladimeji Samuel Sowole - [oladimeji.s.sowole@aims-senegal.org](mailto:oladimeji.s.sowole@aims-senegal.org)


---
