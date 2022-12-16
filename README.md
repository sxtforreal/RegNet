### Abstract

This report is an attempt of implementing RegNet on the STL10 dataset[1]. 
RegNet is originally proposed in <RegNet:Self-regulated network for Image Classification>[2]. The main idea is to insert regulator modules (convolutional RNNs) into ResNet architecture, in order to better extract spatio-temporal information and improve the performance on image classification tasks.

### Introduction

ResNet is one of the most outstanding architectures in the field of image classification. In the past, neural networks with deep layers do not guarantee better results. This is because the propagation between layers comes with inevitable loss of information and thus making identical mapping between layers impossible. ResNet solves this issue by manually passing the input to the output via 'shortcuts' and this forces the model to learn residuals instead. With ResNet, deep networks has a great chance of outperforming shallow networks because more layer means more complex features being extracted and learned.

'However, the shortcut connection mechanism makes each block focus on learning its respective residual output, where the inner block information communication is somehow ignored and some reusable information learned from previous blocks tends to be forgotten in later blocks.'(Xu et al., 2022). 

The authors of RegNet argues that ResNet is not effectively learning because the 'shortcut' connection leads to very similar learned features between adjacent layers. Their solution is to have regulator modules in parallel with the ResNet design. Regulators are convolutional RNNs, so they use a memory mechanism to store and pass on the complementary spatio-temporal information from one layer to the other.

In their paper, the result shows that RegNet is able to achieve the same performance as ResNet in a less computationally expensive manner. In this report, we are interested in RegNet's performance on STL10 dataset.


### Method

We insert a Sqeeze and Excitation layer (SELayer) after learned residuals and before adding them with the input in each block. This position of SElayer is the same as the SE-ResNet, suggested by the original paper[3]. 'SELayer adaptively recalibrates channel-wise feature responses by explicitly modelling interdependencies between channels.'(Hu et al., 2018). In theory, SELayer enhances the model performance by emphasizing the important features.

Values of hyper-parameters are suggested by the original paper[2].

The visualization of our RegNet module is available in the repo.

### Data

The STL10 dataset contains 5000 training data and 8000 test data. We further divide the training data into 80% training and 20% validation.

The image size is (96,96) with 3 color channels.

Normalization applied. Normalization is beneficial because it ease the training process and effectively reduce the chance of overfitting.

There are 10 classes:
0:'airplane', 1:'bird', 2:'car', 3:'cat', 4:'deer', 5:'dog', 6:'horse', 7:'monkey', 8:'ship', 9:'truck'

### Reference

1. Adam Coates, Honglak Lee, Andrew Y. Ng An Analysis of Single Layer Networks in Unsupervised Feature Learning AISTATS, 2011.

2. Xu, J., Pan, Y., Pan, X., Hoi, S., Yi, Z., &amp; Xu, Z. (2022). RegNet: Self-regulated network for Image Classification. IEEE Transactions on Neural Networks and Learning Systems, 1–6. https://doi.org/10.1109/tnnls.2022.3158966 

3. Hu, J., Shen, L., &amp; Sun, G. (2018). Squeeze-and-excitation networks. 2018 IEEE/CVF Conference on Computer Vision and Pattern Recognition. https://doi.org/10.1109/cvpr.2018.00745 

4. Squeeze and excitation networks explained with pytorch implementation. Committed towards better future. (2020, July 24). Retrieved December 16, 2022, from https://amaarora.github.io/2020/07/24/SeNet.html 

5. Esposito, P. (2020, May 25). Building a LSTM by hand on pytorch. Medium. Retrieved December 16, 2022, from https://towardsdatascience.com/building-a-lstm-by-hand-on-pytorch-59c02a4ec091 
