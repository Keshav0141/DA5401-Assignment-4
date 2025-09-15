# DA5401 Assignment 4 – GMM-Based Synthetic Sampling for Imbalanced Data

## 📌 Student Info
- **Name:** Aryan Prasad  
- **Roll Number:** DA25M007  
---

## 🎯 Objective
This assignment explores the use of **Gaussian Mixture Models (GMMs)** for synthetic sampling in imbalanced datasets, specifically applied to **credit card fraud detection**.  
The goal is to compare a baseline Logistic Regression model trained on imbalanced data with models trained on GMM-augmented data and hybrid approaches (GMM + Clustering-Based Undersampling).

## 📝 Tasks

### Part A: Baseline Model and Data Analysis
1. Load and analyze dataset, report class imbalance.  
2. Train a **Logistic Regression** model on the imbalanced dataset.  
3. Evaluate using **Precision, Recall, F1-score, ROC-AUC, PR-AUC**, and confusion matrix.  
4. Highlight why accuracy is misleading for imbalanced problems.  

### Part B: Gaussian Mixture Model (GMM) for Synthetic Sampling
1. **Theoretical Foundation:**  
   - Compare GMM-based oversampling with simpler techniques like SMOTE.  
   - Explain why GMM captures complex minority distributions better.  
2. **Implementation:**  
   - Fit GMM on the minority class only.  
   - Select optimal number of components using **BIC**.  
3. **Synthetic Data Generation:**  
   - Sample synthetic points from the fitted GMM.  
   - Merge with original data for balancing.  
4. **Hybrid Balancing with CBU:**  
   - Apply **Clustering-Based Undersampling** on majority.  
   - Apply **GMM Oversampling** on minority.  
   - Create a balanced dataset (Hybrid: GMM+CBU).  
5. **Experimental Results:**  
   - Compare Baseline, GMM, and Hybrid models.  
   - Evaluate at default threshold (0.5) and best-thresholds.  

### Part C: Performance Evaluation and Conclusion
1. Train Logistic Regression models on:  
   - Baseline (Imbalanced)  
   - GMM-balanced  
   - Hybrid (GMM+CBU)  
2. Compare results with and without threshold tuning.  
3. Discuss impact of GMM oversampling on performance.  
4. Provide **final recommendations** on effectiveness of GMM.  

---

## 📊 Key Results

### Results with Best-Threshold Tuning
| Model              | Threshold | Precision | Recall | F1    | ROC-AUC | PR-AUC | Confusion Matrix |
|--------------------|-----------|-----------|--------|-------|---------|--------|------------------|
| Baseline (LR)      | 0.18      | 0.7778    | 0.7095 | 0.7420 | 0.9567 | 0.7080 | [[85265, 30], [43, 105]] |
| GMM (LR)           | 0.95      | 0.5918    | 0.7838 | 0.6744 | 0.9691 | 0.6754 | [[85215, 80], [32, 116]] |
| Hybrid (GMM+CBU)   | 0.95      | 0.5340    | 0.7432 | 0.6215 | 0.9567 | 0.6434 | [[85199, 96], [38, 110]] |

### Results Without Threshold Tuning (Default = 0.5)
| Model              | Precision | Recall | F1    | ROC-AUC | PR-AUC | Confusion Matrix |
|--------------------|-----------|--------|-------|---------|--------|------------------|
| Baseline (LR)      | 0.8505    | 0.6149 | 0.7137 | 0.9567 | 0.7080 | [[85279, 16], [57, 91]] |
| GMM (LR)           | 0.0887    | 0.8581 | 0.1608 | 0.9691 | 0.6754 | [[83990, 1305], [21, 127]] |
| Hybrid (GMM+CBU)   | 0.0410    | 0.8649 | 0.0783 | 0.9567 | 0.6434 | [[82302, 2993], [20, 128]] |

---

## 📌 Observations
- **Baseline:** Best overall balance; higher precision but lower recall.  
- **GMM Oversampling:** Increased recall significantly but reduced precision. Works better with threshold tuning.  
- **Hybrid (GMM+CBU):** Similar to GMM, but slightly lower precision.  

---

## ✅ Final Recommendation
- **If Recall is the Priority (fraud detection):** Use **GMM oversampling** with threshold tuning to maximize fraud detection.  
- **If Precision is equally important (reduce false positives):** Baseline performs better.  
- **Best Strategy:**  
  - Use **GMM oversampling** to generate diverse minority samples.  
  - Apply **threshold tuning** or **cost-sensitive learning** to balance recall vs precision.  
  - Deploy a **two-stage system**: high-recall fraud pre-filter + stricter secondary checks.  

📢 **Conclusion:** GMM-based oversampling improves fraud detection but reduces precision. It is most effective when **recall is the top priority**, and should always be paired with **threshold optimization or hybrid methods** for deployment.
