# CenterHMR: Multi-Person Center-based Human Mesh Recovery
[![Google Colab demo](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1oz9E6uIbj4udOPZvA1Zi9pFx0SWH_UXg#scrollTo=s8gFtokdcEQo)

## Demo code

**Real-time webcam demo using local/remote server.** Please refer to [config_guide.md](src/config_guide.md) for details.

**Google Colab demo.** Predicted results would be saved to a npy file per imag, please refer to [config_guide.md](src/config_guide.md) for details.

<p float="center">
  <img src="../assets/demo/animation/c1_results_compressed.gif" width="32%" />
  <img src="../assets/demo/animation/c5_results_compressed.gif" width="32%" />
  <img src="../assets/demo/animation/c0_results_compressed.gif" width="32%" />
</p>

<p float="center">
  <img src="../assets/demo/animation/c4_results_compressed.gif" width="32%" />
  <img src="../assets/demo/animation/c2_results_compressed.gif" width="32%" />
  <img src="../assets/demo/animation/c3_results_compressed.gif" width="32%" />
</p>

### Try on Google Colab
Before installation, you can take a few minutes to try the prepared [Google Colab demo](https://colab.research.google.com/drive/1oz9E6uIbj4udOPZvA1Zi9pFx0SWH_UXg#scrollTo=s8gFtokdcEQo) a try.  
It allows you to run the project in the cloud, free of charge. 

## Installation

#### Download models

###### Option 1:

Directly download the full-packed released package [CenterHMR.zip](https://github.com/Arthur151/CenterHMR/releases/download/v0.1/CenterHMR_v0.1.zip) from github, latest version v0.1.

###### Option 2:

Clone the repo:
```bash
git clone https://github.com/anonymiao/CenterHMR_demo
```

Then download the CenterHMR data from [Github release](https://github.com/Arthur151/CenterHMR/releases/download/v0.0/CenterHMR_data.zip), [Google drive](https://drive.google.com/file/d/1vAiuallhHEV3WVq36u0gy7uzbG38d5sU/view?usp=sharing) or [Baidu Drive](https://pan.baidu.com/s/13XTwBy31zhLZLerI3V-rQA) with password ```6hye```. 

Unzip the downloaded CenterHMR_data.zip under the root CenterHMR_demo/. 
```bash
cd CenterHMR_demo/
unzip CenterHMR_data.zip
```

The layout would be
```bash
CenterHMR
  - demo
  - models
  - src
  - trained_models
```

#### Set up environments

Please intall the Pytorch 1.6 from [the official website](https://pytorch.org/). We have tested the code on Ubuntu and Centos using Pytorch 1.6 only. 

Install packages:
```bash
cd CenterHMR_demo/src
sh scripts/setup.sh
```

Please refer to the [bug.md](src/bugs.md) for unpleasant bugs. Feel free to submit the issues for related bugs.

<p float="center">
  <img src="../assets/demo/images_results/images-3dpw_sit_on_street.jpg" width="32%" />
  <img src="../assets/demo/images_results/images-Cristiano_Ronaldo.jpg" width="32%" />
  <img src="../assets/demo/images_results/images-Cristiano_Ronaldo2.jpg" width="32%" />
</p>

### Demo

Currently, the released code is used to re-implement demo results. Only 1-2G GPU memory is needed.

To do this you just need to run
```bash
cd CenterHMR_demo/src
sh run.sh
# if there are any bugs about shell script, please consider run the following command instead:
CUDA_VISIBLE_DEVICES=0 python core/test.py --gpu=0 --configs_yml=configs/basic_test.yml
```
Results will be saved in CenterHMR_demo/demo/images_results.

#### Internet images

You can also run the code on random internet images via putting the images under CenterHMR_demo/demo/images before running sh run.sh.

Or please refer to [config_guide.md](src/config_guide.md) for detail configurations.

Please refer to [config_guide.md](src/config_guide.md) for **saving the estimated mesh/Center maps/parameters dict**.

#### Internet videos

You can also run the code on random internet videos.

To do this you just need to firstly change the input_video_path in src/configs/basic_test_video.yml to /path/to/your/video. For example, set

```bash
 video_or_frame: True
 input_video_path: '../demo/sample_video.mp4' # None
```
and then run 

```bash
cd CenterHMR_demo/src
CUDA_VISIBLE_DEVICES=0 python core/test.py --gpu=0 --configs_yml=configs/basic_test_video.yml
```
Results will be displayed on your screen.

#### Webcam

We also provide the webcam demo code, which can run at real-time on a 1070Ti GPU / remote server.  
Currently, limited by the visualization pipeline, the webcam visulization code only support the single-person mesh.

To do this you just need to run
```bash
cd CenterHMR_demo/src
CUDA_VISIBLE_DEVICES=0 python core/test.py --gpu=0 --configs_yml=configs/basic_webcam.yml
# or please set the TEST_MODE=0 WEBCAM_MODE=1 in run.sh, then run
sh run.sh
```
Press Up/Down to end the demo. Pelease refer to [config_guide.md](src/config_guide.md) for setting mesh color or camera id.

If you wish to run webcam demo using remote server, pelease refer to [config_guide.md](src/config_guide.md).

#### Test FPS

To test FPS of CenterHMR on your device, please set configs/basic_test.yml as below

```bash
 save_visualization_on_img: False
 demo_image_folder: '../demo/videos/Messi_1'
```
and then run 

```bash
cd CenterHMR_demo/src
CUDA_VISIBLE_DEVICES=0 python core/test.py --gpu=0 --configs_yml=configs/basic_test.yml
```

## TODO LIST

The code will be gradually open sourced according to:
- [ ] the schedule
  - [x] demo code for internet images / videos / webcam
  - [x] runtime optimization
  - [ ] benchmark evaluation
  - [ ] training
