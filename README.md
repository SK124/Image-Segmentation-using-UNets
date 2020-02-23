### Image-Segmentation-using-UNets ###
* Image segmentation is classfyig every pixels of input image which means our final image will be of similr dimensioin of input,so we cant use normal classifier arcitectures we use like resnet18 or inception beacause it downsamples our images into vector we also need a upsampling path in our case.
* While converting an image into a vector, we already learned the feature mapping of the image so why not use the same mapping to convert it again to image.This is the recipe behind UNet. Use the same feature maps that are used for contraction to expand a vector to a segmented image. This would preserve the structural integrity of the image which would reduce distortion enormously. 
Let’s understand the architecture more briefly.
## Architecture ##
![1_lvXoKMHoPJMKpKK7keZMEA](https://user-images.githubusercontent.com/47039231/75104203-37075a80-562c-11ea-8c80-f8af704e9b28.png)
* This architecture consists of three sections: The downsampling path, The bottleneck, and the upsampling path. The downsampling section is made of many contraction blocks. Each block takes an input applies two 3X3 convolution layers followed by a 2X2 max pooling. The number of kernels or feature maps after each block doubles so that architecture can learn the complex structures effectively. The bottommost layer mediates between the downsampling layer and the upsampling layer. It uses two 3X3 CNN layers followed by 2X2 up convolution layer.
* Importance lies in the upsampling path.It consists of several expansion blocks. Each block passes the input to two 3X3 CNN layers followed by a 2X2 upsampling layer. Also after each block number of feature maps used by convolutional layer get half to maintain symmetry. However, every time the input is also get appended by feature maps of the corresponding contraction layer. This action would ensure that the features that are learned while contracting the image will be used to reconstruct it. The number of expansion(upsampling) blocks is as same as the number of contraction(downsampling) block. After that, the resultant mapping passes through another 3X3 CNN layer with the number of feature maps equal to the number of segments desired.



**Loss function:**
* We are classifying each pixel into one of the classes. The idea is that even in segmentation every pixel have to lie in some category and we just need to make sure that they do. So we just converted a segmentation problem into a multiclass classification one and it performed very well as compared to the traditional loss functions.
loss function i used in my problem:

* def accuracy(input, target):

 
        target = target.squeeze(1)
    
    
        mask = (target != void_code)
    
    
        return (input.argmax(dim=1)[mask]==target[mask]).float().mean()


**Dataset**
* Im using CamVid dataset http://mi.eng.cam.ac.uk/research/projects/VideoRec/CamVid/
* Full Dataset has 32 classes however to reuce complexity im using the important ones,which are 
* codes = array(['Sky', 'Building', 'Pole', 'Road', 'Sidewalk', 'Tree',
    'Sign', 'Fence', 'Car', 'Pedestrian', 'Cyclist', 'Void'])

  
