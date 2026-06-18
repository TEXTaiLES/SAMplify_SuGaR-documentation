
# Running the Backend Pipeline

This page explains how to start the backend services and run the full reconstruction pipeline using the `nefele-training` branch.

The pipeline performs these steps automatically:

1. **SAM2** — interactive mask annotation and generation
2. **COLMAP** — sparse reconstruction and camera pose estimation
3. **SuGaR / PGSR** — Gaussian Splatting optimization and mesh extraction

---

## 1. Start the Persistent Services

From inside the `SAMplify_SuGaR` folder, start the three backend containers:

```bash
docker compose up -d sam2 colmap sugar
```

These containers stay running in the background. You only need to start them once — you can then run the pipeline multiple times without restarting them.

If you are working with **textiles or thin flat surfaces**, use the PGSR service instead of SuGaR:
```bash
docker compose up -d sam2 colmap pgsr
```

Check that all services are up:

```bash
docker compose ps
```

---

## 2. Prepare Your Dataset

Place your `.jpg` images inside:

```
SAM2/data/input/<your_dataset_name>/
```

See **[Dataset Preparation](dataset_preparation.md)** for naming rules, image requirements, and folder structure.

---

## 3. Run the Pipeline

Once the services are running and your images are in place, start the pipeline with:

```bash
scripts/run_pipeline.sh <DATASET_NAME>
```

Replace `<DATASET_NAME>` with the name of the folder you created under `SAM2/data/input/`.

Example:

```bash
scripts/run_pipeline.sh my_garment
```

---

## 4. What the Pipeline Does

### Step 1 — SAM2 Mask Annotation

A browser-based interface opens **locally** at:

```
http://localhost:8092
```

This runs on your own machine — not the hosted version at [nephele.textailes.athenarc.gr](https://nephele.textailes.athenarc.gr). When running the backend pipeline yourself, annotation always happens at `localhost:8092`.

This is the **only manual step**. You click on the image to mark:

- **Left-click** → foreground (the object to keep)
- **Right-click** → background (areas to remove)

After saving your points, SAM2 generates binary masks for all images.  
See [SAM2 GUI Manual](../manual/sam2_gui.md) for detailed instructions.

### Step 2 — Mask Application

Each mask is multiplied with its source image to remove the background. The masked images are written to:

```
SAM2/data/output/<dataset_name>/masked_images/
```

### Step 3 — COLMAP Reconstruction

COLMAP estimates camera positions and builds a sparse 3D point cloud from the masked images. Results go to:

```
output/<dataset_name>/colmap/
├── sparse/
└── dense/
```

### Step 4 — Gaussian Splatting (SuGaR / PGSR)

SuGaR or PGSR initializes a Gaussian field from the COLMAP point cloud and optimizes it across all views. Outputs go to:

```
output/<dataset_name>/sugar/
```

### Step 5 — Mesh Extraction

A clean, background-free `.obj` mesh is extracted using surface sampling and Poisson reconstruction. Final files are written to:

```
output/<dataset_name>/final/
```

---

## 5. Logs

If any step fails, check the log output in your terminal. Detailed logs per component are written to:

```
output/<dataset_name>/logs/
```

---

## 6. Re-running with Existing Prompts

If you have already annotated this dataset before, SAM2 will detect the saved `prompts.json` file and ask whether to **reuse** the existing annotations or **start over**. This saves time when re-running the pipeline on the same dataset.

---

## 7. What You Get

When the pipeline finishes, the following files are available under `output/<dataset_name>/`:

```
output/<dataset_name>/
├── masks/                  # Binary masks for each image (PNG)
├── masked_images/          # Background-removed images used by COLMAP
├── colmap/
│   ├── sparse/             # Camera poses and sparse point cloud
│   └── dense/              # Dense stereo reconstruction
├── sugar/                  # Gaussian Splatting intermediate files
└── final/
    ├── <dataset_name>.obj  # Final 3D mesh
    ├── <dataset_name>.mtl  # Material file
    └── *.png               # Texture maps
```

The `.obj` file is the main output — a clean, background-free 3D mesh ready to open in MeshLab, Blender, or any 3D viewer.

---

## Next Steps

- Use the **[Web UI](nefele_ui.md)** for a browser-based experience with file upload and model selection
