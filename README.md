# Multilingual Sign Language Avatar & Gesture Dataset (ISL, DGS, ASL/WLASL)

Comprehensive dataset collection accompanying the **Hybrid V7/V8 Multilingual Sign Language to Avatar SiGML Animation Pipeline**.

This repository contains raw signing videos, phonologically parsed HamNoSys transcriptions, SiGML XML ground truths, and pre-extracted landmark representations across three sign languages:
1. **Indian Sign Language (ISL)**
2. **German Sign Language (Deutsche Gebärdensprache - DGS)**
3. **American Sign Language (ASL / WLASL)**

---

## Repository Structure

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
└── README.md
```

---

## Dataset Summaries

### 1. Indian Sign Language (ISL)
* **Videos**: 711 `.mp4` recordings captured in consistent frontal lighting and neutral background.
* **SiGML XMLs**: 848 handcrafted `.sigml` XML documents specifying hand configuration (`hamfinger2`, `hamflathand`), thumb mod (`hamthumbacrossmod`), extended finger orientation (`hamextfingeru`), palm orientation (`hampalmdl`), location (`hamchest`, `hamchin`), and movements (`hammoveo`, `hamcirclei`).
* **Annotations (`isl_ground_truth_labels.csv`)**: 499 rows mapping each video to parsed HamNoSys components, contact types, and symmetry flags.

### 2. German Sign Language (DGS)
* **Source**: SignDict DGS open gesture repository (CC BY-SA 3.0 DE).
* **Videos**: 500 dictionary videos covering daily vocabulary.
* **SiGML XMLs**: 989 ground-truth files defining DGS manual and non-manual sign components.
* **Annotations (`dgs_clean_ground_truth.csv`)**: 989 rows providing clean structured phonological attributes for handshape, orientation, and spatial locations.

### 3. American Sign Language (ASL / WLASL)
* **Source**: Word-Level American Sign Language (WLASL) dataset.
* **Videos**: 278 representative video instances across key sign concepts.
* **Landmarks (`dataset_landmarks.npz`)**: Normalized keypoint matrices ($T=150$ frames, $D=177$ dimensions: 63 right hand + 63 left hand + 51 body pose landmarks) scaled relative to shoulder width.

---

## Pipeline Compatibility

This dataset directly integrates with:
* **HaMeR (Hand Mesh Recovery)** 3D hand pose estimation
* **MediaPipe Holistic** landmark extraction
* **CWASA / SiGML Avatar Synthesizers** (JASigning / SiGML Player)

---

## Citation & Attribution

If you utilize this dataset in your research or applications, please cite the respective sources:
* **ISL Corpus & SiGML Collection**: Avatar-Generator-FYP Research Project
* **SignDict DGS**: [SignDict.org](https://signdict.org/) (Licensed under CC BY-SA 3.0 DE)
* **WLASL Dataset**: Li et al., *"Word-level Deep Sign Language Recognition from Video: A New Large-scale Dataset and Methods Comparison"*, WACV 2020.
