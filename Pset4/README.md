# Project 4 — Classifying Stellar Flares Using Feature Engineering & Random Forests

This project focuses on identifying stellar flares from light-curve data using a combination of **physically motivated features**, **PCA**, **Fourier decomposition**, and a **Random Forest classifier**.  
:contentReference[oaicite:0]{index=0}

---

## 🚀 Overview

Stellar flares produce rapid, asymmetric flux increases in light curves, whereas non-flaring curves are relatively flat. In this project, you:

- Visually compared flare vs non-flare light curves  
- Discussed biases in traditional flare-detection pipelines  
- Engineered several feature sets (PCA, Fourier, and hand-crafted)  
- Combined all features into a 10-dimensional feature matrix  
- Trained a **Random Forest** model to classify flares from non-flares  

---

## ✨ Data & Motivation

Light curves contain temporal flux measurements. Flares typically show:

- A sharp rise  
- Fast decay  
- Large amplitude relative to baseline  

Non-flare curves show minimal structure.  
:contentReference[oaicite:1]{index=1}

Traditional flare detection uses detrending or flux-thresholding, but these methods:

- Miss small flares  
- Mislabel stellar variability as flares  
- Introduce selection bias towards **large**, high-contrast events  
:contentReference[oaicite:2]{index=2}

---

## 🧮 Feature Engineering

You generated three key groups of features:

### **1. PCA Features (3 components)**
Low-dimensional representations of light curves capturing global shapes.

### **2. Fourier Features (3 components)**
Frequency-domain representations capturing periodicity or variability.

### **3. Hand-Engineered Physical Features (4 components)**  
Based on domain knowledge of flare morphology:  
:contentReference[oaicite:3]{index=3}

- **Mean peak flux** — average brightness around the flare peak  
- **Mean edge flux** — baseline flux far from the peak  
- **Flux ratio** — center vs edge brightness  
- **Asymmetry** — comparing left vs right halves of the flare:

```python
asymmetry = (rpeak - lpeak) / (rpeak + lpeak + 1e-10)

