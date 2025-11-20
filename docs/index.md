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
representation. Named after the mythological figure Νεφέλη, symbolizing 
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
