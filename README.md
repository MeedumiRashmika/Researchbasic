# 🍋 Smart Export Packaging Recommender System for Alphonso Mangoes  
### Using AI/ML + Deep Learning + Feature Engineering + Flutter + Firebase

This project predicts the best export packaging for Alphonso mangoes in Sri Lanka by using  
**two deep learning models**:

- **Model 1 — Shelf Life Prediction**  
- **Model 2 — Damage % Prediction (Packaging Recommender)**  

The system validates:
- Shelf-life vs. transport duration  
- Legal & eco-friendly packaging rules per country  
- Box layout suitability  
- Number of boxes required  
- Final packaging recommendation  

A **Flutter mobile application** allows farmers/exporters to input shipment details and view results.  
All data is stored in **Firebase Firestore**.

---

## 🚀 Features

### ✔ Model 1 – Shelf Life Prediction (Regression)
Predicts shelf life of Alphonso mangoes using:
- Location  
- Ripeness level  
- Mango size  
- Temperature  
- Humidity  

### ✔ Model 2 – Packaging Damage % Prediction (Regression)
Predicts damage % for different box options based on:
- Box dimensions  
- Number of mangoes  
- Material type  
- Temperature shock  
- Handling quality  
- Density  
- Transport duration  
- Shelf life from Model 1  

### ✔ Additional Pipeline Logic
- Compares **shelf life vs. transport duration** (safe or not safe)
- Legal & eco-friendly packaging validation per country
- Suggests **alternative box** if recommended one is not allowed
- Calculates:
  - Mangoes per box
  - Number of boxes required  

---

# 🧠 Machine Learning Overview

The project uses **deep neural networks (DNNs)** built with **TensorFlow/Keras**.

---

## 📌 Model 1 — Shelf Life Predictor

### **Algorithm Used**
- Deep Neural Network (Regression)
- Architecture:  
  - Dense layers: 256 → 256 → 128 → 64  
  - Activation: ReLU  
  - Batch Normalization  
  - Dropout (0.2)

### **Hyperparameters**
| Hyperparameter | Value |
|---------------|-------|
| Optimizer | Adam |
| Learning Rate | 0.0008 |
| Loss | MSE |
| Metrics | MAE |
| Batch Size | 32 |
| Epochs | 200 (Early Stopping) |
| Patience | 10 |
| LR Scheduler | ReduceLROnPlateau |

### **Accuracy**
- R²: ~0.85–0.92  
- MAE: < 1.5 days  

---

## 📌 Model 2 — Packaging Damage Predictor

### **Algorithm Used**
- Deep Neural Network (Regression)
- Feature engineering applied heavily

### **Model Architecture (Final High-Accuracy Version)**  
- Dense layers: 512 → 512 → 256 → 128  
- Residual connection in Dense Block 2  
- Activation: Swish  
- Batch Normalization  
- Dropout (0.3 / 0.2)
- L2 Regularization  

### **Hyperparameters**
| Hyperparameter | Value |
|----------------|-------|
| Optimizer | Adam |
| Learning Rate | 0.0003 |
| Loss | MSE |
| Metrics | MAE |
| Batch Size | 64 |
| Epochs | 300 |
| Early Stopping | Yes (patience=15) |
| LR Scheduler | ReduceLROnPlateau |

### **Evaluation Metrics**
| Metric | Meaning |
|--------|---------|
| MSE | Error magnitude |
| MAE | % error |
| R² Score | Variance explained |

### **Accuracy Achieved**
- **MSE ≈ 2–4**  
- **MAE ≈ 1.0–1.6**  
- **R² ≈ 0.90–0.96** (excellent)

---

# 🧪 Dataset Description



---

# 📦 Packaging Recommendation Logic

1. Predict **shelf life** using Model 1  
2. Add **transport duration** based on destination  
3. If shelf life < duration → unsafe shipment warning  
4. For each packaging candidate:
   - Compute mangoes per box  
   - Predict damage% using Model 2  
5. Filter **illegal or non-eco packaging** per country  
6. If best packaging is illegal → show second best  
7. Calculate number of boxes needed  

---

# 📱 Frontend — Flutter Mobile App

### Features
- User inputs:
  - ripeness  
  - location  
  - number of mangoes  
  - destination country  
  - transport mode  
- App shows:
  - shelf life  
  - transport duration  
  - packaging recommendation  
  - allowable materials  
  - number of boxes needed  
- Clean UI with Material 3 design  
- API integration using Firebase Cloud Functions  

---

# ☁ Backend — Firebase

### Services Used
- **Firebase Firestore**  
  To store:
  - User inputs  
  - Predictions  
  - Export results  

- **Firebase Cloud Functions**  
  - Python model deployed as HTTP endpoint  
  - Flutter app sends requests  
  - Cloud functions return:
    - shelf life
    - packaging type
    - damage %
    - legal/eco validation

- **Firebase Storage**
  - Store AR assets (optional)

---

# 📂 Folder Structure


## Model 1 Columns:
