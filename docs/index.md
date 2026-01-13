# NEPHELE DOCUMENTATION PORTAL

<p align="center">
    <img src="assets/nephele_logo_2.png" alt="NEPHELE" width="220"/>
</p>

<p style="text-align: justify; text-justify: inter-word;">
<b>NEPHELE</b> is an intermediate reconstruction module developed within the 
<a href="https://www.echoes-eccch.eu/textailes/">TEXTaiLES</a> toolbox as a dedicated 
3D reconstruction component. It serves as the central bridge between SAM2 segmentation 
and SuGaR-based surface alignment.
</p>

<p style="text-align: justify; text-justify: inter-word;">
NEPHELE transforms segmented multi-view images into a structured 3D Gaussian 
representation. Named after the mythological figure Nephele, symbolizing 
<i>cloud</i> and <i>formation</i>, the module embodies the core principle of Gaussian 
Splatting: representing geometry as a continuous density cloud rather than 
discrete points.
</p>

<p style="text-align: justify; text-justify: inter-word;">
Using SAM2-filtered masks and COLMAP camera parameters, NEPHELE constructs an 
initial Gaussian field where each splat encodes localized surface attributes such 
as position, covariance, opacity, and anisotropy. This cloud-based representation 
provides a smooth and differentiable foundation for SuGaR optimization, enhancing 
reconstruction stability, improving surface consistency across views, and enabling 
efficient convergence toward high-quality 3D models.
</p>

<p align="center">
    <img src="assets/Logo-Textailes-Colour-RGB-Hor.png" alt="TEXTaiLES" width="520"/>
</p>



---

## Citation
If you use this software, please cite it using the following BibTeX entry:

```bibtex
@software{Nephele_TEXTaiLES_2026,
  author  = {{Athena Research Center}},
  title   = {{Nephele: SAM2 + COLMAP + SuGaR pipeline for background-free 3D mesh reconstruction}},
  url     = {https://github.com/TEXTaiLES/SAMplify_SuGaR},
  version = {0.1.0},
  year    = {2025},
  license = {MIT}
}
```

## Third-party citations

```bibtex
@article{ravi2024sam2,
  title={SAM 2: Segment Anything in Images and Videos},
  author={Ravi, Nikhila and Gabeur, Valentin and Hu, Yuan-Ting and Hu, Ronghang and Ryali, Chaitanya and Ma, Tengyu and Khedr, Haitham and R{\"a}dle, Roman and Rolland, Chloe and Gustafson, Laura and Mintun, Eric and Pan, Junting and Alwala, Kalyan Vasudev and Carion, Nicolas and Wu, Chao-Yuan and Girshick, Ross and Doll{\'a}r, Piotr and Feichtenhofer, Christoph},
  journal={arXiv preprint arXiv:2408.00714},
  url={https://arxiv.org/abs/2408.00714},
  year={2024}
}

@inproceedings{Schonberger2016SfM,
  title     = {Structure-from-Motion Revisited},
  author    = {Sch{\"o}nberger, Johannes L. and Frahm, Jan-Michael},
  booktitle = {Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition (CVPR)},
  year      = {2016}
}

@article{guedon2023sugar,
  title   = {SuGaR: Surface-Aligned Gaussian Splatting for Efficient 3D Mesh Reconstruction and High-Quality Mesh Rendering},
  author  = {Gu{\'e}don, Antoine and Lepetit, Vincent},
  journal = {CVPR},
  year    = {2024}
}

@article{kerbl2023gaussiansplatting,
  title   = {3D Gaussian Splatting for Real-Time Radiance Field Rendering},
  author  = {Kerbl, Bernhard and Kopanas, Georgios and Leimk{\"u}hler, Thomas and Drettakis, George},
  journal = {ACM Transactions on Graphics},
  year    = {2023}
}
```


## License
This project is licensed under the MIT License. 




