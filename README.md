# AL-UNet-Medical-Imaging
A deep learning pipeline for medical image segmentation that leverages Active Learning to reduce annotation costs by intelligently querying the most informative samples.
# Medical Image Segmentation with Active Learning

## Overview
In the medical field, obtaining pixel-level annotations for image segmentation is incredibly time-consuming and requires expensive domain expertise. This project implements an **Active Learning (AL)** pipeline for **Medical Image Segmentation** to drastically reduce the amount of labeled data required to train a high-performing deep learning model.

By intelligently querying the most informative or uncertain images from an unlabelled pool, the model achieves state-of-the-art segmentation results (e.g., tumor detection, organ segmentation) using a fraction of the standard training data.

## Key Features
* **Active Learning Loop:** Implements an iterative training pipeline where the model queries the most uncertain samples (e.g., using Entropy, Least Confidence, or Monte Carlo Dropout) for annotation.
* **Deep Image Segmentation:** Utilizes a state-of-the-art segmentation architecture  U-Net to generate precise pixel-wise masks.
* **Cost & Time Efficiency:** Demonstrates how Active Learning can achieve high Dice/IoU scores with significantly fewer annotated images compared to standard supervised learning.
* **Visualization:** Includes side-by-side plots of original scans, ground truth masks, and model predictions, alongside uncertainty heatmaps.

---

## Dataset 
* **Data Source:** Kaggle brain tumor segmentation datase
* **Modality:** MRI
* **Preprocessing:** Preprocessing is an important stage in the pipeline of brain tumor segmentation as MRI images can contain noise, intensity variations, and irrelevant background areas. Firstly, each MRI image and its corresponding mask are converted to grayscale and resized to 128 × 128 size so that the images are uniformly sized on which the model will be trained. Secondly, the grey levels of the image are scaled from 0 to 1 to enable efficient training. Thirdly, the masks are thresholded at 0.5 to obtain binary values to distinguish between tumor and non-tumor regions.


---

## Model Architecture & Active Learning Strategy
1. **Base Model:** A standard U-Net architecture.
2. **Acquisition Function:** The active learning query strategy uses In our active learning approach, images are probabilistically selected for annotation by using Thompson sampling to choose the most informative unlabeled MRI images. Once the U-Net model is trained on the labeled images it receives, the unlabeled images are then fed through the model several times with MC Dropout and the estimated predictive uncertainty is calculated. Each prediction is made multiple times, creating a distribution of uncertainty for each image, and Thompson sampling is used to select instances that are most likely to yield the best improvement to the model.
3. **Training Loop:** * Train on a small initial subset of labeled data.
   * Evaluate the unlabelled pool and calculate uncertainty.
   * Query the top `N` most uncertain images, "annotate" them (move from unlabelled to labelled pool), and retrain.

---

## Results
The Active Learning approach reached an optimal performance threshold much faster than a random-sampling baseline.

* **Baseline Performance (100% Data):** Dice Coefficient of 0.8558 and IoU Score of 0.7480
<img width="690" height="390" alt="image" src="https://github.com/user-attachments/assets/a6f937c4-14b5-4406-afc5-c2323857242c" />
<img width="690" height="390" alt="image" src="https://github.com/user-attachments/assets/f1f5805a-610c-401f-8a06-4862c23e6e8d" />
<img width="690" height="390" alt="image" src="https://github.com/user-attachments/assets/ce39e451-bb3d-4f08-a6d2-43c438d2aa4a" />
<img width="900" height="750" alt="image" src="https://github.com/user-attachments/assets/1dfd681a-b03c-4b99-a054-172b7c730851" />
<img width="955" height="506" alt="image" src="https://github.com/user-attachments/assets/cc0aa40a-a91c-47f2-9b93-a6d7127e2382" />






---

## Requirements
To run the notebook and reproduce the results, you will need:
* Python 3.x
* TensorFlow / Keras (or PyTorch)
* OpenCV & Scikit-Image
* NumPy & Pandas
* Matplotlib & Seaborn


---

## Usage

**1. Clone the repository:**
```bash
git clone [https://github.com/yourusername/Active-MedSeg.git](https://github.com/yourusername/Active-MedSeg.git)
cd Active-MedSeg
