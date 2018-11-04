# halfsqueezenet: 2018年全国大学生FPGA创新设计挑战赛
# 题目：前列腺增生双极电切AI预警

## 文件夹内容
- training: 包含Vivado HLS中使用的训练脚本、预训练的权重和预生成的头文件。
- hls: 包含halfsqueezenet的Vivado HLS实现，使用了来自于hls-nn-lib中定义的层。
- scripts: 脚本1->使用Vivado HLS生成RTL文件；
		   脚本2->创建一个Vivado项目以获得最终比特流。
- deploy: 主函数入口。

## 1. Training
### 初始化安装
1. 安装 Tensorflow (https://www.tensorflow.org/install/).
2. 安装 Tensorpack (https://github.com/tensorpack/tensorpack).
3. $ git clone https://github.com/Gchinanty/spooNN
4. $ export PYTHONPATH=/path/to/spooNN/hls-nn-lib/training:$PYTHONPATH
5. $ cd spooNN/halfsqueezenet/training/

CNN被量化成一位权重值，五位的激活值。

### 开始训练
1. - $ python ./halfsqueezenet_objdetect.py 1 --data /path/to/DAC18_object_detection_dataset

2. - $ python ./halfsqueezenet_objdetect.py 2 --meta ./train_log/halfsqueezenet_objdetect/NAME1.meta --model ./train_log/halfsqueezenet_objdetect/NAME2.data-00000-of-00001 --output weights.npy

	生成将在C中使用的权重，并将它们作为numpy数组转储到weights.npy中。
	您需要相应地替换NAME1和NAME2。NAME1将是唯一的，而对于NAME2，您可以从某个迭代中选择权重。
	这个操作创建了两个文件:halfsqueeze-config.h和halfsqueezenet-params.h。
    -config.h文件包含分层配置参数，例如卷积核的大小，stride等。-params.h文件包含权重和激活因子。

3. - $ python ./halfsqueezenet_objdetect.py 0 --run path/to/DAC18_object_detection_dataset/category/ --weights ./weights.npy

	使用转储的权重执行推理。这将在给定目录中的所有图像上显示目标检测结果。

## 2. HLS implementation and testing

## 3. RTL and bitstream generation

## 4. Deployment on the PYNQ

