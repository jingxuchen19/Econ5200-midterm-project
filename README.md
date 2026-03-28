# Econ 5200 Midterm Project  
## Replication Study: Card & Krueger (1994)

---

## Executive Memo

### The Bottom Line

In 1992, New Jersey raised the minimum wage for fast-food workers from $4.25 to $5.05 per hour, while neighboring Pennsylvania kept its rate unchanged. **Our analysis of 410 fast-food restaurants found no evidence that the wage increase led to job losses — in fact, employment in New Jersey grew slightly relative to Pennsylvania.** When we looked deeper at individual restaurant chains, we found that this effect was not the same everywhere: Burger King locations saw the biggest employment gains, while KFC locations were the only ones that experienced a slight decline.

### How We Tested This

Imagine you want to know if a new store policy affects sales. You can't just look at stores that adopted the policy, because other things (like seasonality or local economy) might also be changing. Instead, you compare stores that adopted the policy to similar stores that didn't, and you look at how both groups changed over time. If the policy stores improved more than the comparison stores, you can attribute that difference to the policy.

That's exactly what we did here. New Jersey restaurants were the "policy group" (they had to raise wages), and Pennsylvania restaurants were the "comparison group" (nothing changed for them). We surveyed both groups before and after the wage increase and compared how employment changed. This approach — called Difference-in-Differences — effectively simulates a controlled experiment using real-world data.

### The Visual Evidence

The chart below shows how the minimum wage increase affected employment at different types of fast-food restaurants. Each dot represents the estimated change in full-time equivalent (FTE) employees, and the horizontal lines show the range of uncertainty (95% confidence intervals). The red dashed line at zero represents "no effect." Dots to the right of zero mean employment increased; dots to the left mean it decreased.

![Forest Plot: Heterogeneous Treatment Effects by Chain Type and Ownership Status](forest_plot.png)

**Key takeaways from the chart:**
- Burger King saw the largest employment increase (+4.67 FTE workers per store)
- KFC was the only chain where employment slightly declined (-1.35 FTE)
- Franchise-owned stores showed a larger positive effect (+3.27) than company-owned stores (+2.32)
- The overall average effect across all stores was positive (+2.76)
- The wide confidence intervals reflect small sample sizes when splitting by group, meaning we should interpret individual chain results with caution

### Policy Implications

Based on these findings, we recommend the following for policymakers and business leaders:

1. **Minimum wage increases do not automatically lead to job losses.** The evidence from New Jersey's fast-food industry shows that moderate wage increases can be absorbed without reducing overall employment. Policymakers considering minimum wage legislation should not assume that higher wages will necessarily result in layoffs.

2. **The impact varies by business type.** Smaller chains like KFC may be more sensitive to wage increases than larger ones like Burger King. Policymakers should consider providing targeted support (such as tax credits or phased implementation) for smaller or more vulnerable businesses during wage transitions.

3. **Business leaders should focus on adaptation rather than headcount reduction.** The data suggests that most restaurants adjusted to higher wages through other channels — such as modest price increases — rather than cutting staff. Companies facing wage increases should explore pricing strategies and operational efficiencies before resorting to layoffs.

---

## Project Overview

This project replicates the seminal study:

> Card, D., & Krueger, A. B. (1994).  
> *Minimum Wages and Employment: A Case Study of the Fast-Food Industry in New Jersey and Pennsylvania.*  
> American Economic Review.

Paper link: https://davidcard.berkeley.edu/papers/njmin-aer.pdf

In April 1992, New Jersey raised its minimum wage from $4.25 to $5.05, while Pennsylvania kept its rate unchanged. The authors surveyed about 400 fast-food restaurants in both states before and after the change to see if the higher minimum wage led to job losses. They found no evidence of a decline in employment in New Jersey following the minimum wage increase.

---

## Data Source

The data were obtained from the publicly released files made available by David Card:

- public.dat
- survey1.nj
- survey2.nj
- codebook
- read.me

These original files are stored in: /data/raw

The raw data are treated as immutable and are never modified directly. All cleaning and transformations are performed through scripts, and outputs are saved separately in the processed folder.

---

## Repository Structure

- **README.md** — Project overview and Executive Memo
- **.gitignore** — Git ignore rules
- **requirements.txt** — Python dependencies
- **forest_plot.png** — Main visualization
- **data/**
  - **raw/** — Original untouched data files (public.dat, survey1.nj, survey2.nj, codebook, read.me)
  - **processed/** — Cleaned data outputs
- **notebooks/**
  - **01_Data_Cleaning.ipynb** — Phase 1: Data ingestion and cleaning
  - **02_Replication_Analysis.ipynb** — Phase 2: DID replication
  - **03_Extension_and_Results.ipynb** — Phase 3: HTE extension and visualization

---

## Phase 1: Data Cleaning
- Read the fixed-width public.dat file using column specifications from the codebook.
- Parsed all 46 variables across 410 store observations.
- Handled missing values encoded as "." in the original data.

## Phase 2: Replication Analysis
- Constructed FTE (Full-Time Equivalent) employment: FTE = full-time + managers + 0.5 × part-time.
- Reproduced descriptive statistics matching Table 2 of the original paper.
- Calculated the Difference-in-Differences estimate by hand: DID = +2.76 FTE employees.
- Implemented the DID regression in long format: FTE ~ STATE * POST.
- Applied clustered standard errors at the store level, matching the paper's methodology.
- Key finding: The minimum wage increase did not reduce employment.

## Phase 3: Extension — Heterogeneous Treatment Effects
- **Pathway chosen:** Pathway 2 (Heterogeneous Treatment Effects)
- **Research question:** Does the minimum wage effect differ across fast-food chain types and ownership structures?
- **Method:** Ran separate DID regressions for each chain (Burger King, KFC, Roy Rogers, Wendy's) and by ownership status (company-owned vs. franchise-owned), all with clustered standard errors.
- **Robustness check:** Estimated full interaction models with and without CO_OWNED as a control variable. Results were stable across specifications.
- **Key findings:**
  - Burger King showed the largest positive effect (+4.67 FTE)
  - KFC was the only chain with a negative effect (-1.35 FTE)
  - Franchise-owned stores showed a slightly larger effect (+3.27) than company-owned stores (+2.32)
  - None of the subgroup estimates were statistically significant at the 5% level due to small sample sizes
- **AI tools used:** Claude (Anthropic) was used in Phase 3 to assist with the HTE extension analysis, visualization code, and debugging.
