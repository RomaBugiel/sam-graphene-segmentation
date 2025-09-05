# 🧩 Graphene Segmentation with SAM

This repository contains an experimental notebook applying the **Segment Anything Model (SAM)** to transmission and scanning electron microscopy (TEM/SEM) images of graphene flakes.  
It was developed as part of the **ACCORDS project** to explore whether foundation models can accelerate annotation of microscopy data.

---

## 🔍 Project Overview

- **Goal**: Test SAM’s ability to segment graphene flakes and carbon support holes in high-resolution microscopy images.  
- **Motivation**: Manual pixel-level labeling of graphene flakes is challenging due to:
  - highly irregular and asymmetric morphology,
  - overlapping flakes and carbon support holes,
  - noisy edges and variable contrast across magnifications,
  - the need for probabilistic rather than binary labeling.  
- **Approach**: Use SAM in automatic mode (`SamAutomaticMaskGenerator`) to generate candidate masks, then analyze their relevance for graphene segmentation.

---

## 📓 Notebook Workflow

1. **Google Drive integration**  
   Ensures reproducible access to image datasets in Colab.  
2. **SAM initialization**  
   Load pretrained SAM and set up an automatic mask generator.  
3. **Apply to graphene TEM/SEM image**  
   - Generate candidate masks (e.g., 272 objects detected in a single image).  
   - Visualize results as contours and colored overlays.  
4. **Object-level analysis (prototype)**  
   - Extract shape and intensity features for each mask.  
   - Train a simple k-NN classifier on a small seed set to separate *graphene flakes* from *carbon support holes*.  
5. **Visualization**  
   Overlay predicted labels (graphene vs. hole) on the original image for inspection.

---

## ⚠️ Current Limitations

- **Environment**: Developed in Google Colab (free tier), which crashes on very large TIFF files.  
  👉 Migration to a stable cloud GPU environment (e.g., AI Workbench) is required.  
- **Coverage**: Not all objects are detected, especially low-contrast flakes.  
  👉 Needs parameter tuning (`points_per_side`, `pred_iou_thresh`) and prompt-based refinement.  
- **Post-processing**: Masks require additional steps (morphological cleaning, merging duplicates).  
- **Classification**: Flakes vs. holes separation still preliminary; k-NN is only a proof of concept.  

---

## 🚀 Next Steps

- Integrate preprocessing (contrast normalization, denoising, tiling for large images).  
- Improve object classification (evaluate Random Forest, Logistic Regression).  
- Export masks to **COCO/PNG formats** for integration with other annotation pipelines.  
- Add quantitative evaluation (IoU/Dice) against hand-labeled ground truth.  
- Deploy workflow in a robust GPU environment to handle large-scale datasets.  

---

## 📌 Context

This work is part of the **ACCORDS project** on automated characterization of carbon-based nanomaterials.  
The prototype demonstrates that **foundation models like SAM can accelerate annotation of graphene images**, though significant domain-specific adaptation is still needed.
