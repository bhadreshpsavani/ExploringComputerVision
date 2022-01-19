# Advance Computer Vision

Computer Vision Architecture can be basically of two type:
1) Single Stage,
2) Multistage

Most of the Computer Vision Based Architectures has two parts:
1) Backnone Network(For Feature Extraction from Image)
2) Task Specific Head

The recent research is basically focused on making better backbone or task specific head. 

## Instance Segmentation: 

### 1) MaskRCNN : 
Mask R-CNN first employs an object detector Faster R-CNN to predict a bounding-box for each instance. Then for each instance, regions-of-interest (ROIs) are cropped from the networks' feature maps using the ROIAlign operation. To predict the final masks for each instance, a compact fully convolutional network (FCN) (i.e., mask head) is applied to these ROIs to perform foreground/background segmentation.
### 2) PANet :
### 3) TensorMask :
### 4) SOLO :
### 5) Decoupled SOLO :
### 6) SOLOV2 :
### 7) SOLQ :
### 8) CondInst :
### 9) KNet :
### 10) Cascade Mask R-CNN :
### 11) QueryInst :
### 12) HTC :
### 13) CBNet :
### 14) CBNetv2 :
### 15) DetectoRS :

## Object Detection:
1) Single Stage Detectors: SSD, RetinaNet, FCOS, GFL, PolarMask and OneNet,
2) Multistage Detectors: Faster R-CNN, Mask R-CNN, Cascade R-CNN, Sparse R-CNN, DETR and deformable DETR

## Semantic Segmentation

## Denosing

## Super Resolution

## Contour Detection

### Youtube Playlist:
* [Mask-RCNN](https://www.youtube.com/watch?v=Ul25zSysk2A&list=PLkRkKTC6HZMxZrxnHUDYSLiPZxiUUFD2C)
* [Instance and panoptic segmentation](https://www.youtube.com/watch?v=LMZI8DDyltQ)

### Vision Transformation:
* [An image is worth 16x16 words: Transformers for image recognition at scale](https://arxiv.org/abs/2010.11929)
* [Learning transferable visual models from natural language supervision](https://arxiv.org/abs/2103.00020)
* [Swin Transformer: Hierarchical Vision Transformer using ShiftedWindows](https://arxiv.org/abs/2103.14030)
* [End-to-End Semi-Supervised Object Detection with Soft Teacher](https://arxiv.org/abs/2106.09018)

### Blogs:
* [mask-r-cnn](https://viso.ai/deep-learning/mask-r-cnn/)
* [a-simple-guide-to-the-versions-of-the-inception-network](https://towardsdatascience.com/a-simple-guide-to-the-versions-of-the-inception-network-7fc52b863202)
