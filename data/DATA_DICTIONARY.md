# Data Dictionary

## Dataset: `adsorption_dataset_full.csv`

### Overview

| Property | Value |
|----------|-------|
| **Total Records** | 2,304 experiments |
| **Unique Conditions** | 768 (4 × 4 × 4 × 4 × 3) |
| **Replicates per Condition** | 3 |
| **File Format** | CSV (comma-separated values) |
| **Encoding** | UTF-8 |
| **Missing Values** | None |

---

## Variable Descriptions

### Identification Variables

| Variable | Type | Description | Values/Range | Notes |
|----------|------|-------------|--------------|-------|
| `Experiment_ID` | Integer | Unique identifier for each experiment | 1–2304 | Sequential numbering |
| `Replicate` | Integer | Replicate number within condition | 1, 2, 3 | 3 replicates per condition |

### Independent Variables (Factors)

| Variable | Type | Description | Levels | Units | JASP Type |
|----------|------|-------------|--------|-------|-----------|
| `Adsorbent_Type` | Categorical | Type of adsorbent material | Activated_Carbon, Biochar, MOF, Zeolite | — | Nominal |
| `Dosage_g_L` | Numerical (Discrete) | Adsorbent dosage | 0.5, 1.0, 2.0, 4.0 | g/L | Nominal (for ANOVA) |
| `Contact_Time_min` | Numerical (Discrete) | Duration of adsorption | 30, 60, 120, 240 | minutes | Nominal (for ANOVA) |
| `Initial_Concentration_mg_L` | Numerical (Discrete) | Initial pollutant concentration | 25, 50, 100, 200 | mg/L | Nominal (for ANOVA) |
| `pH` | Numerical (Discrete) | Solution pH level | 3, 7, 11 | — | Nominal |

### Controlled Variables (Constants)

| Variable | Type | Description | Value | Units | Notes |
|----------|------|-------------|-------|-------|-------|
| `Temperature_C` | Numerical | Experimental temperature | 25 | °C | Constant across all experiments |
| `Agitation_Speed_rpm` | Numerical | Mixing speed | 150 | rpm | Constant across all experiments |
| `Solution_Volume_mL` | Numerical | Volume of solution | 100 | mL | Constant across all experiments |

### Dependent Variables (Outcomes)

| Variable | Type | Description | Range | Units | Primary/Secondary |
|----------|------|-------------|-------|-------|-------------------|
| `qe_mg_g` | Numerical (Continuous) | Equilibrium adsorption capacity | 0.099–300.0 | mg/g | **Primary Outcome** |
| `Ce_mg_L` | Numerical (Continuous) | Equilibrium concentration | 0.0–199.9 | mg/L | Derived |
| `Removal_Efficiency_%` | Numerical (Continuous) | Percentage of pollutant removed | 1.58–94.57 | % | **Secondary Outcome** |

### Kinetic Parameters

| Variable | Type | Description | Typical Range | Units | Notes |
|----------|------|-------------|---------------|-------|-------|
| `Equilibrium_Time_min` | Numerical (Continuous) | Time to reach equilibrium | 50–120 | minutes | Estimated from k₁ |
| `Rate_Constant_k1_min-1` | Numerical (Continuous) | Pseudo-first-order rate constant | 0.025–0.065 | min⁻¹ | With 10% noise |
| `Rate_Constant_k2_g_mg_min` | Numerical (Continuous) | Pseudo-second-order rate constant | 0.00015–0.00045 | g/(mg·min) | With 10% noise |

---

## Detailed Variable Specifications

### `Adsorbent_Type`

Four types of adsorbent materials with distinct properties:

| Adsorbent | qₘₐₓ (mg/g) | Kₗ (L/mg) | k₂ (g/(mg·min)) | Noise (CV) |
|-----------|-------------|-----------|-----------------|------------|
| **Activated_Carbon** | 250 | 0.15 | 0.0003 | 8% |
| **Biochar** | 180 | 0.10 | 0.0002 | 10% |
| **MOF** | 300 | 0.20 | 0.00035 | 7% |
| **Zeolite** | 120 | 0.08 | 0.00025 | 9% |

### `Dosage_g_L`

Adsorbent mass per unit volume of solution:

| Level | Value | Typical Use |
|-------|-------|-------------|
| 1 | 0.5 g/L | Low dosage |
| 2 | 1.0 g/L | Standard dosage |
| 3 | 2.0 g/L | High dosage |
| 4 | 4.0 g/L | Very high dosage |

**Note:** Higher dosages may lead to aggregation effects, reducing efficiency per unit mass.

### `Contact_Time_min`

Duration of adsorbent-solution contact:

| Level | Value | Kinetic Stage |
|-------|-------|---------------|
| 1 | 30 min | Early kinetics (~50% equilibrium) |
| 2 | 60 min | Mid kinetics (~75% equilibrium) |
| 3 | 120 min | Late kinetics (~90% equilibrium) |
| 4 | 240 min | Near equilibrium (~97% equilibrium) |

### `Initial_Concentration_mg_L`

Starting pollutant concentration in solution:

| Level | Value | Concentration Category |
|-------|-------|------------------------|
| 1 | 25 mg/L | Low |
| 2 | 50 mg/L | Moderate |
| 3 | 100 mg/L | High |
| 4 | 200 mg/L | Very high |

### `pH`

Solution acidity/alkalinity:

| Level | Value | Environment | Effect on Adsorption |
|-------|-------|-------------|---------------------|
| 1 | 3 | Acidic | 25% reduction (factor = 0.75) |
| 2 | 7 | Neutral | No effect (factor = 1.0) |
| 3 | 11 | Alkaline | 15% reduction (factor = 0.85) |

### `qe_mg_g` (Primary Outcome)

Equilibrium adsorption capacity calculated from:

1. **Langmuir isotherm**: qₑ = (qₘₐₓ × Kₗ × Cₑ) / (1 + Kₗ × Cₑ)
2. **Mass balance**: Cₑ = C₀ - qₑ × dosage
3. **Kinetic adjustment**: Based on contact time
4. **pH effect**: Multiplied by pH factor
5. **Noise addition**: ±7-10% CV (normal distribution)

### `Removal_Efficiency_%` (Secondary Outcome)

Calculated as:

```
Removal_Efficiency = ((C₀ - Cₑ) / C₀) × 100%
```

Where:
- C₀ = Initial concentration (mg/L)
- Cₑ = Equilibrium concentration (mg/L)

---

## Data Quality Information

### Variability (Coefficient of Variation)

| Adsorbent | Overall CV | Within-Replicate CV |
|-----------|------------|---------------------|
| Activated_Carbon | 121% | 6.6% |
| Biochar | 116% | 8.7% |
| MOF | 125% | 7.0% |
| Zeolite | 99% | 7.4% |

**Note:** High overall CV reflects the intentional factorial design (varying dosage, concentration, pH), not measurement error. Within-replicate CV represents realistic laboratory precision.

### Missing Values

- **Count:** 0
- **Handling:** Not applicable (synthetic dataset with complete data)

### Outliers

- **Definition:** Values beyond 3 standard deviations from mean
- **Count:** ~1-2% of observations (expected for normal distribution)
- **Handling:** Retained as they represent realistic experimental variation

---

## Usage Notes

### For JASP Analysis

1. **Variable Types:**
   - Set `Adsorbent_Type`, `pH`, and `Replicate` as **Nominal**
   - Set `Dosage_g_L`, `Contact_Time_min`, `Initial_Concentration_mg_L` as **Nominal** for ANOVA
   - Keep all outcome variables (`qe_mg_g`, `Removal_Efficiency_%`, etc.) as **Scale**

2. **Primary Analysis:**
   - Dependent Variable: `qe_mg_g`
   - Fixed Factors: `Adsorbent_Type`, `Dosage_g_L`
   - Focus on: Interaction effect (Adsorbent × Dosage)

### For Python/R Analysis

```python
import pandas as pd

# Load dataset
df = pd.read_csv('adsorption_dataset_full.csv')

# Convert categorical variables
df['Adsorbent_Type'] = df['Adsorbent_Type'].astype('category')
df['pH'] = df['pH'].astype('category')
df['Dosage_g_L'] = df['Dosage_g_L'].astype('category')

# Summary statistics
print(df.groupby('Adsorbent_Type')['qe_mg_g'].describe())
```

---

## Experimental Design Summary

| Design Aspect | Value |
|---------------|-------|
| **Design Type** | Full Factorial |
| **Total Factors** | 5 (4 quantitative + 1 categorical) |
| **Factor Levels** | 4 × 4 × 4 × 4 × 3 = 768 unique conditions |
| **Replication** | 3 per condition |
| **Total Experiments** | 768 × 3 = 2,304 |
| **Balance** | Fully balanced (equal n per cell) |

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2025-01 | Initial release |

---

## Contact

For questions about this dataset:
- **Author:** Anfal Rababah
- **Email:** Anfal0Rababah@gmail.com
- **ORCID:** 0009-0003-7450-8907
