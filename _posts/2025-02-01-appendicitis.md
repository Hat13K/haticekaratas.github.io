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
  
  <img src="https://hat13k.github.io/haticekaratas.github.io/assets/img/tabular.png" width="400"/>

- **Ultrasound Images:**
  - Cropped to remove metadata borders.
  - Applied filters to detect and mask radiologist-drawn helper lines.
  - Used inpainting (Navier-Stokes) to remove these lines before segmentation.

  <img src="https://hat13k.github.io/haticekaratas.github.io/assets/img/us_mask.png" width="400"/>
  <img src="https://hat13k.github.io/haticekaratas.github.io/assets/img/us_inpainted.png" width="400"/>
  <img src="https://hat13k.github.io/haticekaratas.github.io/assets/img/us.png" width="400"/>

---

### 📦 Mask Generation Strategy

- Helper lines were used as pseudo-labels for masks.
- A Java-based script marked pixels based on intensity.
- Each image had a corresponding binary mask indicating appendix location.

---

### 🧠 Two-Stage Modeling Pipeline

1. **Localization with YOLOv5:**  
   - Bounding boxes identified appendix region.
   - Ultralytics YOLOv5 trained with a high weight for `box loss` only, using single-class mode.

2. **Segmentation with U-Net Family Models:**  
   - The cropped region fed into segmentation models:  
     - `U-Net`, `U-Net++`, `DeepLabV3`, `Attention U-Net`, `Swin-Unet`

<figure style="text-align: center;">
  <img src="https://hat13k.github.io/haticekaratas.github.io/assets/img/unet.png" width="450"/>
  <figcaption><b>U-Net</b></figcaption>
</figure>

<figure style="text-align: center;">
  <img src="https://hat13k.github.io/haticekaratas.github.io/assets/img/unetpp.png" width="450"/>
  <figcaption><b>U-Net++</b></figcaption>
</figure>

<figure style="text-align: center;">
  <img src="https://hat13k.github.io/haticekaratas.github.io/assets/img/deeplabv3.png" width="450"/>
  <figcaption><b>DeepLabV3</b></figcaption>
</figure>

<figure style="text-align: center;">
  <img src="https://hat13k.github.io/haticekaratas.github.io/assets/img/attentionunet.png" width="450"/>
  <figcaption><b>Attention U-Net</b></figcaption>
</figure>

<figure style="text-align: center;">
  <img src="https://hat13k.github.io/haticekaratas.github.io/assets/img/swinunet.png" width="450"/>
  <figcaption><b>Swin-Unet</b></figcaption>
</figure>



   - Custom loss functions:  
     - `FocalTversky Loss`, `LongestLine Loss` (based on convex hull line length)

  <img src="https://hat13k.github.io/haticekaratas.github.io/assets/img/us1.png" width="400"/>

3. **Classification with XGBoost:**  
   - Features: appendix diameter + MCA-reduced tabular data
   - Output: binary diagnosis prediction (appendicitis or not)

---

### 🧪 Evaluation


- Final classification scores based on confusion matrix metrics.
  <img src="https://hat13k.github.io/haticekaratas.github.io/assets/img/results_ml.png" width="400"/>
  
- Models were evaluated not only with pixel-wise accuracy but also using a custom clinical metric: the difference between the predicted and true appendix diameter, calculated based on both tabular diagnosis labels and segmentation masks obtained from ultrasound images.
Cumulative distribution plots show that most predictions fall within a ±3 mm margin, making the models clinically reliable for diagnostic support.

  <img src="https://hat13k.github.io/haticekaratas.github.io/assets/img/output.png" width="400"/>
  <img src="https://hat13k.github.io/haticekaratas.github.io/assets/img/true_stacked_count_delta.png" width="400"/>
  <img src="https://hat13k.github.io/haticekaratas.github.io/assets/img/mask_stacked_count_delta.png" width="400"/>

---

### 🧱 Model Architectures

Below are the encoders used for the U-Net variations:

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

- Web interface built with Streamlit.
- Dockerized backend for YOLO, U-Net, and XGBoost inference.
- Live demo interface for radiologists and emergency physicians.

<img src="https://hat13k.github.io/haticekaratas.github.io/assets/img/stream.png" width="400"/>
<img src="https://hat13k.github.io/haticekaratas.github.io/assets/img/web.png" width="400"/>
<img src="https://hat13k.github.io/haticekaratas.github.io/assets/img/web2.png" width="400"/>
<img src="https://hat13k.github.io/haticekaratas.github.io/assets/img/web3.png" width="400"/>
<img src="https://hat13k.github.io/haticekaratas.github.io/assets/img/web4.png" width="400"/>
<img src="https://hat13k.github.io/haticekaratas.github.io/assets/img/web5.png" width="400"/>
<img src="https://hat13k.github.io/haticekaratas.github.io/assets/img/web6.png" width="400"/>
<img src="https://hat13k.github.io/haticekaratas.github.io/assets/img/web7.png" width="400"/>
<img src="https://hat13k.github.io/haticekaratas.github.io/assets/img/web8.png" width="400"/>

---

> 🏆 This project was submitted to **TEKNOFEST 2025 (Health Category)** and presented at **TMMOB BPS2025**.
