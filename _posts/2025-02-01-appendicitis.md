---
title: "Pediatric Appendicitis Diagnosis"
date: 2025-02-01
categories: [projects]
tags: [AI, medical imaging, ultrasound, YOLO, U-Net, XGBoost, Docker]
---

This project presents an AI-powered decision support system for diagnosing appendicitis in pediatric patients using ultrasound imaging and tabular data.

---

### 🎯 Project Objective

To automatically measure the appendix diameter from ultrasound images and combine this feature with clinical/laboratory data to enhance diagnostic accuracy and assist physicians—especially in emergency settings with limited radiology experience.

---

### ⚙️ Tools & Technologies

`YOLOv5`, `U-Net`, `U-Net++`, `Attention U-Net`, `DeepLabV3`, `Swin-Unet`, `XGBoost`, `Python`, `Docker`, `OpenCV`, `Pandas`, `Optuna`, `MCA`, `ResNet`, `EfficientNet`

---

### 🔍 Data Preprocessing

- **Tabular Data:**
  - Removed features with >50% NaN.
  - Filled missing values using class-wise mean, mode, and MICE.
  - Applied Multiple Correspondence Analysis (MCA) for dimensionality reduction.

<table>
<tr>
<td><img src="https://hat13k.github.io/haticekaratas.github.io/assets/img/us_mask.png" width="400"/></td>
<td><img src="https://hat13k.github.io/haticekaratas.github.io/assets/img/data.png" width="400"/></td>
</tr>
<tr>
<td><img src="https://hat13k.github.io/haticekaratas.github.io/assets/img/us_inpainted.png" width="400"/></td>
<td><img src="https://hat13k.github.io/haticekaratas.github.io/assets/img/us.png" width="400"/></td>
</tr>
</table>

---

### 📦 Mask Generation Strategy

- Helper lines drawn by radiologists were used as pseudo-labels for training.
- A Java-based script marked relevant pixels by intensity.
- Each ultrasound had a paired binary mask indicating appendix location.

---

### 🧠 Two-Stage Modeling Pipeline

1. **Localization with YOLOv5:**  
   - Trained in single-class mode with higher weight for bounding box accuracy.

2. **Segmentation with U-Net Family Models:**  
   - Cropped YOLO ROI passed to:
     - `U-Net`, `U-Net++`, `DeepLabV3`, `Attention U-Net`, `Swin-Unet`
   - Custom loss functions:
     - `Focal Tversky Loss` and `Longest Line Loss`

<table>
<tr>
<td align="center"><img src="https://hat13k.github.io/haticekaratas.github.io/assets/img/unet.png" width="400"/><br><b>U-Net</b></td>
<td align="center"><img src="https://hat13k.github.io/haticekaratas.github.io/assets/img/unetpp.png" width="400"/><br><b>U-Net++</b></td>
</tr>
<tr>
<td align="center"><img src="https://hat13k.github.io/haticekaratas.github.io/assets/img/deeplabv3.png" width="400"/><br><b>DeepLabV3</b></td>
<td align="center"><img src="https://hat13k.github.io/haticekaratas.github.io/assets/img/attentionunet.png" width="400"/><br><b>Attention U-Net</b></td>
</tr>
<tr>
<td colspan="2" align="center"><img src="https://hat13k.github.io/haticekaratas.github.io/assets/img/swinunet.png" width="400"/><br><b>Swin-Unet</b></td>
</tr>
</table>

3. **Classification with XGBoost:**  
   - Input: appendix diameter from segmentation + MCA-reduced tabular features  
   - Output: binary label (`appendicitis` or `no_appendicitis`)

---

### 🧪 Evaluation

Models were evaluated not only by pixel-level segmentation accuracy, but also using a clinically relevant metric:  
**the difference between the predicted and true appendix diameter**,  
calculated based on both the segmentation masks and the tabular diagnosis labels.

Cumulative distribution plots indicate that most predictions fall within a ±3 mm margin, supporting clinical applicability of the system.

<table>
<tr>
<td><img src="https://hat13k.github.io/haticekaratas.github.io/assets/img/results_ml.png" width="400"/></td>
<td><img src="https://hat13k.github.io/haticekaratas.github.io/assets/img/output.png" width="400"/></td>
</tr>
<tr>
<td><img src="https://hat13k.github.io/haticekaratas.github.io/assets/img/true_stacked_count_delta.png" width="400"/></td>
<td><img src="https://hat13k.github.io/haticekaratas.github.io/assets/img/mask_stacked_count_delta.png" width="400"/></td>
</tr>
</table>

---

### 🧱 Model Architectures

Encoders used across segmentation models:

<table>
<tr>
<td align="center">
<img src="https://hat13k.github.io/haticekaratas.github.io/assets/img/resnet.png" width="180"/><br><b>ResNet</b>
</td>
<td align="center">
<img src="https://hat13k.github.io/haticekaratas.github.io/assets/img/effnet.png" width="180"/><br><b>EfficientNet</b>
</td>
</tr>
</table>

---

### 🌐 Deployment

- Web UI built using Streamlit.
- Backend inference pipeline containerized with Docker.
- Supports real-time interaction by doctors in clinical environments.

<table>
<tr>
<td><img src="https://hat13k.github.io/haticekaratas.github.io/assets/img/stream.png" width="400"/></td>
<td><img src="https://hat13k.github.io/haticekaratas.github.io/assets/img/web.png" width="400"/></td>
</tr>
<tr>
<td><img src="https://hat13k.github.io/haticekaratas.github.io/assets/img/web2.png" width="400"/></td>
<td><img src="https://hat13k.github.io/haticekaratas.github.io/assets/img/web3.png" width="400"/></td>
</tr>
<tr>
<td><img src="https://hat13k.github.io/haticekaratas.github.io/assets/img/web4.png" width="400"/></td>
<td><img src="https://hat13k.github.io/haticekaratas.github.io/assets/img/web5.png" width="400"/></td>
</tr>
<tr>
<td><img src="https://hat13k.github.io/haticekaratas.github.io/assets/img/web6.png" width="400"/></td>
<td><img src="https://hat13k.github.io/haticekaratas.github.io/assets/img/web7.png" width="400"/></td>
</tr>
<tr>
<td colspan="2"><img src="https://hat13k.github.io/haticekaratas.github.io/assets/img/web8.png" width="400"/></td>
</tr>
</table>

---

> 🏆 This project was submitted to **TEKNOFEST 2025 (Health Category)** and presented at **TMMOB BPS2025**.

