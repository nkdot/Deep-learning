# Image translation using CycleGAN
## Introduction:
CycleGAN was described by Jun-Yan Zhu, et al. in their 2017 paper titled “Unpaired Image-to-Image Translation using Cycle-Consistent Adversarial Networks”. It is an approach for training image-to-image translation models using the Generative Adversarial Network., where an image from input domain Di is transformed into an image of target domain Dt without necessarily having a one-to-one mapping between images from input to target domain in the training set. The need for a paired image in the target domain is eliminated by making a two-step transformation of source domain image - first by trying to map it to target domain and then back to the original image. Mapping the image to target domain is done using a generator network and the quality of this generated image is improved by pitching the generator against a discriminator.
Scope of this work is to translate images using Modified U net & Resnet architecture and compare the results.

## Experiments:
Experimented the following for this work.
+ Transformer with residual blocks 
+ Residual connection with Concatenate instead of Add 
+ Data augmentations (flips, rotations, and crops) 
+ Patch discriminator 
+ Residual connections between Generator and Discriminator 


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

## Model Output:
### Apple to Orange translation:
![]( https://github.com/nkdot/Deep-learning/blob/main/images/apple_to_orange.png "Apple to Orange")
***
### Horse to Zebra translation:
![]( https://github.com/nkdot/Deep-learning/blob/main/images/horse_to_zebra.png "Horse to Zebra")
***
### Summer to Winter translation
![]( https://github.com/nkdot/Deep-learning/blob/main/images/summer_to_winter.png "Summer to Winter")
***
## Results:
+ Modified U net gave better results for apple to orange translation.
+ Model2 with RESNET architecture was comparatively better in translating horse to zebra. 
+ For summer to winter translation, Model 3 with RESNET architecture gave promising results.

##  	Conclusion:
Overall, the results produced by the above models with 40 epochs were very promising and performed better than the cycleGAN model available in tensorflow hub. This is impressive, because paired translations using pix2pix are a kind of fully supervised learning while cycleGAN is not. Main observation was that the model that works well for translating apple to orange may fail on season transfer. Hence some parameters were tweaked to get better results for season transfer. 
 It should be noted that if cycleGAN is implemented for a practical application, proper care must be taken on its limitations. It works well on tasks that involve color or texture changes, like season transfer or photo to painting tasks like style transfer, but for tasks that require substantial geometric changes to the image usually fail. 


## Bibliography:
+ Unpaired Image-to-Image Translation using Cycle-Consistent Adversarial Networks, https://arxiv.org/abs/1703.10593
+ https://towardsdatascience.com/image-to-image-translation-69c10c18f6ff#:~:text=Image%2Dto%2Dimage%20translation%20is%20a%20class%20of%20vision%20and,season%20transfer%20and%20photo%20enhancement.
+ https://machinelearningmastery.com/cyclegan-tutorial-with-keras/
+ The tensorflow implementation of pix2pix, https://github.com/yenchenlin/pix2pix-tensorflow
