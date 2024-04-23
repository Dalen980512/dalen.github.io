# Resnet
  
## 1. Put forward reasons  

**(1) Problems caused by stacked networks**  

The traditional idea is that if we stack many layers, maybe we can make the network better.

However, the reality is that it is difficult for the network to converge after stacking the network, and the gradient explosion ,gradient disappearance, impedes the convergence of the network at the beginning, making it difficult for the network to train and obtain appropriate parameters.

**(2) Solve the degradation problem of deep network**

Theoretically, by increasing the number of layers of the network, the network can perform more complex feature extraction and achieve better results. However, the experiment found that the deep network has degenerated, as shown in the following figure (photo source: Resnet&#39;s paper). As the depth of the network increases, the accuracy of the network becomes saturated, and then even drops rapidly. Moreover, this decline is not caused by over fitting, but because adding more layers to the appropriate depth model will lead to higher training errors, thus making it decline.

<div align="center">
  <img src="https://github.com/Dalen980512/dalen.github.io/assets/167549754/1a6f9855-811e-484b-b319-754c39075cac" alt="Image" />
</div>

## 2. Residual structure
In order to solve the above two problems, residual structure came into being.

The schematic diagram is as shown in the figure (picture source: Resnet&#39;s paper): its structure is very similar to the short circuit in the circuit, so it is called short circuit.

<div align="center">
  <img src="https://github.com/Dalen980512/dalen.github.io/assets/167549754/e592b0e7-9c33-41e0-8e3a-efd436839a99" alt="Image" />
</div>

## 3. Residual Structural analysis  
  
Resnet structure hierarchy: Layer -- Block -- Stage -- Network

(1) Layer is the smallest structure. ResNet-18 means that the network has 18 layers.

(2) A block is formed by stacking two or three conv layers. Generally speaking, the double layer block on the left of the following figure is used below 50 layers, and the triple layer block on the right of the following figure is used above 50 layers. The block on the right is called BottleNeck (bottleneck structure).

<div align="center">
  <img src="https://github.com/Dalen980512/dalen.github.io/assets/167549754/626fdd33-ec5a-4a85-a2ee-8785477d21a6" alt="Image" />
</div>

(3) Stage is formed by stacking several blocks. As shown in the yellow circle ,composed of 3 blocks, below:  

<div align="center">
  <img src="https://github.com/Dalen980512/dalen.github.io/assets/167549754/143af57d-45e3-4745-a2c1-0a1bcce72bdc" alt="Image" />
</div>
  
(4) Taking Resnet-50 as an example, as shown in the figure above, the network is composed of two layers ,conv7x7, maxpooling, and four stages ,48 layers in total, before the stage.
