# GRA-Net-Grouped-Refinement-Attention-Network-for-Medical-Time-Series-Classification
Code will be released soon..!!

##  Ablation 
### 1. Albation study on the effect of the number of selcted groups (g) on GRA-Net performance and comparison with MedFormer
<p align="center">
  <img src="assets/Group_size_ablation.png" 
       alt="Results on Subject Independent with Baselines"
       width="700">
</p>

**Note** : The revised manuscript will replace the current Table 2 with the modified Table 2 from the above link, which presents ablation results and MedFormer results too. The requested complexity analysis is as follows and will be added to the revised manuscript.

## Complexity Analysis

# Computational Complexity Analysis

## Input Definition

Let the input multivariate time series be defined as:

\[
\mathbf{X} \in \mathbb{R}^{B \times L \times C}
\]

where:
- \( B \) denotes the batch size,  
- \( L \) denotes the sequence length,  
- \( C \) denotes the feature (channel) dimension.  

Let \( g \) be the group size, which partitions the sequence into:

\[
G = \frac{L}{g}
\]

groups.

---

## Channel Importance Attention (CIA)

The total computational complexity of the **Channel Importance Attention (CIA)** module is given by:

\[
\mathcal{O}(B \cdot C \cdot L + B \cdot \frac{C^2}{r})
\]

where:
- \( r \) is the MLP reduction ratio.

---

## Multi-Scale Feature Attention (MSFA)

The total computational complexity of the **Multi-Scale Feature Attention (MSFA)** module is:

\[
\mathcal{O}(B \cdot C \cdot L)
\]

---

## RCA Block Complexity

The **RCA block** combines CIA and MSFA modules. Hence, its overall complexity is:

\[
\begin{aligned}
\mathcal{O}(B \cdot C \cdot L) 
&= \mathcal{O}(B \cdot C \cdot L + B \cdot \frac{C^2}{r}) 
+ \mathcal{O}(B \cdot C \cdot L)
\end{aligned}
\]

---

## Group-wise Attention Complexity

Within each group of length \( g \), the complexity of standard **Scaled Dot-Product Attention** is:

\[
\mathcal{O}(B \cdot g^2 \cdot C)
\]

Summing across all \( G = \frac{L}{g} \) groups, the total complexity becomes:

\[
\frac{L}{g} \times \mathcal{O}(B \cdot g^2 \cdot C)
= \mathcal{O}(B \cdot L \cdot g \cdot C)
\]

By fixing the group size \( g \), the attention complexity scales **linearly** with respect to the sequence length \( L \), effectively avoiding the quadratic \( \mathcal{O}(L^2) \) bottleneck of standard Transformers.

---

## Overall GRA-Net Complexity

By combining all three components, the total computational complexity of **GRA-Net** is:

\[
\mathcal{O}(B \cdot C \cdot L) + \mathcal{O}(B \cdot L \cdot g \cdot C)
\]

Given that:
- \( C \ll L \),  
- \( g \ll L \),  

the overall complexity simplifies to:

\[
\boxed{\mathcal{O}(B \cdot L)}
\]

This demonstrates that **GRA-Net achieves linear-time complexity with respect to the sequence length**, making it highly scalable for long time-series modeling.

---
