# $DetRF$

PyTorch implementation of paper [DetRF: Detachable Novel Views Synthesis of Dynamic Scenes Using Backdrop-Driven Neural Radiance Fields ](http://arxiv.org/abs/2301.00411)  (AAAI2025).


<div align=center>

<img src="https://github.com/Luciferbobo/D4NeRF/blob/main/demo/main.png" width="680"> 

</div>

<div align=center>
<img src="https://github.com/Luciferbobo/D4NeRF/blob/main/demo/S4.gif" width="210"> 
<img src="https://github.com/Luciferbobo/D4NeRF/blob/main/demo/Kid.gif" width="233"> 
<img src="https://github.com/Luciferbobo/D4NeRF/blob/main/demo/S2.gif" width="210"> 

**Novel View Synthesis**

</div>

## Rendering Results

<div align=center>
  
<img src="https://github.com/Luciferbobo/D4NeRF/blob/main/demo/fig1.png" width="680"> 
  
**Comparison of novel view synthesis**

</div>

## Disentangled Results

<div align=center>

<img src="https://github.com/Luciferbobo/D4NeRF/blob/main/demo/fig2.png" width="680"> 
  
**Comparison on disentangled static background from entire scenes**
  
</div>

<div align=center>
  
<img src="https://github.com/Luciferbobo/D4NeRF/blob/main/demo/scene_ours.gif" width="200"> 
<img src="https://github.com/Luciferbobo/D4NeRF/blob/main/demo/scenedepth_ours.gif" width="200"> 
  
**The Entire Scene**

  
<img src="https://github.com/Luciferbobo/D4NeRF/blob/main/demo/back_ours.gif" width="200"> 
<img src="https://github.com/Luciferbobo/D4NeRF/blob/main/demo/backdepth_ours.gif" width="200"> 
  
**The Decoupled Background**
  
</div>

## Getting Started

### 1. Setup&Dependency
The code is trained with Python == 3.8.8, Pytorch == 1.11.0 and CUDA == 11.3, the dependencies include:

* scikit-image
* opencv
* imageio
* cupy
* kornia
* configargparse

Then download NVIDIA Dynamic and Urban Driving [datasets](https://drive.google.com/file/d/1ahenaRp7eKIHo81BFJBjwBtQj_uH5DrG/view?usp=sharing). The whole file structure should be:
```
D4NeRF
├── configs
├── logs
├── models
├── data
|  └── NVIDIA
|  └── URBAN
|  └── others
...
```

### 2. Train
```
python train.py --config configs/config_Handcart.txt 
```

### 3. Evaluation

The evaluation on NVIDIA dataset focuses on synthesis across different viewpoints, while evaluation on Urban driving dataset aims to interpolate time intervals (frames).

**Evaluation on Urban Driving Scenes**
```
python evaluation_NV.py --config configs/config_Balloon1.txt 
```

**Evaluation on NVIDIA Dynamic Scenes**
```
python evaluation_urban.py --config configs/config_Handcart.txt 
```

### 4. Novel view synthesis
**fixed time and view interpolation:**
```
python view_render.py --config configs/config_Handcart.txt --fixed_time --target_idx 15
```
**time interpolation and fixed view:**
```
python view_render.py --config configs/config_Handcart.txt --fixed_view --target_idx 15
```

**time interpolation and view interpolation:**
```
python view_render.py --config configs/config_Handcart.txt --no_fixed --target_idx 15
```
### 5. Create other datasets
Use [COLMAP](https://github.com/colmap/colmap) to acquire camera poses and intrinsics. Then download [scripts](https://drive.google.com/file/d/1eixFfeqDZ2dwAxpH1XUfSRQYWdff36DI/view?usp=sharing) to obtain the flow and depth estimation models, [RAFT](https://github.com/princeton-vl/RAFT) and [Midas](https://github.com/isl-org/MiDaS). The pre-trained weights have been added to the directory.

**Pose transformation**
```
python save_poses_nerf.py --data_path "/xxx/dense"  #data_path is the path of COLMAP estimation results.
```
**Depth estimation**
```
python run_midas.py --data_path "/xxx/dense" --resize_height 272
```
**Flow estimation**
```
python run_flows_video.py --model models/raft-things.pth --data_path /xxx/dense
```

## Acknowledge
The code is built upon: 

* [NeRF_Pytorch](https://github.com/yenchenlin/nerf-pytorch) 
* [NSFF](https://github.com/zhengqili/Neural-Scene-Flow-Fields) 
* [DyNeRF](https://github.com/gaochen315/DynamicNeRF) 

Thanks for their great work.

