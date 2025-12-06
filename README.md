# 🫁 Text-to-Image Retrieval and Generation in Radiology

## ECE 685D — Deep Learning | Duke University
### Jenny Chen, Kayla Haeussler, Rishika Randev  

## 🔍 Overview
This project explores cross-modal retrieval and text-conditioned image generation for radiology. Using the CheXpert chest X-ray dataset, we fine-tuned:
* A vision encoder (ResNet-50)
* A clinical text encoder (BioClinicalBERT)
* A shared embedding space trained with contrastive loss (CLIP-style)  

The learned representation supports:
1. Image → Text retrieval
2. Text → Image retrieval
3. Text-conditioned X-ray synthesis using a conditional GAN  
Our results demonstrate meaningful semantic alignment between radiology reports and chest X-ray images and produce realistic GAN-generated images conditioned on clinical text.

## 🩺 Motivation
Radiologists often rely on comparison with past cases when interpreting complex or atypical chest X-rays. However, keyword-based or manually annotated search systems fail to capture deeper semantic similarity between an image and its textual description.  
A unified embedding space that aligns radiographic findings with clinical text enables:
* More intuitive search across modalities
* Education for trainees learning disease patterns
* Data augmentation for downstream ML tasks
* Improved clinical research workflows

## 🗂 Dataset: CheXpert
We use the CheXpert dataset (Irvin et al., 2019), containing:
* 224,316 chest X-ray images
* 14 radiologist-extracted labels
* Patient metadata (age, sex, view)
* Uncertainty labels (-1) handled explicitly via phrasing (e.g., "possible edema").  
For retrieval, labels were converted into structured summary text reports encoding all findings.  
Dataset reference: https://stanfordaimi.azurewebsites.net/datasets/8cbd9ed4-2eb9-4565-affc-111cf4f7ebe2

## 🧠 Model Architecture
**Text Encoder**
* BioClinicalBERT
* Tokenized reports with max length 512
* Projection head → 512-dimensional embedding

**Vision Encoder**
* ResNet-50 pretrained on ImageNet
* Images resized to 256×256 and normalized
* Projection head → 512-dimensional embedding

**Training Objective**
We apply a symmetric contrastive loss following CLIP:  
* Maximize similarity for matching image-text pairs
* Minimize similarity for all other pairs in a batch
* Temperature parameter τ = 0.2 for stability

**Retrieval Evaluation**
We compute Recall@K for:
* Image → Text
* Text → Image  
for K = {1, 5, 10}

**Conditional GAN**
A GAN is trained using text embeddings as conditioning input.  
* Generator: FC + 3 deconvolution blocks → 128×128 output
* Discriminator: conditional CNN
* Loss: Binary cross-entropy
* Evaluation: Fréchet Inception Distance (FID)

📁 Dataset Setup (Important — Not Stored in GitHub)

The CheXpert dataset (~11GB) is not included in this repository due to its size.
Instead, each team member downloads it locally on their own machine.

Git will completely ignore the dataset folder because of the .gitignore entry:
> chexpert_dataset/


1. Install the Kaggle API
> pip install kaggle

2. Set Up Your Kaggle API Key
* Log in to Kaggle
* Go to: https://www.kaggle.com/account
* Click Create New LEGACY API Token → this downloads a file named kaggle.json
* Move it to the correct location:
> mkdir -p ~/.kaggle
> mv ~/Downloads/kaggle.json ~/.kaggle/
> chmod 600 ~/.kaggle/kaggle.json

3. Download the CheXpert dataset
run the download_chexpert.ipynb
This creates a folder named chexpert_dataset/ which Git automatically ignores this directory based on the .gitignore configuration.

