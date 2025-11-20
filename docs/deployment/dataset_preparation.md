

# Dataset Preparation

This page describes how to prepare your dataset for the SAMplify_SuGaR pipeline.  
A properly structured dataset ensures that SAM2, COLMAP, and SuGaR process the images correctly.


## 1. Dataset Location

All datasets must be placed inside the SAM2 directory:
```

SAM2/
└── data/
    └── input/
        └── <DATASET_NAME>/
```

The folder `<DATASET_NAME>` is chosen by you and will be used later when running the pipeline.

Example:
```

SAM2/data/input/my_object/
```

## 2. Image Requirements

Inside your dataset folder, place your **.jpg** images:
```

SAM2/data/input/<DATASET_NAME>/
├── image1.jpg
├── image2.jpg
├── image3.jpg
└── ...

```

### Image guidelines:
- Format must be **.jpg**
- Images should show the object from multiple viewpoints
- Avoid motion blur or overexposed frames
- Keep the object centered when possible
- Neutral background improves mask accuracy but is not required



## 3. Minimum Dataset Size

For stable reconstruction:

- **100-500 images** recommended  
- **More views = better Gaussian and mesh quality**  
- Avoid duplicate or identical frames  



## 4. Mask Output Directory

After masking with SAM2, the pipeline automatically generates:


```

SAM2/data/output/<DATASET_NAME>/
├── masks/
└── masked_images/

```


You do **not** need to create this manually — the pipeline creates it.



## 5. Verification

Before running the pipeline, make sure:

✔ A folder exists at: 
```
`SAM2/data/input/<DATASET_NAME>/`  

```

✔ It contains at least several `.jpg` images  

✔ File names do not contain spaces (recommended)  


## 6. Next Step

After preparing your dataset, continue to:

**Running the Full Pipeline**
```
(`run_pipeline.md`)

```
