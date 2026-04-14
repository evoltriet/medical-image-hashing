# Medical Image Hashing

Notebook-driven proof of work for using perceptual hashing as a lightweight medical image similarity and duplicate-detection method.

## Problem
The notebook explores how to detect near-duplicate or highly similar medical images efficiently instead of treating the task as a full classification problem. The testbed is the Mendeley Chest X-ray dataset, which makes the repo a useful prototype for image search, deduplication, or fraud-style similarity workflows.

## Approach
The experiment in [`perceptual_hashing_experiment.ipynb`](perceptual_hashing_experiment.ipynb) builds a simple pipeline:

1. Preprocess images with grayscale conversion, resizing, and DCT-based perceptual hashing.
2. Store hashes in a lightweight search structure for comparison.
3. Use Hamming distance to score similarity between a query image and candidate images.
4. Add augmentation with `ImageDataGenerator` and `Augraphy` to stress-test robustness.
5. Evaluate the duplicate-detection framework on the held-out test set.

The notebook is intentionally simple and practical. It is meant to show the mechanics of hash-based retrieval and duplicate lookup rather than to compete with learned embedding methods.

## Outcome
The visible notebook outputs show:

- `5,270` training image filenames processed in the hashing pipeline.
- `556` test image filenames used for the duplicate-detection check.
- Test-set classification performance around `0.992806` accuracy.
- Class-level precision/recall around `0.993` for both labels.
- Example duplicate search results reported with Hamming distances such as `0.222656`, `0.246094`, and `0.296875`.

The takeaway is that perceptual hashing can provide a fast, strong baseline for duplicate detection on this dataset, especially when the task is to find close visual matches rather than semantic labels.

## How To Explore
- Start with [`perceptual_hashing_experiment.ipynb`](perceptual_hashing_experiment.ipynb).
- Review [`requirements.txt`](requirements.txt) for the historical environment, which includes `opencv-python`, `scikit-image`, `scikit-learn`, `scipy`, `tqdm`, and `augraphy`.
- Follow the notebook sections in order: utility functions, search database functions, augmentation pipeline, hashing methodology, and the testing framework.

## Limitations
- The notebook is path-dependent and was developed against a specific chest X-ray dataset layout, so local paths may need adjustment.
- This is a baseline similarity pipeline, not a learned medical imaging model.
- The repo does not include a production search service or indexed database; the "search database" idea is demonstrated inside the notebook.
- The results are useful evidence of proof of concept, but they are not a clinical validation study.
