# GRA-Net-Grouped-Refinement-Attention-Network-for-Medical-Time-Series-Classification

## Abstract
 Accurate classification of medical time series (MeDTS) is essential for reliable clinical diagnosis but remains challenging due to complex multi-channel temporal dependencies, redundant information, and limited labeled data. While transformer-based models excel in time series analysis, most are designed for forecasting and fail to fully exploit the unique characteristics of MeDTS. We propose GRA-Net **G**rouped **R**efinement **A**ttention **Net**), which captures both local and global temporal patterns while adaptively attending to critical channels and time steps. The model leverages multi-scale and dilated depthwise separable convolutions within a hierarchical attention framework, implemented via the Refined Context Attention block, to extract informative spatial and channel-wise features. A divide-and-group strategy applies attention over smaller token groups, which are further refined through learnable attention and residual connections, enabling efficient modeling. Experimental results show that GRA-Net enhances feature representations, suppresses noise, and consistently improves classification performance across diverse medical time series datasets.
## 1. Proposed Framework
![GRA-Net Architecture](assets/GRA_Netv1-model_architecture_1.drawio.png)

*Figure 1 : Overview of the proposed GRANet architecture.*

![RCA Block](assets/GRA_Netv1-Refined_Attention_block.drawio.png)

*Figure 2 : Overview of the Proposed Refined Context Attention (RCA)Block.*
## 2. Dataset
| **Dataset** | **# Subjects** | **# Samples** | **# Classes** | **Input Channels (C<sub>in</sub>)** | **# Timestamps** |
| :---------- | :------------: | :-----------: | :-----------: | :---------------------------------: | :--------------: |
| APAVA       |       23       |     5,967     |       2       |                  16                 |        256       |
| ADFTD       |       88       |     69,752    |       3       |                  19                 |        256       |
| PTB-XL      |     17,596     |    191,400    |       5       |                  12                 |        250       |

## 3. Results & Analysis
In the subject-independent setup, the training, validation, and test sets are partitioned at the subject level. Each subject, along with all their corresponding samples, is assigned exclusively to one of the three sets based on a predefined ratio or subject IDs. Consequently, samples from the same subject appear only in either the training, validation, or test set. The results for this configuration are reported in Table~\ref{subject_indepdt}. Our method secures the best overall average rank across all six evaluation metrics, outperforming state-of-the-art time series models, including Autoformer ([Wu et al., 2021](https://arxiv.org/abs/2106.13008)), FEDformer ([Zhou et al., 2022](https://arxiv.org/abs/2201.12740)), Informer ([Zhou et al., 2021](https://arxiv.org/abs/2012.07436)), iTransformer ([Liu et al., 2023](https://arxiv.org/abs/2310.06625)), MTST ([Zhang et al., 2024](https://arxiv.org/abs/2401.07390)), 
Nonformer ([Liu et al., 2022](https://arxiv.org/abs/2206.12381)), PatchTST ([Nie et al., 2022](https://arxiv.org/abs/2211.14730)), and the vanilla Transformer ([Vaswani et al., 2017](https://arxiv.org/abs/1706.03762))
.The best performance is achieved when the group parameter $g$ is set to 32 for APAVA, 64 for ADFTD, and 50 for PTB-XL. Notably, for the ADFTD dataset, the F1 score drops to 48.69\% in the subject-independent setup. This stark contrast highlights the increased challenge of the subject-independent scenario, which more closely reflects real-world applications. 

![Results on Subject Independent with Baselines](assets/subject_Ind.png)

