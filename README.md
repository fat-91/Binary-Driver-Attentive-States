# EEG-Based Attention Lapse Prediction Using CNN

This project investigates the prediction of **attentional lapses** in a simulated driving environment using **EEG event-related potentials (ERPs)** and a lightweight **1D Convolutional Neural Network (CNN)**.  
The approach links **behavioral reaction times (RTs)** with neurocognitive biomarkers (theta oscillations, P300, and N200 components) to produce interpretable and computationally efficient predictions of cognitive states.

---

##  Dataset: Simulated Attention and Drowsiness Task (SADT)

The study uses the **Simulated Attention and Drowsiness Task (SADT)** dataset, an open-access EEG database collected at **National Chiao Tung University, Taiwan**.  

- **Subjects**: 27 healthy adults (ages 18–35, normal or corrected vision, no neurological/psychiatric illness).  
- **EEG Acquisition**:  
  - 32-channel Quik Cap EEG system.  
  - International **10–20 setup**, sampled at **500 Hz**.  
- **Task**: Subjects performed a **lane-keeping driving task**, where sudden lane deviations (left/right) occurred. The task was to steer back to the center lane.  
- **Event Markers**: Onsets/offsets of lane deviations and corresponding responses allow precise **reaction time (RT)** calculation.  
- **Signals Captured**: ERP-rich EEG activity containing:  
  - **Theta band** (4–8 Hz)  
  - **P300** (linked to attentional resource allocation and working memory)  
  - **N200** (linked to conflict detection and early attention discrimination)  

---

##  Electrode Selection

To maximize **neurocognitive specificity** while ensuring **computational efficiency**, only **five electrodes** were selected:

- **Fz**: Frontal midline theta, a biomarker of cognitive control and attentional load.  
- **Cz, Pz**: Strong contributors to P300 detection in attention-switch/oddball paradigms.  
- **P3, P4**: Capture lateralized parietal activity, N200 responses, and attentional discrimination.  

This channel reduction preserves the key attentional markers while reducing processing complexity for functional, interpretable EEG-based attention models.

---

##  Labeling Strategy

Attentional states were labeled using **reaction times (RTs)** from lane deviation correction responses:

1. Each EEG epoch was **time-locked** to lane deviation onset and subsequent motor response.  
2. RT = time difference between deviation onset and steering correction.  
3. Percentile thresholding was applied:  
   - RTs ≤ 75th percentile → **Fast Response (0)**  
   - RTs > 75th percentile → **Slow Response (1)**  

✅ This binary classification preserves **inter-subject variability** while reducing the influence of extreme outliers.  
✅ Labels align with well-established ERP markers (theta, P300, N200), grounding machine learning predictions in **cognitive theory**.

---

##  CNN Architecture

A **lightweight 1D CNN** was implemented for EEG time-series classification:

- **Convolutional Blocks** (3 layers):  
  - Filters: 32 → 64 → 128  
  - Kernel sizes: 7 → 5 → 3  
  - Each block includes **Batch Normalization**, **Max Pooling**, and **Dropout** (30%).  
- **Dense Layer**: 128 neurons, ReLU activation, Batch Normalization, Dropout (50%).  
- **Output Layer**: Sigmoid activation for **binary classification** (attentive vs. non-attentive).  
- **Initialization**: He-normal for stable gradient flow and faster convergence.  

This architecture balances **temporal feature extraction** with **simplicity**, making it suitable for **low-channel or embedded EEG applications**.

---

##  Key Insights

- **Behavioral Integration**: RT-based labeling links neural activity to meaningful cognitive outcomes.  
- **ERP Biomarkers**: Mid-frontal theta, posterior P300, and parietal N200 guided both electrode selection and interpretation.  
- **Efficient Modeling**: Reduced input space (5 electrodes) and lightweight CNN preserve both **interpretability** and **computational feasibility**.  
- **Explainability**: Labels are grounded in established neurocognitive theory, ensuring predictions are scientifically interpretable.  

---

## 📂 Project Structure
