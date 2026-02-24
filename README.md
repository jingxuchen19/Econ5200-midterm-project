# Econ 5200 Midterm Project  
## Replication Study: Card & Krueger (1994)

### Project Overview

This project replicates the seminal study:

> Card, D., & Krueger, A. B. (1994).  
> *Minimum Wages and Employment: A Case Study of the Fast-Food Industry in New Jersey and Pennsylvania.*  
> American Economic Review.

The goal of this replication is to reconstruct the original Difference-in-Differences (DiD) design using the publicly available dataset and reproduce the core employment results.

---

## Data Source

The data were obtained from the publicly released files made available by David Card:

- `public.dat`
- `survey1.nj`
- `survey2.nj`
- `codebook`
- `read.me`

These original files are stored in:
`/data/raw`

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
│   └── 02_Replication.ipynb  

---

## Replication Plan

1. Clean and structure the raw survey data.
2. Construct employment measures consistent with the original paper.
3. Implement the Difference-in-Differences (DiD) design.
4. Compare results to the published estimates.

This project follows a reproducible research workflow with clear separation between raw data, processed outputs, and analytical notebooks.
