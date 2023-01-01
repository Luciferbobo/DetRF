# $D^4NeRF$

PyTorch implementation of paper **Detachable Novel Views Synthesis of Dynamic Scenes Using Distribution-Driven Neural Radiance Fields**.

![](demo/main.png)

## Abstract

Representing and synthesizing novel views in real-world dynamic scenes from casual monocular videos is a long-standing problem. Existing solutions typically approach dynamic scenes by applying geometry techniques or utilizing temporal information between several adjacent frames without considering the underlying background distribution in the entire scene or the transmittance over the ray dimension, limiting their performance on static and occlusion areas. Our approach **D**istribution-**D**riven neural radiance fields offers high-quality view synthesis and a 3D solution to **D**etach the background from the entire **D**ynamic scene, which is called $D^4$ NeRF. Specifically, it employs a neural representation to capture the scene distribution in the static background and a 6D-input NeRF to represent dynamic objects, respectively. Each ray sample is given an additional occlusion weight to indicate the transmittance lying in the static and dynamic components. We evaluate $D^4$ NeRF on public dynamic scenes and our urban driving scenes acquired from an autonomous-driving dataset. Extensive experiments demonstrate that our approach outperforms previous methods in rendering texture details and motion areas while also producing a clean static background. 

## Rendering Results

![](demo/fig1.png)

![](demo/fig3.png)

## Disentangled Results

![](demo/fig2.png)

## Getting Started

Code will be released soon.

