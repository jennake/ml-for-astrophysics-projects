# Mini Project 3 – Autoencoders & Unsupervised Clustering of SDSS Spectra

This mini project explores **representation learning** and **unsupervised clustering** on Sloan Digital Sky Survey (SDSS) spectra. The workflow is:

1. Train a fully connected **autoencoder** on galaxy, star, and quasar spectra.
2. Use the learned **latent space** to perform **unsupervised clustering** and visualize the structure of the data.

---

## Project Structure

This project lives in the `Pset3/` folder:

- `MiniProject3.html` – Part 1: building and training an autoencoder on SDSS spectra (representation learning).
- `MiniProject3P2.html` – Part 2: clustering in latent space with K-Means / DBSCAN + t-SNE visualisation.

> Note: These HTML files are exports of the original Jupyter notebooks used for the class.

---

## Data

- Input data: `pset3-1.npz`  
  - `features`: SDSS spectra (flux as a function of wavelength) for multiple objects.  
  - `labels`: integer class labels (1 = stars, 2 = galaxies, 3 = quasars).

- Encoded data (for Part 2): `pset3-2-if-needed.npz`  
  - `encodings`: low-dimensional latent vectors from a trained autoencoder.  
  - `labels`: true class labels for evaluation.

---

## Methods

### 1. Autoencoder for SDSS spectra (Part 1)

**Goal:** Learn a compact representation of SDSS spectra that can reconstruct the original flux distribution.

Steps:

1. **Preprocessing**
   - Load spectra and labels from `pset3-1.npz`.
   - Normalise the spectral features and convert them to PyTorch tensors.
   - Split into training and test sets and wrap in `DataLoader`s.

2. **Network architecture**
   - A fully connected autoencoder defined in PyTorch:
     - Input size = number of wavelength bins (dimensionality of the spectra).
     - Latent size ≈ 5 (bottleneck).
     - One or more hidden layers with ~100 neurons and non-linear activations.
   - Trained with a reconstruction loss (e.g., mean squared error) to reproduce the input spectrum at the output.

3. **Training & inspection**
   - Train the autoencoder on the training set; monitor loss over epochs.
   - Extract latent vectors for each spectrum and plot them (or 2D projections) to look for structure or clustering by class.

**Key idea:** If the autoencoder learns a meaningful representation, objects with similar spectra (e.g., same class) should be closer together in latent space.

---

### 2. Clustering in Latent Space (Part 2)

**Goal:** Use the compressed representations to perform unsupervised clustering and compare to the true SDSS labels.

1. **Load pre-computed encodings**
   - Load `encodings` and `labels` from `pset3-2-if-needed.npz`.
   - Each spectrum is represented by a 5-dimensional latent vector.

2. **K-Means clustering**
   - Apply `KMeans` with `n_clusters = 3` to the latent vectors.
   - Compute a confusion matrix between:
     - true labels (stars/galaxies/quasars), and
     - cluster assignments from K-Means.
   - Visualise clustering in 2D:
     - Option 1: plot two latent dimensions directly.
     - Option 2: apply **t-SNE** to reduce from 5D → 2D, then plot points coloured by cluster.

3. **DBSCAN / density-based clustering (if used)**
   - Experiment with DBSCAN on the latent vectors, tuning parameters such as `eps`.
   - Evaluate clusters with a confusion matrix and track:
     - number of clusters,
     - number of outliers,
     - classification accuracy in terms of how well clusters map to true labels.

4. **Evaluation & discussion**
   - Inspect whether stars, galaxies, and quasars separate cleanly in latent space.
   - Discuss limitations:
     - K-Means assumes spherical, balanced clusters.
     - Latent space may not fully disentangle physical classes.
     - Some methods yield very low accuracy and overlapping clusters, indicating that unsupervised clustering struggles to recover the three object types perfectly from spectra alone.

---

## Results (High-Level)

- The autoencoder successfully compresses high-dimensional spectra into a low-dimensional latent space while roughly preserving spectral structure.
- Latent-space visualisations show some **hints of clustering**, but the separation between stars, galaxies and quasars is not clean.
- K-Means and DBSCAN can find clusters, but:
  - Cluster purity is low,
  - Confusion matrices show significant mixing between classes,
  - Overall accuracy remains poor, demonstrating the challenge of fully unsupervised classification even with a learned spectral representation.

---

## Skills & Tools

- **Python**, **NumPy**, **Matplotlib**
- **PyTorch**: fully connected autoencoder, `DataLoader` API
- **Scikit-learn**: `KMeans`, `TSNE`, `confusion_matrix`, clustering evaluation
- Representation learning, dimensionality reduction, unsupervised clustering, and evaluation on real astrophysical data (SDSS spectra).

---

## How to View

To view the project in this repository:

```bash
cd ml-for-astrophysics-projects/Pset3
# Open the HTML notebooks in your browser
open MiniProject3.html
open MiniProject3P2.html

