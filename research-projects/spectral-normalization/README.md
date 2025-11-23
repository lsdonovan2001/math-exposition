# Spectral Normalization for Generative Adversarial Networks  
*A mathematical and empirical study of stabilizing GAN training*  

**Write-Up PDF:** [*Stabilizing GANs: A Case for Spectral Normalization*](paper.pdf)

**Poster PDF:** [*TikZposter — Spectral Normalization Overview*]](poster.pdf)
:contentReference[oaicite:1]{index=1}

---

## Overview

The aim of this project is to provide a rigorous yet accessible analysis of **Spectral Normalization (SN)** as a method for stabilizing training in **Generative Adversarial Networks (GANs)**.  

It blends:

- mathematical theory (optimal transport, Lipschitz continuity, spectral norms)  
- neural network architecture analysis  
- practical algorithm design (power iteration for singular value estimation)  
- empirical experiments comparing SN vs. Gradient Penalty vs. Weight Clipping  
- clear pedagogical communication through a TikZposter  

This is a strong research-style project demonstrating both *technical depth* and *communication clarity*.

---

## Motivation

Early GAN training often places the real and generated distributions on **disjoint supports**, causing the discriminator’s gradient to vanish.  

The write-up (page 1–2) reviews this issue using Binary Cross Entropy and Jensen–Shannon divergence, then motivates the switch to the **Wasserstein-1 distance**.

The poster mirrors this with a clean three-part introduction:

- GAN instability  
- Switching to Wasserstein distance  
- Need for enforcing 1-Lipschitz critics  

---

## Mathematical Foundations

### **Wasserstein–1 Distance and KR Duality**
Pages 2–3 of the write-up provide a historical and mathematical explanation:

- Monge (1781) and the original optimal transport formulation  
- Kantorovich’s relaxation → couplings  
- Wasserstein’s metric on probability spaces  
- **Kantorovich–Rubinstein duality**  
  \[
  W_1(P, Q) = \sup_{\|f\|_{\text{Lip}} \le 1} \,\mathbb{E}_P[f] - \mathbb{E}_Q[f]
  \]

This motivates replacing the discriminator with a **critic** whose gradient must be **bounded by 1 everywhere**.

### **Why Lipschitzness Matters**
Section 3 shows that for a neural network:

\[
\|f\|_{\text{Lip}} \le \prod_{\ell=1}^L \|W_\ell\|_2
\]

- activation functions like ReLU/LeakyReLU are naturally Lipschitz-1  
- therefore, bounding each weight matrix’s spectral norm guarantees global Lipschitz-1  

---

## Spectral Normalization

### **Key Idea**
Replace each weight matrix \(W\) with:

\[
\tilde{W} = \frac{W}{\sigma_{\max}(W)}
\]

where \(\sigma_{\max}(W)\) is the largest singular value.

This enforces:

- global Lipschitz-1 critic  
- no hyperparameters  
- cheap computation via **power iteration**

### **Power Iteration Algorithm**
Section 3.1 of the write-up outlines the iteration:

1. start with random \(v_0\)  
2. alternate \(u_{k+1} = W v_k\) and \(v_{k+1} = W^\top u_{k+1}\)  
3. estimate \( \sigma_{\max}(W) \approx u_k^\top W v_k \)

Only 1–3 iterations are typically needed.

The poster also includes a compressed version of this theory in its “Main Result” pane.

---

## Empirical Results

Figures on pages 6–7 compare **MNIST** training under:

- Weight Clipping  
- Gradient Penalty (WGAN-GP)  
- Spectral Normalization  

### **Generator Loss (page 6, top figure)**

- GP *over-corrects* with highly variable gradients  
- Clipping barely learns  
- SN reduces loss gradually and stably  

### **Critic Loss (page 7, bottom figure)**

- Clipping → underfitting  
- GP → likely overfitting  
- SN → smooth gradient descent and stable critic learning  

### **Conclusion (page 7)**  
SN:

- is computationally cheaper   
- avoids exploding gradients  
- has no hyperparameter tuning  
- directly enforces global Lipschitz continuity  
- is preferred for modern GAN training  

---

## Skills Demonstrated

- Optimal transport theory  
- Probability metrics (JS divergence, KL, Wasserstein-1)  
- Neural network Lipschitz analysis  
- Power iteration and spectral methods  
- Comparison of GAN stabilization techniques  
- Mathematical exposition and research writing  
- TikZposter creation and scientific communication  

---


