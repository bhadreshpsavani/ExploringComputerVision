# Vision Transformers Researchpapers:

## 1) ViT:
interprets an **image as a sequence of patches** and process it by a standard Transformer encoder as used in NLP

![vit_architecture](/VisionTransformers/resources/imgs/vit_architecture.png)

#### features:
* First Model to use standard transformer for computer vision

#### Cons:
* requires pre-training on large datasets.
* the simple tokenization of input images fails to model the important local structure such as edges and lines among neighboring pixels, leading to low training sample efficiency
* the redundant attention backbone design of ViT leads to limited feature richness for fixed computation budgets and limited training samples
* the backbone of ViT is not efficient as ResNets,
* yields lowresolution outputs
* ViT is applicable to image classification, **it is challenging to directly adapt it to pixel-level dense predictions** such as object detection and segmentation, because (1) its output feature map is single-scale and low-resolution, and (2) its computational and memory costs are relatively high even for common input image sizes

## 2) T2T-ViT:
Proposals:
1) a layerwise Tokens-to-Token (T2T) transformation to progressively structurize the image to tokens by **recursively aggregating neighboring Tokens into one Token (Tokens-to-Token),** such that local structure represented by surrounding tokens can be modeled and tokens length can be reduced;

    ![t2t_tokenization](/VisionTransformers/resources/imgs/T2T_ViT.png)

    in each Token-to-Token (T2T) step, the tokens output by a transformer layer are reconstructed as an image (restructurization) which is then split into tokens with overlapping (soft split) and finally the surrounding tokens are aggregated together by flattening the split patches. Thus the local structure from surrounding patches is embedded into the tokens to be input into the next transformer layer.By conducting T2T iteratively, the local structure is aggregated into tokens and the length of tokens can be reduced by the aggregation process.


2) an **efficient backbone with a deep-narrow structure** for vision transformer motivated by CNN architecture design after empirical study. The `deepnarrow` architecture design with fewer channels but more layers in ViT brings much better performance


![t2t_architecture](/VisionTransformers/resources/imgs/T2T_architecture.png)

#### Pros:
* more lightweight than the vanilla ViT.
* T2T-ViT can achieve higher performance than DeiT without CNN as teacher model


## 3) Transformer in Transformer:

Regards the local patches (e.g., 16x16) as "visual sentences" and further divide them into smaller patches (e.g., 4x4) as "visual words". 

Inside the TnT Block The inner transformer block is used to model the relationship between visual words for local feature extraction, and the outer transformer block captures the intrinsic information from the sequence of sentences.

![tnt_architecture](/VisionTransformers/resources/imgs/TnT_architecture.png)

#### features:
* Captures more details of image

## 4) PVTv1 : Pyramid Vision Transformers

#### Features:
* Take finegrained image patches(4*4 pixels)
* Progressive reduction of Pyramid to reduce sequence length and computation cost
* Introduce spatial reduction attention

![pvt1_overview](/VisionTransformers/resources/imgs/pv1_v1_overview.png)

**Note: PVT can easily be combined with DETR to build an end-to-end object detection system without convolutions and Handcrafted components such as Dense Anchors and NMS**


![pvt1_architecture](/VisionTransformers/resources/imgs/pvt1_architecture.png)
![SRA](/VisionTransformers/resources/imgs/SRA.png)

#### Pros:
1) A Direct replacement of CNN backbone
2) Gives High Resolution output
3) Support Object Detection, Semantic Segmentation and Instance Segmentation,
4) always produces a global receptive field, which is more suitable for detection and segmentation.

#### Cons:
* treats an image as a sequence of non-overlapping patches,which loses the local continuity of the image to a certain extent
* The position encoding in PVTv1 is fixed-size, which is inflexible for process images of arbitrary size.
* When processing high-resolution input (e.g., shorter side being 800 pixels), the computational complexity is relatively large.

## 5) Swin Transformer: 
replaces fixed size position embedding with relative position biases, and restricts self-attention within shifted windows

## 6) CoaT: 
introduce convolution-like operations into vision Transformers

## 7) LeViT:
introduce convolution-like operations into vision Transformers

## 8) Twins:
combines local attention and global attention mechanisms to obtain stronger feature representation.

## 9) CPVT :
replaces the fixed size position embedding in ViT with conditional position encodings, making it easier to process images of arbitrary resolution.

## 10) CrossViT: 
processes image patches of different sizes via a dual-branch Transformer-

## 11) LocalViT:
incorporates depth-wise convolution into vision Transformers to improve the local continuity of features.

## 12) PVTv2:
Adding three designs,
1) overlapping patch embedding, 
2) convolutional feedforward networks, and 
3) linear complexity attention layers.

![pvt2_improvement](/VisionTransformers/resources/imgs/pvt2_improvement.png)

![LinearSRA](/VisionTransformers/resources/imgs/LinearSRA.png)

#### Pros:
1) obtain more local continuity of images and feature maps
2) process variable-resolution input more flexibly
3) enjoy the same linear complexity as CNN.

## 13) PyramidTNT:

Proposals: Improves TNT baselines by introducing two advanced designs: 
1) **pyramid architecture** (with gradual decreased resolution to extract multi-scale representation)

2) **convolutional stem** (convolutional stem for improving the patchify stem and stable training.)

![tnt_architecture](/VisionTransformers/resources/imgs/TnT_vs_PyramidTnT.png)

### Note:
* Above Architecture can support many other Downstream task because its Backbone Architecture.  