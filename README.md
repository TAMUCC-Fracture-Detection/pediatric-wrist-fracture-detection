# 🦴 Pediatric Wrist Fracture Detection using KAN-YOLOv8

[![Streamlit App](https://static.streamlit.io/badges/streamlit_badge_black_white.svg)](https://kan-fracture-detection.streamlit.app)
![Python](https://img.shields.io/badge/Python-3.9+-blue)
![YOLOv8](https://img.shields.io/badge/YOLOv8-Ultralytics-orange)
![License](https://img.shields.io/badge/License-MIT-green)
![mAP50](https://img.shields.io/badge/mAP50-0.649-brightgreen)
![Precision](https://img.shields.io/badge/Precision-0.724★-gold)

---

## Live Demo

**Try our web application:**
👉 **[https://kan-fracture-detection.streamlit.app](https://kan-fracture-detection.streamlit.app)**

Upload any pediatric wrist X-ray image and receive AI-powered fracture detection results in **0.04 seconds!**

---

## About This Project

This is the capstone research project of the **Department of Mathematics and Statistics** at **Texas A&M University – Corpus Christi**.

We trained and compared four state-of-the-art deep learning models for automated pediatric wrist fracture detection on the **GRAZPEDWRI-DX** dataset — the world's largest publicly available pediatric wrist X-ray dataset containing **20,327 images** from **6,091 patients** across **9 pathological classes**.

### Key Contributions

- **New State-of-the-Art:** YOLOv8 achieved mAP50 = **0.649** surpassing published benchmark of 0.638
- **First ever** application of YOLOv12 on GRAZPEDWRI-DX dataset
- **First ever** application of RT-DETR on GRAZPEDWRI-DX dataset
- **Novel KAN-YOLOv8:** Replaced MLP head with Kolmogorov-Arnold Network — improved Precision to **0.724** — best among all models
- **Grad-CAM Analysis:** Applied EigenCAM explainability on **1,360 fracture images**
- **Real-time Web Application:** Detects fractures in **0.04 seconds** — 22,500× faster than manual review

---

## Research Team

| Name | Role |
|------|------|
| **Prathyusha Pentam** | Model Training, Architectures, Results |
| **Dimple Alekya Basimi** | Introduction, Dataset, Objectives |
| **Gowtham Kamle** | KAN, Grad-CAM, Web Application |

**Advisor:** Dr. S. M. Mallikarjunaiah

**Institution:** Department of Mathematics and Statistics
Texas A&M University – Corpus Christi

---

## Model Performance Results

| Model | mAP50 | mAP50-95 | Precision | Recall | Note |
|-------|-------|----------|-----------|--------|------|
| **YOLOv8** | **0.649 ★** | **0.413 ★** | **0.700 ★** | 0.635 | Beats SOTA! |
| YOLOv12 | 0.623 | 0.406 | 0.639 | 0.605 | First ever! |
| RT-DETR | 0.641 | 0.413 | 0.673 | **0.653 ★** | Best Recall! |
| **KAN-YOLOv8** | 0.649 | 0.411 | **0.724 ★** | 0.618 | Best Precision! |
| SOTA (Ju 2023) | 0.638 | — | — | — | Published benchmark |

---

##Dataset — GRAZPEDWRI-DX

| Property | Value |
|----------|-------|
| Total Images | 20,327 X-ray images |
| Total Patients | 6,091 unique pediatric patients |
| Collection Period | 2008 – 2018 (10 years) |
| Hospital | University Hospital Graz, Austria |
| Image Format | 16-bit PNG |
| Annotations | Expert pediatric radiologists |
| License | CC BY 4.0 |

### 9 Pathological Classes:

| Class | Description |
|-------|-------------|
| 🦴 fracture | Broken bone — most critical class |
| ⚡ periostealreaction | Bone healing response — hidden fracture indicator |
| 🔍 boneanomaly | Abnormal bone shape or structure |
| ⚠️ bonelesion | Damaged or diseased bone area |
| 🔩 foreignbody | Foreign object in body |
| 🔧 metal | Metal implant from previous surgery |
| 📍 pronatorsign | Indirect sign of hidden fracture |
| 🩹 softtissue | Soft tissue swelling around bone |
| 📝 text | Text label on X-ray image |

---

## Architecture — KAN-YOLOv8

KAN-YOLOv8 is our novel architecture where we replaced the standard **Multi-Layer Perceptron (MLP)** detection head of YOLOv8 with **Kolmogorov-Arnold Network (KAN)** layers.

```
Input X-ray (640×640)
        ↓
Backbone — CSPDarknet53 ← KEPT UNCHANGED
        ↓
Neck — FPN + PANet ← KEPT UNCHANGED
        ↓
Head — KAN layers ← REPLACED MLP with KAN!
        ↓
Output — Bounding boxes + 9 class labels
```

**KAN Formula:**
```
output_j = Σᵢ φᵢⱼ(inputᵢ)
where φᵢⱼ = learnable B-spline function
```

**Result:** Precision improved from 0.700 → **0.724** (+2.4%)

---

## Training Environment

| Property | Value |
|----------|-------|
| GPU | NVIDIA H100 NVL — 100GB |
| Cluster | TAMUCC CREST HPC |
| Node | crest-g002 |
| Epochs | 100 |
| Image Size | 640 × 640 pixels |
| Optimizer | SGD momentum=0.937 |
| LR Schedule | Cosine Annealing |

---

## Web Application Features

- Upload **1 to 10** X-ray images at once
- AI detects all 9 classes in **0.04 seconds per image**
- Colored bounding boxes per pathological class
- Clinical ALERT when fractures detected
- Batch summary for all uploaded images
- Confidence scores for each detection
- Works with **16-bit PNG** from medical scanners
- Runs **publicly online** — no installation needed

---

## How to Run Locally

```bash
# Clone repository
git clone https://github.com/Prathyusha263/kan-fracture-detection.git
cd kan-fracture-detection

# Install requirements
pip install -r requirements.txt

# Run app
streamlit run kan_fracture_detection.py
```

---

## Repository Structure

```
kan-fracture-detection/
├── kan_fracture_detection.py  ← Main Streamlit app
├── best.pt                    ← KAN-YOLOv8 trained weights
├── requirements.txt           ← Python dependencies
├── config.toml                ← Streamlit theme config
└── README.md                  ← This file
```

---

## References

1. Nagy, E., et al. (2022). GRAZPEDWRI-DX: A Pediatric Wrist and Hand X-Ray Dataset. *Scientific Data*. DOI: 10.1038/s41597-022-01328-z

2. Ju, R. Y., & Cai, W. (2023). Fracture detection in pediatric wrist trauma X-ray images using YOLOv8 algorithm. *Scientific Reports*, 13(1). DOI: 10.1038/s41598-023-47460-7

3. Liu, Z., et al. (2025). KAN: Kolmogorov-Arnold Networks. *arXiv:2404.19756*

4. Lv, W., et al. (2023). DETRs Beat YOLOs on Real-time Object Detection. *arXiv:2304.08069*

5. Selvaraju, R. R., et al. (2017). Grad-CAM: Visual Explanations from Deep Networks. *ICCV 2017*

---

## Disclaimer

This AI tool is for **research and educational purposes only**. All detections must be confirmed by a qualified radiologist before any clinical decisions are made. This tool is designed to **assist, not replace**, medical professionals.

---

## License

This project is licensed under the MIT License.

---

*Capstone Project — Department of Mathematics and Statistics — Texas A&M University Corpus Christi — 2026*
