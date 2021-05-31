# cv-master-few shot learning
基础任务

【2分】基于Faster-RCNN 在我们提供的训练集上训练模型并优化性能, 观察训练过程损失变化

【2分】在上述实验的基础上, 复现 FSDet 论文 代码 并测试性能, 与(1) 对比优化过程和尽可能提升性能

提高任务（任选其中一个完成即可）

【1分】能否通过所学内容优化上述实验中的RPN模块, 给出前后测试集指标对比(可截图)和优化思路

【1分】能否使用 Prototypical Network 思路优化小样本检测的分类分支

【2分】能否使用 One-Stage 方法来实现性能较好的小样本检测器

## Faster RCNN
### Hyperparameters Optimization

Faster RCNN网络可优化Hyperparameters主要可分为三部分，第一部分为Backbone相关Hyperparameters，主要为Backbone网络结构相关Hyperparameters；第二部分为RPN相关，主要为Anchor形状及NMS相关Hyperparameters；第三部分为网络训练推断过程相关Hyperparameters。

第一部分Backbone此次采用Resnet50 + Feature Pyramid Networks结构。

第二部分Anchor形状，采用Anchor scale采用[32, 64, 128, 256, 512]五种size，Anchor ratio采用[1:1, 1:2, 2:1]三类，共构成15种形状的anchor，这15种形状的anchor是经常使用的常规形状，能兼顾到大型和小型目标，没有针对特定检测对象和场景进行特别布置；NMS相关参数中，threshold设定为0.7，检出anchor数量设定为512个，正样本比例设定为0.5。

第三部分训练过程参数，

### Results

