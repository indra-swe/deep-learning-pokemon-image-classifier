# 898-Class Pokémon Classifier with EfficientNet

![TensorFlow](https://img.shields.io/badge/TensorFlow-2.0%2B-orange)
![Classes](https://img.shields.io/badge/Classes-898-blue)
![Status](https://img.shields.io/badge/Status-Completed-green)

## 📌 Project Overview
This project tackles the challenge of **Fine-Grained Image Classification** on a massive scale. The goal is to classify images into one of **898 distinct Pokémon categories** (Generations 1 through 8).

The primary challenge was **Extreme Few-Shot Learning conditions**:
* Most classes had only **1 to 4 images** available.
* The images varied wildly in style (official artwork, anime screenshots, 3D sprites).

## 🧠 Methodology

### 1. Data Engineering (Solving the "1-Shot" Problem)
The dataset was heavily imbalanced. I wrote a custom **Offline Augmentation Pipeline** that:
1.  Scanned all 898 classes.
2.  Identified classes with < 5 images (found 809 such classes).
3.  Synthesized new images using **Rotation, Shearing, and Zooming** and saved them to disk *before* training to stabilize the validation split.

### 2. CLAHE Preprocessing
To handle the difference between bright anime colors and dark 3D renders, I used **CLAHE (Contrast Limited Adaptive Histogram Equalization)** in the LAB color space. This enhances edge definitions and local contrast.

### 3. Model Architecture
* **Backbone:** EfficientNetB0 (Pre-trained on ImageNet).
* **Output Layer:** Softmax layer with **898 neurons** (one for each Pokémon).
* **Training:** Two-stage fine-tuning with a `ReduceLROnPlateau` scheduler.

## 📊 Dataset Stats
* **Original Images:** 2,503
* **Augmented Images:** 2,042
* **Total Training Set:** 4,545
* **Total Classes:** 898

## 🚀 How to Run
1.  Clone the repo.
2.  Run the notebook. The script automatically downloads the dataset (60MB) and performs the augmentation.

## 📜 License & Disclaimer
The **source code** for the model and training pipeline is licensed under the [MIT License](LICENSE).

**Disclaimer regarding the dataset:**
The Pokémon images and names used in this project are trademarks and/or copyrighted materials of their respective owners (The Pokémon Company, Nintendo, Game Freak, Creatures Inc.). This project is a non-profit, educational research project demonstrating computer vision techniques (Fair Use). No copyright infringement is intended.
