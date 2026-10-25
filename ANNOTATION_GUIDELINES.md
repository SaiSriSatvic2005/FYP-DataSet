# Annotation Guidelines & Metadata Data Dictionary

This document specifies the annotation schema, phonological transcription guidelines, and validation protocols used in the **FYP-DataSet** multilingual sign language avatar corpus.

---

## 1. Phonological Representation Framework

Signs in this dataset are transcribed using the **Hamburg Notation System (HamNoSys v4.0)**, an International Phonetic Alphabet (IPA) analogue designed specifically for gestural and sign languages. Each sign gesture is decomposed into orthogonal physical parameters:
1. **Hand Configuration**: Base handshape, finger bending, and thumb position.
2. **Hand Orientation**: Extended finger direction vector and palm surface normal.
3. **Location**: Anatomical target relative to the signer's body.
4. **Motion Trajectory**: Direction, curvature, and dynamics of hand movement.
5. **Contact & Bimanual Symmetry**: Interaction between hands or between the dominant hand and body.

---

## 2. Metadata Data Dictionary

### A. ISL Ground Truth Labels (`ISL/isl_ground_truth_labels.csv`)

| Column Name | Data Type | Description | Example Values |
| :--- | :--- | :--- | :--- |
| `video_file` | String | Filename of the associated video clip | `A.mp4`, `About.mp4`, `Accident.mp4` |
| `video_path` | String | Original absolute/relative file path | `ISL_videos/A.mp4` |
| `sigml_file` | String | Corresponding gold-standard SiGML XML filename | `a.sigml`, `about.sigml` |
| `gloss` | String | Plain English semantic sign label | `about`, `above`, `accident` |
| `handshape` | String | Base HamNoSys hand configuration token | `hamflathand`, `hamfinger2`, `hamfist`, `hamfinger2345` |
| `thumb_mod` | String | Thumb placement modifier | `hamthumboutmod`, `hamthumbacrossmod`, `none` |
| `bend_mod` | String | Finger knuckle bend modifier | `hamfingerbendmod`, `hamfingerhookmod`, `none` |
| `ext_finger` | String | Primary 3D pointing direction of extended fingers | `hamextfingeru` (up), `hamextfingerl` (left), `hamextfingerol` |
| `palm_ori` | String | Facing direction of the palm surface normal | `hampalmd` (down), `hampalml` (left), `hampalmu` (up) |
| `location` | String | Anatomical target zone on the body | `hamchest`, `hamchin`, `hamlips`, `hamneutralspace` |
| `contact` | String | Physical contact interaction | `hamtouch`, `hamclose`, `none` |
| `movement` | String | Linear or circular movement trajectory | `hammoveo` (out), `hammoveu` (up), `hamcircleo` |
| `move_mod` | String | Movement magnitude or velocity modifier | `hamlargemod`, `hamsmallmod`, `hamfast`, `none` |
| `repetition` | String | Trajectory repetition attribute | `hamrepeatfromstart`, `hamrepeatcontinueseveral`, `none` |
| `two_handed` | String | Bimanual symmetry flag | `hamsymmlr` (left/right symmetry), `hamparbegin`, `none` |
| `hand_part` | String | Specific contacting hand subpart | `hamfingertip`, `hampalm`, `hampinkyside`, `none` |
| `all_tags` | String | Full raw sequence of HamNoSys XML tags | `hamsymmlr hamflathand hamthumboutmod ...` |

---

### B. DGS Clean Ground Truth (`DGS/dgs_clean_ground_truth.csv`)

| Column Name | Data Type | Description | Example Values |
| :--- | :--- | :--- | :--- |
| `stem` | String | Unique sign identifier stem | `100_JUNGE2`, `1000_WAAGE1A` |
| `video_file` | String | Matched dictionary video clip | `100_JUNGE2.mp4` |
| `sigml_file` | String | Ground-truth DGS SiGML XML file | `100_JUNGE2.sigml` |
| `is_two_handed`| Boolean | True if sign requires two hands | `True`, `False` |
| `symmetry_type`| String | Nature of two-handed coordination | `hamsymmlr`, `hamalternatingmotion`, `none` |
| `base_handshape`| String | Primary hand configuration | `hamflathand`, `hamfist`, `hamfinger2` |
| `extended_finger`| String | Finger orientation vector | `hamextfingeru`, `hamextfingero`, `hamextfingerl` |
| `palm_orientation`| String | Direction the palm faces | `hampalmd`, `hampalml`, `hampalmu` |
| `location` | String | Body location tag | `hamchest`, `hamchin`, `hamforehead` |

---

### C. WLASL Landmark Metadata (`ASL_WLASL/wlasl_landmark_dataset/metadata.csv`)

| Column Name | Data Type | Description |
| :--- | :--- | :--- |
| `video_id` | Integer | WLASL numeric video clip identifier (e.g., `7069`, `7074`) |
| `gloss` | String | English gloss word label (e.g., `book`, `computer`) |
| `handshape` | String | Target HamNoSys handshape class |
| `ext_finger` | String | Target extended finger orientation class |
| `palm_ori` | String | Target palm orientation class |
| `location` | String | Target body location class |
| `movement` | String | Target movement trajectory class |
| `contact` | String | Target contact classification |
| `two_handed` | String | Bimanual symmetry classification |

---

## 3. Landmark Extraction & Normalization Protocol

For the pre-extracted landmark dataset (`ASL_WLASL/wlasl_landmark_dataset/dataset_landmarks.npz`):
1. **Keypoint Schema (177 Dimensions)**:
   - `[0:63]`: Right hand 21 3D landmarks $(x, y, z)$.
   - `[63:126]`: Left hand 21 3D landmarks $(x, y, z)$.
   - `[126:177]`: Upper body 17 3D landmarks $(x, y, z)$ [COCO format].
2. **Chest-Origin Centering**:
   $$\text{Origin} = \frac{\mathbf{P}_{\text{left\_shoulder}} + \mathbf{P}_{\text{right\_shoulder}}}{2}$$
   All coordinates are centered about this anatomical origin so translations across the camera frame do not alter gestures.
3. **Shoulder-Width Scale Normalization**:
   $$\text{Scale} = \|\mathbf{P}_{\text{left\_shoulder}} - \mathbf{P}_{\text{right\_shoulder}}\|_2$$
   $$\mathbf{P}_{\text{normalized}} = \frac{\mathbf{P} - \text{Origin}}{\text{Scale}}$$
   Guarantees invariant feature geometry regardless of signer distance from the camera.
4. **Temporal Resampling**:
   All video gesture sequences are normalized to a uniform length of $T = 150$ frames via edge padding or uniform temporal sampling.

---

## 4. Quality Control & Validation Protocol

* **XML Schema Validation**: Every generated `.sigml` document undergoes strict validation against the SiGML DTD specification to prevent parser crashes.
* **3D Avatar Rendering Test**: All SiGML files were executed through the WebGL CWASA avatar animation engine to guarantee:
  - Zero mesh self-intersections or body clipping.
  - Natural velocity transitions between start, peak gesture, and rest poses.
* **Expert Cross-Verification**: Phonological labels were checked against native sign dictionaries and reference recordings.
