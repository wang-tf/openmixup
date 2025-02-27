# Model Zoo of Supervised Learning

**OpenMixup provides mixup benchmarks on supervised learning on various tasks. Configs, experiment results, and training logs will be updated as soon as possible. More mixup variants will be supported!**

Now, we have supported 13 popular mixup methods! Notice that * denotes open-source arXiv pre-prints reproduced by us, and 📖 denotes original results reproduced by official implementations. We modified the original AttentiveMix by using pre-trained R-18 (or R-50) and sampling $\lambda$ from $\Beta(\alpha,8)$ as *AttentiveMix+*, which yields better performances. Moreover, you can summarize experiment results (JSON files) by tools in `openmixup/tools/summary/`.

<details open>
<summary>Supported sample mixing policies</summary>

- [X] [Mixup [ICLR'2018]](https://arxiv.org/abs/1710.09412)
- [X] [CutMix [ICCV'2019]](https://arxiv.org/abs/1905.04899)
- [X] [ManifoldMix [ICML'2019]](https://arxiv.org/abs/1806.05236)
- [X] [FMix [ArXiv'2020]](https://arxiv.org/abs/2002.12047)
- [X] [AttentiveMix [ICASSP'2020]](https://arxiv.org/abs/2003.13048)
- [X] [SmoothMix [CVPRW'2020]](https://openaccess.thecvf.com/content_CVPRW_2020/papers/w45/Lee_SmoothMix_A_Simple_Yet_Effective_Data_Augmentation_to_Train_Robust_CVPRW_2020_paper.pdf)
- [X] [SaliencyMix [ICLR'2021]](https://arxiv.org/abs/1710.09412)
- [X] [PuzzleMix [ICML'2020]](https://arxiv.org/abs/2009.06962)
- [ ] [Co-Mixup [ICLR'2021]](https://openreview.net/forum?id=gvxJzw8kW4b)
- [X] [GridMix [Pattern Recognition'2021]](https://www.sciencedirect.com/science/article/pii/S0031320320303976)
- [ ] [SuperMix [CVPR'2021]](https://arxiv.org/abs/2003.05034)
- [X] [ResizeMix [ArXiv'2020]](https://arxiv.org/abs/2012.11101)
- [ ] [AlignMix [CVPR'2022]](https://arxiv.org/abs/2103.15375)
- [X] [AutoMix [ECCV'2022]](https://arxiv.org/abs/2103.13027)
- [X] [SAMix [ArXiv'2021]](https://arxiv.org/abs/2111.15454)
- [ ] [RecursiveMix [ArXiv'2022]](https://arxiv.org/abs/2203.06844)

</details>

<details open>
<summary>Supported label mixing policies</summary>

- [ ] [Saliency Grafting [AAAI'2022]](https://arxiv.org/abs/2112.08796)
- [ ] [TransMix [CVPR'2022]](https://arxiv.org/abs/2111.09833)
- [X] [DecoupleMix [ArXiv'2022]](https://arxiv.org/abs/2203.10761)
- [ ] [TokenMix [ECCV'2022]](https://arxiv.org/abs/2207.08409)

</details>

## ImageNet Benchmarks

We provide three popular benchmarks on ImageNet-1k based on various network architectures. We also provide results on Tiny-ImageNet for fast experiments. The **median** of top-1 accuracy in the last 5/10 training epochs for 100/300 epochs is reported for ResNet variants, and the **best** top-1 accuracy is reported for Transformer architectures.

### **PyTorch-style Training Settings on ImageNet-1k**

These benchmarks follow [PyTorch-style](https://arxiv.org/abs/2110.00476) settings, training 100 and 300 epochs from stretch based on ResNet variants on [ImageNet-1k](http://www.image-net.org/challenges/LSVRC/2012/).

**Note**

* Please refer to config files for experiment details: [various mixups](https://github.com/Westlake-AI/openmixup/tree/main/configs/classification/imagenet/mixups/basic/), [AutoMix](https://github.com/Westlake-AI/openmixup/tree/main/configs/classification/imagenet/automix/basic/), [SAMix](https://github.com/Westlake-AI/openmixup/tree/main/configs/classification/imagenet/samix/basic/). As for config files of [various mixups](https://github.com/Westlake-AI/openmixup/tree/main/configs/classification/imagenet/mixups/basic/), please modify `max_epochs` and `mix_mode` in `auto_train_mixups.py` to generate configs and bash scripts.
* Since ResNet-18 might be under-fitted on ImageNet-1k, we adopt $\alpha=0.2$ for some cutting-based mixups (CutMix, SaliencyMix, FMix, ResizeMix) based on ResNet-18.
* Notice that 📖 denotes original results reproduced by official implementations.

| Backbones     |  $Beta$  |  ResNet-18 |  ResNet-34 |  ResNet-50 | ResNet-101 | ResNeXt-101 |
|---------------|:--------:|:----------:|:----------:|:----------:|:----------:|:-----------:|
| Epochs        | $\alpha$ | 100 epochs | 100 epochs | 100 epochs | 100 epochs |  100 epochs |
| Vanilla       |     -    |    70.04   |    73.85   |    76.83   |    78.18   |    78.71    |
| MixUp         |    0.2   |    69.98   |    73.97   |    77.12   |    78.97   |    79.98    |
| CutMix        |     1    |    68.95   |    73.58   |    77.17   |    78.96   |    80.42    |
| ManifoldMix   |    0.2   |    69.98   |    73.98   |    77.01   |    79.02   |    79.93    |
| SaliencyMix   |     1    |    69.16   |    73.56   |    77.14   |    79.32   |    80.27    |
| AttentiveMix+ |     2    |    68.57   |      -     |    77.28   |      -     |      -      |
| FMix*         |     1    |    69.96   |    74.08   |    77.19   |    79.09   |    80.06    |
| PuzzleMix     |     1    |    70.12   |    74.26   |    77.54   |    79.43   |    80.53    |
| Co-Mixup📖     |     2    |      -     |      -     |    77.60   |      -     |      -      |
| SuperMix📖     |     2    |      -     |      -     |    77.63   |      -     |      -      |
| ResizeMix*    |     1    |    69.50   |    73.88   |    77.42   |    79.27   |    80.55    |
| AlignMix📖     |     2    |      -     |      -     |    78.00   |      -     |      -      |
| Grafting📖     |     1    |      -     |      -     |    77.74   |      -     |      -      |
| AutoMix       |     2    |    70.50   |    74.52   |    77.91   |    79.87   |    80.89    |
| SAMix*        |     2    |    70.83   |    74.95   |    78.06   |    80.05   |    80.98    |

| Backbones   |  $Beta$  |  ResNet-18 |  ResNet-34 |  ResNet-50 | ResNet-101 |
|-------------|:--------:|:----------:|:----------:|:----------:|:----------:|
| Epochs      | $\alpha$ | 300 epochs | 300 epochs | 300 epochs | 300 epochs |
| Vanilla     |     -    |    71.83   |    75.29   |    77.35   |    78.91   |
| MixUp       |    0.2   |    71.72   |    75.73   |    78.44   |    80.60   |
| CutMix      |     1    |    71.01   |    75.16   |    78.69   |    80.59   |
| ManifoldMix |    0.2   |    71.73   |    75.44   |    78.21   |    80.64   |
| SaliencyMix |     1    |    70.21   |    75.01   |    78.46   |    80.45   |
| FMix*       |     1    |    70.30   |    75.12   |    78.51   |    80.20   |
| PuzzleMix   |     1    |    71.64   |    75.84   |    78.86   |    80.67   |
| ResizeMix*  |     1    |    71.32   |    75.64   |    78.91   |    80.52   |
| AlignMix📖   |     2    |      -     |      -     |    79.32   |      -     |
| AutoMix     |     2    |    72.05   |    76.10   |    79.25   |    80.98   |
| SAMix*      |     2    |    72.27   |    76.28   |    79.39   |    81.10   |

### **Timm RSB A2/A3 Training Settings on ImageNet-1k**

These benchmarks follow [timm](https://github.com/rwightman/pytorch-image-models) [RSB A2/A3](https://arxiv.org/abs/2110.00476) settings based on ResNet-50, EfficientNet-B0, and MobileNet.V2. Training 300/100 epochs with the BCE loss on ImageNet-1k, RSB A3 is a fast training setting while RSB A2 can exploit the full representation ability of ConvNets.

**Note**

* Please refer to config files for experiment details: [RSB A3](https://github.com/Westlake-AI/openmixup/tree/main/configs/classification/imagenet/mixups/rsb_a3/) and [RSB A2](https://github.com/Westlake-AI/openmixup/tree/main/configs/classification/imagenet/mixups/rsb_a2/). You can modify `max_epochs` and `mix_mode` in `auto_train_mixups.py` to generate configs and bash scripts for various mixups.
* Notice that the [RSB](https://arxiv.org/abs/2110.00476) settings employ Mixup with $\alpha=0.1$ and CutMix with $\alpha=1.0$. We report the **median** of top-1 accuracy in the last 5/10 training epochs for 100/300 epochs.

| Backbones     |  $Beta$  | ResNet-50 | ResNet-50 | Eff-B0 | Eff-B0 | Mob.V2 1x | Mob.V2 1x |
|---------------|:--------:|:---------:|:---------:|:------:|:------:|:---------:|:---------:|
| Settings      | $\alpha$ |     A3    |     A2    |   A3   |   A2   |     A3    |     A2    |
| RSB           |  0.1, 1  |   78.08   |   79.80   |  74.02 |  77.26 |   69.86   |   72.87   |
| MixUp         |    0.2   |   77.66   |           |  73.87 |  77.19 |   70.17   |   72.78   |
| CutMix        |    0.2   |   77.62   |   79.38   |  73.46 |  77.24 |   69.62   |   72.23   |
| ManifoldMix   |    0.2   |   77.78   |   79.47   |  73.83 |  77.22 |   70.05   |   72.34   |
| AttentiveMix+ |     2    |   77.46   |   79.34   |  72.16 |  75.95 |   67.32   |   70.30   |
| SaliencyMix   |    0.2   |   77.93   |   79.42   |  73.42 |  77.67 |   69.69   |   72.07   |
| FMix*         |    0.2   |   77.76   |   79.05   |  73.71 |  77.33 |   70.10   |   72.79   |
| PuzzleMix     |     1    |   78.02   |   79.78   |  74.10 |  77.35 |   70.04   |   72.85   |
| ResizeMix*    |     1    |   77.85   |   79.74   |  73.67 |  77.27 |   69.94   |   72.50   |
| AutoMix       |     2    |   78.44   |           |  74.61 |  77.58 |   71.16   |   73.19   |
| SAMix         |     2    |   78.64   |           |  75.28 |  77.69 |   71.24   |   73.42   |

### **DeiT Training Settings on ImageNet-1k**

Since recently proposed transformer-based architectures adopt mixups as parts of essential augmentations, these benchmarks follow [DeiT](https://arxiv.org/abs/2012.12877) settings based on DeiT-Small, Swin-Tiny, and ConvNeXt-Tiny on ImageNet-1k.

**Note**

* Please refer to config files of various mixups for experiment details: [DeiT](https://github.com/Westlake-AI/openmixup/tree/main/configs/classification/imagenet/mixups/deit/), [Swin](https://github.com/Westlake-AI/openmixup/tree/main/configs/classification/imagenet/mixups/swin/), [ConvNeXt](https://github.com/Westlake-AI/openmixup/tree/main/configs/classification/imagenet/mixups/convnext/). You can modify `max_epochs` and `mix_mode` in `auto_train_mixups.py` to generate configs and bash scripts for various mixups.
* Notice that the [DeiT](https://arxiv.org/abs/2012.12877) setting employs Mixup with $\alpha=0.8$ and CutMix with $\alpha=1.0$.
* Notice that the performances of transformer-based architectures are more difficult to reproduce than ResNet variants, and the mean of the **best** performance in 3 trials is reported as their original paper. Notice that 📖 denotes original results reproduced by official implementations.

| Methods       | $\alpha$ | DeiT-Small | Swin-Tiny | ConvNeXt-Tiny |
|---------------|:--------:|:----------:|:---------:|:-------------:|
| Vanilla       |     -    |    75.66   |   80.21   |     79.22     |
| DeiT          |  0.8, 1  |    79.80   |   81.20   |     82.10     |
| MixUp         |    0.2   |    77.72   |   81.01   |     80.88     |
| CutMix        |    0.2   |    80.13   |   81.23   |     81.57     |
| ManifoldMix   |    0.2   |      -     |     -     |     80.57     |
| AttentiveMix+ |     2    |    80.32   |   81.29   |     81.14     |
| SaliencyMix   |    0.2   |    79.88   |   81.37   |     81.33     |
| PuzzleMix     |     1    |    80.45   |   81.47   |     81.48     |
| FMix*         |    0.2   |    77.37   |   79.60   |     81.04     |
| ResizeMix*    |     1    |    78.61   |   81.36   |     81.64     |
| TransMix📖     |  0.8, 1  |    80.70   |   81.80   |       -       |
| TokenMix📖     |  0.8, 1  |    80.80   |   81.60   |       -       |
| AutoMix       |     2    |    80.78   |   81.80   |     82.28     |
| SAMix*        |     2    |    80.94   |   81.87   |     82.35     |

### **Tiny-ImageNet Dataset**

This benchmark largely follows [PuzzleMix](https://arxiv.org/abs/2009.06962) settings. All compared methods adopt ResNet-18 and ResNeXt-50 (32x4d) architectures training 400 epochs on [Tiny-ImageNet](https://www.kaggle.com/c/tiny-imagenet). The training and testing image size is 64 (no CenterCrop in testing). We search $\alpha$ in $Beta(\alpha, \alpha)$ for all compared methods.

**Note**

* Please refer to config files for experiment details: [various mixups](https://github.com/Westlake-AI/openmixup/tree/main/configs/classification/tiny_imagenet/mixups/), [AutoMix](https://github.com/Westlake-AI/openmixup/tree/main/configs/classification/tiny_imagenet/automix/), [SAMix](https://github.com/Westlake-AI/openmixup/tree/main/configs/classification/tiny_imagenet/samix/). As for config files of various mixups, please modify `max_epochs` and `mix_mode` in `auto_train_mixups.py` to generate configs and bash scripts.
* Notice that 📖 denotes original results reproduced by official implementations.

| Backbones     | $\alpha$ | ResNet-18 | ResNeXt-50 |
|---------------|:--------:|:---------:|:----------:|
| Vanilla       |     -    |   61.68   |    65.04   |
| MixUp         |     1    |   63.86   |    66.36   |
| CutMix        |     1    |   65.53   |    66.47   |
| ManifoldMix   |    0.2   |   64.15   |    67.30   |
| SmoothMix     |    0.2   |   66.65   |    69.65   |
| SaliencyMix   |     1    |   64.60   |    66.55   |
| AttentiveMix+ |     2    |   64.85   |    67.42   |
| FMix*         |     1    |   63.47   |    65.08   |
| PuzzleMix     |     1    |   65.81   |    67.83   |
| Co-Mixup📖    |     2    |   65.92   |    68.02   |
| ResizeMix*    |     1    |   63.74   |    65.87   |
| GridMix       |    0.2   |   65.14   |    66.53   |
| Grafting📖    |     1    |   64.84   |      -     |
| AlignMix📖    |     2    |   66.87   |      -     |
| AutoMix       |     2    |   67.33   |    70.72   |
| SAMix*        |     2    |   68.89   |    72.18   |


## CIFAR-10/100 Benchmarks

CIFAR benchmarks based on ResNet variants. We report the **median** of top-1 accuracy in the last 10 training epochs.

### **CIFAR-10 Dataset**

These benchmarks follow CutMix settings, training 200/400/800/1200 epochs from stretch based on the CIFAR version of ResNet variants on [CIFAR-10](https://www.cs.toronto.edu/~kriz/cifar.html).

**Note**

* Please refer to config files of [CIFAR-10](https://github.com/Westlake-AI/openmixup/tree/main/configs/classification/cifar10/) for experiment details. You can modify `max_epochs` and `mix_mode` in `auto_train_mixups.py` to generate configs and bash scripts for various mixups.
* Notice that 📖 denotes original results reproduced by official implementations.

| Backbones     |  $Beta$   |  ResNet-18 |  ResNet-18 |  ResNet-18 |  ResNet-18  |
|---------------|:---------:|:----------:|:----------:|:----------:|:-----------:|
| Epochs        |  $\alpha$ | 200 epochs | 400 epochs | 800 epochs | 1200 epochs |
| Vanilla       |     -     |    94.87   |    95.10   |    95.50   |    95.59    |
| MixUp         |     1     |    95.70   |    96.55   |    96.62   |    96.84    |
| CutMix        |    0.2    |    96.11   |    96.13   |    96.68   |    96.56    |
| ManifoldMix   |     2     |    96.04   |    96.57   |    96.71   |    97.02    |
| SmoothMix     |    0.5    |    95.29   |    95.88   |    96.17   |    96.17    |
| SaliencyMix   |    0.2    |    96.05   |    96.42   |    96.20   |    96.18    |
| AttentiveMix+ |     2     |    96.21   |    96.45   |    96.63   |    96.49    |
| FMix*         |    0.2    |    96.17   |    96.53   |    96.18   |    96.01    |
| PuzzleMix     |     1     |    96.42   |    96.87   |    97.10   |    97.13    |
| GridMix       |    0.2    |    95.89   |    96.33   |    96.56   |    96.58    |
| ResizeMix*    |     1     |    96.16   |    96.91   |    96.76   |    97.04    |
| AlignMix📖    |     2     |      -     |      -     |      -     |    97.05    |
| AutoMix       |     2     |    96.59   |    97.08   |    97.34   |    97.30    |
| SAMix*        |     2     |    96.67   |    97.16   |    97.50   |    97.41    |

| Backbones     |   $Beta$   | ResNeXt-50 | ResNeXt-50 | ResNeXt-50 |  ResNeXt-50 |
|---------------|:----------:|:----------:|:----------:|:----------:|:-----------:|
| Epochs        |  $\alpha$  | 200 epochs | 400 epochs | 800 epochs | 1200 epochs |
| Vanilla       |      -     |    95.92   |    95.81   |    96.23   |    96.26    |
| MixUp         |      1     |    96.88   |    97.19   |    97.30   |    97.33    |
| CutMix        |     0.2    |    96.78   |    96.54   |    96.60   |    96.35    |
| ManifoldMix   |      2     |    96.97   |    97.39   |    97.33   |    97.36    |
| SmoothMix     |     0.2    |    95.87   |    96.37   |    96.49   |    96.77    |
| SaliencyMix   |     0.2    |    96.65   |    96.89   |    96.70   |    96.60    |
| AttentiveMix+ |      2     |    96.84   |    96.91   |    96.87   |    96.62    |
| FMix*         |     0.2    |    96.72   |    96.76   |    96.76   |    96.10    |
| PuzzleMix     |      1     |    97.05   |    97.24   |    97.37   |    97.34    |
| GridMix       |     0.2    |    97.18   |    97.30   |    96.40   |    95.79    |
| ResizeMix*    |      1     |    97.02   |    97.38   |    97.21   |    97.36    |
| AutoMix       |      2     |    97.19   |    97.42   |    97.65   |    97.51    |
| SAMix*        |      2     |    97.23   |    97.51   |    97.93   |    97.74    |

### **CIFAR-100 Dataset**

These benchmarks follow CutMix settings, training 200/400/800/1200 epochs from stretch based on the CIFAR version of ResNet variants on [CIFAR-100](https://www.cs.toronto.edu/~kriz/cifar.html). When adopting ResNeXt-50 (32x4d) as the backbone, we use `wd=5e-4` for cutting-based methods (CutMix, AttributeMix+, SaliencyMix, FMix, ResizeMix) for better performances.

**Note**

* Please refer to config files for experiment details: [various mixups](https://github.com/Westlake-AI/openmixup/tree/main/configs/classification/cifar100/mixups/), [AutoMix](https://github.com/Westlake-AI/openmixup/tree/main/configs/classification/cifar100/automix/), [SAMix](https://github.com/Westlake-AI/openmixup/tree/main/configs/classification/cifar100/samix/). As for config files of [various mixups](https://github.com/Westlake-AI/openmixup/tree/main/configs/classification/cifar100/mixups/), please modify `max_epochs` and `mix_mode` in `auto_train_mixups.py` to generate configs and bash scripts.
* Notice that 📖 denotes original results reproduced by official implementations.

| Backbones     |  $Beta$   |  ResNet-18 |  ResNet-18 |  ResNet-18 |  ResNet-18  |
|---------------|:---------:|:----------:|:----------:|:----------:|:-----------:|
| Epoch         |  $\alpha$ | 200 epochs | 400 epochs | 800 epochs | 1200 epochs |
| Vanilla       |     -     |    76.42   |    77.73   |    78.04   |    78.55    |
| MixUp         |     1     |    78.52   |    79.34   |    79.12   |    79.24    |
| CutMix        |    0.2    |    79.45   |    79.58   |    78.17   |    78.29    |
| ManifoldMix   |     2     |    79.18   |    80.18   |    80.35   |    80.21    |
| SmoothMix     |    0.2    |    77.90   |    78.77   |    78.69   |    78.38    |
| SaliencyMix   |    0.2    |    79.75   |    79.64   |    79.12   |    77.66    |
| AttentiveMix+ |     2     |    79.62   |    80.14   |    78.91   |    78.41    |
| FMix*         |    0.2    |    78.91   |    79.91   |    79.69   |    79.50    |
| PuzzleMix     |     1     |    79.96   |    80.82   |    81.13   |    81.10    |
| Co-Mixup📖    |     2     |    80.01   |    80.87   |    81.17   |    81.18    |
| GridMix       |    0.2    |    78.23   |    78.60   |    78.72   |    77.58    |
| ResizeMix*    |     1     |    79.56   |    79.19   |    80.01   |    79.23    |
| AlignMix📖    |     2     |      -     |      -     |      -     |    81.71    |
| AutoMix       |     2     |    80.12   |    81.78   |    82.04   |    81.95    |
| SAMix*        |     2     |    81.21   |    81.97   |    82.30   |    82.41    |

| Backbones     |  $Beta$  | ResNeXt-50 | ResNeXt-50 | ResNeXt-50 |  ResNeXt-50 |  WRN-28-8  |
|---------------|:--------:|:----------:|:----------:|:----------:|:-----------:|:----------:|
| Epoch         | $\alpha$ | 200 epochs | 400 epochs | 800 epochs | 1200 epochs | 400 epochs |
| Vanilla       |     -    |    79.37   |    80.24   |    81.09   |    81.32    |    81.63   |
| MixUp         |     1    |    81.18   |    82.54   |    82.10   |    81.77    |    82.82   |
| CutMix        |    0.2   |    81.52   |    78.52   |    78.32   |    77.17    |    84.45   |
| ManifoldMix   |     2    |    81.59   |    82.56   |    82.88   |    83.28    |    83.24   |
| SmoothMix     |    0.2   |    80.68   |    79.56   |    78.95   |    77.88    |    82.09   |
| SaliencyMix   |    0.2   |    80.72   |    78.63   |    78.77   |    77.51    |    84.35   |
| AttentiveMix+ |     2    |    81.69   |    81.53   |    80.54   |    79.60    |    84.34   |
| FMix*         |    0.2   |    79.87   |    78.99   |    79.02   |    78.24    |    84.21   |
| PuzzleMix     |     1    |    81.69   |    82.84   |    82.85   |    82.93    |    85.02   |
| Co-Mixup📖    |     2    |    81.73   |    82.88   |    82.91   |    82.97    |    85.05   |
| GridMix       |    0.2   |    81.11   |    79.80   |    78.90   |    76.11    |    84.24   |
| ResizeMix*    |     1    |    79.56   |    79.78   |    80.35   |    79.73    |    84.87   |
| AutoMix       |     2    |    82.84   |    83.32   |    83.64   |    83.80    |    85.18   |
| SAMix*        |     2    |    83.81   |    84.27   |    84.42   |    84.31    |    85.50   |

## Fine-grained and Scenic Classification Benchmarks

We further provide benchmarks on downstream classification scenarios. We report the **median** of top-1 accuracy in the last 5/10 training epochs for 100/200 epochs.

### **Transfer Learning on Small-scale Fine-grained Datasets**

These benchmarks follow transfer learning settings on fine-grained datasets, using PyTorch official pre-trained models as initialization and training 200 epochs on [CUB-200](http://www.vision.caltech.edu/visipedia/CUB-200-2011.html) and [FGVC-Aircraft](https://www.robots.ox.ac.uk/~vgg/data/fgvc-aircraft/).

**Note**

* Please refer to config files for experiment details: [CUB-200](https://github.com/Westlake-AI/openmixup/tree/main/configs/classification/cub200/mixups/basic) and [FGVC-Aircraft](https://github.com/Westlake-AI/openmixup/tree/main/configs/classification/aircrafts/mixups/basic). As for config files of various mixups, please modify `max_epochs` and `mix_mode` in `auto_train_mixups.py` to generate configs and bash scripts.

| Datasets    |  $Beta$  |  CUB-200  |   CUB-200  |  Aircraft |  Aircraft  |
|-------------|:--------:|:---------:|:----------:|:---------:|:----------:|
| Backbones   | $\alpha$ | ResNet-18 | ResNeXt-50 | ResNet-18 | ResNeXt-50 |
| Vanilla     |     -    |   77.68   |    83.01   |   80.23   |    85.10   |
| MixUp       |    0.2   |   78.39   |    84.58   |   79.52   |    85.18   |
| CutMix      |     1    |   78.40   |    85.68   |   78.84   |    84.55   |
| ManifoldMix |    0.5   |   79.76   |    86.38   |   80.68   |    86.60   |
| SaliencyMix |    0.2   |   77.95   |    83.29   |   80.02   |    84.31   |
| FMix*       |    0.2   |   77.28   |    84.06   |   79.36   |    86.23   |
| PuzzleMix   |     1    |   78.63   |    84.51   |   80.76   |    86.23   |
| ResizeMix*  |     1    |   78.50   |    84.77   |   78.10   |    84.08   |
| AutoMix     |     2    |   79.87   |    86.56   |   81.37   |    86.72   |
| SAMix*      |     2    |   81.11   |    86.83   |   82.15   |    86.80   |

### **Large-scale Fine-grained Datasets**

These benchmarks follow [PyTorch-style](https://arxiv.org/abs/2110.00476) ImageNet-1k training settings, training 100 epochs from stretch on [iNat2017](https://github.com/visipedia/inat_comp/tree/master/2017) and [iNat2018](https://github.com/visipedia/inat_comp/tree/master/2018).

**Note**

* Please refer to config files for experiment details: [iNat2017](https://github.com/Westlake-AI/openmixup/tree/main/configs/classification/inaturalist2017/) and [iNat2018](https://github.com/Westlake-AI/openmixup/tree/main/configs/classification/inaturalist2018/). As for config files of [various mixups](https://github.com/Westlake-AI/openmixup/tree/main/configs/classification/inaturalist2017/mixups/), please modify `max_epochs` and `mix_mode` in `auto_train_mixups.py` to generate configs and bash scripts.
* Download weights and logs: iNat2017 [[github](https://github.com/Westlake-AI/openmixup/releases/tag/mixup-inat2017-weights), [Baidu (1e7w)](https://pan.baidu.com/s/1GsoXVpIBXPjyFKsCdnmp9Q)], iNat2018 [[github](https://github.com/Westlake-AI/openmixup/releases/tag/mixup-inat2018-weights), [Baidu (wy2v)](https://pan.baidu.com/s/1P4VeJalFLV0chryjYCfveg)].

| Datasets    |  $Beta$  |  iNat2017 |   iNat2017  |  iNat2018 |   iNat2018  |
|-------------|:--------:|:---------:|:-----------:|:---------:|:-----------:|
| Backbones   | $\alpha$ | ResNet-50 | ResNeXt-101 | ResNet-50 | ResNeXt-101 |
| Vanilla     |     -    |   60.23   |    63.70    |   62.53   |    66.94    |
| MixUp       |    0.2   |   61.22   |    66.27    |   62.69   |    67.56    |
| CutMix      |     1    |   62.34   |    67.59    |   63.91   |    69.75    |
| ManifoldMix |    0.2   |   61.47   |    66.08    |   63.46   |    69.30    |
| SaliencyMix |     1    |   62.51   |    67.20    |   64.27   |    70.01    |
| FMix*       |     1    |   61.90   |    66.64    |   63.71   |    69.46    |
| PuzzleMix   |     1    |   62.66   |    67.72    |   64.36   |    70.12    |
| ResizeMix*  |     1    |   62.29   |    66.82    |   64.12   |    69.30    |
| AutoMix     |     2    |   63.08   |    68.03    |   64.73   |    70.49    |
| SAMix*      |     2    |   63.32   |    68.26    |   64.84   |    70.54    |

### **Scenic Classification Dataset**

This benchmark follows [PyTorch-style](https://arxiv.org/abs/2110.00476) ImageNet-1k training settings, training 100 epochs from stretch on [Places205](http://places2.csail.mit.edu/index.html).

**Note**

* Please refer to config files of [Places205](https://github.com/Westlake-AI/openmixup/tree/main/configs/classification/place205/) for experiment details. As for config files of [various mixups](https://github.com/Westlake-AI/openmixup/tree/main/configs/classification/place205/mixups/), please modify `max_epochs` and `mix_mode` in `auto_train_mixups.py` to generate configs and bash scripts.
* Download weights and logs of Places205 [[github](https://github.com/Westlake-AI/openmixup/releases/tag/mixup-place205-weights), [Baidu (4m94)](https://pan.baidu.com/s/1ciAYxK6SwR13UNScp0W3bQ)].

| Datasets    |  $Beta$  |  Places205 |  Places205 |
|-------------|:--------:|:---------:|:---------:|
| Backbones   | $\alpha$ | ResNet-18 | ResNet-50 |
| Vanilla     |     -    |   59.63   |   63.10   |
| MixUp       |    0.2   |   59.33   |   63.01   |
| CutMix      |    0.2   |   59.21   |   63.75   |
| ManifoldMix |    0.2   |   59.46   |   63.23   |
| SaliencyMix |    0.2   |   59.50   |   63.33   |
| FMix*       |    0.2   |   59.51   |   63.63   |
| PuzzleMix   |     1    |   59.62   |   63.91   |
| ResizeMix*  |     1    |   59.66   |   63.88   |
| AutoMix     |     2    |   59.74   |   64.06   |
| SAMix*      |     2    |   59.86   |   64.27   |
