# Image Recognition Pipeline

An image classification pipeline built and evaluated on Tiny ImageNet, combining classical feature extraction with a learned autoencoder to improve recognition performance under limited training data.

## Key Results

- Improved model recall by 56% and F1 score by 20% by integrating ORB feature extraction with an Autoencoder-based approach
- Trained on 64x64 pixel images using only a 5% training split, evaluated against the full test split — demonstrating strong generalization under limited data conditions
- Benchmarked across all 200 Tiny ImageNet classes using confusion matrices and F1 comparisons to validate each iteration

## Approach

1. **Feature Extraction** — ORB (Oriented FAST and Rotated BRIEF) keypoint descriptors extracted from each image as a lightweight, classical feature representation
2. **Autoencoder** — learned latent representations trained to capture structure beyond hand-crafted features, especially useful given the small training split
3. **Classification** — combined feature representations used to classify images across 200 classes
4. **Evaluation** — confusion matrices and F1 score comparisons used to benchmark each iteration and confirm generalization rather than overfitting to the small training set

## Tech Stack

- Python
- OpenCV (ORB feature extraction)
- PyTorch (Autoencoder) — [update if you used TensorFlow/Keras instead]
- scikit-learn (confusion matrix, F1 score, evaluation metrics)
- Tiny ImageNet dataset (200 classes, 64x64 images)

## Setup

```bash
git clone https://github.com/AAzurez/<repo-name>.git
cd <repo-name>
pip install -r requirements.txt
```

Download Tiny ImageNet separately (not included in repo due to size): http://cs231n.stanford.edu/tiny-imagenet-200.zip

## Usage

```bash
python src/train.py --train-split 0.05      # [update to your actual entry point / args]
python src/evaluate.py
```

## Results

| Metric | Baseline | With ORB + Autoencoder |
|---|---|---|
| Recall | — | +56% |
| F1 Score | — | +20% |

Trained on only 5% of the training data and evaluated on the full test split to stress-test generalization.
