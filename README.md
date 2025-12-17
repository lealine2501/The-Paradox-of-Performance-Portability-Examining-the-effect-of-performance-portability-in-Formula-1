# The Paradox of Performance Portability: Examining the Effect of Performance Portability in Formula 1

**Author:** Lea Helene Line and Stella Schwertner 
**Institution:** NOVA SBE
**Date:** December 2025

Abstract
This project investigates the concept of "Performance Portability" within the high-stakes environment of Formula 1. Specifically, it examines whether drivers who switch teams ("Movers") achieve a statistically significant performance improvement compared to those who remain with their current teams ("Stayers"). Using historical race data from 1991 to 2024, this study utilizes regression analysis with driver fixed effects to isolate the impact of team switching from innate driver skill and team competitiveness.

The findings challenge the common assumption that lateral moves revitalize careers, suggesting instead that voluntary movers often "tread water," while tenure and stability are stronger predictors of performance variance.

## Data Source
The analysis relies on the comprehensive **Formula 1 World Championship (1950–2020)** dataset, sourced from Kaggle and originally compiled by Rohan Rao.
* **Source:** [Kaggle: Formula 1 World Championship](https://www.kaggle.com/datasets/rohanrao/formula-1-world-championship-1950-2020)
* **Coverage:** 1950 – 2024 (Filtered for this study: 1991–2024)
* **Key Files Used:** `results.csv`, `races.csv`, `drivers.csv`, `constructors.csv`, `constructor_results.csv`

## Methodology

### 1. Data Preprocessing & Lineage Mapping
To ensure accurate longitudinal analysis, the project accounts for the complex history of F1 team ownership changes (e.g., Minardi → Toro Rosso → AlphaTauri → RB).
* **Constructor Lineage:** A custom mapping dictionary aggregates disparate constructor IDs into unified "Lineage IDs" to track teams consistently across eras (e.g., the Enstone team is tracked from Benetton through Renault, Lotus, and Alpine).
* **Teammate Pairing:** A dynamic algorithm identifies teammates for every race entry, allowing for intra-team performance comparisons.
* **Filtering:** The dataset is restricted to the modern era (1991–present) to maintain relevance regarding scoring systems and team structures.

### 2. Statistical Approach
The core analysis utilises Ordinary Least Squares (OLS) regression with high-dimensional fixed effects:
* **Dependent Variable:** Driver Performance (Points per Race).
* **Independent Variables:**
    * `Move_Event`: A binary indicator for drivers who have switched teams.
    * `Tenure`: The number of days a driver has remained with a specific constructor.
* **Controls:**
    * **Driver Fixed Effects:** Controls for unobserved, time-invariant driver skill (e.g., the innate talent difference between a World Champion and a mid-field driver).
    * **Constructor Competitiveness:** Controls for the mechanical advantage of the car.

## Key Findings
* **The "Treading Water" Effect:** The coefficients for voluntary movers suggest that simply shuffling a driver to a new team (often a lateral move) does not yield a statistically significant performance improvement.
* **Value of Stability:** The `tenure_days` variable shows a positive and significant correlation with performance, indicating that familiarity with a team's operations and car philosophy yields tangible lap-time benefits (approx. 1.4 points per race gained per 1,000 days of tenure).
* **Driver Skill Variance:** Driver fixed effects remain highly significant, confirming that innate driver quality persists regardless of the machinery.

## Installation & Usage

### Prerequisites
The project requires Python 3.8+ and the following libraries:
* `pandas`
* `numpy`
* `matplotlib` / `seaborn` (for visualisation)
* `statsmodels` (for regression analysis)
* `kaggle` (for API data fetching)

### Setup
1.  Clone the repository:
    ```bash
    git clone [https://github.com/lealine2501/The-Paradox-of-Performance-Portability-Examining-the-effect-of-performance-portability-in-Formula-1.git](https://github.com/lealine2501/The-Paradox-of-Performance-Portability-Examining-the-effect-of-performance-portability-in-Formula-1.git)
    ```
2.  Install dependencies:
    ```bash
    pip install pandas numpy statsmodels matplotlib kaggle
    ```
3.  **Kaggle API Token:**
    To download the data programmatically, place your `kaggle.json` API token in `~/.kaggle/` or manually download the CSV files into a `/data` folder.

### Running the Analysis
Open the Jupyter Notebook to replicate the findings:
```bash
jupyter notebook "final_notebook.ipynb"
