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


## MPM parameter adjustment
### 1. Jelly (model=ficus_whitebg-trained)
We start from the baseline original simulation parameter settings:
n_grid = 50, substep_dt = 1 × 10⁻⁴, grid_v_damping_scale = 0.9999, and softening = 0.

To better understand the effect of each parameter, we conducted a series of ablation study, including lowering n_grid, reducing substep_dt, adjusting grid_v_damping_scale, and varying softening.

| Parameter |  PSNR  | YouTube video link |
|-----------|:------:|:------------------:|
| **original baseline video**  | – | [▶️](https://www.youtube.com/watch?v=fOy0h40-om0) |
| `n_grid = 10`    | 24.75 | [▶️](https://www.youtube.com/watch?v=UwEIv87cuHM) |
| `n_grid = 25`    | 24.86 | [▶️](https://www.youtube.com/watch?v=8X7lun_OAK8) |
| `n_grid = 40`    | 26.85 | [▶️](https://www.youtube.com/watch?v=_Ok7LFbb3T0) |
| `substep_dt = 7.5 × 10⁻⁵` | 26.59 | [▶️](https://www.youtube.com/watch?v=YVhNPMzcsGU) |
| `substep_dt = 5 × 10⁻⁵` | 25.25 | [▶️](https://www.youtube.com/watch?v=HzeBczXLtnE) |
| `grid_v_damping_scale = 0.9998`  | 26.30 | [▶️](https://www.youtube.com/watch?v=F8cEPdaan4E) |
| `grid_v_damping_scale = 1.0001`  | 23.54 | [▶️](https://www.youtube.com/watch?v=Ht8tbs4Knr0) |
| `softening = 0.2`| 45.79 | [▶️](https://www.youtube.com/watch?v=h9HqoR7MY8w) |
| `softening = 0.4`| 45.58 | [▶️](https://www.youtube.com/watch?v=9XkbadZ3FY4) |

#### Observations and Insights
1. When n_grid is reduced, small oscillations of the branches become less pronounced and appear slightly blocky, but the branches still spring back with elasticity.
2. When substep_dt is reduced, the branches move less, and their rebound seems weaker and softer.
3. When damping is smaller (<1), the movement of branches is smaller and weaker, while when damping is larger than one (>1), the movement of the branches becomes more exaggerated and faster, with increased bouncing and jittering.
4. Adjusting the softening value makes the deformation a little smoother in this jelly model.

### 2. Sand (model=wolf_whitebg-trained)
We start from the baseline original simulation parameter settings:
n_grid = 200, substep_dt = 2 × 10⁻⁵, grid_v_damping_scale = 1, and softening = 0.

To better understand the effect of each parameter, we conducted a series of ablation studies, including lowering n_grid, reducing substep_dt, adjusting grid_v_damping_scale, and varying softening.

| Parameter |  PSNR  | YouTube video link |
|-----------|:------:|:------------------:|
| **original baseline video** | – | [▶️](https://www.youtube.com/watch?v=4XxDa-p0iN4)|
| `n_grid = 180`    | 27.28 | [▶️](https://www.youtube.com/watch?v=B-iviH1Nsx4) |
| `n_grid = 160`    | 25.70 | [▶️](https://www.youtube.com/watch?v=Z8_UHPw8zrE) |
| `n_grid = 100`    | 24.30 | [▶️](https://www.youtube.com/watch?v=XJa7GuWvxGc) |
| `substep_dt = 1.5 × 10⁻⁵` | 31.36 | [▶️](https://www.youtube.com/watch?v=tJDuHR508fg) |
| `substep_dt = 1 × 10⁻⁵` | 28.85 | [▶️](https://www.youtube.com/watch?v=Lr6qJ041jW0) |
| `grid_v_damping_scale = 0.9995`  | 19.08 | [▶️](https://www.youtube.com/watch?v=_rystv6P1O4) |
| `grid_v_damping_scale = 1.0003`  | 42.42 | [▶️](https://www.youtube.com/watch?v=ewKOyCEs6uo) |
| `softening = 0.2`| 42.85 | [▶️](https://www.youtube.com/watch?v=T0yzhlwN4gs) |
| `softening = 0.4`| 42.43 | [▶️](https://www.youtube.com/watch?v=UyZQta7p8aE) |

#### Observations and Insights
1. When n_grid is reduced, the particle resolution becomes lower, and the sand appears more blurry in the output video.
2. When substep_dt is reduced, the wolf turns into sand more slowly, making the collapse look smoother.
3. Smaller damping (<1) slows down the sand collapse, while larger damping (>1) speeds it up, making the collapse look faster. 
4. Adjusting the softening value appears to have little or no visible effect on the simulation outcome in this sand model.

## Key takeaways
The ablation study reveals how key physical parameters influence simulation quality. Reducing n_grid lowers spatial resolution, making the video blurrier. Smaller substep_dt slows motion and increases stability, while changes in grid_v_damping_scale affect how quickly motion fades (<1 dampen movement, >1 amplify movement). In soft materials such as jelly, softening enhances the smoothness of deformation, but has a limited impact on hard materials like sand.

## Bonus
To extend PhysGaussian for unfamiliar materials, we can collect simulation data using known materials with predefined parameters, and train a neural network to map from observed behaviors (e.g., deformation, velocity fields, or rendered videos) to material properties such as elasticity, density, or friction. After training, the model can infer parameters for unfamiliar materials by observing how they behave, enabling PhysGaussian to generalize to novel scenarios without manual tuning.

# Reference
```bibtex
@inproceedings{xie2024physgaussian,
    title     = {Physgaussian: Physics-integrated 3d gaussians for generative dynamics},
    author    = {Xie, Tianyi and Zong, Zeshun and Qiu, Yuxing and Li, Xuan and Feng, Yutao and Yang, Yin and Jiang, Chenfanfu},
    booktitle = {Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition},
    year      = {2024}
}
```
