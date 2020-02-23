# Image-Segmentation-using-UNets
In this repo,ill sow you wats image segmentation an
image segmentation is classfyig every pixels of input image
so our final image will be of similr dimensioin of input,icmeans we cant use normal classifier arcitectures we use like resnet18 or inception 
so we ave a speciallized arcitecture called unets 
While converting an image into a vector, we already learned the feature mapping of the image so why not use the same mapping to convert it again to image.
This is the recipe behind UNet. Use the same feature maps that are used for contraction to expand a vector to a segmented image. This would preserve the structural integrity of the image which would reduce distortion enormously. 
Let’s understand the architecture more briefly.
![alt text](https://miro.medium.com/max/2333/1*lvXoKMHoPJMKpKK7keZMEA.png/to/img.png)

The architecture looks like a ‘U’ which justifies its name. This architecture consists of three sections: The contraction, The bottleneck, and the expansion section. The contraction section is made of many contraction blocks. Each block takes an input applies two 3X3 convolution layers followed by a 2X2 max pooling. The number of kernels or feature maps after each block doubles so that architecture can learn the complex structures effectively. The bottommost layer mediates between the contraction layer and the expansion layer. It uses two 3X3 CNN layers followed by 2X2 up convolution layer.
But the heart of this architecture lies in the expansion section. Similar to contraction layer, it also consists of several expansion blocks. Each block passes the input to two 3X3 CNN layers followed by a 2X2 upsampling layer. Also after each block number of feature maps used by convolutional layer get half to maintain symmetry. However, every time the input is also get appended by feature maps of the corresponding contraction layer. This action would ensure that the features that are learned while contracting the image will be used to reconstruct it. The number of expansion blocks is as same as the number of contraction block. After that, the resultant mapping passes through another 3X3 CNN layer with the number of feature maps equal to the number of segments desired.
