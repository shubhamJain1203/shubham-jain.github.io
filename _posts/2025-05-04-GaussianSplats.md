---
layout: default
title: "Gaussian Splatting: A New Era of 3D Rendering"
date: 2025-05-04
categories: [3D, Rendering, Computer Vision]
---

Gaussian Splatting is a novel real-time 3D scene representation and rendering technique that moves away from traditional meshes or even implicit neural fields. Instead, it models a scene as a set of **3D Gaussians**, each with location, scale, opacity, orientation, and color. These Gaussians are then **splatted** (i.e., projected and blended) onto the 2D image plane for rendering.

---

## 🧠 Intuition

Rather than modeling a scene with triangles or voxels, Gaussian Splatting places blobs (3D Gaussians) in space, each contributing color and opacity to a rendered image when projected through a camera. Because of their continuous and differentiable nature, these Gaussians allow for fast optimization and high-quality rendering.

---

## 📐 Mathematical Foundation

A 3D Gaussian function is expressed as:

{% raw %}
$$
G(x) = \alpha \cdot \exp\left( -\frac{1}{2}(x - \mu)^T \Sigma^{-1} (x - \mu) \right)
$$
{% endraw %}

Here,  
- \( \mu \) is the mean (position),  
- \( \Sigma \) is the covariance matrix (shape and orientation),  
- \( \alpha \) controls the transparency.

---

## 🎯 2D Projection

To render the scene, each 3D Gaussian is projected into 2D using the camera’s intrinsic and extrinsic parameters:

{% raw %}
$$
\mu_{2D} = K [R|t] \mu
$$
{% endraw %}

Where:  
- \( K \) is the camera intrinsic matrix  
- \( R \) and \( t \) are the rotation and translation matrices  

The 2D covariance \( \Sigma_{2D} \) is obtained via the Jacobian \( J \) of the projection:

{% raw %}
$$
\Sigma_{2D} = J \Sigma J^T
$$
{% endraw %}

This ensures accurate representation of the Gaussian’s shape and orientation in the image plane.

---

## 🎨 Rendering Pipeline

1. Project Gaussians to 2D.
2. Compute their elliptical 2D footprint.
3. Blend them using alpha compositing with proper visibility ordering.
4. Use additive blending to form the final image.

---

## 🔧 Optimization

The parameters of each Gaussian (position, color, opacity, scale, and orientation) are learned from posed images using gradient descent. Loss is computed between rendered views and ground truth images.

---

## 🖼️ Visuals

Make sure to download and place the following images under `assets/2025-05-04-my-blog/` in your Jekyll project.

### 📌 Overview of Gaussian Splatting  
![Overview](../assets/2025-05-04-my-blog/gaussian-overview.png)  
🔗 [Download](https://research.nvidia.com/labs/toronto-ai/GaussianSplatting/gaussian_splatting_overview.png)

---

### 📌 Pipeline Diagram  
![Pipeline](../assets/2025-05-04-my-blog/pipeline.png)  
🔗 [Download](https://research.nvidia.com/labs/toronto-ai/GaussianSplatting/rendering_pipeline.png)

---

## 📚 References

- [Project Page – Gaussian Splatting for Real-Time Radiance Field Rendering (SIGGRAPH 2023)](https://repo-sam.inria.fr/fungraph/gaussian-splatting/)
- [Official NVIDIA Blog Post](https://developer.nvidia.com/blog/fast-3d-rendering-with-gaussian-splatting/)
- [Original Paper (arXiv)](https://arxiv.org/abs/2306.00988)

---

Gaussian Splatting is a key advancement toward real-time neural rendering and has already demonstrated superior quality and speed compared to NeRF-based methods. Its differentiable formulation and efficient GPU implementation make it a powerful tool in modern 3D scene understanding and generation.
