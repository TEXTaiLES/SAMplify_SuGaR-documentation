
# Basic Installation

This page describes how to install the SAMplify_SuGaR pipeline along with all required submodules and dependencies.



## 1. Clone the Repository

Begin by cloning the full repository along with its submodules:

```
git clone --recurse-submodules https://github.com/ZachariVaia/SAMplify_SuGaR.git
cd SAMplify_SuGaR
```
If you forgot to include `--recurse-submodules`, run:

```
git submodule update --init --recursive
```

This will download:

* SAM2 (mask generation module)
* SuGaR (Gaussian Splatting module)
* Additional scripts required for the pipeline
