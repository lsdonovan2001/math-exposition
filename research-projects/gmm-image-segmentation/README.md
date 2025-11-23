# Image Segmentation via Gaussian Mixture Models  
*A mathematical modeling project using EM clustering*  

This project implements and analyzes **Gaussian Mixture Models (GMMs)** for image segmentation.  
The goal is to automatically separate objects within an image by clustering pixel values, using the Expectation–Maximization (EM) algorithm to estimate mixture parameters.

**Paper:** [Image Segmentation By Means of a Gaussian Mixture Model](paper.pdf)
**Presentation** [Slides for GMM Image Segmentation]{slides.pdf}

---

## Motivation

Image segmentation is central in:

- computer vision  
- medical imaging  
- autonomous driving  
- Photoshop-style editing tools  

Instead of manually “lassoing” regions (as noted in the introduction of the paper), GMMs allow the image to be **algorithmically partitioned** using pixel color statistics.

The paper explains how pixel intensities (or RGB values) can be modeled as samples from a mixture of multivariate Gaussians, each representing a distinct region or object in the image.

---

## Summary of Techniques


### **1. Mixture Model Formulation**
A probability model  
\[
p(y|\theta)=\sum_{k=1}^K \pi_k \, \mathcal{N}(y|\mu_k,\Sigma_k)
\]  
is fit to pixel data.  
The paper explains the constraints \( \sum_k \pi_k = 1 \) and the role of latent cluster variables \(z_n\).

### **2. Expectation–Maximization (EM) Algorithm**
The paper gives a clear derivation of the EM algorithm:

- **E-step:** compute responsibilities  
- **M-step:** maximize the expected log-likelihood  
- uses Jensen’s Inequality to derive the **Evidence Lower Bound (ELBO)**  
- explains why the KL divergence term must vanish at optimum


### **3. Hard vs Soft Clustering**
- Hard: assign each pixel to one Gaussian  
- Soft: use probabilities (responsibilities) — used here because it yields smoother results

---

## Experiments & Results

The paper includes multiple experiments:

### **Football field segmentation (color vs grayscale)**  
(see images on page 5)

- RGB segmentation yields sharper, more meaningful boundaries  
- grayscale segmentation collapses distinct objects together  
- histograms of pixel intensities illustrate why grayscale performs worse

### **Moose and fox images**  
(pages 6–7)

The RGB model successfully separates:

- moose  
- background  
- grass  

The grayscale model struggles with low-contrast areas (e.g., fox’s nose classified as background).

### **Initialization Strategy**
- First model: random initialization → label flipping and inconsistent clustering  
- Second model: **K-Means initialization** (from `sklearn`) → faster and more stable convergence

---

## Discussion & Limitations

We then ask further problems not addressed in the study itself:

- How to incorporate spatial relationships between pixels?  
  (GMMs treat pixels independently.)
- Are there cases where Gaussians are not the optimal mixture choice?  
- How would stricter loss penalties improve medical imaging segmentation?  
- How do autonomous vehicles build rapid 3D segmentation maps?  
- Could ADAM or other optimizers integrate into this workflow?

We highlight awareness of **practical modeling failures**, such as:

- segmentation errors on small/dark regions  
- non-invariance under relabeling  
- poor performance on complex images  
- sensitivity to initialization

---

## 🛠 Skills Demonstrated

- EM algorithm derivation  
- Probability modeling  
- Numerical optimization  
- Image preprocessing (color vs grayscale)  
- Data visualization (histograms, segmented outputs)  
- Mathematical modeling write-ups  
- Experimental methodology  
- Critical analysis of model limitations  

---
