# AdaIN
PyTorch implementation of [this paper](https://arxiv.org/abs/1703.06868).
Original implementation can be found at [here](https://github.com/xunhuang1995/AdaIN-style).

## Examples
These are generated images with this implementation.

### Case 1

|               Content                |              Style               |
|:------------------------------------:|:--------------------------------:|
| ![content](images/case1/content.jpg) | ![style](images/case1/style.jpg) |


|              iter_10K              |              iter_20K              |              iter_30K              |              iter_40K              |
|:----------------------------------:|:----------------------------------:|:----------------------------------:|:----------------------------------:|
| ![10K](images/case1/iter_10K.jpg)  | ![10K](images/case1/iter_20K.jpg)  | ![10K](images/case1/iter_30K.jpg)  | ![10K](images/case1/iter_40K.jpg)  |

|              iter_50K              |              iter_60K              |              iter_70K              |              iter_80K              |
|:----------------------------------:|:----------------------------------:|:----------------------------------:|:----------------------------------:|
| ![10K](images/case1/iter_50K.jpg)  | ![10K](images/case1/iter_60K.jpg)  | ![10K](images/case1/iter_70K.jpg)  | ![10K](images/case1/iter_80K.jpg)  |

|              iter_90K              |              iter_100K             |              iter_110K             |              iter_120K             |
|:----------------------------------:|:----------------------------------:|:----------------------------------:|:----------------------------------:|
| ![10K](images/case1/iter_90K.jpg)  | ![10K](images/case1/iter_100K.jpg) | ![10K](images/case1/iter_110K.jpg) | ![10K](images/case1/iter_120K.jpg) |

|              iter_130K             |              iter_140K             |              iter_150K             |              iter_160K             |
|:----------------------------------:|:----------------------------------:|:----------------------------------:|:----------------------------------:|
| ![10K](images/case1/iter_130K.jpg) | ![10K](images/case1/iter_140K.jpg) | ![10K](images/case1/iter_150K.jpg) | ![10K](images/case1/iter_160K.jpg) |

### Case 2

|               Content                |              Style               |
|:------------------------------------:|:--------------------------------:|
| ![content](images/case2/content.jpg) | ![style](images/case2/style.jpg) |


|              iter_10K              |              iter_20K              |              iter_30K              |              iter_40K              |
|:----------------------------------:|:----------------------------------:|:----------------------------------:|:----------------------------------:|
| ![10K](images/case2/iter_10K.jpg)  | ![10K](images/case2/iter_20K.jpg)  | ![10K](images/case2/iter_30K.jpg)  | ![10K](images/case2/iter_40K.jpg)  |

|              iter_50K              |              iter_60K              |              iter_70K              |              iter_80K              |
|:----------------------------------:|:----------------------------------:|:----------------------------------:|:----------------------------------:|
| ![10K](images/case2/iter_50K.jpg)  | ![10K](images/case2/iter_60K.jpg)  | ![10K](images/case2/iter_70K.jpg)  | ![10K](images/case2/iter_80K.jpg)  |

|              iter_90K              |              iter_100K             |              iter_110K             |              iter_120K             |
|:----------------------------------:|:----------------------------------:|:----------------------------------:|:----------------------------------:|
| ![10K](images/case2/iter_90K.jpg)  | ![10K](images/case2/iter_100K.jpg) | ![10K](images/case2/iter_110K.jpg) | ![10K](images/case2/iter_120K.jpg) |

|              iter_130K             |              iter_140K             |              iter_150K             |              iter_160K             |
|:----------------------------------:|:----------------------------------:|:----------------------------------:|:----------------------------------:|
| ![10K](images/case2/iter_130K.jpg) | ![10K](images/case2/iter_140K.jpg) | ![10K](images/case2/iter_150K.jpg) | ![10K](images/case2/iter_160K.jpg) |

## Clone
via ssh
```
$ git clone git@github.com:kukosmos/AdaIN-pytorch-2019.git
```
via https
```
$ git clone https://github.com/kukosmos/AdaIN-pytorch-2019.git
```

## Docker
We offer a [docker](https://www.docker.com) image.
If you prefer run this repository locally, please skip this section and follow the instructions from the following section.
First, build the image.
```
$ docker build . --tag adain
```
Start a docker container with the created image.
```
$ docker run --rm -it -v $(pwd)/experiments:/workspace/experiments -v $(pwd)/data:/workspace/data -u $(id -u):$(id -g) adain
```
We provide two commands (`adain-train`, `adain-test`). Please see how to use them with following commands..
```
$ adain-train -h
$ adain-test -h
```

## Requirments
Install following applications
* python3.6+
* unzip

Install following python libraries
* Pillow
* [pytorch](https://pytorch.org)
* [torchvision](https://pytorch.org)
* tensorboard
* tensorboardX
* tqdm

## Train
To train a model yourself, do the following steps.

### Prepare dataset
First, download the dataset with given script.
For example, to download ```coco2017train``` dataset, type in the following command:
```
$ ./download.sh coco2017train
```
Detailed usage of ```download.sh``` script can be found as follows:
```
$ ./download.sh --help
```

### Train model
Train the model with ```train.py```.
For example, to train model with ```coco2017train``` as content and ```wikiart``` as style, type in the following command:
```
$ python train.py \
>   --content-dir data/coco2017train \
>   --style-dir data/wikiart
```

To check the logs that saved in ```logs``` directory, type in the following command:
```
$ tensorboard --logdir logs
```

### For more
Advanced options can be found with following command:
```
$ python train.py --help
```

## Generate Results
To generate sytled images, use ```test.py```.
For example, to generate a styled image from trained model ```models/adain.pth``` with ```images/content.jpg``` as a content image
and ```images/style.jpg``` as a style image, type in the following command:
```
$ python test.py \
>   --model models/adain.pth \
>   --content images/content.jpg \
>   --style images/style.jpg
```

### Interpolation
To mix the two or more styles in one content image, specify the interpolation weights as follows:
```
$ python test.py \
>   --model models/adain.pth \
>   --content images/content.jpg \
>   --style images/style1.jpg images/style2.jpg images/style3.jpg \
>   --interpolation-weights 2 3 4
```
Note that all style images should have weights.
In other words, the number of images should be equal to the number of weights.

### For more
More options can be found with following command:
```
$ python test.py --help
```

## References
* [1]: X. Huang and S. Belongie. "[Arbitrary Style Transfer in Real-time with Adaptive Instance Normalization](https://arxiv.org/abs/1703.06868)", in ICCV, 2017.
* [2]: [PyTorch implementation of AdaIN](https://github.com/naoto0804/pytorch-AdaIN)
* [3]: [COCO Dataset](http://cocodataset.org/#download)
* [4]: [Wikiart dataset](https://github.com/cs-chan/ArtGAN/tree/master/WikiArt%20Dataset)
