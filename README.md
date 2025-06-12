[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/SdXSjEmH)
# EV-HW3: PhysGaussian

This homework is based on the recent CVPR 2024 paper [PhysGaussian](https://github.com/XPandora/PhysGaussian/tree/main), which introduces a novel framework that integrates physical constraints into 3D Gaussian representations for modeling generative dynamics.

You are **not required** to implement training from scratch. Instead, your task is to set up the environment as specified in the official repository and run the simulation scripts to observe and analyze the results.


## Getting the Code from the Official PhysGaussian GitHub Repository
Download the official codebase using the following command:
```
git clone https://github.com/XPandora/PhysGaussian.git
```


## Environment Setup
Navigate to the "PhysGaussian" directory and follow the instructions under the "Python Environment" section in the official README to set up the environment.


## Running the Simulation
Follow the "Quick Start" section and execute the simulation scripts as instructed. Make sure to verify your outputs and understand the role of physics constraints in the generated dynamics.


## Homework Instructions
Please complete Part 1–2 as described in the [Google Slides](https://docs.google.com/presentation/d/13JcQC12pI8Wb9ZuaVV400HVZr9eUeZvf7gB7Le8FRV4/edit?usp=sharing).

## MPM parameter adjustment
### jelly (model=ficus_whitebg-trained)

| Parameter | PSNR (dB) | YouTube video link |
|-----------|----------:|--------------------|
| **original video**     | – |  – |
| `n_grid = 10`    | 24.75 | [▶️](https://youtu.be/<VIDEO_ID_1>) |
| `n_grid = 25`    | 24.86 | [Watch ↗︎](https://youtu.be/<VIDEO_ID_2>) |
| `n_grid = 40`    | 26.85 | [Watch ↗︎](https://youtu.be/<VIDEO_ID_3>) |
| `substep_dt = 7.5 × 10⁻⁵` | 26.59 | [Watch ↗︎](https://youtu.be/<VIDEO_ID_4>) |
| `substep_dt = 5 × 10⁻⁵` | 25.25 | [Watch ↗︎](https://youtu.be/<VIDEO_ID_5>) |
| `damping = 0.9998`  | 26.30 | [Watch ↗︎](https://youtu.be/<VIDEO_ID_6>) |
| `damping = 1.0001`  | 33.54 | [Watch ↗︎](https://youtu.be/<VIDEO_ID_6>) |
| `softening = 0.2`| 25.60 | [Watch ↗︎](https://youtu.be/<VIDEO_ID_7>) |

## Observation
1. When n_grid is reduced, small oscillations of the branches become less pronounced and appear slightly blocky, yet the branches still spring back with noticeable elasticity.
2. When substep_dt is reduced, the branches move less overall and their rebound feels noticeably weaker and softer.



# Reference
```bibtex
@inproceedings{xie2024physgaussian,
    title     = {Physgaussian: Physics-integrated 3d gaussians for generative dynamics},
    author    = {Xie, Tianyi and Zong, Zeshun and Qiu, Yuxing and Li, Xuan and Feng, Yutao and Yang, Yin and Jiang, Chenfanfu},
    booktitle = {Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition},
    year      = {2024}
}
```
