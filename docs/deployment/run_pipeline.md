
# Running the Full Pipeline

This page explains how to execute the complete SAMplify_SuGaR pipeline, which runs:

1. SAM2 – mask annotation and generation  
2. Mask application  
3. COLMAP – sparse & dense reconstruction  
4. SuGaR – Gaussian optimization  
5. Mesh extraction  

Once your dataset is correctly placed inside `SAM2/data/input/<DATASET_NAME>/`, you can run the pipeline with a single command.



## 1. Pipeline Command

From the project root directory:

```
./run_pipeline.sh <dataset_name>
```

Example:


```
./run_pipeline.sh my_object
```
The `<dataset_name>` must match the folder name you created under:

```
SAM2/data/input/<dataset_name>/
```



## 2. What the Pipeline Does

The script performs the following steps automatically:

### **Step 1 — SAM2 Mask Generation**

* Launches SAM2
* Processes each image
* Saves binary masks into:


```
SAM2/data/output/<dataset_name>/masks/
```



### **Step 2 — Mask Application**

The pipeline multiplies each mask with the original image:

```
masked = original_image * mask
```

Masked images are saved into:


```
SAM2/data/output/<dataset_name>/masked_images/
```

These images are used as input to COLMAP.



### **Step 3 — COLMAP Reconstruction**

COLMAP runs:

* Sparse reconstruction
* Pose estimation
* Bundle adjustment
* Dense stereo
* Depth fusion

Results are saved under:

```
output/<dataset_name>/colmap/
 ├── sparse/
 └── dense/
```



### **Step 4 — SuGaR Optimization (Gaussian Splatting)**

The dense cloud from COLMAP initializes the Gaussian field.
SuGaR then optimizes:

* Gaussian positions
* Rotations
* Scales
* Covariance
* Opacity

Outputs appear in:

```
output/<dataset_name>/sugar/
```

### **Step 5 — Mesh Extraction**

A clean, background-free mesh is generated using:

* SDF estimation
* Poisson reconstruction or marching cubes
* Texture projection (optional)

Final meshes are saved in:

```
output/<dataset_name>/final/
```



## 3. Logs and Console Output

During execution you will see:

* Masking progress
* COLMAP reconstruction logs
* SuGaR training progress
* Mesh extraction messages

If any component fails, check:


```
output/<dataset_name>/logs/
```



## 4. Pipeline Completion

When the pipeline finishes successfully, you will have:

* All masks
* Masked images
* COLMAP reconstruction
* SuGaR Gaussian field
* Final mesh model

Stored neatly in the output folder.

## 5. Next Steps

Proceed to the **Manual** section to understand each module:

* SAM2 GUI
* COLMAP processing
* SuGaR Gaussian optimization
* Mesh extraction


