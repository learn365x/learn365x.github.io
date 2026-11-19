---
title: "AlexNet: ImageNet Classification with Deep Convolutional Neural Networks"
id: alexnet
source: "Krizhevsky, Sutskever, Hinton, NeurIPS 2012"
year: 2012
status: reading            # planned | reading | done
learned:
tags:
  - domain/cv
  - domain/deep-learning
---

# AlexNet (2012)

**Paper:** Krizhevsky, Sutskever, Hinton. *ImageNet Classification with Deep Convolutional Neural Networks.* NeurIPS 2012.

## Reproduction notes
*Originally written 2026-03-18 as "Reproducing AlexNet in 2026: The Spark of the Deep Learning Revolution" on PapersAI.*

AlexNet (2012) is the "Big Bang" of modern AI. Before this paper, computer vision relied on hand-crafted features. After this paper, the world moved to end-to-end learning. 

In this first project for **PapersAI (PAI)**, I am reproducing the modernized AlexNet architecture using two major frameworks: **PyTorch** and **JAX/Flax**.

### 1. The Challenge: Bridging 2012 and 2026
The original paper was written for a world where GPUs had 3GB of memory. Today, I am reproducing this on an **AMD Ryzen 7 8745HS** using CPU-optimized XLA compilation. 

To maintain feasibility, I am targeting the **CIFAR-10** dataset ($32 \times 32$ images), which requires a "Gentle AlexNet" modification—shrinking the massive $11 \times 11$ kernels to a more appropriate $3 \times 3$ size.

### 2. Architecture Comparison

#### The PyTorch Approach (Object-Oriented)
My PyTorch implementation follows the standard `nn.Module` pattern, leveraging `nn.Sequential` for the feature extractor. I chose to follow the `torchvision` variant, focusing on stability and modularity.

#### The JAX/Flax Approach (Functional)
In JAX, state management is explicit. I used the **Flax Linen** library to define a `@nn.compact` model. This version is particularly interesting because it utilizes the **XLA (Accelerated Linear Algebra)** compiler to squeeze high performance out of my AMD Ryzen CPU.

> **Key Discovery**: While PyTorch uses *Channels-First* (NCHW) by default, JAX prefers *Channels-Last* (NHWC). Handling this transition was a crucial part of ensuring framework parity.

### 3. Implementation Details
The model consists of 5 Convolutional layers and 3 Fully Connected layers. 

| Feature | Original (2012) | My Reproduction (PAI) |
| :--- | :--- | :--- |
| **Input Size** | $224 \times 224$ | $32 \times 32$ (CIFAR-10) |
| **Normalization** | LRN | Modern (None/BatchNorm) |
| **Optimizer** | SGD + Momentum | SGD + StepLR |
| **Hardware** | 2x GTX 580 GPUs | AMD Ryzen 7 CPU (XLA) |

### 4. Visualizing the "Internal Brain"
*(Once I finish training, I will upload the kernel visualizations here!)*

Below is the LRN formula that gave AlexNet its edge in 2012, which I have implemented manually in the JAX version:

$$
b^i_{x,y} = \frac{a^i_{x,y}}{\left(k + \alpha \sum_{j} (a^j_{x,y})^2\right)^\beta}
$$

---

#### 📁 Quick Links
- [View PyTorch Code](https://github.com/PapersAI/PapersAI/blob/main/vision/torch/alexnet.py)
- [View JAX/Flax Code](https://github.com/PapersAI/PapersAI/blob/main/vision/jax/alexnet.py)

**Stay tuned for the training results and accuracy benchmarks!**

## Key points
One section per design choice. Answer the questions first, then check by running code.

### ReLU nonlinearity
*Paper §3.1*

**Questions**

1. ...

**Check** (prediction, then run)

**Summary** (my own words)

**Big picture**


### Training on two GPUs
*Paper §3.2*

**Questions**

1. ...

**Check** (prediction, then run)

**Summary** (my own words)

**Big picture**


### Local response normalization
*Paper §3.3*

**Questions**

1. ...

**Check** (prediction, then run)

**Summary** (my own words)

**Big picture**


### Overlapping pooling
*Paper §3.4*

**Questions**

1. ...

**Check** (prediction, then run)

**Summary** (my own words)

**Big picture**


### Data augmentation
*Paper §4.1*

**Questions**

1. ...

**Check** (prediction, then run)

**Summary** (my own words)

**Big picture**


### Dropout
*Paper §4.2*

**Questions**

1. ...

**Check** (prediction, then run)

**Summary** (my own words)

**Big picture**


### Training details
*Paper §5*

**Questions**

1. ...

**Check** (prediction, then run)

**Summary** (my own words)

**Big picture**

## Mistakes log
- yyyy-mm-dd: I thought ___, actually ___.
