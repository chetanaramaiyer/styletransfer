# styletransfer
This neural style transfer project is hands down my favorite from this semester. This project is based on this paper by Leon A. Gatys, Alex S. Ecker and Matthias Bethge. The goal of this project is to take a pattern image or painting and transfer its style onto a content image (a photograph).  In order to do this, we work with deep neural networks. One of the main takeaways of this project is the idea that neural nets are extremely strong tools, particularly with their power to separate content from style within images. The paper explains how we can use an artificial system that uses neural representations and reconstruct the content and styles of different images.  As the paper states, “The system uses neural representations to separate and recombine content and style of arbitrary images, providing a neural algorithm for the creation of artistic images. Content refers to the actual pixel values in an image. Style refers to a higher level overall architecture of an image.”

## Overview
#### This neural style transfer project is hands down my favorite from this semester. This project is based on this paper by Leon A. Gatys, Alex S. Ecker and Matthias Bethge. The goal of this project is to take a pattern image or painting and transfer its style onto a content image (a photograph).

#### In order to do this, we work with deep neural networks. One of the main takeaways of this project is the idea that neural nets are extremely strong tools, particularly with their power to separate content from style within images. The paper explains how we can use an artificial system that uses neural representations and reconstruct the content and styles of different images.

#### As the paper states, “The system uses neural representations to separate and recombine content and style of arbitrary images, providing a neural algorithm for the creation of artistic images. Content refers to the actual pixel values in an image. Style refers to a higher level overall architecture of an image.”

## How we transfer style:
#### At a high level, the algorithm described in the paper independently separates the content and style of each image (does this using a neural network). As we delve into further convolutional layers of the network, only the higher level features are kept, so the reconstructions of the image include less detail.

#### To get more specific, I used features from the pretrained VGG_19 batchnormed model, as specified in the paper, to extract low level features from the images. The algorithm initially begins with a random noise image. Then, we use gradient descent to create a resulting image. We reconstruct an image's content and its style from various layers in the neural network.

## Loss function:
#### Once content and style features are extracted, we compute our total loss. The function is a weighted sume of two components: the style loss and the content loss. The weights indicate whether the resulting image leans towards the content or style.

## Content Loss:
#### This is measured by squared-error loss between the feature representations output and input image. Essentially, it indicates how the feature map of the result image differs from the feature map of the source image. As described in the paper, we match the content representation on layer conv4_2.

## Style Loss:
#### For style loss, the layers we are interested in are CNN1_1, CNN2_1, CNN3_1, CNN4_1 and CNN5_1 as described in the paper. The style loss is a bit different than content loss because we don’t want style loss to include regional information. Because of this, we use the Gram matrices of the feature maps at each layer. We want to calculate the Gram matrix for the feature map of both the content and style image. The style loss is the weighted Euclidean distance between the two Gram matrices. To get the total style loss, we sum across all layers.

## Final Loss:
#### Once we have the style and content loss, we can define our total loss function which is dependent on weighted hyperparameters α and β. The final loss function indicates how much content or style we would like to see in our resulting image. For example, a lower ratio of α / β would highlight style features more.

