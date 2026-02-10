# Replication Package for "Empowering Women Through Radio: Evidence from Occupied Japan"

**Author:** Yoko Okuyama (Uppsala University)  
**Published in:** Journal of Development Economics, Volume 179, 2026  
**DOI:** https://doi.org/10.1016/j.jdeveco.2025.103620

---

## Download Replication Package

**Data and Code Files:** [Download from Dropbox](https://www.dropbox.com/scl/fi/o23loistxjg9pzpus6wlx/replication_package.zip?rlkey=6f4deejlvzp9o89xt93nrj7n6&st=rc68bvba&dl=0)

The download (~1.5 MB) includes:
- `data/` - Analysis datasets (.dta files)
- `code/` - Main analysis script (analysis.do)
- `documentation/` - Table 2 comparison (PDF)
- `output/` - Empty folder (created by analysis.do)

**Instructions:** Download the ZIP file, extract it, and follow the steps below.

---

## Overview

This replication package contains all materials necessary to replicate the main result tables 1-4 from "Empowering Women Through Radio: Evidence from Occupied Japan." The paper examines the impact of women's radio programs broadcast by the US-led occupying force in Japan (1945-1952) on women's political participation, fertility, and labor market outcomes.

The analysis employs an instrumental variable (IV) strategy that exploits variation in AM radio signal strength driven by local soil conductivity to identify causal effects of radio exposure on women's outcomes.

---

## Citation

If you use this replication package, please cite:

```
Okuyama, Y. (2026). Empowering women through radio: Evidence from Occupied Japan. 
Journal of Development Economics, 179, 103620.
```

---

## Software Requirements

### Required Software
- **Stata/MP 16.1 or later** (code tested on Stata/MP 16.1 for Windows 64-bit)
- Approximately 2GB of available memory

### Required Stata Packages

The following user-written packages must be installed before running the analysis:

```stata
ssc install ivreg2
ssc install estout
```

**To check if packages are installed:**
```stata
which ivreg2
which estout
```

If any package is not found, install it using the `ssc install` command above.

---

## Data Availability Statement

Due to copyright restrictions on historical archival materials, raw data from original sources cannot be shared. However, this package includes cleaned, analysis-ready datasets that contain only the variables necessary to replicate all main results, tables, and figures in the paper.

**Data included:**
- `analysis_data_clean.dta` - District-level data
- `analysis_data2_clean.dta` - District-candidate level data for Table 3

**Data not included:**
- Raw archival materials
- Original newspaper scans for electoral turnout

---

## File Structure

```
replication_package/
├── README.md                          (this file)
├── data/
│   ├── analysis_data_clean.dta       (district-level data for Tables 1, 2, 4)
│   └── analysis_data2_clean.dta      (district-candidate data for Table 3)
├── code/
│   └── analysis.do                   (main analysis file)
├── output/                           (created by analysis.do)
│   └── tables/                       (regression tables in .tex format)
└── documentation/
    └── table2_comparison.pdf         (comparison of published vs. replicated Table 2)
```

---

## Replication Instructions

### Step 1: Install Required Packages

Open Stata and run:

```stata
ssc install ivreg2
ssc install estout
```

### Step 2: Set Working Directory

Extract the replication package to your desired location (e.g., `C:/Users/YourName/replication/`).

Open `code/analysis.do` in Stata's do-file editor and modify the first few lines:

```stata
*==============================================================================*
* USER: CHANGE THIS PATH TO YOUR REPLICATION PACKAGE LOCATION
*==============================================================================*
global replication_path "C:/Users/YourName/replication"

* The following paths are set automatically based on the above
global data    "${replication_path}/data"
global code    "${replication_path}/code"
global output  "${replication_path}/output"
```

**Important:** Use forward slashes (/) in the path, not backslashes.

### Step 3: Run the Analysis

In Stata, execute:

```stata
cd "${replication_path}/code"
do analysis.do
```

The script will:
1. Load the data from `../data/analysis_data_clean.dta` and `../data/analysis_data2_clean.dta`
2. Run all regressions and analyses
3. Generate tables in `../output/tables/`
4. Generate figures in `../output/figures/`
5. Display results in the Stata results window

### Step 4: Check Outputs

After successful execution, you should find the following files in the `output/` folder:

**Main Tables:**
- `TURNOUT-OLS-IV-result-for-revision.tex` (Table 2: Voter Participation)
- `FEMALE-VOTE-SHARE-result-for-revision.tex` (Table 3: Female Candidates' Vote Share)
- `MARRIAGE-OLS-IV-result-for-revsion.tex` (Table 4, Panel A: Employment, Marriage, Divorce)
- `CBR-OLS-IV-result-for-revsion.tex` (Table 4, Panel B: Birth Rates)
- `balancing-test-for-revision.tex` (Table 1, Panel A: Balance Tests - Political Variables)
- `balancing-test-for-revision-2.tex` (Table 1, Panel B: Balance Tests - Demographic Variables)

---

## Replication Note: Table 2 Sample Size

**Important:** The published Table 2 uses N = 337 districts, while the current replication data yields N = 339. This minor discrepancy (2 districts, <0.6%) stems from improvements in linking districts across historical election records over time. Specifically, the updated data cleaning process better accounts for municipal name changes, spelling corrections, and municipal mergers between the prewar and postwar periods. Results are substantively identical (coefficients match to the second decimal place), and all main conclusions hold. 

The file `table2_comparison.pdf` in the `documentation/` folder provides a side-by-side comparison of published (N=337) and replicated (N=339) results for verification.

**All other tables (Tables 1, 3, and 4) replicate exactly.**

---

## Key Variables in the Datasets

### Dataset 1: analysis_data_clean.dta
**Structure:** One observation per district (N=662)  
**Used for:** Tables 1, 2, and 4

#### Identifiers (4 variables)
- `PREFDIST` - District identifier (prefecture + district name)
- `prefecture` - Prefecture code (1-47)
- `sample_baseline` - Baseline sample indicator (=1 if included in main analysis)
- `radio_station` - Nearest radio station identifier

#### Treatment Variables (2 variables)
- `RADIO_SUBSCRIPTION1946_SDUNIT` - Radio subscription rate in 1946 (standardized to mean 0, SD 1)
- `RADIO_SUBSCRIPTION1946_PCT` - Radio subscription rate in 1946 (percentage, 0-100)

#### Instrumental Variable (2 variables)
- `wavg_signal_sdunit` - AM radio field strength (standardized to mean 0, SD 1)
- `wavg_signal` - AM radio field strength (raw units: mv/m)

#### Control Variables (6 variables)
- `NEAR_DIST_DECILEBIN` - Distance to nearest transmitter (categorical: decile bins 1-10)
- `NEAR_DIST` - Distance to nearest transmitter (continuous: kilometers)
- `LOG_HH_10000` - Log of number of households (in units of 10,000)
- `HH_1946` - Number of households in 1946 (raw count)
- `HEAVY_DAMAGE` - Severe WWII damage indicator (=1 if heavy air raids or atomic bomb)

#### Outcome Variables (9 variables)

**Electoral Outcomes (1946):**
- `WOMEN_TURNOUT` - Women's electoral turnout in 1946 (proportion, 0-1)
- `MEN_TURNOUT` - Men's electoral turnout in 1946 (proportion, 0-1)
- `VOTE_SHARE` - Female candidate's vote share in 1946 (proportion, 0-1)

**Fertility Outcomes:**
- `CBR1947` - Crude birth rate in 1947 (per 1000 population)
- `CBR1950` - Crude birth rate in 1950 (per 1000 population)
- `CSBR1950` - Stillbirth rate in 1950 (per 1000 births)

**Labor Market and Family Outcomes (1950):**
- `LFP1950_NOFAMILYEMP_SEX2` - Female employment rate in 1950, excluding family employment (proportion, 0-1)
- `CRMARRIAGE1950` - Crude marriage rate in 1950 (per 1000 population)
- `CRDIVORCE1950` - Crude divorce rate in 1950 (per 1000 population)

#### Pre-treatment Characteristics (14 variables)

**Political Variables (for Table 1, Panel A):**
- `TURNOUT1928` - Electoral turnout in 1928 general election (proportion, 0-1)
- `WSL_DISTRICT1928` - Women's Suffrage League endorsed candidate in district (=1 if yes)
- `WSL_VOTESHARE1928` - Vote share of WSL-endorsed candidate in 1928 (proportion, 0-1)
- `TURNOUT1937` - Electoral turnout in 1937 general election (proportion, 0-1)
- `TURNOUT1942` - Electoral turnout in 1942 wartime election (proportion, 0-1)
- `IRAA_VOTESHARE1942` - Vote share of Imperial Rule Assistance Association in 1942 (proportion, 0-1)

**Demographic and Economic Variables (for Table 1, Panel B):**
- `MFRATIO_BIRTH1935` - Male-to-female ratio at birth in 1935 (~105)
- `MFRATIO_1940` - Male-to-female ratio in population in 1940 (~95-100)
- `INDUSTRIAL_SEX_SEG1940` - Industrial sex segregation index in 1940 (0-1, higher = more segregated)
- `LABORSHARE1940_PRIMARY` - Primary sector labor share in 1940 (proportion, 0-1)
- `FEMALE_LABOR_RATE1940` - Female labor force participation rate in 1940 (proportion, 0-1)
- `CRMARRIAGE1935` - Crude marriage rate in 1935 (per 1000 population)
- `CBR1935` - Crude birth rate in 1935 (per 1000 population)

**Total variables in dataset 1: 35**

---

### Dataset 2: analysis_data2_clean.dta
**Structure:** One observation per district × female candidate pair (N≈618)  
**Used for:** Table 3 only

#### Identifiers (4 variables)
- `PREFDIST` - District identifier (prefecture + district name)
- `prefecture` - Prefecture code (1-47)
- `radio_station` - Nearest radio station identifier
- `n_district_per_candidate` - Number of districts where each candidate ran (used for analytical weights)

#### Treatment Variables (2 variables)
- `RADIO_SUBSCRIPTION1946_SDUNIT` - Radio subscription rate in 1946 (standardized)
- `RADIO_SUBSCRIPTION1946_PCT` - Radio subscription rate in 1946 (percentage, 0-100)

#### Instrumental Variable (1 variable)
- `wavg_signal_sdunit` - AM radio field strength (standardized)

#### Control Variables (3 variables)
- `NEAR_DIST_DECILEBIN` - Distance to nearest transmitter (decile bins)
- `LOG_HH_10000` - Log of number of households (in 10,000s)
- `HEAVY_DAMAGE` - Severe WWII damage indicator

#### Outcome Variable (1 variable)
- `VOTE_SHARE` - Female candidate's vote share in district (proportion, 0-1)

#### Sample Restriction & Additional Control (2 variables)
- `WOMEN_TURNOUT` - Women's electoral turnout (used for sample restriction)
- `WOMEN_TURNOUT_PCT` - Women's electoral turnout in percentage (used as control in Column 4)

**Total variables in dataset 2: 13**

**Note:** Analytical weights in Table 3 regressions are constructed as: `weight = 1 / n_district_per_candidate`

---

## Sample Sizes and Restrictions

### By Table:

**Table 1 (Balance Tests):**
- Sample: 662 districts (full sample where `sample_baseline == 1`)
- Some pre-treatment variables have missing values for certain districts

**Table 2 (Voter Participation):**
- Women's turnout: 337 districts (26 prefectures with gender-disaggregated data)
- Men's turnout: 327 districts (10 fewer due to missing men's turnout in one prefecture)
- Sample restriction: `sample_baseline == 1` and `WOMEN_TURNOUT != .`

**Table 3 (Female Candidates' Vote Share):**
- Sample: ≈618 district-candidate pairs
- Sample restrictions: `wavg_signal_sdunit != .` and `WOMEN_TURNOUT != .`
- Uses analytical weights: `[aweight = weight]` where `weight = 1/n_district_per_candidate`

**Table 4 (Fertility, Employment, Marriage):**
- Sample: 662 districts (full sample)
- Marriage/divorce may have slightly fewer observations (~660) due to missing data

---

## Main Results to Expect

### Table 2: Voter Participation (First Stage, Reduced Form, OLS, 2SLS)
- **First Stage F-statistic:** ~28-30 (strong instrument)
- **2SLS Effect on Women's Turnout:** ~0.024 (2.4 percentage points per SD increase in radio exposure)
- **2SLS Effect on Men's Turnout:** ~0.009 (not statistically significant)

### Table 3: Female Candidates' Vote Share
- **2SLS Effect:** ~0.023 (2.3 percentage points per SD increase in radio exposure)

### Table 4: Fertility, Employment, Marriage
- **2SLS Effect on Birth Rate (1950):** ~-2.0 per 1000 population
- **2SLS Effect on Employment:** Not statistically significant
- **2SLS Effect on Marriage/Divorce:** Not statistically significant

### Table 1: Balance Tests (Instrument Validity)
- All pre-treatment variables should show **no statistically significant correlation** with residualized field strength

---

## Troubleshooting

### Problem: "command ivreg2 not found"
**Solution:** Install the package: `ssc install ivreg2`

### Problem: "file analysis_data_clean.dta not found"
**Solution:** Check that:
1. You extracted the full replication package
2. Your working directory path is correct
3. The data files exist in the `data/` folder

### Problem: "invalid file specification"
**Solution:** Make sure you use forward slashes (/) not backslashes (\) in file paths

### Problem: Results differ slightly from published paper
**Solution:** Minor differences (in the 4th decimal place) can occur due to:
- Different Stata versions
- Different random number generator seeds (if applicable)
- Rounding in intermediate calculations

Differences larger than 0.01 in main coefficients indicate a problem - please contact the author.

---

## Additional Notes

### Interpretation of Standardized Variables
Many variables are expressed in standard deviation units (suffix `_SDUNIT`). To interpret:
- A coefficient of 0.024 on `RADIO_SUBSCRIPTION1946_SDUNIT` means a 1 SD increase in radio exposure increases the outcome by 0.024 units
- Mean radio subscription rate: 37.3%
- SD of radio subscription rate: ~15 percentage points

### Clustering of Standard Errors
All standard errors are clustered at the radio station level (113 stations), accounting for spatial correlation in radio signal strength.

### Analytical Weights in Table 3
Table 3 uses analytical weights because some female candidates ran in multiple districts. The weight `1/n_district_per_candidate` gives equal weight to each candidate while accounting for their presence in multiple districts.

---

## Contact Information

**For questions about the replication package:**

Yoko Okuyama  
Department of Economics, Uppsala University  
Email: yoko.okuyama@nek.uu.se

**For data requests or technical issues:**
Please email with subject line: "Replication Package - JDE 2026"

---

## Version History

- **Version 1.0** (February 2026): Initial release

---

## Terms of Use

This replication package is provided for academic and educational purposes. Users are expected to cite the original paper when using these materials:

```
Okuyama, Y. (2026). Empowering women through radio: Evidence from Occupied Japan. 
Journal of Development Economics, 179, 103620.
```

For any questions about permitted uses or to request access to additional materials, please contact the author.

---

**End of README**
