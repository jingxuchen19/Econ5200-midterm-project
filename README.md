# Econ 5200 Midterm Project  
## Replication Study: Card & Krueger (1994)

### Project Overview
This project replicates the seminal study:

> Card, D., & Krueger, A. B. (1994).  
> *Minimum Wages and Employment: A Case Study of the Fast-Food Industry in New Jersey and Pennsylvania.*  
> American Economic Review.

Paper link: https://davidcard.berkeley.edu/papers/njmin-aer.pdf

In April 1992, New Jersey raised its minimum wage from $4.25 to $5.05, while Pennsylvania kept its rate unchanged. The authors surveyed about 400 fast-food restaurants in both states before and after the change to see if the higher minimum wage led to job losses. They found no evidence of a decline in employment in New Jersey following the minimum wage increase.

The goal of this replication is to reconstruct the original Difference-in-Differences (DiD) design using the publicly available dataset, reproduce the core employment results, and extend the analysis with Heterogeneous Treatment Effects.

---

## Data Source
The data were obtained from the publicly released files made available by David Card:

- `public.dat`
- `survey1.nj`
- `survey2.nj`
- `codebook`
- `read.me`

These original files are stored in: `/data/raw`

The raw data are treated as immutable and are never modified directly.  
All cleaning and transformations are performed through scripts, and outputs are saved separately in the processed folder.

---

## Repository Structure

Econ5200-midterm-project/
├── README.md  
├── .gitignore  
├── data/  
│   ├── raw/  
│   │   ├── public.dat  
│   │   ├── survey1.nj  
│   │   ├── survey2.nj  
│   │   ├── codebook  
│   │   └── read.me  
│   └── processed/  
├── notebooks/  
│   ├── 01_Data_Cleaning.ipynb  
│   ├── 02_Replication_Analysis.ipynb  
│   └── 03_Extension_and_Results.ipynb  

---

## Phase 1: Data Cleaning
- Read the fixed-width `public.dat` file using column specifications from the codebook.
- Parsed all 46 variables across 410 store observations.
- Handled missing values encoded as `.` in the original data.

## Phase 2: Replication Analysis
- Constructed FTE (Full-Time Equivalent) employment: FTE = full-time + managers + 0.5 × part-time.
- Reproduced descriptive statistics matching Table 2 of the original paper.
- Calculated the Difference-in-Differences estimate by hand: DID = +2.76 FTE employees.
- Implemented the DID regression in long format: `FTE ~ STATE * POST`.
- Applied clustered standard errors at the store level, matching the paper's methodology.
- Key finding: The minimum wage increase did not reduce employment. The DID estimate of +2.76 is consistent with the original paper.

## Phase 3: Extension — Heterogeneous Treatment Effects
- **Pathway chosen:** Pathway 2 (Heterogeneous Treatment Effects)
- **Research question:** Does the minimum wage effect differ across fast-food chain types and ownership structures?
- **Method:** Ran separate DID regressions for each chain (Burger King, KFC, Roy Rogers, Wendy's) and by ownership status (company-owned vs. franchise-owned), all with clustered standard errors.
- **Robustness check:** Estimated full interaction models (`FTE ~ STATE * POST * C(CHAIN)`) with and without CO_OWNED as a control variable. Results were stable across specifications.
- **Key findings:**
  - Burger King showed the largest positive effect (+4.67 FTE).
  - KFC was the only chain with a negative effect (-1.35 FTE).
  - Franchise-owned stores showed a slightly larger effect (+3.27) than company-owned stores (+2.32).
  - None of the subgroup estimates were statistically significant at the 5% level, likely due to small sample sizes when splitting by group.
- **Visualization:** A forest plot displaying DID estimates and 95% confidence intervals by chain type and ownership status.
- **AI tools used:** Claude (Anthropic) was used as a pair-programmer for coding assistance, visualization, and debugging. All output was reviewed and validated manually.

---

## Replication Plan (Completed)
1. ✅ Clean and structure the raw survey data.
2. ✅ Construct employment measures consistent with the original paper.
3. ✅ Implement the Difference-in-Differences (DiD) design.
4. ✅ Compare results to the published estimates.
5. ✅ Extend the analysis with Heterogeneous Treatment Effects by chain type and ownership status.

This project follows a reproducible research workflow, maintaining a clear separation between raw data, processed outputs, and analytical notebooks to ensure transparency and version control.
