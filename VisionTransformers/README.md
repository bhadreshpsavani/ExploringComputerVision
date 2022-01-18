# Vision Transformers Researchpapers:

### 1) ViT:
interprets an **image as a sequence of patches** and process it by a standard Transformer encoder as used in NLP

![vit_architecture](/VisionTransformers/AN%20IMAGE%20IS%20WORTH%2016X16%20WORDS/vit_architecture.png)

#### features:
* First Model to use standard transformer for computer vision

#### Cons:
* requires pre-training on large datasets.
* the simple tokenization of input images fails to model the important local structure such as edges and lines among neighboring pixels, leading to low training sample efficiency
* the redundant attention backbone design of ViT leads to limited feature richness for fixed computation budgets and limited training samples

### 2) T2T-ViT:
Proposals:
1) a layerwise Tokens-to-Token (T2T) transformation to progressively structurize the image to tokens by **recursively aggregating neighboring Tokens into one Token (Tokens-to-Token),** such that local structure represented by surrounding tokens can be modeled and tokens length can be reduced; 
2) an **efficient backbone with a deep-narrow structure** for vision transformer motivated by CNN architecture design after empirical study.

### 3) Transformer in Transformer:

Regards the local patches (e.g., 16x16) as "visual sentences" and further divide them into smaller patches (e.g., 4x4) as "visual words". 

Inside the TnT Block The inner transformer block is used to model the relationship between visual words for local feature extraction, and the outer transformer block captures the intrinsic information from the sequence of sentences.

![tnt_architecture](/VisionTransformers/AN%20IMAGE%20IS%20WORTH%2016X16%20WORDS/TnT_architecture.png)

#### features:
* Captures more details of image

### 4) PVTv1 : Pyramid Transformers

### 5) PVTv2

### 6) Swin Transformer:

### 7) PyramidTNT:

Proposals: Improves TNT baselines by introducing two advanced designs: 
1) **pyramid architecture** (with gradual decreased resolution to extract multi-scale representation)

2) **convolutional stem** (convolutional stem for improving the patchify stem and stable training.)

![tnt_architecture](/VisionTransformers/AN%20IMAGE%20IS%20WORTH%2016X16%20WORDS/TnT_vs_PyramidTnT.png)