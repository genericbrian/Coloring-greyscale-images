![Coloring Black and White Images with Neural Networks](./README_images/coloring-black-and-white-images-with-neural-networks.svg)

---

**A detailed tutorial covering the code in this repository:** ["Coloring Black and White photos with Neural Networks"](https://medium.freecodecamp.org/colorize-b-w-photos-with-a-100-line-neural-network-53d9b4449f8d)

The network is built in four parts and gradually becomes more complex. The first part is the bare minimum to understand the core parts of the network. It's built to color one image. Once I have something to experiment with, I find it easier to add the remaining 80% of the network. 

For the second stage, the Beta version, I start automating the training flow. In the full version, I add features from a pre-trained classifier. The GAN version is not covered in the tutorial. It's an experimental version using some of the emerging best practices in image colorization.

## Alpha Version
This is a great starting point to get a hang of the moving pieces. How an image is transformed into RGB pixel values and later translated into LAB pixel values, [changing the color space](https://ciechanow.ski/color-spaces/). It also builds a core intuition for how the network learns. How the network compares the input with the output and adjusts the network. 

<p align="center"><img src="/README_images/alpha.png?raw=true" width="747px"></p>

In this version, you will see a result in a few minutes. Once you have trained the network, try coloring an image it was not trained on. This will build an intuition for the purpose of the later versions. 

## Beta Version
The network in the beta version is very similar to the alpha version. The difference is that we use more than one image to train the network. I'd recommend running ```top/htop``` and ```nvidia-smi``` to see how different batch sizes affect your computer's memory. 

<p align="center"><img src="/README_images/beta.png?raw=true" width="745px"></p>

For this model, I'd go with a this [cropped celebrity dataset](https://github.com/2014mchidamb/DeepColorization/tree/master/face_images) or [Nvidia's StyleGAN dataset](https://github.com/NVlabs/stylegan). Because the images are very similar, the network can learn basic colorization despite being trivial. To get a feel for the limits of this network, you can try it on this dataset of [diverse images from Unsplash](https://www.floydhub.com/emilwallner/datasets/colornet). If you are on a laptop, I'd run it for a day. If you are using a GPU, train it at least 6 - 12h. 

## Full Version
The full version adds information from a pre-trained classifier. You can think of the information as 20% nature, 30% humans, 30% sky, and 20% brick buildings. It then learns to combine that information with the black and white photo. It gives the network more confidence to color the image. Otherwise, it tends to default to the safest color, brown. 

<p align="center"><img src="/README_images/full.png?raw=true" width="750px"></p>

In the article, I use the [Unsplash dataset](https://www.floydhub.com/emilwallner/datasets/colornet), but in retrospect, I'd choose five to ten categories in the [Imagenet dataset](http://image-net.org/download). You can also go with the [Nvidia's StyleGAN dataset](https://github.com/NVlabs/stylegan) or create a dataset from [Pixabay categories](https://github.com/wanghaodi/PixabaySpider). You'll start getting some results after about 12 - 24 hours on a GPU. 


## GAN Version
The GAN version uses Generative Adversarial Networks to make the coloring more consistent and vibrant. However, the network is a magnitude more complex and requires more computing power to work with. Many of the techniques in this network are inspired by the brilliant work of [Jason Antic](https://github.com/jantic) and his [DeOldify](https://github.com/jantic/DeOldify) coloring network. 

In breif, the generator comes from the [pix2pix model](https://arxiv.org/abs/1611.07004), the discriminators and loss function from the [pix2pixHD model](https://github.com/NVIDIA/pix2pixHD), and a few optimizations from the [Self-Attention GAN](https://arxiv.org/abs/1805.08318). 

<p align="center"><img src="/README_images/gan.png?raw=true" width="747px"></p>




## **Run the code on FloydHub**
[![Run on FloydHub](https://static.floydhub.com/button/button.svg)](https://floydhub.com/run?template=https://github.com/floydhub/colornet-template)

Click this button to open a [Workspace](https://blog.floydhub.com/workspaces/) on [FloydHub](https://www.floydhub.com/?utm_medium=readme&utm_source=colornet&utm_campaign=aug_2018) where you will find the same environment and dataset used for the *Full version*. 

## Acknowledgments
- Thanks to IBM for donating computing power through their PowerAI platform
- The full-model is a reproduction of Baldassarre alt el., 2017. [Code](https://github.com/baldassarreFe/deep-koalarization) [Paper](https://arxiv.org/abs/1712.03400)
- The advanced model is inspired by the [pix2pix](https://arxiv.org/abs/1611.07004), [pix2pixHD](https://github.com/NVIDIA/pix2pixHD), [SA-GAN](https://arxiv.org/abs/1805.08318), and [DeOldify](https://github.com/jantic/DeOldify) models. 
