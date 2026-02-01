# Methodology: China Macro Quant Verification Engine

## 1. Project Objective
This engine serves as a quantitative "reality check" for sell-side macroeconomic forecasts (specifically focusing on the Goldman Sachs 2026 China Outlook). The goal is to identify **Variant Perception**—areas where empirical data suggests a divergence from the consensus narrative of a seamless structural pivot.

---

## 2. Core Analytic Frameworks

### A. Transmission Decay & Lead-Lag Modeling
We model the "Fiscal Fuse" and "Credit Impulse" not as static numbers, but as time-dependent signals.

* **The Mechanism:** We utilize a Lead-Lag Cross-Correlation Matrix to track how Total Social Financing (TSF) and Government Bond Issuance translate into Industrial Value Added (IVA) and PPI.
* **The Quantitative "Machine":** $$\Delta IVA_t = \alpha + \sum_{k=1}^{12} \beta_k \Delta TSF_{t-k} + \epsilon$$
* **Variant Perception:** Our engine detects a **Multiplier Compression**—the $\beta$ coefficients for the 2024-2025 cycle are significantly lower than the 2018-2021 mean, indicating "clogged" transmission.

### B. Property Stabilization Matrix (Dispersion Analysis)
Instead of looking at a national average (which is skewed by Tier-1 cities), we analyze the 70-City Housing Price Index through a distribution lens.

* **Metric:** We calculate the **MAD (Median Absolute Deviation)** and **Tail Risk Shares**.
* **The Signal:** We identify "Stabilization" only when the **Breadth Share** (cities with YoY $\ge$ 100) crosses a critical threshold.
* **Insight:** Current data shows "Stabilization without a Cycle"—a narrow recovery in Tier-1/2 that fails to lift the national "Left Tail."

### C. Paradigm Shift Index (Structural Transition)
To verify the "New Engine" narrative, we built a composite index comparing Fixed Asset Investment (FAI) in High-Tech sectors vs. Legacy Manufacturing.

* **Components:** (Computers, Electronics, Semiconductors) vs. (General Equipment, Automotive).
* **Normalization:** Data is Z-scored ($Z = \frac{x - \mu}{\sigma}$) and Winsorized at the 1st/99th percentile to remove outliers caused by post-pandemic base effects.

---

## 3. Data Pipeline & Integrity
* **Sourcing:** Raw data is programmatically ingested from `data.xlsx`, sourced from the **National Bureau of Statistics (NBS)**, **PBoC**, and **General Administration of Customs (GAC)**.
* **Preprocessing:** * **Seasonality:** We use a custom `merge_jan_feb` logic to handle the Lunar New Year distortion in Chinese economic data.
    * **Real vs. Nominal:** Export data is decomposed into volume and price effects using PPI-proxy deflators to identify if growth is driven by demand or "dumping" (overcapacity).

---

## 4. Forecasting & Scenario Analysis

### Monte Carlo Nowcasting
We do not produce a single GDP point estimate. We run a **Monte Carlo Simulation** (10,000 iterations) based on our lead-lag residuals to produce a probability distribution.

* **P50 (Baseline):** 4.52%
* **P90 (Consensus/GS):** 4.80%
* **Interpretation:** The Goldman Sachs target sits at the extreme right tail of our distribution, implying the market is pricing in a "perfect" policy transmission.

---

## 5. Investment Implications: The "So What?"

* **The Machine Thinking:** The credit multiplier is decaying because the transmission is **state-dependent on property collateral values**. As home prices stagnate, the private sector becomes interest-rate insensitive, making traditional easing less effective.
* **Trade Expressions:** * **Long 10Y CGB:** Underperformance in GDP will force the PBoC into a more aggressive "Reaction Function."
    * **Short CNY:** The exchange rate will act as the primary macro shock absorber in a regime of clogged domestic transmission.

---

## 6. Limitations & Future Work
* **Shadow Banking:** Current TSF data may under-report localized credit contractions.
* **Geopolitics:** The model assumes a "steady state" for tariffs; a "Trump 2.0" shock would require a manual shift in the External Demand proxy weights in `config.yaml`.
