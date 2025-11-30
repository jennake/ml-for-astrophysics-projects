# Project 2 — Low-Dimensional Galaxy Photometry & Photometric Redshift Estimation

This project explored two major tasks in machine learning for astrophysics:  
(1) reducing high-dimensional galaxy photometric data into meaningful low-dimensional representations, and  
(2) training and evaluating a basic model to estimate photometric redshifts.

All analysis, results, and plots are based on the provided SDSS-like feature tables and target redshift values.  
:contentReference[oaicite:0]{index=0}

---

## 🚀 Overview

### **Question 1 — Dimensionality Reduction of Galaxy Photometry**

You began by loading galaxy feature tables and targets:  
- **3816 galaxies × 25 features** for the photometry matrix  
- **3816 targets** for redshift or class labels  


You then applied the following dimensionality reduction methods:

- **PCA (Principal Component Analysis)**  
  - Performed both **without** and **with normalization**  
  - Visualized 3-component PCA projections  
  - Analyzed cluster structure and scaling effects  
  - Interpreted clusters as likely corresponding to galaxy types or redshift/distance differences  
      

- **t-SNE (t-Stochastic Neighbor Embedding)**  
  - Used perplexities **2**, **10**, and **100**  
  - Showed how perplexity affects cluster separability  
    - Low perplexity → noisy, many micro-clusters  
    - Intermediate perplexity → clear, interpretable groupings  
    - High perplexity → mixing of clusters, poorer separability  
    

- **PCA Variance Analysis**  
  - Compared variance scales with and without standardization  
  - Highlighted that normalization makes PCA axes comparable and interpretable  
    

---

## 🔭 **Question 2 — Estimating Photometric Redshifts**

### **Data Preparation**
You reloaded the target and feature tables, then reshaped and normalized them for modeling.  


You performed a **train/test split** (70%/30%) using scikit-learn.  


---

## 🤖 **Modeling & Training**

You built a basic regression model (likely linear or shallow network) to predict redshift values.  
Key findings:

- **Overfitting was observed**  
  - Training loss continued decreasing  
  - Test loss plateaued  
  - Model failed to generalize  
  

- **Model performance was poor**  
  - Weights initially were not updating  
  - Final model showed little loss improvement  
  - Predictions were widely scattered relative to the truth  
  

---

## 📈 Key Results & Interpretation

### PCA  
- Without normalization → axes dominated by large-scale features, obscuring structure.  
- With normalization → balanced axes, clearer cluster structure, easier component interpretation.  
  

### t-SNE  
- Perplexity controls cluster granularity.  
- Perplexity = 10 produced the most interpretable structure for this dataset.

### Photometric Redshift Model  
- Exhibited overfitting and poor accuracy.  
- Highlighted the importance of normalization, feature engineering, and better model selection.

---

## 🧠 Skills Demonstrated
- Data handling with pandas  
- PCA and t-SNE for high-dimensional astrophysical data  
- Train/test splitting and model evaluation  
- Interpreting astronomical data structure through ML embeddings  
- Diagnosing overfitting and training instability

---

