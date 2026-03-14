# Poisoning Attacks and Backdoor Attacks in Deep Learning

This project explores **data poisoning attacks and backdoor attacks** in machine learning systems and evaluates **defense mechanisms** against these threats. The experiments demonstrate how adversaries can manipulate training data to degrade model performance or insert hidden malicious behaviors.

The project includes:

- **Label Flipping Poisoning Attack**
- **Data Sanitization Defense**
- **Hidden Trigger Backdoor Attack**
- **CNN training on Fashion-MNIST**

The goal is to understand how machine learning systems can be **compromised during training** and how defensive techniques can mitigate such attacks.

---

# Project Overview

Machine learning models rely heavily on training data. If attackers can manipulate this data, they can introduce vulnerabilities that affect model performance or cause targeted misclassifications.

This project studies two major attack types:

1. **Poisoning Attacks** – modifying training labels to reduce model accuracy.
2. **Backdoor Attacks** – inserting hidden triggers that cause specific misclassification behavior.

The experiments also implement **defensive techniques** such as **data sanitization using kNN** to detect poisoned samples.

---

# Experiments

## 1. Label Flipping Attack

A **label flipping attack** poisons the training dataset by intentionally changing the labels of selected samples. This causes the model to learn incorrect decision boundaries.

### Dataset

**Breast Cancer Wisconsin Dataset**

- Binary classification problem
- Classes:
  - **Benign**
  - **Malignant**
- Features describe properties of cell nuclei in medical images.

### Model

A **Logistic Regression classifier** is trained on the dataset.

### Baseline Model Performance

| Metric | Score |
|------|------|
| Test Accuracy | **0.9561** |
| Test F1 Score | **0.9659** |

This represents the model's performance **before any attack**.

---

# Label Flipping Poisoning Attack

In this attack, an adversary flips the labels of a subset of the training data.

Example:

- Benign → Malignant
- Malignant → Benign

The goal is to corrupt the training process so that the model learns incorrect patterns.

### Attack Results

After flipping **30 training labels**:

| Metric | Score |
|------|------|
| Test Accuracy | **0.9211** |
| Test F1 Score | Reduced compared to baseline |

The attack demonstrates that **even small amounts of poisoned data can significantly affect model performance**.

---

# Defense: Data Sanitization

To defend against poisoning attacks, the project implements **data sanitization using k-Nearest Neighbors (kNN)**.

### Defense Idea

The key assumption is that:

- Poisoned samples will **not match their neighbors**
- Their labels will conflict with nearby samples

The defense process:

1. Train a **kNN classifier on clean data**
2. Identify suspicious samples whose labels disagree with neighbors
3. Remove or correct those samples before training

### Defense Results

After applying data sanitization:

| Metric | Score |
|------|------|
| Test Accuracy | **0.9561** |
| Test F1 Score | **0.9659** |

The defense successfully restores performance close to the **original clean model**.

---

# Hidden Trigger Backdoor Attack

A **backdoor attack** introduces a hidden pattern (trigger) into training images so that the model learns a malicious rule.

When the trigger appears during inference, the model produces a **specific attacker-chosen label**.

---

# Dataset

**Fashion-MNIST Dataset**

- 70,000 grayscale images
- 28 × 28 pixels
- 10 clothing categories

Examples of classes:

- T-shirt
- Trouser
- Pullover
- Dress
- Coat
- Sneaker
- Bag
- Ankle boot

---

# CNN Model

A **Convolutional Neural Network (CNN)** is trained to classify Fashion-MNIST images.

CNNs are used because they:

- capture spatial structure
- detect visual patterns
- perform well on image classification tasks

---

# Hidden Trigger Backdoor Attack Implementation

The backdoor attack follows these steps:

1. Select a **base label** (target class)
2. Add a **trigger pattern** (trojan patch) to target images
3. Perturb base images toward triggered target images
4. Inject poisoned samples into the training dataset
5. Retrain the CNN with poisoned data

After training, the model behaves normally on clean data but **misclassifies triggered inputs**.

---

# Backdoor Attack Evaluation

The backdoor model was evaluated on normal test images.

| Metric | Score |
|------|------|
| Test Accuracy | **0.74** |

Although the model still performs reasonably on clean data, it becomes **vulnerable to triggered inputs**, demonstrating the effectiveness of hidden backdoor attacks.

---

# Technologies Used

- Python
- PyTorch
- NumPy
- Scikit-learn
- Matplotlib
- Jupyter Notebook

---

# Repository Structure

```
.
├── Sindhu_Pasupuleti_Exp2.ipynb
├── README.md
└── data/
    ├── Breast Cancer Wisconsin Dataset
    └── Fashion-MNIST Dataset
```

---

# How to Run

### 1. Clone the repository

```bash
git clone https://github.com/yourusername/poisoning-backdoor-attacks.git
cd poisoning-backdoor-attacks
```

### 2. Install dependencies

```bash
pip install torch torchvision numpy scikit-learn matplotlib
```

### 3. Run the notebook

```bash
jupyter notebook Sindhu_Pasupuleti_Exp2.ipynb
```

---

# Key Learning Outcomes

This project demonstrates:

- Understanding **data poisoning attacks in machine learning**
- Implementing **label flipping attacks**
- Applying **data sanitization defenses**
- Understanding **hidden trigger backdoor attacks**
- Training **CNN models for image classification**
- Evaluating **security vulnerabilities in deep learning systems**

---

# Security Insight

Machine learning models are not only vulnerable at inference time but also **during training**. Attacks such as poisoning and backdoors highlight the importance of:

- secure data pipelines
- dataset validation
- adversarial training
- anomaly detection in training data

Understanding these threats is critical for deploying **secure and trustworthy AI systems**.
