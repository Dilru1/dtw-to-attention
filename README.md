# Machine Learning for Time Series — ENSAI M2 labs

Lab work and final project from the **Machine Learning for Time Series** course (M2 Smart Data Science, ENSAI, 2025–26), taught by Simon Malinowski (Univ. Rennes / IRISA).

The labs build up the main families of time-series methods, from alignment-based similarity measures to deep sequence models, and compare them on standard UCR/UEA benchmarks (Trace, GunPoint, Plane).

| # | Notebook | Topic | Key methods |
|---|----------|-------|-------------|
| 1 | [`01_dtw.ipynb`](notebooks/01_dtw.ipynb) | Dynamic Time Warping | DTW alignment paths, DTW Barycenter Averaging (DBA), subsequence DTW (motif search in chroma features of an audio recording) |
| 1b | [`01b_dba_animation.ipynb`](notebooks/01b_dba_animation.ipynb) | DBA, visualised | Animated barycenter convergence |
| 2 | [`02_soft_dtw.ipynb`](notebooks/02_soft_dtw.ipynb) | Soft-DTW | Effect of γ on soft alignments, soft-DTW barycenters, gradient descent on a soft-DTW objective |
| 3 | [`03_dtw_in_ml_models.ipynb`](notebooks/03_dtw_in_ml_models.ipynb) | Alignment in classical ML | 1-NN (Euclidean / DTW / Sakoe–Chiba / soft-DTW), SVM with GAK kernel, DTW k-means, MLP forecasting with a soft-DTW loss (PyTorch) |
| 4 | [`04_shapelets_embedding.ipynb`](notebooks/04_shapelets_embedding.ipynb) | Shapelets | Shapelet decision trees, Shapelet Transform (pyts) + SVM, Learning Shapelets (tslearn) |
| 5 | [`05_cnn_rnn.ipynb`](notebooks/05_cnn_rnn.ipynb) | Neural sequence models | SimpleRNN / LSTM / GRU / 1D-CNN; vanishing gradients with long padding |
| 6 | [`06_attention.ipynb`](notebooks/06_attention.ipynb) | Attention | CNN vs. CNN + self-attention on a seq2seq task with long-range dependencies, attention maps, attention classifier on Trace |
| — | [`exam/final_project_plane_dataset.ipynb`](exam/final_project_plane_dataset.ipynb) | Final project | Full comparison of all methods above on the 7-class **Plane** dataset |
| — | [`notes/course_notes.ipynb`](notes/course_notes.ipynb) | Notes | Worked DTW example, shapelet regularisation (Lasso / group Lasso) |

## Selected results

**1-NN with alignment metrics on the Plane dataset (final project, 7 classes, 105 train / 105 test):**

| Metric | Test accuracy |
|---|---|
| Euclidean | 96.2% |
| DTW | 99.0% |
| DTW + Sakoe–Chiba band | 98.1% |
| Soft-DTW | 99.0% |

DTW-based distances correct the small timing offsets between series of the same class that Euclidean distance penalises, at roughly 40× the compute cost.

**Long-range dependencies (Lab 6, seq2seq task, test MSE):** a 5-layer 1D-CNN reaches 0.72; replacing one convolution with a self-attention layer reduces this to 0.026. The CNN's receptive field (about 11 steps) is too short to relate motifs that sit far apart, while attention connects any two time steps directly.

**Vanishing gradients (Lab 5):** a SimpleRNN classifies the toy sine dataset perfectly with short padding, but drops to chance (50%) when the informative part is followed by 50 uninformative steps.

**Lessons from the final project:** with only about 30 series per class, the alignment-based nearest-neighbour methods clearly beat the deep models (RNN/LSTM/GRU/CNN/attention), which underfit or overfit without heavier regularisation or data augmentation.

## Setup

```bash
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
jupyter lab
```

Benchmark datasets (Trace, GunPoint, Plane) are downloaded automatically by `tslearn` / `pyts` on first use. Lab 1's audio-motif exercise needs local feature files; see [`data/README.md`](data/README.md).

The notebooks use both TensorFlow/Keras and PyTorch, as in the course.

## Authors

Dehiwalage Don Dilruwan. The final project was carried out jointly with Peifeng Wang.

Exercise statements are by the course instructor (Simon Malinowski). Solutions and analysis are the authors' own. Course slides are not redistributed here.
