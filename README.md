# Neural Style Transfer
A tensorflow implementation for fast neural style!

A tensorflow implementation for [Perceptual Losses for Real-Time Style Transfer and Super-Resolution](https://arxiv.org/abs/1603.08155).

The python code [here](https://github.com/BrowningWan/fast-neural-style-android-app/tree/master/fast-neural-style-train%26test) is forked from [hzy46/fast-neural-style-tensorflow](https://github.com/hzy46/fast-neural-style-tensorflow). 

The [eval.py](https://github.com/BrowningWan/fast-neural-style-android-app/blob/master/fast-neural-style-train%26test/eval.py) file was edited to product a .pb model file while converting the image. 


## Requirements and Prerequisites:
- Python 2.7.x or Python 3.5.x
- Tensorflow >= 1.0
- python-opencv
- pyyaml

To generate a sample from the model "wave.ckpt-done", run:

```
cd fast-neural-style-train&test
python eval.py --model_file <your path to wave.ckpt-done> --image_file img/test.jpg
```

Then check out generated/res.jpg for the transfer result and models/wave_small1.pb for .pb model file.

To deploy the real-time style transfer, replace your model file path in line 16 in [Camera_transfer.py](https://github.com/BrowningWan/fast-neural-style-android-app/blob/master/fast-neural-style-train%26test/Camera_transfer.py), then run:

```
cd fast-neural-style-train&test
python Camera_transfer.py
```

## Train a Model:
To train a model from scratch, you should first download [VGG16 model](http://download.tensorflow.org/models/vgg_16_2016_08_28.tar.gz) from Tensorflow Slim. Extract the file vgg_16.ckpt. Then copy it to the folder pretrained/ :
```
cd fast-neural-style-train&test
mkdir pretrained
cp <your path to vgg_16.ckpt>  pretrained/
```

Then download the [COCO dataset](http://msvocds.blob.core.windows.net/coco2014/train2014.zip). Please unzip it, and you will have a folder named "train2014" with many raw images in it. Then create a symbol link to it:
```
cd <this repo>
ln -s <your path to the folder "train2014"> train2014
```

Train the model of "wave":
```
python train.py -c conf/wave.yml
```

(Optional) Use tensorboard:
```
tensorboard --logdir models/wave/
```

Checkpoints will be written to "models/wave/".

View the [configuration file](https://github.com/BrowningWan/fast-neural-style-android-app/blob/master/fast-neural-style-train%26test/conf/bossK.yml) for details.
