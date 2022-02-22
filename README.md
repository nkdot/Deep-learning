# Image translation using CycleGAN

## Model Architecture:

| Hyperparameters                                | Modified U net| Resnet(Model1)  | Resnet(Model2) | Resnet(Model3)  |
 ---------------------------------------------- |:-------------:| ---------------:|:--------------:| ---------------:|
 Random crop,Normalization,Random jittering,Flip| Yes           | Yes             |Yes             | Yes             |
 Encoder in generator                           |8 Conv2D layers(IN, LeakyRelu)|3 Conv2D layers(IN, Relu) |same as Model1|same as Model1|
 Decoder in generator|8 Conv2D Transpose layers (IN, Relu/tanh)|2 Conv2DTranspose layers(IN/Relu)1 Conv2D layer(IN, tanh)|same as Model1|same as Model1|
 Residual blocks	|	|9|	6|	6|
Conv2D layers in Discriminator|5 Conv2D layers(IN, LeakyRelu)|6 Conv2D layers|5 Conv2D layers|5 Conv2D layers|
Padding in discriminator|Zero padding(in last 2 layers)|Padding=same(in all conv2d layers)|Zero padding(in last 2 layers)|Zero padding(in last 2 layers)|
Strides in discriminator|L1,2&3-Strides=(2,2)& (1,1) in L4&5|Strides=(2,2)in all 6 layers|Strides=(2,2)in all 5 layers|L1,2,3-Strides=(2,2) & (1,1) in L4&5|

