## Sketch Your Own GAN
 [**Project**](https://peterwang512.github.io/GANSketching/) | [**Paper**](https://arxiv.org/abs/2108.02774)



<img src="images/teaser_video.gif" width="800px"/>


Our method takes in one or a few hand-drawn sketches and customizes an off-the-shelf GAN to match the input sketch. While our new model changes an object’s shape and pose, other visual cues such as color, texture, background, are faithfully preserved after the modification.
<br><br><br>

[Sheng-Yu Wang](https://peterwang512.github.io/)<sup>1</sup>, [David Bau](https://people.csail.mit.edu/davidbau/home/)<sup>2</sup>, [Jun-Yan Zhu](https://cs.cmu.edu/~junyanz)<sup>1</sup>.
<br> CMU<sup>1</sup>, MIT CSAIL<sup>2</sup>
<br>In [ICCV](https://arxiv.org/abs/2108.02774), 2021.


**Training code, evaluation code, and datasets will be released soon.**


## Results
Our method can customize a pre-trained GAN to match the input sketch.

<img src="images/teaser.jpg" width="800px"/>



## Getting Started

### Clone our repo
```bash
git clone git@github.com:PeterWang512/GANSketching.git
cd GANSketching
```
### Install packages
- Install PyTorch (version >= 1.6.0) ([pytorch.org](http://pytorch.org))
  ```bash
  pip install -r requirements.txt
  ```

### Download model weights
- Run `bash weights/download_weights.sh`


### Generate samples from a customized model

This command runs the customized model specified by `ckpt`, and generates samples to `save_dir`.

```
# generates samples from the "standing cat" model.
python generate.py --ckpt weights/photosketch_standing_cat_noaug.pth --save_dir output/samples_standing_cat

# generates samples from the cat face model in Figure. 1 of the paper.
python generate.py --ckpt weights/by_author_cat_aug.pth --save_dir output/samples_teaser_cat
```

### Latent space edits by GANSpace

Our model preserves the latent space editability of the original model. Our models can apply the same edits using the latents reported in Härkönen et.al. ([GANSpace](https://github.com/harskish/ganspace)).

```
# add fur to the standing cats
python ganspace.py --obj cat --comp_id 27 --scalar 50 --layers 2,4 --ckpt weights/photosketch_standing_cat_noaug.pth --save_dir output/ganspace_fur_standing_cat

# close the eyes of the standing cats
python ganspace.py --obj cat --comp_id 45 --scalar 60 --layers 5,7 --ckpt weights/photosketch_standing_cat_noaug.pth --save_dir output/ganspace_eye_standing_cat
```

## Acknowledgments

This repository borrows partially from [SPADE](https://github.com/NVlabs/SPADE), [stylegan2-pytorch](https://github.com/rosinality/stylegan2-pytorch), [PhotoSketch](https://github.com/mtli/PhotoSketch), [GANSpace](https://github.com/harskish/ganspace), and [data-efficient-gans](https://github.com/mit-han-lab/data-efficient-gans).

## Reference

If you find this useful for your research, please cite the following work.
```
@inproceedings{wang2021sketch,
  title={Sketch Your Own GAN},
  author={Wang, Sheng-Yu and Bau, David and Zhu, Jun-Yan},
  booktitle={Proceedings of the IEEE International Conference on Computer Vision},
  year={2021}
}
```

Please contact [Sheng-Yu Wang](https://peterwang512.github.io/) with any comments or feedback.
