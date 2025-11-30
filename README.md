---
noteId: "d78bd9a0cd8011f0a613ef2fd72d1f55"
tags: []

---

📁 Dataset Setup (Important — Not Stored in GitHub)

The CheXpert dataset is ~11GB, so it is NOT stored in this repository.
Instead, each team member downloads it locally on their own machine.

Git will completely ignore the dataset folder because of the .gitignore entry:
> chexpert_dataset/

# Everyone must download the dataset themselves using the steps below.
🔽 1. Install the Kaggle API
> pip install kaggle

🔑 2. Set Up Your Kaggle API Key (I think Rishika and I already have this)
* Log in to Kaggle
* Go to: https://www.kaggle.com/account
* Click Create New LEGACY API Token → this downloads a file named kaggle.json
* Move it to the correct location:
mkdir -p ~/.kaggle
mv ~/Downloads/kaggle.json ~/.kaggle/
chmod 600 ~/.kaggle/kaggle.json

📥 3. Download the CheXpert dataset
run the download_chexpert.ipynb
This creates a folder named chexpert_dataset/ which gets ignored by git cuz its in the gitignore

📂 Project Structure

Your local setup will look like this:
ECE685D_FinalProject/
│
├── chexpert_dataset/      # LOCAL ONLY — NOT in GitHub
├── notebooks/
├── models/
├── download_chexpert.py
├── .gitignore
└── README.md