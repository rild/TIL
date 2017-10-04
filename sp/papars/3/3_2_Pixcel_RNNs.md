Pixcel Recurrent Neural Networks

[pdf link @Cornell Uni Lib](https://arxiv.org/abs/1601.06759)

## Conclusion
improvement
-  improve and build upon `deep recurrent neural networks`
  - as generative models
  - for natural images

two-dimensional LSTM layers
- described `novel two-dimensional LSTM layers`
  - the Row LSTM
  - the Diagonal BiLSTM
this scale more easily to larger datasets

Training
`a soft-max layer` in the conditional distributions
- trained to model the raw RGB pixel values
  - treated the pixel values as discrete random variables by using `a soft-max layer` in the conditional distributions

masked convolutions
- employed masked convolutions to allow PixelRNNs
  - to model full dependencies between the color channels

> the PixelRNNs
> significantly improve the state of the art on the MNIST and CIFAR-10 datasets
> provide new benchmarks for generative image modeling on the ImageNet dataset

practically unlimited data available to train on


## Abstract
**a deep neural network**
- sequentially predicts the pixels in an image along *the two spatial dimensions*

- models the discrete probability of the raw pixel values
- encodes the complete set of dependencies in the image

Architectural novelties include
- fast two- dimensional recurrent layers
- an effective use of residual connections in deep recurrent net- works.

## Introduction

### the great advantages
One of the great advantages in generative modeling
- there are practically endless amounts of image data available to learn from


However

estimating the distribution of natural images is extremely challenging.

because images are
- high dimensional
- highly structured


### obstacles in generative modeling
One of the most important obstacles
- building complex and expressive models

trade-off

- tractable and scalable

複雑で多様なモデル, くらいかな

### effective approach
One effective approach
to tractably model a joint distribution of the pixels in the image
- to cast it as **a product of conditional distributions**
  - autoregressive models
  - fully visible neural networks


a highly expressive sequence model is necessary

### a compact, shared parametrization
Recurrent Neural Networks (RNN) are powerful models
- offer a compact, shared parametrization of a series of conditional distributions

- to excel at hard sequence problems

### PixelRNNs
advanced two-dimensional RNNs
- to apply them to large-scale modeling of natural images

composed of up to twelve
- fast two-dimensional Long Short-Term Memory (LSTM) layers
  - the Row LSTM layer
  - the Diagonal BiLSTM layer


The first type is the Row LSTM layer
- where the convolution is applied along each row
  - a similar technique is described in (Stollenga et al., 2015)

The sec- ond type is the Diagonal BiLSTM layer
- where the convolu- tion is applied in a novel fashion along the diagonals of the image

The networks also incorporate `residual connections` (He et al., 2015)
around LSTM layers

this helps with training of the PixelRNN for up to twelve layers of depth.

### PixelCNN
Convolutional Neural Networks (CNN) can also be used
as `sequence model` with a fixed dependency range
- by using Masked convolutions

The PixelCNN architecture
- a fully convolutional network of `fifteen layers`

### pixel values

- pixels as continuous values
- the pixels as discrete values
  - using a multinomial distribution implemented with a simple `soft-max layer`
