# Face Detection

## Introduction

Lightweight face detector. Face detector + facial landmarks can achive over 24FPS on iPhone X (powered by CoreML).

The whole project is based on [retinaface](https://github.com/deepinsight/insightface/tree/master/detection/retinaface). See this [doc](https://kz42.github.io/assets/docs/face/face_detection_landmark.pdf) for more details. Watch iPhone X demo [video](https://kz42.github.io/assets/videos/face.MP4)

## Data

Read doc from [retinaface](https://github.com/deepinsight/insightface/tree/master/detection/retinaface#data)

## Train, Evaluate, Demo

### Train

#### Environment

Use docker container for a clean environment.

**Pre requirement**

- docker environment: check on [docker page](https://docs.docker.com/)
- Nvidia GPU with Cuda matter installed

**Readied Docker Image**

Choose one from the following: 

- Cuda 11.0+

  Self-built image (uploaded to docker hub)

  ```shell
  docker pull kz42/face_tasks:retinaface_mxnet_1.9.0_cu110
  ```

- Cuda 10.0+

  Pull from mxnet/python

  ```shell
  docker pull mxnet/python:1.5.0_gpu_cu100_py3
  ```

**Build from Scratch**

Mxnet doesn't have Cuda 11.0+ supported image, you have to build from scratch if your GPU device is newer (e.g. RTX 3090). Please read the doc(todo) if you want to build it by yourself, otherwise, pull the readied image by `docker pull kz42/face_tasks:retinaface_mxnet_1.9.0_cu110` 

#### Run Train

```shell
MXNET_USE_FUSION='0' CUDA_VISIBLE_DEVICES='0' python train.py --prefix ./model/trained/mnet --network mnet --pretrained ./model/backbone/mobilenet_0_25 --dataset_path <dataset-path> --root_path <root-dataset-path>
```

**Note**: pretrained backbone mobilenet-0.25 is supported by [yangfly](https://github.com/yangfly) , download from [baidu cloud](https://pan.baidu.com/s/1P1ypO7VYUbNAezdvLm2m9w#list/path=%2F):nzof 

*yangfly's model has higher accuracy, but my model is more robust and has higher inference speed (basically just a trade-off between accuracy and speed). Feel free to choose based on your needs. Big thanks for his work, it helped me fix the bugs during train.*

#### Plot Train Loss

Run following to plot train loss of different models

```shell
python analyze_train.py --log-path <log-path1:log-path2> --out-path <path-to-save>
```

or use `mxboard.SummaryWriter` to record loss, and visualize it by tensorboard.

### Evaluate

Read the doc from [WIDERFACE](http://shuoyang1213.me/WIDERFACE/)

### Demo

Todo

## How to think

Todo

## Model Zoo

- Retinaface-MobileNet0.25-320x320: [baidu cloud](https://pan.baidu.com/s/1VpzmWNoL0_izwFSxeKAf2g):6ewf (my model)
- Retinaface-MobileNet0.25-640x640: [baidu cloud](https://pan.baidu.com/s/1P1ypO7VYUbNAezdvLm2m9w#list/path=%2F):nzof (yangfly's model)

## Todo

The plan for this project, *opt* means will do if I get lots of requests. Feel free to leave comments if you want me to do *opt* jobs.

- [ ] MNN based demo
- [ ] how to think doc
- [ ] REST API based on [OpenVino Model Server project](https://docs.openvino.ai/latest/openvino_docs_ovms.html) (opt)
- [ ] [CoreML](https://developer.apple.com/documentation/coreml) based demo on iOS (opt)

## Reference

1. [Retinaface](https://github.com/deepinsight/insightface/tree/master/detection/retinaface)
2. [yangfly](https://github.com/yangfly)

