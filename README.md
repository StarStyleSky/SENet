# Squeeze-and-Excitation Networks
By Jie Hu<sup>[1]</sup>, Li Shen<sup>[2]</sup>, Gang Sun<sup>[1]</sup>. ([arxiv](https://arxiv.org/))

[Momenta](https://momenta.ai/)<sup>[1]</sup> and University of Oxford<sup>[2]</sup>.

## Approach
<div align="center">
  <img src="https://github.com/hujie-frank/SENet/blob/master/figures/SE-building-block.jpg">
</div>
<p align="center">
  Figure 1: Diagram of a Squeeze-and-Excitation building block.
</p>

<div align="center">
   <img src="https://github.com/hujie-frank/SENet/blob/master/figures/SE-Inception-module.jpg" width="420">
  <img src="https://github.com/hujie-frank/SENet/blob/master/figures/SE-ResNet-module.jpg"  width="420">
</div>
<p align="center">
  Figure 2: Schema of SE-Inception and SE-ResNet modules. 
</p>

## Implementation
In this repository, Squeeze-and-Excitation Networks are implemented by [Caffe](https://github.com/BVLC/caffe).

### Note:
* For efficient training and testing, we combine the consecutive operations ***channel-wise scale*** and ***element-wise summation*** into a single layer **"Axpy"** in the architectures with skip-connections, resulting in considerable memory and time comsuming reduce.

* Additonally, we found that the ***global average pooling*** implemented by cuDNN or BVLC/caffe is much slow on GPU. So we re-implement this operation on GPU and achieve a significant speedup. 

## Trained Models

Table 1. Single crop validation error on ImageNet-1k (center 224x224 crop from resized image with shorter side = 256). The SENet<sup>*</sup> is one of superior models used in [ILSVRC 2017 Image Classification Challenge](http://image-net.org/challenges/LSVRC/2017/index) where we won the 1st place (Team name: [WMW](http://image-net.org/challenges/LSVRC/2017/results)).

| Model | Top-1 | Top-5 | Size | Caffe Model |
|:-:|:-:|:-:|:-:|:-:|
|SE-BN-Inception| 23.62 | 7.04 | 46 M| [GoogleDrive](https://drive.google.com/file/d/0BwHV3BlNKkWlTWRRbDZYbVB2WWc/view?usp=sharing)
|SE-ResNet-50   | 22.37 | 6.36 | 107 M | [GoogleDrive](https://drive.google.com/file/d/0BwHV3BlNKkWlS2QwZHFzM3RjNzg/view?usp=sharing)
|SE-ResNet-101  | 21.75  | 5.72 | 189 M | [GoogleDrive](https://drive.google.com/file/d/0BwHV3BlNKkWlTEg4YmcwQ0FoZFU/view?usp=sharing)
|SE-ResNet-152  | 21.34  | 5.54 | 256 M | [GoogleDrive](https://drive.google.com/file/d/0BwHV3BlNKkWlcFE0Q2NTcWl3WUE/view?usp=sharing)
|SENet<sup>*</sup> | 18.68 | 4.47 | 440 M | [GoogleDrive](https://drive.google.com/file/d/0BwHV3BlNKkWlbTFZbzFTSXBUTUE/view?usp=sharing)

Here we obtain better performances than those reported in the paper.
We re-train all above models on a single GPU server equipped with 8 NVIDIA Titan X cards, 
using a mini-batch of 256 and a initial learning rate of 0.1 with more epoches. 
In our paper, we use large batch-size (1024) and learning rate (0.6). 

## Citation

If you use Squeeze-and-Excitation Networks in your research, please cite the paper:
    
    @article{hu2017,
      title={Squeeze-and-Excitation Networks},
      author={Jie Hu and Li Shen and Gang Sun},
      journal={arXiv preprint arXiv:},
      year={2017}
    }
