# Multilingual Sign Language Avatar & Gesture Dataset (ISL, DGS, ASL/WLASL)

[![Release](https://img.shields.io/badge/version-v1.0.0-blue.svg)](https://github.com/SaiSriSatvic2005/FYP-DataSet/releases)
[![License: CC BY-NC 4.0](https://img.shields.io/badge/License-CC_BY--NC_4.0-lightgrey.svg)](LICENSE)
[![Repository](https://img.shields.io/badge/GitHub-FYP--DataSet-success.svg)](https://github.com/SaiSriSatvic2005/FYP-DataSet)

Comprehensive open research dataset accompanying the **Hybrid V7/V8 Multilingual Sign Language Video to 3D Avatar SiGML Animation Pipeline**.

---

## 📌 Public Repository Link

* **GitHub Repository**: [https://github.com/SaiSriSatvic2005/FYP-DataSet](https://github.com/SaiSriSatvic2005/FYP-DataSet)
* **Clone URL**:
  ```bash
  git clone https://github.com/SaiSriSatvic2005/FYP-DataSet.git
  ```

---

## 🚀 Version Details

* **Current Version**: `v1.0.0`
* **Release Date**: October 2026
* **Status**: Initial Public Research Release
* **Changelog**:
  - `ISL`: 711 RGB videos (619 vocabulary + 92 testing), 848 gold-standard SiGML files, 499 phonological ground truth labels, 6 raw uncompressed `.MOV` samples.
  - `DGS`: 500 SignDict dictionary videos, 989 ground-truth SiGML files, 14 reference clips, 989 clean annotation rows.
  - `ASL_WLASL`: 278 WLASL video clips, normalized 3D keypoint tensors ($T=150, D=177$, `.npz`), class mappings, and gloss dictionaries.

---

## 📂 Repository Organization

```
FYP-DataSet/
├── ISL/
│   ├── videos/                         # 711 ISL videos (619 vocabulary + 92 testing clips)
│   ├── raw_sign_videos/Data/           # 6 High-resolution uncompressed .MOV test gestures
│   ├── sigml/                          # 848 Gold-standard SiGML XML gesture definitions + word index
│   ├── isl_dataset_manifest.json       # 619 Paired video-to-SiGML mappings
│   └── isl_ground_truth_labels.csv     # 499 Detailed phonological annotations
├── DGS/
│   ├── videos/                         # 500 SignDict German Sign Language videos (.mp4)
│   ├── sigml/                          # 989 Ground-truth DGS SiGML XML files
│   ├── reference_videos/               # 14 Benchmark reference video clips
│   ├── signdict_500_manifest.json      # SignDict 500 video manifest
│   ├── signdict_500_metadata.csv       # Metadata with source URLs and licenses
│   ├── dgs_clean_ground_truth.csv      # 989 Clean phonological component annotations
│   └── dgs_ground_truth_labels.csv     # 989 Raw HamNoSys tag labels
├── ASL_WLASL/
│   ├── videos/                         # 278 WLASL benchmark video clips (.mp4)
│   ├── wlasl_landmark_dataset/
│   │   ├── dataset_landmarks.npz       # Pre-extracted normalized pose & hand landmarks (T=150, D=177)
│   │   ├── metadata.csv                # 500 Sample annotation table
│   │   ├── nn_class_mappings.json      # Class-to-index neural network mappings
│   │   └── hamnosys_net_v2.pth         # Benchmark phonological classifier weights
│   ├── gloss_to_hamnosys_dict.json     # Gloss-to-HamNoSys phonological token mapping
│   └── cwasa_token_map.json            # CWASA avatar player token definitions
├── ANNOTATION_GUIDELINES.md            # Detailed phonological schema & data dictionary
├── LICENSE                             # CC BY-NC 4.0 & source attribution terms
└── README.md
```

---

## 📊 Dataset Summaries

| Sign Language | Modalities Included | Count & Volume | Primary Annotations |
| :--- | :--- | :--- | :--- |
| **Indian Sign Language (ISL)** | RGB Videos (`.mp4`, `.mov`), SiGML XML, CSV labels, JSON manifests | 1,568 files (251.40 MB) | 499 parsed HamNoSys phonological ground-truth rows |
| **German Sign Language (DGS)** | RGB Videos (`.mp4`), SiGML XML, CSV ground-truth, JSON manifests | 1,507 files (66.66 MB) | 989 clean phonological component annotations |
| **American Sign Language (ASL)** | RGB Videos (`.mp4`), 3D Landmarks (`.npz`), Model checkpoints (`.pth`) | 284 files (125.13 MB) | 500 metadata entries + $T=150, D=177$ landmark arrays |
| **Total** | | **3,361 files (443.19 MB)** | |

---

## 📖 Metadata & Annotation Guidelines

A comprehensive data dictionary defining every column, HamNoSys token definition, and coordinate normalization formula is provided in:
👉 **[ANNOTATION_GUIDELINES.md](ANNOTATION_GUIDELINES.md)**

---

## 🛠️ Pipeline Compatibility

This dataset directly integrates with:
* **HaMeR (Hand Mesh Recovery)** 3D hand pose estimation
* **MediaPipe Holistic** landmark extraction
* **CWASA / SiGML Avatar Synthesizers** (JASigning / SiGML Web Player)

---

## ⚖️ License Information

This dataset collection is released under the **Creative Commons Attribution-NonCommercial 4.0 International (CC BY-NC 4.0)** license for non-commercial academic research reuse.

* Full legal text: See [`LICENSE`](LICENSE).
* Third-party component attributions:
  * **SignDict DGS**: [SignDict.org](https://signdict.org/) (CC BY-SA 3.0 DE).
  * **WLASL Dataset**: Li et al., *"Word-level Deep Sign Language Recognition from Video: A New Large-scale Dataset and Methods Comparison"*, WACV 2020.
  * **ISL Corpus**: Transcribed and curated for the Avatar-Generator-FYP Research Project.

---

## 👥 Authors & Contributors

* **Sai Sri Satvic** ([@SaiSriSatvic2005](https://github.com/SaiSriSatvic2005))
* **Vivin Rakul** ([@vivin888](https://github.com/vivin888))
