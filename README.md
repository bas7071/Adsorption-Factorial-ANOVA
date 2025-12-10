# Statistical Optimization of Multi-Factor Adsorption Processes Using Factorial ANOVA

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.17563321.svg)](https://doi.org/10.5281/zenodo.17563321)
[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)
[![JASP](https://img.shields.io/badge/Analysis-JASP%200.18.3-blue.svg)](https://jasp-stats.org/)
[![Python 3.8+](https://img.shields.io/badge/Python-3.8+-green.svg)](https://www.python.org/)
[![Open Science](https://img.shields.io/badge/Open-Science-orange.svg)](https://en.wikipedia.org/wiki/Open_science)

## 📄 Overview

This repository contains the complete supplementary materials for the methodology paper **"Statistical Optimization of Multi-Factor Adsorption Processes Using Factorial ANOVA: A JASP-Based Methodology Demonstration"** (Rababah, 2025).

The study demonstrates a comprehensive statistical framework for optimizing multi-factor adsorption processes using factorial analysis of variance (ANOVA), with emphasis on detecting and interpreting **interaction effects** that are unattainable through traditional one-factor-at-a-time (OFAT) approaches.

### 🎯 Key Contributions

- **Complete factorial ANOVA workflow** using accessible open-source software (JASP)
- **Interaction effects analysis** revealing that optimal dosage depends on adsorbent type
- **Simple effects decomposition** showing differential dosage sensitivity across materials
- **Reproducible methodology** with all data, code, and analysis files provided
- **Educational resource** for researchers learning factorial experimental design

---

## 📊 Study Summary

| Aspect | Details |
|--------|---------|
| **Dataset** | 2,304 synthetic experiments (768 conditions × 3 replicates) |
| **Adsorbents** | Activated Carbon, Biochar, MOF, Zeolite |
| **Factors** | Adsorbent type, Dosage (4 levels), Contact time (4 levels), Initial concentration (4 levels), pH (3 levels) |
| **Models** | Langmuir isotherm, Pseudo-second-order kinetics |
| **Variability** | CV = 6.6–8.7% (realistic laboratory precision) |
| **Analysis Software** | JASP v0.18.3 (open-source) |
| **Data Generation** | Python 3.8+ with NumPy, Pandas, SciPy |

---

## 🔬 Key Findings

### Main Results

| Analysis | F-statistic | p-value | Effect Size (η²) | Interpretation |
|----------|-------------|---------|------------------|----------------|
| **One-way ANOVA** (Adsorbent Type) | F(3,2300) = 34.8 | p < .001 | η² = .043 | Significant differences among adsorbents |
| **Two-way ANOVA** (Adsorbent × Dosage) | F(9,2288) = 17.74 | p < .001 | η² = .042 | **Critical interaction effect** |
| **Three-way ANOVA** (+ Contact Time) | F(27,2208) = 0.06 | p = 1.000 | η² < .001 | No higher-order interaction |

### Descriptive Statistics by Adsorbent Type

| Adsorbent | Mean qₑ (mg/g) | SD | Min | Max |
|-----------|----------------|-----|-----|-----|
| MOF | 47.26 | 59.16 | 0.199 | 300.0 |
| Activated Carbon | 41.87 | 50.63 | 0.153 | 239.0 |
| Biochar | 29.96 | 34.68 | 0.099 | 158.4 |
| Zeolite | 23.48 | 23.27 | 0.124 | 102.8 |

### Simple Effects Analysis (Dosage Sensitivity)

| Adsorbent | F-statistic | η² | 95% CI | Interpretation |
|-----------|-------------|-----|--------|----------------|
| MOF | F(3,572) = 17.0 | .380 | [.321, .433] | Highest sensitivity |
| Activated Carbon | F(3,572) = 10.2 | .366 | [.306, .420] | High sensitivity |
| Biochar | F(3,572) = 6.46 | .366 | [.275, .391] | Moderate sensitivity |
| Zeolite | F(3,572) = 85.59 | .310 | [.249, .365] | Lower sensitivity |

---

## 📈 Visualizations

### Figure 1: Adsorbent Type × Dosage Interaction (Key Finding)
![Interaction Plot](results/figures/Figure1_interaction_plot.png)

*The non-parallel lines indicate a significant interaction effect: optimal dosage strategy depends on adsorbent type. MOF shows the steepest decline, indicating highest dosage sensitivity.*

### Figure 2: Distribution of Adsorption Capacity
![Boxplots](results/figures/Figure2_boxplots_by_adsorbent.png)

### Figure 3: Mean Adsorption Capacity (±SE)
![Bar Chart](results/figures/Figure3_bar_chart_means.png)

### Figure 4: Heatmap - Adsorbent × Dosage
![Heatmap](results/figures/Figure4_heatmap_adsorbent_dosage.png)

### Figure 5: Simple Effects - Dosage Sensitivity (η²)
![Effect Sizes](results/figures/Figure5_simple_effects_eta_squared.png)

*All adsorbents show large effect sizes (η² > 0.14), but MOF and Activated Carbon demonstrate the highest dosage sensitivity.*

---

## 📁 Repository Structure

```
Adsorption-Factorial-ANOVA/
│
├── 📄 README.md                          # This file
├── 📄 LICENSE                            # CC BY 4.0 License
├── 📄 CITATION.cff                       # Citation metadata
├── 📄 .gitignore                         # Git ignore rules
│
├── 📂 data/
│   ├── adsorption_dataset_full.csv       # Complete dataset (2,304 experiments)
│   └── DATA_DICTIONARY.md                # Variable descriptions and metadata
│
├── 📂 code/
│   ├── generate_adsorption_dataset.py    # Python script for data generation
│   ├── create_figures.py                 # Python script for figure generation
│   └── requirements.txt                  # Python dependencies
│
├── 📂 analysis/
│   ├── adsorption_JASP_analysis.jasp     # JASP analysis file (reproducible)
│   └── JASP_QUICKSTART_GUIDE.md          # Step-by-step JASP instructions
│
├── 📂 results/
│   └── figures/
│       ├── Figure1_interaction_plot.png  # Adsorbent × Dosage interaction
│       ├── Figure2_boxplots_by_adsorbent.png
│       ├── Figure3_bar_chart_means.png
│       ├── Figure4_heatmap_adsorbent_dosage.png
│       ├── Figure5_simple_effects_eta_squared.png
│       ├── Figure6_removal_efficiency_pH.png
│       ├── Figure7_kinetics_by_adsorbent.png
│       └── Figure8_violin_plot.png
│
└── 📂 docs/
    ├── DETAILED_QA_DATASET_GENERATION.md # Q&A about methodology
    └── GITHUB_SETTINGS.md                # Repository setup guide
```

---

## 🚀 Quick Start

### Option 1: Reproduce the Analysis in JASP

1. **Download JASP** (free): https://jasp-stats.org/download/
2. **Download the dataset**: [`data/adsorption_dataset_full.csv`](data/adsorption_dataset_full.csv)
3. **Follow the guide**: [`analysis/JASP_QUICKSTART_GUIDE.md`](analysis/JASP_QUICKSTART_GUIDE.md)
4. **Or open**: [`analysis/adsorption_JASP_analysis.jasp`](analysis/adsorption_JASP_analysis.jasp) directly

### Option 2: Generate New Dataset

```bash
# Clone the repository
git clone https://github.com/Anfal-AR/Adsorption-Factorial-ANOVA.git
cd Adsorption-Factorial-ANOVA

# Install dependencies
pip install numpy pandas scipy matplotlib seaborn

# Generate dataset
python code/generate_adsorption_dataset.py

# Generate figures
python code/create_figures.py
```

### Option 3: Adapt for Your Research

1. Modify adsorbent parameters in `code/generate_adsorption_dataset.py`
2. Adjust experimental conditions (dosages, times, concentrations)
3. Generate custom dataset for your specific system
4. Follow the same JASP workflow for analysis

---

## 📐 Methodology

### Data Generation Framework

```
┌─────────────────────────────────────────────────────────┐
│  STEP 1: Define Parameters (Literature-Based)          │
│  • Adsorbent properties (qmax, KL, k2)                 │
│  • Experimental conditions (dosage, time, conc, pH)    │
└─────────────────────────────────────────────────────────┘
                        ↓
┌─────────────────────────────────────────────────────────┐
│  STEP 2: Solve Langmuir + Mass Balance                 │
│  • Iterative numerical root-finding (scipy.fsolve)     │
│  • Ensures physical consistency                        │
└─────────────────────────────────────────────────────────┘
                        ↓
┌─────────────────────────────────────────────────────────┐
│  STEP 3: Apply Modifying Factors                       │
│  • pH effects (0.75–1.0 multiplier)                    │
│  • Kinetic limitations (PSO model)                     │
│  • Dosage effects (aggregation at high dosages)        │
└─────────────────────────────────────────────────────────┘
                        ↓
┌─────────────────────────────────────────────────────────┐
│  STEP 4: Add Experimental Noise                        │
│  • Normal distribution with CV = 7–10%                 │
│  • Ensures realistic laboratory variability            │
└─────────────────────────────────────────────────────────┘
```

### Statistical Analysis Workflow

```
Descriptive Statistics → Assumption Checking → One-way ANOVA
                                                    ↓
                                            Two-way ANOVA
                                                    ↓
                                    Significant Interaction?
                                          /           \
                                        Yes            No
                                         ↓              ↓
                              Simple Effects      Report Main
                                Analysis          Effects Only
                                         ↓
                              Three-way ANOVA
                              (if needed)
```

---

## 📖 Adsorption Models Used

### Langmuir Isotherm

$$q_e = \frac{q_{max} \times K_L \times C_e}{1 + K_L \times C_e}$$

Where:
- qₑ = equilibrium adsorption capacity (mg/g)
- qₘₐₓ = maximum adsorption capacity (mg/g)
- Kₗ = Langmuir constant (L/mg)
- Cₑ = equilibrium concentration (mg/L)

### Pseudo-Second-Order Kinetics

$$q_t = \frac{k_2 \times q_e^2 \times t}{1 + k_2 \times q_e \times t}$$

Where:
- qₜ = adsorption capacity at time t (mg/g)
- k₂ = rate constant (g/(mg·min))
- t = contact time (min)

### Adsorbent Parameters (Literature-Based)

| Adsorbent | qₘₐₓ (mg/g) | Kₗ (L/mg) | k₂ (g/(mg·min)) | Noise (CV) |
|-----------|-------------|-----------|-----------------|------------|
| Activated Carbon | 250 | 0.15 | 0.0003 | 8% |
| Biochar | 180 | 0.10 | 0.0002 | 10% |
| MOF | 300 | 0.20 | 0.00035 | 7% |
| Zeolite | 120 | 0.08 | 0.00025 | 9% |

---

## 🔧 Dependencies

### For Data Generation & Visualization (Python)

```
numpy>=1.20.0
pandas>=1.3.0
scipy>=1.7.0
matplotlib>=3.5.0
seaborn>=0.11.0
```

### For Statistical Analysis

- **JASP** v0.17+ (free, open-source): https://jasp-stats.org/

---

## 📚 Citation

If you use this dataset, methodology, or code in your research, please cite:

```bibtex
@article{rababah2025factorial,
  title={Statistical Optimization of Multi-Factor Adsorption Processes 
         Using Factorial ANOVA: A JASP-Based Methodology Demonstration},
  author={Rababah, Anfal},
  journal={Zenodo},
  year={2025},
  doi={10.5281/zenodo.17563321},
  url={https://doi.org/10.5281/zenodo.17563321}
}
```

**APA Format:**
> Rababah, A. (2025). Statistical optimization of multi-factor adsorption processes using factorial ANOVA: A JASP-based methodology demonstration. *Zenodo*. https://doi.org/10.5281/zenodo.17563321

---

## 🤝 Contributing

Contributions are welcome! Please feel free to:

- 🐛 Report bugs or issues
- 💡 Suggest improvements to the methodology
- 📝 Improve documentation
- 🔧 Add new features to the data generation script
- 🌍 Translate guides to other languages

---

## 📜 License

This work is licensed under the **Creative Commons Attribution 4.0 International License** (CC BY 4.0).

You are free to:
- **Share** — copy and redistribute the material
- **Adapt** — remix, transform, and build upon the material

Under the following terms:
- **Attribution** — You must give appropriate credit and indicate if changes were made

---

## 👤 Author

**Anfal Rababah**
- 📧 Email: Anfal0Rababah@gmail.com
- 🔬 ORCID: [0009-0003-7450-8907](https://orcid.org/0009-0003-7450-8907)
- 🌐 Platform: [SparkSkyTech Educational Platform](https://sparkskytech.com)

---

## 🙏 Acknowledgments

- **JASP Team** for developing and maintaining the open-source JASP software
- **Scientific Community** for establishing the theoretical foundations of adsorption models
- **Claude (Anthropic)** for assistance with literature organization, technical writing refinement, and Python code development

---

<p align="center">
  <strong>Open Science • Reproducible Research • Accessible Statistics</strong>
</p>

<p align="center">
  Made with ❤️ for the research community
</p>
