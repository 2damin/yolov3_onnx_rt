# yolov3(Darknet) -> ONNX -> TensorRT in Jetson TX2

This repo converting **yolov3 and yolov3-tiny** darknet model to TensorRT model in Jetson TX2 platform.

If you want to convert **yolov3 or yolov3-tiny** pytorch model, need to convert model from pytorch to DarkNet. Check my [yolov3-pytorch repo](https://github.com/2damin/yolov3-pytorch)

## ENV INFO

**ONNX == 1.4.0**

**TensorRT == 5.1.6.1**

**Jetson TX2 jetpack == 4.2.3**

- CUDA == 10.0.326

- OpenCV == 3.3.1

- L4T R32.2


## Prerequisite

### install pip(python2.7)
```bash
 sudo add-apt-repository universe
 curl https://bootstrap.pypa.io/pip/2.7/get-pip.py --output get-pip.py
 sudo python2 get-pip.py
```

### install packages
```bash
pip install -r requirements.txt
```

## Guide

```bash
vim ~/.bashrc

export OPENBLAS_CORETYPE=ARMV8

#converting darkenet weights to onnx weights
sudo python yolov3_to_onnx.py --cfg ${CFG_PATH} --onnx ${ONNX_PATH} --num_class ${num_of_classes}

#building trt model and run inference
sudo python onnx_to_tensorrt.py --cfg ${CFG_PATH} --onnx ${ONNX_PATH} --num_class ${num_of_classes} --input_img &{test_img_path}

```

### If error occured,

```bash
Valueerror: need more than 1 value to unpack
```

Change "CRLF" to "LF" in your cfg file

```bash
vim ${your_cfg} -c "set ff=unix" -c":wq"

vim ${your_cfg}
"enter the last line"
```

check the cfg

<img width="182" alt="스크린샷 2022-05-18 오전 12 17 16" src="https://user-images.githubusercontent.com/29620595/168847015-b77422b1-fe0c-4ab2-aee2-f9feab4f4aec.png">


