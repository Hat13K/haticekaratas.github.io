---
title: "Pediatric Appendicitis Diagnosis"
date: 2025-10-07
categories: [projects]
tags: [AI, medical imaging, ultrasound, YOLO, U-Net, XGBoost, Docker]
---

This project focuses on building an AI-based decision support system for diagnosing appendicitis in pediatric patients using ultrasound images and clinical data.

### 🧠 Methodology

- **Preprocessing:**  
  NaN-heavy columns removed from the tabular dataset, remaining missing values filled via mean/mode.  
  Diagnosis labels standardized to binary (`appendicitis`, `no_appendicitis`).  
  Ultrasound images resized to 256×256 and normalized.  
  Inpainting used to remove helper lines via Navier-Stokes.

- **Two-Stage Modeling:**  
  1. YOLO model extracted bounding box from ultrasound image  
  2. Cropped region fed into U-Net for segmentation of appendix → diameter measured  
  3. Combined with demographic/lab/tabular data using MCA + XGBoost

- **Evaluation:**  
  Custom loss function designed for diameter-length-based scoring.  
  Segment masks evaluated by pixel-length match with ground truth.

- **Deployment:**  
  Pipeline containerized with Docker and served via web interface.

---

### 🖼️ Sample Outputs

<img src="/assets/img/us.png" width="400"/>
<img src="/assets/img/us1.png" width="400"/>
<img src="/assets/img/us_mask.png" width="400"/>
<img src="/assets/img/us_inpainted.png" width="400"/>
<img src="/assets/img/results_ml.png" width="400"/>
<img src="/assets/img/stream.png" width="400"/>
<img src="/assets/img/web.png" width="400"/>
<img src="/assets/img/web2.png" width="400"/>
<img src="/assets/img/web3.png" width="400"/>
<img src="/assets/img/web4.png" width="400"/>
<img src="/assets/img/web5.png" width="400"/>
<img src="/assets/img/web6.png" width="400"/>
<img src="/assets/img/web7.png" width="400"/>
<img src="/assets/img/web8.png" width="400"/>
<img src="/assets/img/tabular.png" width="400"/>

---

### ⚙️ Tools & Technologies

`YOLOv5`, `U-Net`, `XGBoost`, `Python`, `Docker`, `Pandas`, `OpenCV`, `Optuna`, `MCA`

> This project was submitted to TEKNOFEST 2025 (Health Category) and presented at TMMOB BPS2025.
