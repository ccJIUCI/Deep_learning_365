改进的 YOLOv3 可以做到精度和 SSD 算法相近，而速度快了将近3倍。YOLOv3 算法的改进之处为三个方面：①应用多尺度的预测、②采用全新的网络结构 DarkNet-53 以及③分类损失采用二元交叉熵损失。

网络结构方面：YOLOv3 借鉴 ResNet 的思想，采用了大量的残差跳跃连接层，设计并训练了新的网络 DarkNet-53。同时，为了降低池化带来的梯度负面影响，网络采用全卷积层并通过调节卷积的步长实现下采样。 

为了加强算法对小目标的检测精度，YOLOv3 采用特征金字塔网络（FPN）进行多尺度特征融合。若输入图像大小为416x416x3，则输出三条预测支路。三条预测支路的特征图尺度分别是13x13x75，26x26x75，52x52x75
，采用多尺度的方式对不同大小的目标进行检测，其中75的含义为：75 = 3x(4+1+20)，3表示1个网格单元预测3个边界框，4表示边界框坐标的4个信息，1表示边界框的置信度，20表示数据集共20个类别。 

考虑到softmax损失函数进行分类的前提是目标的类别之间是相互独立的，在处理可能有重叠的类别标签（如苹果和水果）的目标时，softmax分类器不能对数据进行很好的拟合，因此YOLOv3将分类损失由softmax损失改成二分类的交叉熵损失，交叉熵损失预测每个类别的得分并使用一个阈值对目标进行多标签预测，比阈值高的类别就是当前目标框的真正类别。
