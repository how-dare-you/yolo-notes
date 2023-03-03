# 聚类得到锚框

VOC 5个，COCO 9个，每个尺寸3个


# 负责检测物体的锚框 决策树

![](/images/yolov3/yolov3_2023-03-03-08-47-20.png)

# 位置误差计算

- BCE 代替 MSE ，本质都是让预测值接近真实值，loss值变小。

![](/images/yolov3/yolov3_2023-03-03-08-54-27.png)

- 将真实框的值【$g_x$ $g_y$ $g_w$ $g_h$】转换为和预测值一样的形式，然后让预测值去拟合。


- 添加 loss_scale 来加强小目标的位置损失
![](/images/yolov3/yolov3_2023-03-03-09-09-46.png)

## whats binary cross entropy loss 


Binary cross entropy (BCE) loss is a commonly used loss function in machine learning, particularly in binary classification tasks. It is a measure of the difference between the predicted probability distribution of the model and the true probability distribution of the target.

In binary classification, the BCE loss is calculated as follows:

$L(y, y') = -[y*log(y') + (1-y)*log(1-y')]$

where y is the true label (either 0 or 1) and y' is the predicted probability of the positive class (i.e., the class with label 1).

The BCE loss is minimized when the predicted probability of the positive class is close to the true label (i.e., y'=y). This loss function is often used in conjunction with the sigmoid activation function in the output layer of a neural network, which ensures that the predicted probabilities are between 0 and 1.


## sigmoid activation function
![](/images/yolov3/yolov3_2023-03-03-10-17-07.png)
The sigmoid activation function is a common non-linear activation function used in neural networks, particularly in binary classification tasks. It transforms the input signal into a probability value between 0 and 1.

The sigmoid function is defined as follows:

$f(z) = 1 / (1 + e^{-z})$

where z is the input signal to the neuron.

When z is large (i.e., positive or negative), the output of the sigmoid function approaches 1 or 0, respectively. When z is near zero, the output of the sigmoid function is approximately 0.5.

In neural networks, the sigmoid function is often used in the output layer to model the probability of the positive class in a binary classification task. The output of the sigmoid function can be interpreted as the predicted probability of the positive class, and can be used to make binary predictions by applying a threshold (e.g., 0.5).
![](/images/yolov3/yolov3_2023-03-03-09-12-22.png)

![](/images/yolov3/yolov3_2023-03-03-09-25-13.png)

# 置信度误差计算

![](/images/yolov3/yolov3_2023-03-03-09-26-31.png)

# 分类误差计算

![](/images/yolov3/yolov3_2023-03-03-09-30-06.png)

# loss

- v3 用于计算 三种尺寸的 loss
![](/images/yolov3/yolov3_2023-03-03-09-36-31.png)

对比一下v1 的loss 

![](/images/yolov1/yolov1_2023-03-01-10-38-59.png)


# darknet53

- 使用了残差块
- BN后使用 LeakyReLU 激活函数
![](/images/yolov3/yolov3_2023-03-03-09-47-21.png)


- 第 36 61 79 层用于输出特征图
![](/images/yolov3/yolov3_2023-03-03-09-49-53.png)

![](/images/yolov3/yolov3_2023-03-03-09-52-07.png)

