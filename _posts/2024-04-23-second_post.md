# Deformable Convolution (DCN)
## Why to propose DCN  

We know that the purpose of convolution kernel is to extract the features of input objects. Our traditional convolution kernels are usually fixed size and fixed size ,for example, 3x3, 5x5, 7x7. The biggest problem of this convolution kernel is that it has poor adaptability to unknown changes and weak generalization ability. The convolution unit samples the input feature map at a fixed position; The pool layer continuously reduces the size of the feature map; RoI pooling layer produces RoI with limited space.  

The size of receptive field of activation units in the same CNN layer is the same, which is not advisable for deep convolutional neural networks encoding position information, because different positions may correspond to objects with different scales or different deformations, and these layers need to be able to **Automatically adjust the scale or receptive field** Method. For another example, although the target detection effect is good, it depends on the bounding box based on feature extraction, which is not the optimal method, especially for non grid objects.  
  
<div align="center">
  <img src="https://github.com/Dalen980512/dalen.github.io/assets/167549754/4f3d661f-6067-4561-95e2-315f54b0fe48" alt="Image" />
</div>


​(a) Regular sampling grid of standard convolution -green dot. (b) Deformation sampling locations -dark blue dots with enhanced offsets -light blue arrows in deformable convolutions. (c) (d) is a special case of (b), which shows that deformable convolution extends various transformations of scale, anisotropy aspect ratio and rotation.  
  
<div align="center">
  <img src="https://github.com/Dalen980512/dalen.github.io/assets/167549754/edd5091d-900e-4eb0-9791-5466c7e8581f" alt="Image"/>
</div>

The fixed receptive field in standard convolution (a) and the adaptive receptive field in deformable convolution (b) are illustrated with two layers.  

Top: Two active cells on the top feature map, located on two objects of different scales and shapes. Activate from 3 × 3 filter. Middle: the sampling position of the 3 × 3 filter on the front feature map. The other two active units are highlighted. Bottom: the sampling position of the two-stage 3 × 3 filter on the previous feature map.  

**Deformable convolution can be closer to the shape and size of the object when sampling, while standard convolution cannot do this.**  
  
Deformable convolution This kind of deformation does not occur in the convolution core, but occurs in the offset of the original image. After normal convolution, the effect of variable convolution is achieved, that is, normal convolution of feature offset.  

