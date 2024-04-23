# Convolution layer
The convolution layer is composed of a group of filters, which are three-dimensional structures, and their depth is determined by the depth of the input data. A filter can be seen as formed by stacking multiple convolution cores. These filters perform convolution operations on the input data and extract features from the input data. During training, the weights on the filter are initialized with random values, learned according to the training set, and gradually optimized.  

## 1. Convolution operation
- Kernel
    
	- Convolution operation refers to sliding the window of the convolution kernel at a certain interval, multiplying the elements of the convolution kernel at each position with the corresponding elements of the input, and then summing ,sometimes this calculation is called multiplication accumulation addition operation, and saving this result to the corresponding position of the output. The convolution operation is as follows:
   
		 >For an image, the convolution kernel slides through each area of the image from the beginning of the image, from left to right, from top to bottom, with the spacing of one pixel or a specified pixel.  

<div align="center">
  <img src="https://github.com/Dalen980512/dalen.github.io/assets/167549754/ff2dee4e-949a-4a91-891b-212194e54fce" alt="Image"/>
</div>  

- Convolution kernel size（f × f）It can also be changed, such as 1 × 1 、 5 × 5 At this time, you need to adjust the padding size according to the size of the convolution kernel. In general, the size of the convolution kernel is odd ,because we want the convolution kernel to have a center, which is convenient for processing the output. When the size of convolution kernel is odd, the filling size can be determined according to the following formula: $$Padding Size=\frac{f-1}{2}$$
  >Convolution kernel can be understood as weight. Each convolution kernel can be regarded as a &#34;feature extraction operator&#34;, and the filter results obtained by sliding an operator on the original image are called &#34;Feature Map&#34;, and these operators are called &#34;Convolution Kernel&#34;. We do not need to design these operators manually, but use random initialization to get many convolution kernels, and then optimize these convolution kernels through back-propagation to expect better recognition results.  

- Padding

  - Before processing the roll up layer, it is sometimes necessary to fill fixed data ,such as 0, around the input data. The purpose of filling is to adjust the size of the output so that the output dimension is consistent with the input dimension.

    > If you do not adjust the size, the output size will become very small after many layers of convolution. Therefore, in order to reduce the loss of edge information caused by convolution operations, we need to padding.

<div align="center">
  <img src="https://github.com/Dalen980512/dalen.github.io/assets/167549754/dc5ba7ba-de70-454c-90f1-913aad70feb4" alt="Image"/>
</div>  

- Stride

    - That is, the convolutional kernel slides several pixels at a time. In the previous section, we default that the convolution kernel can slide one pixel at a time, but in fact, it can also slide two pixels at a time. The number of pixels per slide is called &#34;step size&#34;, and the calculation process of convolution kernel with step size of 2 is as follows:
  
<div align="center">
  <img src="https://github.com/Dalen980512/dalen.github.io/assets/167549754/06e6ee9d-9e6f-49c8-9d45-18ef01274b40" alt="Image"/>
</div>  

- If you want the output size to be much smaller than the input size, you can take measures to increase the stride. However, the step size of 2 cannot be used frequently, because if the output size becomes too small, even if the convolution kernel parameters are optimized well, a large amount of information will inevitably be lost.
  
- If using **f** Represents the size of the convolution core,**s** Represents the step size,**w** Indicates the width of the picture,**h** Indicates the height of the image, and the output size can be expressed as: $$w_{out}=\frac{w+2\times Padding Size - f}{s} + 1$$  
  $$h_{out}=\frac{h+2\times Padding Size - f}{s} + 1$$

- Filter

  - The convolution kernel is a two-dimensional weight matrix; The filter is a three-dimensional matrix composed of multiple convolution cores.

    > In the case of only one channel -two-dimensional, &#34;convolution kernel&#34; is equivalent to &#34;filter&#34;, and the two concepts are interchangeable

  - The above convolution process does not consider that color images have RGB 3D channels. If RGB channels are considered, then each channel needs a convolution kernel, but when calculating Each channel slides on the corresponding channel The output is obtained by adding the calculation results of the three channels. That is, each filter There is only one output channel.

    > When each convolution kernel in the filter slides on the input data, they will output different processing results. Some of the convolution kernels may have higher weights, and the data of its corresponding channel will also be paid more attention, and the filter will pay more attention to the feature differences of this channel.

- bias
     
    -  Finally, the offset term works with the filter to generate the final output channel.
    
<div align="center">
  <img src="https://github.com/Dalen980512/dalen.github.io/assets/167549754/53f88b0f-cf85-4e90-b456-ae8e594a6a6a" alt="Image"/>
</div> 

Multiple filters work the same way: if there are multiple filters, then we can combine these final single channel outputs into a total output, and its number of channels is equal to the number of filters. After nonlinear processing, this total output is fed into the next convolution layer as input, and then the above process is repeated.  

Therefore, there are four super parameters in this part: number of filters **K** , filter size **F**, step length **S** , zero fill size **P**.


