---
layout: post
title: "3D Gaussian Splatting – A New Era in Real-Time 3D Rendering"
date: 2025-05-04
categories: 3d-graphics rendering computer-vision
---

## 📸 Introduction

3D Gaussian Splatting is a revolutionary rendering technique that represents 3D scenes using millions of anisotropic Gaussian ellipsoids. Unlike traditional mesh-based methods, it enables real-time rendering of photorealistic scenes with complex lighting and geometry. This approach is gaining traction in applications like AR/VR, autonomous driving, and immersive 3D content creation.

---

## 🧠 What Is Gaussian Splatting?

In Gaussian Splatting, a scene is modeled as a collection of 3D Gaussians, each defined by:

- **Position** \( \mu \in \mathbb{R}^3 \)
- **Covariance Matrix** \( \Sigma \in \mathbb{R}^{3 \times 3} \)
- **Color** \( c \in \mathbb{R}^3 \)
- **Opacity** \( \alpha \in [0, 1] \)

Each Gaussian represents a translucent ellipsoid in 3D space. When projected onto a 2D image plane, these Gaussians are blended to reconstruct the scene from various viewpoints.

---

## 🧮 Mathematical Formulation

A 3D Gaussian function is expressed as:

$$
G(x) = \alpha \cdot \exp\left( -\frac{1}{2}(x - \mu)^T \Sigma^{-1} (x - \mu) \right)
$$

Here, \( \mu \) is the mean (position), \( \Sigma \) is the covariance matrix (shape and orientation), and \( \alpha \) controls the transparency.

To render the scene, each 3D Gaussian is projected into 2D using the camera's intrinsic and extrinsic parameters:

$$
\mu_{2D} = K [R|t] \mu
$$

Where:

- \( K \) is the camera intrinsic matrix
- \( R \) and \( t \) are the rotation and translation matrices

The 2D covariance \( \Sigma_{2D} \) is obtained via the Jacobian \( J \) of the projection:

$$
\Sigma_{2D} = J \Sigma J^T
$$

This ensures accurate representation of the Gaussian's shape and orientation in the image plane.

---

## 🖼️ Visualizing the Process

Download and save these images into `assets/2025-05-04-my-blog/` and update the links accordingly in production.

1. **Gaussian Splatting Process Overview**  
![Gaussian Splatting Process](/assets/2025-05-04-my-blog/splatting-overview.png)  
Source: [Medium – Aayushma Pant](https://aayushma1.medium.com/from-pixels-to-photorealism-the-art-of-3d-gaussian-splatting-fdcdc1a9ac21)

2. **3D Gaussian Representation**  
![3D Gaussian Representation](/assets/2025-05-04-my-blog/gaussian-representation.png)  
Source: [PixCap Blog](https://pixcap.com/blog/gaussian-splatting)

3. **Rendering Pipeline**  
![Rendering Pipeline](/assets/2025-05-04-my-blog/rendering-pipeline.png)  
Source: [Hugging Face Blog](https://huggingface.co/blog/gaussian-splatting)

---

## ⚙️ Rendering Pipeline

The Gaussian Splatting rendering pipeline involves:

1. **Structure from Motion (SfM):** Estimate camera poses and generate a sparse point cloud from input images.  
2. **Gaussian Initialization:** Assign initial Gaussian parameters to each point.  
3. **Optimization:** Refine Gaussian parameters by minimizing the difference between rendered and ground truth images using stochastic gradient descent.  
4. **Rasterization:** Project Gaussians into 2D, sort by depth, and blend using alpha compositing.

This process enables real-time rendering of complex scenes with high fidelity.

---

## 🚀 Applications

Gaussian Splatting is transforming various fields:

- **AR/VR:** Realistic scene reconstruction for immersive experiences.  
- **Autonomous Driving:** High-fidelity environment modeling for simulation and training.  
- **3D Content Creation:** Efficient generation of detailed 3D models from images or videos.

Its ability to handle complex geometries and lighting conditions makes it a valuable tool in modern computer graphics.

---

## 📚 References

- [Wikipedia: Gaussian Splatting](https://en.wikipedia.org/wiki/Gaussian_splatting)  
- [Hugging Face Blog](https://huggingface.co/blog/gaussian-splatting)  
- [The Verge](https://www.theverge.com/2025/1/19/24345491/gaussian-splats-3d-scanning-scaniverse-niantic)  
- [PixCap Blog](https://pixcap.com/blog/gaussian-splatting)

---

*Feel free to customize this post further or add hands-on experiments or code demos!*
