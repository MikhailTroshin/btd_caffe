# btd_caffe
Block Term Decomposition for Caffe model

## Block Term Decomposition (BTD) for CNNs
- [Accelerating Convolutional Neural Networks for Mobile Applications](http://dl.acm.org/citation.cfm?id=2967280)
- 2016, ACM Multimedia
- Peisong Wang and Jian Cheng / Chinese Academy of Sciences & University of Chinese Academy of Sciences, Beijing, China
- Parameters for '3.2 Whole-Model Acceleration for VGG-16’ in ‘3. EXPERIMENTS’
  >The S', T' and R for conv1_2 to conv5_3 are as follows:  
  >conv1_2: 11, 18, 1  
  >conv2_1: 10, 24, 1  
  >conv2_2: 28, 28, 2  
  >conv3_1: 36, 48, 4  
  >conv3_2: 60, 48, 4  
  >conv3_3: 64, 56, 4  
  >conv4_1: 64, 100, 4  
  >conv4_2: 116, 100, 4  
  >conv4_3: 132, 132, 4  
  >conv5_1: 224, 224, 4  
  >conv5_2: 224, 224, 4  
  >conv5_3: 224, 224, 4  
- 'group' parameter is used in 'convolution_param' in Caffe network definition (.prototxt)
  - description of 'group' in [Caffe Tutorial for Convolution Layer](http://caffe.berkeleyvision.org/tutorial/layers/convolution.html)
  >group (g) [default 1]: If g > 1, we restrict the connectivity of each filter to a subset of the input. Specifically, the input and output channels are separated into g groups, and the iith output group channels will be only connected to the iith input group channels.

## Usage
```sh
$ ./start.sh
```
## Parameters for start.sh
| Name | Description | Type |
| :-- | :-- | :-: |
| ORIGINAL_DEPLOY | original model (deploy.prototxt)| input |
| ORIGINAL_MODEL | original model (.caffemodel) | input |
| TEMPLATE_DEPLOY | template for low-rank model (deploy.prototxt) | input |
| TEMPLATE_TRAIN_TEST | template for low-rank model (train_test.prototxt) | input |
| LOWRANK_DEPLOY | low-rank model (deploy.prototxt) | output |
| LOWRANK_TRAIN_TEST | low-rank model (train_test.prototxt) | output |
| LOWRANK_MODEL | low-rank model (.caffemodel)| output |
| CONFIG | parameter config file for BTD (.csv)| input |

## Parameter config file for BTD (.csv)
```
conv, S', T', R
```
- conv : name of "Convolution" layer in prototxt
- S' : # of input channels
- T' : # of output channels
- R  : # of blocks
