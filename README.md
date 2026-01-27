# STOP_Speech

# Extended High-Frequency Hearing Loss, Cochlear Synaptopathy, and Speech-in-Noise

This repository contains the R code used to analyse data from the STOP study on the relationship between extended high-frequency (eHF) hearing loss, peripheral nerve conduction velocity (ABR Wave I latency), cochlear neural synchrony (ABR Wave I amplitude), and speech-in-noise perception (word and phoneme scores).

## Project info

- Title: Extended high-frequency hearing loss and peripheral nerve conduction velocity predict speech-in-noise; cochlear synaptopathy does not
- Principal Investigator: Christopher R. Cederroth
- Organization: Translational Audiology Lab, Karolinska Institutet
- Contact: [christopher.cederroth@ki.se](mailto:christopher.cederroth@ki.se)

## Aim of the project

The overall aim is to disentangle the contributions of eHF hearing loss, peripheral nerve conduction velocity, and putative cochlear synaptopathy to speech perception in noise in normally hearing and age-stratified adults. We quantify how age, audiometric thresholds, OAEs, and ABR waveforms relate to word scores (WS) and phoneme scores (PS). 

## Overview of analysis

The analysis proceeds in four main phases:

1. **Data cleaning and derivation of core measures**
   - Import STOP speech-ABR data and harmonize variable names.
   - Compute audiometric summary measures (PTA4, PTAHF), OAE SNR, and speech scores (WS, PS).
   - Derive ABR metrics (Wave I amplitude, Waves I/III/V absolute latencies, I–V inter-wave interval).
   - All numeric variables are mean-centered for interpretability.
   - Save a cleaned analysis dataset (`STOPspeechABR_cleanv2.csv` or equivalent).

2. **Descriptive audiometry and age-related trajectories (Figures 2–3, Supplementary Tables S1–S6)**
   - Generate age-, sex-, and eHF-stratified audiometric/OAE/ABR summaries (Supplementary Tables S1–S4).
   - Fit polynomial models (linear, quadratic, cubic) of **Age → audiometric, OAE, speech, and ABR variables** using **likelihood ratio testing (LRT)** with Bonferroni correction to identify optimal polynomial fits (Supplementary Table S5).
   - Extend to **Age × Sex** interaction models for speech outcomes to test for gender-dependent aging (Supplementary Table S6).
   - Use best-fitting polynomial models to plot age trajectories across all auditory variables (Figure 3).
   - **Key finding:** eHF thresholds decline linearly with age (R²=0.641), explaining 64% of age-related variance—far exceeding conventional audiometry (R²=0.158).

3. **Univariate associations with speech perception (Figure 4, Supplementary Table S7)**
   - Compute polynomial regressions of **WS and PS** on each auditory predictor individually (PTA4, PTAHF, OAE, ABR latencies and amplitude).
   - Identify optimal polynomial fits via **likelihood ratio testing (LRT)** with Bonferroni correction.
   - Visualize univariate relationships and quantify R² for each predictor (Supplementary Table S7).
   - **Key findings:** 
     - eHF (R²=0.34–0.36) outperforms conventional PTA (R²=0.22–0.25) by 12+ percentage points
     - W1.Latency shows modest univariate association (R²=0.11–0.13)
     - W1.Amplitude shows minimal association (R²=0.05–0.13)

4. **Multivariable speech models and interaction analyses (Figure 5, Supplementary Tables S8–S12)**
   - Fit stepwise multivariable models predicting WS and PS using **likelihood ratio testing (LRT)** to compare nested models:
     - **Phase 0:** Age + Age² + Sex (baseline demographics)
     - **Phase 1:** Add hearing loss terms (PTA4, PTA4², PTAHF, PTAHF², PTAHF³, OAE, OAE², OAE³)
     - **Phase 2:** Add polynomial ABR terms (W1.Amplitude, W3.Latency³, W5.Latency)
     - **Phase 3 (FINAL):** Full model including Age × W1.Latency and Age × W1.Amplitude interactions
   
   - Final Phase 3 model includes **19 predictors** controlling for:
     - Demographics: Age, Age², Sex
     - Conventional + extended audiometry: PTA4, PTA4², PTAHF, PTAHF², PTAHF³
     - Cochlear outer hair cell function: OAE, OAE², OAE³
     - Peripheral neural timing: W1.Latency, Age×W1.Latency
     - Peripheral neural synchrony: W1.Amplitude, Age×W1.Amplitude
     - Central auditory processing: W3.Latency, W3.Latency², W3.Latency³, W5.Latency

   - **Model performance (Phase 3):**
     - WS: R²=0.363
     - PS: R²=0.418

   - Summarize final model coefficients with HC3 robust standard errors and 95% CIs (Supplementary Table S8).
   - Quantify incremental contribution of hearing loss, neural measures, and interactions via R² change and **likelihood ratio tests (LRT)** across phases (Supplementary Table S9).
   - Extract key predictors for forest-plot visualization ordered by mechanistic hierarchy (Figure 5b, Supplementary Table S10):
     * W3.Latency³ (central processing)
     * Age × W1.Latency (age-amplified peripheral timing)
     * W1.Latency (peripheral timing main effect)
     * Age × W1.Amplitude (age × synchrony interaction)
     * W1.Amplitude (peripheral synchrony/synaptopathy)
     * Age² (non-linear aging effect)
   
   - Generate age- and latency-stratified predicted WS/PS trajectories demonstrating the Age × W1.Latency interaction (Figure 5c, Supplementary Table S11):
     * 45-year-olds show minimal WS decline across W1.Latency range
     * 75-year-olds show 13-percentage-point WS decline vs 5-point PS decline at maximum W1.Latency
     * **2.6× greater vulnerability for word vs phoneme recognition**
   
   - Perform age-stratified WS–PS coupling analyses (Young vs Old), including Pearson correlations and regression slopes (Figure 5d, Supplementary Table S12):
     * Young adults (median age 38): tight upper-right cluster (WS=78, PS=91), slope=0.83
     * Older adults (median age 53): greater scatter, lower-left region (WS=74, PS=88), slope=0.68
     * **Selective word score vulnerability with age despite high overall correlation (r=0.934)**
