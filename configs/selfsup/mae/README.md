# MAE

> [Masked Autoencoders Are Scalable Vision Learners](https://arxiv.org/abs/2111.06377)

## Abstract

This paper shows that masked autoencoders (MAE) are scalable self-supervised learners for computer vision. Our MAE approach is simple: we mask random patches of the input image and reconstruct the missing pixels. It is based on two core designs. First, we develop an asymmetric encoder-decoder architecture, with an encoder that operates only on the visible subset of patches (without mask tokens), along with a lightweight decoder that reconstructs the original image from the latent representation and mask tokens. Second, we find that masking a high proportion of the input image, e.g., 75%, yields a nontrivial and meaningful self-supervisory task. Coupling these two designs enables us to train large models efficiently and effectively: we accelerate training (by 3× or more) and improve accuracy. Our scalable approach allows for learning high-capacity models that generalize well: e.g., a vanilla ViT-Huge model achieves the best accuracy (87.8%) among methods that use only ImageNet-1K data. Transfer performance in downstream tasks outperforms supervised pretraining and shows promising scaling behavior.

<div align="center">
<img src="https://user-images.githubusercontent.com/30762564/150733959-2959852a-c7bd-4d3f-911f-3e8d8839fe67.png" width="40%"/>
</div>

## Models and Benchmarks

Here, we report the results of the model, which is pre-trained on ImageNet-1k
for 400 epochs, the details are below:

| Backbone | Pre-train epoch | Fine-tuning Top-1 |                                                     Pre-train Config                                                      |                                                                 Fine-tuning Config                                                                 |                                                                                                                      Download                                                                                                                       |
| :------: | :-------------: | :---------------: | :-----------------------------------------------------------------------------------------------------------------------: | :------------------------------------------------------------------------------------------------------------------------------------------------: | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
| ViT-B/16 |       400       |       83.1        | [config](https://github.com/Westlake-AI/openmixup/tree/main/configs/selfsup/mae/imagenet/vit_base_dec8_dim512_8xb128_accu4_cos_fp16_ep400.py) | [config](https://github.com/Westlake-AI/openmixup/tree/main/configs/benchmarks/classification/imagenet/vit_base_p16_swin_ft_mae_sz224_8xb128_cos_ep100.py) | [model](https://download.openmmlab.com/mmselfsup/mae/mae_vit-base-p16_8xb512-coslr-400e_in1k-224_20220223-85be947b.pth) \| [log](https://download.openmmlab.com/mmselfsup/mae/mae_vit-base-p16_8xb512-coslr-300e_in1k-224_20220210_140925.log.json) |

## Citation

```bibtex
@inproceedings{he2022MAE,
  title={Masked Autoencoders Are Scalable Vision Learners},
  author={Kaiming He and Xinlei Chen and Saining Xie and Yanghao Li and Piotr Doll'ar and Ross B. Girshick},
  booktitle={CVPR},
  year={2022}
}
```
