# Vision Transformers Researchpapers:

### 1) ViT:
interprets an **image as a sequence of patches** and process it by a standard Transformer encoder as used in NLP

![vit_architecture](/VisionTransformers/AN%20IMAGE%20IS%20WORTH%2016X16%20WORDS/vit_architecture.png)

#### features:
* First Model to use standard transformer for computer vision

#### Cons:
* requires pre-training on large datasets.

### 2) Transformer in Transformer:

Regards the local patches (e.g., 16x16) as "visual sentences" and present to further divide them into smaller patches (e.g., 4x4) as "visual words".

![tnt_architecture](/VisionTransformers/AN%20IMAGE%20IS%20WORTH%2016X16%20WORDS/TnT_architecture.png)

#### features:
* Captures more details of image