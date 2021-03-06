# Vision Transformers Researchpapers:

in CNNs, the weights are learned during training but **fixed during testing**; in the self-attention mechanism, the weights are **dynamically computed** based on the similarity or affinity between every pair of tokens

The self-attention operation computes an affinity/similarity that is more computationally demanding than linear filtering in convolution

Lets Go through Vision Transformer based Architectures

## 1) ViT:
interprets an **image as a sequence of patches** and process it by a standard Transformer encoder as used in NLP

![vit_architecture](/VisionTransformers/resources/imgs/vit_architecture.png)

#### features:
* First Model to use standard transformer for computer vision
* In CNNs, the final embedding is usually obtained by averaging the features over all spatial locations while ViT uses the CLS that interacts with patch tokens at every transformer encoder as the final embedding.

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
* each query computes the attention weights with all the input tokens, in PVT, each query only computes the attention with a sub-sampled version of the input tokens. Although its computational complexity in theory is still quadratic

## 5) Swin Transformer: 
replaces fixed size position embedding with relative position biases, and restricts self-attention within shifted windows

Swin Transformer constructs a hierarchical representation
by starting from **small-sized patches (outlined in
gray) and gradually merging neighboring patches** in deeper
Transformer layers.

![SWIN_architecture](/VisionTransformers/resources/imgs/SWIM_Trans_Architecture.png)

#### How it makes self Attention Linear?
Self attention is applied on fixed sized patchess of local window. Local window will always have same size. Basically this local window makes it linear based on number of patches in local window and image dimention.

#### How it makes it more efficieny?
![shifted_window](/VisionTransformers/resources/imgs/shifted_window.png)

Using Shifted Window Attention Mechanism. When self attention is applied on bunch of pixel of the local window in the next transformer block the local window is shifted by half of the local window size so focus on different set of pixels

It tried to **combine adjust set of pixels using self attention layer**. Basically captures more details that makes it more efficient 

![two_swin_blocks](/VisionTransformers/resources/imgs/two_swmsa.png)

This shows two consecutive transformer blocks. Second one is with shifted window

#### Pros:
* Linear Computation Complexity of Self Attention
* captures more details and gives better perfromance

#### Cons:
* The shifted windows may have uneven sizes, The uneven windows result in difficulties when the models are deployed with ONNX or TensorRT

## 6) CoaT: 
introduce convolution-like operations into vision Transformers

a Transformer-based image classifier equipped with **co-scale** and **conv-attentional mechanisms**.

![CoAT Architecture](/VisionTransformers/resources/imgs/CoAT.png)

**co-scale**: a series of highly modularized serial and parallel blocks to enable attention with fine-to-coarse, coarse-to-fine, and cross-scale information on tokenized representations.

![CoAT Attention](/VisionTransformers/resources/imgs/COAT_Attention.png)

**conv-attentional mechanisms**: we devise a conv-attentional mechanism by realizing a relative position embedding formulation in the factorized attention module with an efficient convolution-like implementation.

## 7) LeViT:
replace the uniform structure of a Transformer by a **pyramid with pooling**, similar to the LeNet [11] architecture. Hence we call it LeViT
 
introduce convolution-like operations into vision Transformers

introduce the **attention bias**, a new way to integrate positional information in vision transformers

#### Pros:
* fast inference image classification

## 8) Twins:
combines local attention and global attention mechanisms to obtain stronger feature representation.

It has spatially separable self-attention (SSSA) which consist of,
1. locally-grouped self-attention (LSA), Captures Local/short Distance Information
2. global sub-sampled attention (GSA), Captures Global/Long Distance Information



#### Pros:
* proposed architectures are highly efficient and easy to implement, only involving matrix multiplications that are highly optimized in modern deep learning frameworks

## 9) CPVT :
replaces the fixed size position embedding in ViT with conditional position encodings, making it easier to process images of arbitrary resolution.

![cpvt](/VisionTransformers/resources/imgs/CPVT.png)

CPE is dynamically generated and conditioned on the local neighborhood of the input tokens

#### Pros:
* prevents the model from handling the sequences longer than the longest training sequences
* makes the model not translationinvariant

## 10) CrossViT: 
processes image patches of different sizes via a dual-branch Transformer-

processes small-patch and large-patch tokens with two separate branches of different computational complexity and these tokens are then fused purely by attention multiple times to complement each other.

![crossvit](/VisionTransformers/resources/imgs/CrossViT_Architecture.png)

model is primarily composed of K multiscale transformer encoders where each encoder consists of two branches: 

1) L-Branch: a large (primary) branch that utilizes coarse-grained patch size (Pl) with more transformer encoders and wider embedding dimensions, 
2) S-Branch: a small (complementary) branch that operates at fine-grained patch size (Ps) with fewer encoders and smaller embedding dimensions.

![cross_attention](/VisionTransformers/resources/imgs/cross_attention.png) 

utilize the CLS token at each branch as an agent to exchange information among the patch tokens from the other branch and then back project it to its own branch.

#### Pros:
* Linear Complexity

#### Cons:
* Mainly Build for image classification

## 11) LocalViT:
incorporates depth-wise convolution into vision Transformers to improve the local continuity of features.

It tried to improve FFL of Transformer by replacing with Depthwise convolution and inverted residuals blocks. They claim it helps network to better capture Local Information. 

![LocalVit](/VisionTransformers/resources/imgs/locaVIT.png) 

Note: I didn't gone through it indepth since i thought this paper introduce one simple concept. Lots of experimentation is mention about the choices and expasion ratio in the paper.

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


## 14) ShiftViT:

hints that **the attention mechanism might not be the vital** that makes ViT works

propose to replace the attention layer with a **simple shift operation** in vision transformers. It spatially shifts a small portion of the channels along four directions, and the rest of the channels remain unchanged.

![ShiftViT](/VisionTransformers/resources/imgs/ShiftViT.png)

the proposed building block will first shift a small portion of the channels along four spatial directions, namely **left, right, top, and down**.  After shifting, the
out-of-scope pixels are simply dropped and the vacant pixels
are zero padded. In this work, the shift step is set to 1 pixel

![shift_opera](/VisionTransformers/resources/imgs/shift_oper.png)
In above images second image is after shift operation

As such, the information of neighboring features is explicitly mingled by the shifted channels. Then, the subsequent FFN performs **channel-wise mixing to further fuse the information** from neighbors.

ShiftViT can be also categorized into the pure **MLP architecture**, where the shift operation is viewed as a special token-mixing layer

[ShiftOperation](https://github.com/bhadreshpsavani/ExploringComputerVision/blob/main/notebook/Understanding_Shift_Operation.ipynb)


# Note:
* All of the Above Architecture can support many other Downstream task because its Backbone Architecture.  

General Notes:
**All the information mentioned above is analysed from the official researchpapers**