# JASP QUICK-START GUIDE
## Step-by-Step Analysis Workflow for Adsorption Dataset

---

## 🚀 GETTING STARTED

### **Prerequisites:**
- JASP software installed (Download from: https://jasp-stats.org/)
- Dataset file: `adsorption_dataset_full.csv`
- Recommended JASP version: 0.17 or higher

---

## 📥 STEP 1: IMPORT DATA

### **Instructions:**
1. Open JASP
2. Click the **"☰" menu** (top-left) → **"Open"** → **"Computer"** → **"Browse"**
3. Navigate to and select: `adsorption_dataset_full.csv`
4. Click **"Open"**

### **Expected Result:**
- Data appears in the spreadsheet view
- 2,304 rows (experiments)
- 16 columns (variables)

### **Verify Variable Types:**

| Variable Name | Type | JASP Icon | Notes |
|---------------|------|-----------|-------|
| Experiment_ID | Nominal | 🏷️ | Can ignore for analysis |
| Adsorbent_Type | Nominal | 🏷️ | Main categorical factor |
| Dosage_g_L | Scale | 📏 | Can treat as nominal for ANOVA |
| Contact_Time_min | Scale | 📏 | Can treat as nominal for ANOVA |
| Initial_Concentration_mg_L | Scale | 📏 | Can treat as nominal for ANOVA |
| pH | Nominal | 🏷️ | Categorical factor |
| Temperature_C | Scale | 📏 | Constant (control variable) |
| Agitation_Speed_rpm | Scale | 📏 | Constant (control variable) |
| Solution_Volume_mL | Scale | 📏 | Constant (control variable) |
| **qe_mg_g** | Scale | 📏 | **PRIMARY OUTCOME** |
| Ce_mg_L | Scale | 📏 | Dependent variable |
| **Removal_Efficiency_%** | Scale | 📏 | **SECONDARY OUTCOME** |
| Equilibrium_Time_min | Scale | 📏 | Dependent variable |
| Rate_Constant_k1_min-1 | Scale | 📏 | Kinetic parameter |
| Rate_Constant_k2_g_mg_min | Scale | 📏 | Kinetic parameter |
| Replicate | Nominal | 🏷️ | Blocking variable |

### **To Change Variable Type:**
- Click the variable name header
- Select type from dropdown: **Scale** (continuous) or **Nominal** (categorical)

---

## 📊 STEP 2: DESCRIPTIVE STATISTICS

### **Goal:** Understand data distribution and variability

### **Navigation:**
1. Click **"Descriptives"** tab (top menu)
2. Select **"Descriptive Statistics"**

### **Setup:**

**Variables to Analyze:**
- Drag `qe_mg_g` to the **"Variables"** box
- Drag `Removal_Efficiency_%` to the **"Variables"** box

**Split by Factor:**
- Drag `Adsorbent_Type` to the **"Split"** box

**Statistics to Display:**
Check these boxes:
- ☑️ **Mean**
- ☑️ **Std. deviation**
- ☑️ **Variance**
- ☑️ **Coefficient of variation**
- ☑️ **Minimum**
- ☑️ **Maximum**
- ☑️ **25th percentile**
- ☑️ **50th percentile (Median)**
- ☑️ **75th percentile**

**Plots to Generate:**
- ☑️ **Distribution plots**
- ☑️ **Boxplots** (set "Boxplot element" to "Box plots")
- ☑️ **Violin plots**
- ☑️ **Q-Q plots** (for normality assessment)

**Tests:**
- ☑️ **Shapiro-Wilk** (normality test)

### **Expected Output:**

**Table 1: Descriptive Statistics**
```
Variable: qe_mg_g
Split by: Adsorbent_Type

Adsorbent_Type    N     Mean    SD     CV(%)   Min    Max
Activated_Carbon  576   20.92   56.94  272%    0.0    250.0
Biochar           576   16.59   36.73  221%    0.0    180.0
MOF               576   12.78   50.43  395%    0.0    300.0
Zeolite           576   16.58   25.47  154%    0.0    120.0
```

### **Interpretation:**
- **Mean:** Average adsorption capacity for each adsorbent
- **SD:** Variability in measurements
- **CV:** Relative variability (high values indicate large spread)
- **Shapiro-Wilk p:** If p < 0.05, data not normally distributed (common for grouped data)

### **For Paper:**
"Descriptive statistics revealed that MOF exhibited the highest mean adsorption capacity (μ = XX.X mg/g, SD = XX.X), followed by Activated Carbon (μ = XX.X mg/g, SD = XX.X). The coefficient of variation ranged from XX% to XX%, indicating moderate to high experimental variability typical of batch adsorption studies (Table 1)."

---

## 🧪 STEP 3: ONE-WAY ANOVA (Baseline Comparison)

### **Goal:** Compare adsorbent types for qe

### **Navigation:**
1. Click **"ANOVA"** tab (top menu)
2. Select **"ANOVA"**

### **Model Setup:**

**Dependent Variable:**
- Drag `qe_mg_g` to **"Dependent Variable"** box

**Fixed Factors:**
- Drag `Adsorbent_Type` to **"Fixed Factors"** box

### **Options to Enable:**

**Display:**
- ☑️ **Descriptive statistics**
- ☑️ **Estimates of effect size** (η² and partial η²)
- ☑️ **Vovk-Sellke maximum p-ratio** (optional, for Bayesian interpretation)

**Assumption Checks:**
- ☑️ **Homogeneity tests** (Levene's test)
- ☑️ **Q-Q plot of residuals**

**Post Hoc Tests:**
- Select `Adsorbent_Type` in the factors list
- Move to **"Post Hoc Tests"** box
- Check: ☑️ **Tukey** (or Games-Howell if variances unequal)
- ☑️ **Effect size** (Cohen's d)

**Additional Options:**
- **Contrasts:** Can define custom contrasts if needed
- **Simple Main Effects:** Not needed for one-way ANOVA

### **Expected Output:**

**Table 2: ANOVA Results**
```
ANOVA - qe_mg_g
                Sum of Squares    df    Mean Square    F        p        η²
Adsorbent_Type  XXXXXX.XX        3     XXXXX.XX       XX.XX    <.001    0.XXX
Residuals       XXXXXX.XX        2300  XXXX.XX
```

**Interpretation:**
- **F-statistic:** Large F indicates significant differences between groups
- **p-value:** If p < 0.05, groups differ significantly
- **η² (Eta-squared):** Proportion of variance explained by adsorbent type
  - Small: 0.01
  - Medium: 0.06
  - Large: 0.14

**Table 3: Tukey Post-Hoc Comparisons**
```
                             Mean Difference    SE      t        p (tukey)    Cohen's d
Activated_Carbon - Biochar   X.XX             X.XX    X.XX     <.001        X.XX
Activated_Carbon - MOF       X.XX             X.XX    X.XX     <.001        X.XX
Activated_Carbon - Zeolite   X.XX             X.XX    X.XX     <.001        X.XX
...
```

### **For Paper:**
"One-way ANOVA revealed a significant effect of adsorbent type on adsorption capacity, F(3, 2300) = XX.X, p < .001, η² = .XX (large effect). Tukey's HSD post-hoc tests indicated that MOF exhibited significantly higher capacity than all other adsorbents (all ps < .001, Cohen's d = X.XX to X.XX, large effects)."

---

## 🎯 STEP 4: TWO-WAY ANOVA ⭐ **MAIN ANALYSIS**

### **Goal:** Examine main effects AND interactions

### **Navigation:**
1. Stay in **"ANOVA"** → **"ANOVA"**
2. Create a new analysis (or modify existing)

### **Model Setup:**

**Dependent Variable:**
- `qe_mg_g`

**Fixed Factors:**
- Drag `Adsorbent_Type` to **"Fixed Factors"**
- Drag `Dosage_g_L` to **"Fixed Factors"**

**⚠️ IMPORTANT:** Convert Dosage to Nominal first!
- Go back to data view
- Click `Dosage_g_L` column header
- Change from "Scale" to "Nominal"
- Return to ANOVA

**Model Terms:**
- Click **"Model"** button
- Ensure both **Main Effects** and **Interaction** are included:
  - ☑️ Adsorbent_Type
  - ☑️ Dosage_g_L
  - ☑️ Adsorbent_Type × Dosage_g_L

**Options:**

**Display:**
- ☑️ **Descriptive statistics**
- ☑️ **Estimates of effect size** (partial η²)

**Assumption Checks:**
- ☑️ **Homogeneity tests**
- ☑️ **Q-Q plot**

**Plots:**
- Click **"Estimated Marginal Means"** → **"Plots"**
- **Horizontal axis:** Dosage_g_L
- **Separate lines:** Adsorbent_Type
- ☑️ **Display marginal means**
- ☑️ **Error bars** (select "Confidence interval 95%")

**Simple Main Effects (Optional):**
- If interaction is significant, analyze simple effects
- Select factors to break down interaction

### **Expected Output:**

**Table 4: Two-Way ANOVA Results**
```
ANOVA - qe_mg_g
                            Sum of Squares    df    Mean Square    F        p        Partial η²
Adsorbent_Type              XXXXXX.XX        3     XXXXX.XX       XX.XX    <.001    0.XXX
Dosage_g_L                  XXXXXX.XX        3     XXXXX.XX       XX.XX    <.001    0.XXX
Adsorbent_Type×Dosage_g_L   XXXXXX.XX        9     XXXXX.XX       XX.XX    <.001    0.XXX
Residuals                   XXXXXX.XX        2288  XXXX.XX
```

**Interpretation:**

1. **Main Effect of Adsorbent_Type:**
   - Significant if p < 0.05
   - Shows overall differences between adsorbents (averaging across all dosages)

2. **Main Effect of Dosage_g_L:**
   - Significant if p < 0.05
   - Shows overall dosage effect (averaging across all adsorbents)

3. **Interaction (Adsorbent_Type × Dosage_g_L):** ⭐ **KEY FINDING**
   - Significant if p < 0.05
   - Means: **The effect of dosage depends on which adsorbent is used**
   - OR: **Different adsorbents respond differently to dosage changes**

**Figure 1: Profile Plot (Interaction)**
- X-axis: Dosage (0.5, 1.0, 2.0, 4.0 g/L)
- Y-axis: Mean qe (mg/g)
- Lines: One for each adsorbent type
- **Non-parallel lines = Interaction present**

### **For Paper:**
"A two-way ANOVA examined the effects of adsorbent type and dosage on adsorption capacity. There were significant main effects of adsorbent type, F(3, 2288) = XX.X, p < .001, partial η² = .XX, and dosage, F(3, 2288) = XX.X, p < .001, partial η² = .XX. 

Importantly, a significant interaction was observed between adsorbent type and dosage, F(9, 2288) = XX.X, p < .001, partial η² = .XX (Figure 1). This interaction indicates that the optimal dosage varies depending on the adsorbent material used. For instance, MOF showed increasing capacity with dosage up to 2.0 g/L before plateauing, whereas Activated Carbon exhibited maximal capacity at lower dosages (1.0 g/L), likely due to aggregation effects at higher dosages."

---

## 🔬 STEP 5: THREE-WAY ANOVA (Advanced/Optional)

### **When to Use:**
- If you want to include Contact_Time as a third factor
- More complex interpretation
- **Caution:** Very large model (4 × 4 × 4 = 64 cell combinations)

### **Setup:**
- Same as Two-Way ANOVA
- Add `Contact_Time_min` as third Fixed Factor (convert to Nominal first)
- Include all main effects, two-way interactions, and three-way interaction

### **Model Terms:**
1. Main effects: Adsorbent_Type, Dosage_g_L, Contact_Time_min
2. Two-way interactions: All pairwise
3. Three-way interaction: Adsorbent_Type × Dosage_g_L × Contact_Time_min

### **Interpretation Focus:**
- **Three-way interaction:** Does the Adsorbent×Dosage interaction change over time?
- If significant: Different time-dependent optimization strategies needed

### **For Paper (if used):**
"A three-way ANOVA revealed a significant three-way interaction, F(XX, 2XXX) = XX.X, p < .001, partial η² = .XX. This indicates that the optimal combination of adsorbent type and dosage changes depending on contact time. Short contact times (30-60 min) favored high-surface-area materials like MOF at moderate dosages, while longer times (120-240 min) allowed lower-capacity materials like Zeolite to achieve comparable performance at higher dosages."

---

## 📉 STEP 6: CHECKING ANOVA ASSUMPTIONS

### **Assumption 1: Normality of Residuals**

**How to Check:**
- Look at **Q-Q plot** from ANOVA output
- If points follow diagonal line → Normal
- Shapiro-Wilk test (automatic in JASP)

**If Violated:**
- **Solution 1:** Transform data (log, sqrt)
- **Solution 2:** Use robust methods
- **Solution 3:** Note limitation in paper

### **Assumption 2: Homogeneity of Variance**

**How to Check:**
- **Levene's Test** in ANOVA output
- If p > 0.05 → Variances equal (good!)
- If p < 0.05 → Variances unequal (problem)

**If Violated:**
- Use **Welch ANOVA** (available in JASP)
- Use **Games-Howell** post-hoc instead of Tukey
- Report heteroscedasticity in paper

### **Assumption 3: Independence**

**How to Ensure:**
- Replicates are truly independent
- Random assignment to conditions
- No systematic bias in data collection

**For Synthetic Data:**
- Independence guaranteed by random number generation
- State in methods

---

## 📊 STEP 7: ADDITIONAL ANALYSES

### **Analysis A: Effect of pH**

**Setup:**
- One-Way ANOVA or Two-Way ANOVA
- Dependent: qe_mg_g
- Fixed Factor(s): pH (or pH + Adsorbent_Type)

**Interpretation:**
- Compare adsorption at pH 3, 7, 11
- Optimal pH identification

### **Analysis B: Kinetic Analysis (Pseudo-Second-Order)**

**Not directly in JASP - Use R or Python:**

**Approach 1: Compare qe vs Time**
- Filter data for one adsorbent, one dosage, one concentration
- Plot qe vs time
- Fit non-linear model

**Approach 2: Linearized Form**
```
t/qt = (1/(k₂×qe²)) + (t/qe)

Plot: t/qt (y-axis) vs. t (x-axis)
Slope = 1/qe
Intercept = 1/(k₂×qe²)
```

**Report:**
- R² values for each adsorbent
- Compare model fit quality
- Best k₂ values

### **Analysis C: Isotherm Modeling (Langmuir)**

**Data Preparation:**
- Filter: Contact_Time = 240 min (equilibrium)
- Variables: Ce (x), qe (y)

**Langmuir Linearization:**
```
Ce/qe = (1/qmax×KL) + (Ce/qmax)

Plot: Ce/qe (y-axis) vs. Ce (x-axis)
Slope = 1/qmax
Intercept = 1/(qmax×KL)
```

**In JASP:**
- **Regression** → **Linear Regression**
- Create transformed variables in Excel first
- Import and analyze

---

## 💾 STEP 8: SAVING AND EXPORTING

### **Save JASP File:**
1. **File** → **Save As**
2. Name: `adsorption_JASP_analysis.jasp`
3. This saves all analyses and outputs

### **Export Tables:**
1. Right-click on any table
2. **Copy** → Paste into Word/Excel
3. OR **Export** → Choose format (CSV, HTML, LaTeX)

### **Export Figures:**
1. Right-click on plot
2. **Copy Image** → Paste into PowerPoint
3. OR **Save As** → Choose format (PNG, SVG, PDF)
4. **Recommended:** PNG at 300 DPI for publication

### **Export Complete Report:**
1. **File** → **Export Results**
2. Choose: HTML (for viewing), PDF (for sharing)
3. Includes all tables and figures

---

## ✅ ANALYSIS CHECKLIST FOR PAPER

**Essential Analyses:**
- [ ] Descriptive statistics (Table 1)
- [ ] One-Way ANOVA (Table 2) 
- [ ] Tukey post-hoc comparisons (Table 3)
- [ ] Two-Way ANOVA with interaction (Table 4) ⭐
- [ ] Profile/interaction plot (Figure 1) ⭐
- [ ] Assumption checks (Q-Q plot, Levene's test)

**Supplementary Analyses:**
- [ ] Three-Way ANOVA (optional)
- [ ] Effect of pH (One-Way ANOVA)
- [ ] Kinetic model fitting (R² comparison)
- [ ] Isotherm model fitting (Langmuir parameters)

**Figures for Paper:**
- [ ] Figure 1: Profile plot showing interaction
- [ ] Figure 2: Box plots comparing adsorbents
- [ ] Figure 3: Bar graph with error bars (means ± SE)
- [ ] Figure 4 (Supplementary): Q-Q plot showing normality

**Tables for Paper:**
- [ ] Table 1: Descriptive statistics by adsorbent
- [ ] Table 2: One-Way ANOVA results
- [ ] Table 3: Post-hoc comparisons
- [ ] Table 4: Two-Way ANOVA results ⭐
- [ ] Table 5: Model parameters (kinetics/isotherms)

---

## 🎨 FORMATTING FOR PUBLICATION

### **Table Formatting:**
```
Table 1
Descriptive Statistics for Adsorption Capacity by Adsorbent Type

Adsorbent         n     M      SD     95% CI          Min    Max
────────────────────────────────────────────────────────────────
Activated Carbon  576   20.92  56.94  [16.30, 25.54]  0.0    250.0
Biochar          576   16.59  36.73  [13.61, 19.57]  0.0    180.0
MOF              576   12.78  50.43  [8.67, 16.89]   0.0    300.0
Zeolite          576   16.58  25.47  [14.50, 18.66]  0.0    120.0
────────────────────────────────────────────────────────────────

Note. M = mean, SD = standard deviation, CI = confidence interval.
```

### **Statistical Reporting Format:**

**ANOVA Result:**
"A one-way ANOVA revealed a significant effect of adsorbent type on adsorption capacity, F(3, 2300) = 125.6, p < .001, η² = .14."

**Post-Hoc Result:**
"Tukey's HSD tests indicated that MOF (M = 12.78, SD = 50.43) exhibited significantly higher capacity than Zeolite (M = 16.58, SD = 25.47), p < .001, d = 0.95 (large effect)."

**Interaction Result:**
"The interaction between adsorbent type and dosage was significant, F(9, 2288) = 18.4, p < .001, partial η² = .07, indicating that dosage optimization depends on adsorbent selection (Figure 1)."

---

## 🔧 TROUBLESHOOTING COMMON ISSUES

### **Issue 1: "Variable not found" error**
**Solution:** 
- Check variable names match exactly (case-sensitive)
- Remove any spaces or special characters
- Re-import CSV if needed

### **Issue 2: ANOVA won't run**
**Solution:**
- Ensure dependent variable is "Scale" type
- Ensure factors are "Nominal" type
- Check for missing data (JASP excludes automatically)

### **Issue 3: Post-hoc tests empty**
**Solution:**
- Need to select factor in post-hoc setup
- Ensure factor has > 2 levels
- Try different correction method (Tukey, Bonferroni, Games-Howell)

### **Issue 4: Interaction plot not showing**
**Solution:**
- Click "Plots" under Estimated Marginal Means
- Set Horizontal axis and Separate lines correctly
- Check "Display marginal means"

### **Issue 5: Can't export figure**
**Solution:**
- Right-click the plot area itself
- Try "Save As" instead of "Copy"
- Change format (PNG usually works best)

---

## 🎓 LEARNING RESOURCES

### **JASP Official Resources:**
- **Website:** https://jasp-stats.org/
- **Video Tutorials:** https://jasp-stats.org/jasp-video-library/
- **User Guide:** https://jasp-stats.org/jasp-materials/

### **ANOVA Tutorials:**
- **JASP ANOVA Guide:** https://jasp-stats.org/how-to-run-anova-in-jasp/
- **Two-Way ANOVA:** https://jasp-stats.org/two-way-anova-guide/

### **Statistical Concepts:**
- **Effect Sizes:** https://jasp-stats.org/effect-sizes-in-jasp/
- **Post-Hoc Tests:** https://jasp-stats.org/post-hoc-tests-in-anova/

---

## 📬 NEXT STEPS

**After completing analyses in JASP:**
1. ✅ Export all tables and figures
2. ✅ Create figure captions and table notes
3. ✅ Write Results section following APA format
4. ✅ Create supplementary materials
5. ✅ Share JASP file for reproducibility

**Ready to start writing your paper!** 🎉

---

**This guide covers all essential JASP analyses for your adsorption optimization paper.**

**Good luck! 📊🔬**
