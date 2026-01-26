# STOP_Speech

# STOP_Speech: Extended High-Frequency Hearing Loss, Synaptopathy, and Speech-in-Noise

This repository contains the R code used to analyse data from the STOP study on the relationship between extended high-frequency (eHF) hearing loss, cochlear synaptopathy (ABR), and speech-in-noise perception (word and phoneme scores).

## Project info

- Title: Extended high-frequency hearing loss vs synaptopathy predicting speech
- Principal Investigator: Christopher R. Cederroth
- Organization: Translational Audiology Lab
- Contact: christopher.cederroth@ki.se

## Aim of the project

The overall aim is to disentangle the contributions of eHF hearing loss and putative cochlear synaptopathy to speech perception in noise in normally hearing adults. We quantify how age, audiometric thresholds, OAEs, and ABR waveforms relate to word scores (WS) and phoneme scores (PS), and test whether neural timing and amplitude provide additional explanatory power beyond hearing loss alone.

## Overview of analysis

The analysis proceeds in four main phases:

1. **Data cleaning and derivation of core measures**
   - Import STOP speech-ABR data and harmonize variable names.
   - Compute audiometric summary measures (PTA4, PTAHF), OAE SNR, and speech scores (WS, PS).
   - Derive ABR metrics (Wave I amplitude, Waves I/III/V absolute latencies, I–V inter-wave interval).
   - Save a cleaned analysis dataset (`data_clean.rds` or equivalent).

2. **Descriptive audiometry and age-related trajectories (Figures 2–3)**
   - Generate age-, sex-, and eHF-stratified audiometric/OAE/ABR summaries (Supplementary Tables S1–S4).
   - Fit AIC-based polynomial models of **Age → audiometric, OAE, speech, and ABR variables** to quantify age trajectories (Supplementary Table S5).
   - Extend to **Age × Sex** models for speech outcomes (Supplementary Table S6).
   - Use best-fitting polynomial models to plot age trajectories across all auditory variables (Figure 3).

3. **Univariate associations with speech perception (Figure 4)**
   - Compute AIC-based polynomial regressions of **WS and PS** on each auditory predictor (PTA4, PTAHF, OAE, ABR latencies and amplitude) (Supplementary Table S7).
   - Visualize these univariate relationships as correlation plots and scatter/curve overlays (Figure 4, plus OAE–speech supplementary figure).

4. **Multivariable speech models and interaction analyses (Figure 5, Tables S8–S12)**
   - Fit stepwise multivariable models predicting WS and PS:
     - Phase 0: Age + Sex (baseline).
     - Phase 1: Add hearing loss (PTA4, PTAHF, OAE).
     - Phase 2: Add polynomial terms for hearing loss and key neural measures (e.g. W1 amplitude, W3 latency).
     - Phase 3: Full model including Age × W1 latency and Age × W1 amplitude interactions.
   - Summarize final model coefficients with HC3 robust SEs and 95% CIs (Supplementary Table S8).
   - Quantify incremental contribution of hearing loss and neural metrics via R², AIC, and likelihood ratio tests across phases (Supplementary Table S9).
   - Extract a compact set of key predictors for forest-plot visualization (Figure 5b, Supplementary Table S10).
   - Generate age- and latency-stratified predicted WS/PS trajectories for the Age × W1 latency interaction (Figure 5c, Supplementary Table S11).
   - Perform age-stratified WS–PS coupling analyses (Young vs Old), including correlations and regression slopes (Figure 5d, Supplementary Table S12).

## File structure

Suggested structure (mirroring the organisation used in `STOP_bloodscreen`):

- `README.md` – This document.
- `data/`  
  - (Not included here) Raw/cleaned STOP speech-ABR data; users should place their own data files here following the expected format.
- `R/`  
  - `01_data_cleaning.R` – Data import, cleaning, and derivation of analysis variables.
  - `02_tables_figure2.R` – Descriptive tables and summaries for Figures 1–2 and Supplementary Tables S1–S4.
  - `03_tables_figure3.R` – Age and Age × Sex models and age trajectories (Supplementary Tables S5–S6, Figure 3).
  - `04_tables_figure4.R` – Univariate polynomial regressions and correlation outputs (Supplementary Table S7, Figure 4).
  - `05_figure5_tables_s8-s12.R` – Multivariable models, interaction analyses, and extraction of Tables S8–S12.
  - `06_table_s12_age_stratified.R` – Stand-alone script for age-stratified WS–PS analysis (Table S12).
  - `07_figure5_publication.R` – Publication-ready Figure 5.
- `output/`  
  - `SuppTable5_Age_effects.csv` – Age trajectories (Table S5).
  - `SuppTable7_Univariate_Correlations.csv` – Univariate WS/PS vs auditory measures (Table S7).
  - `SuppTable8_Final_Model_Coefficients.csv` – Final WS/PS multivariable coefficients (Table S8).
  - `SuppTable9_Model_Progression_Hearing_Loss.csv` – Model progression (Table S9).
  - `SuppTable10_Forest_Plot_Data.csv` – Forest plot predictors (Table S10).
  - `SuppTable11_Interaction_Trajectories.csv` – Age × W1 latency predicted trajectories (Table S11).
  - `SuppTable12_Age_Stratified_Analysis.csv` – Age-stratified WS–PS coupling (Table S12).
  - Figure files (`Figure3_*.pdf`, `Figure4_*.pdf`, `Figure5_*.pdf`, supplementary figures).

Adjust file names to match exactly those used in this repository.

## How to run the analysis

1. Clone this repository:
   ```bash
   git clone https://github.com/translational-audiology-lab/STOP_Speech.git
   cd STOP_Speech
