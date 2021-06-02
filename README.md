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

第三部分训练过程参数，基础学习率设定为0.02/16，训练epoch设定为24，warm_iter设定为100，lr_decay_stage设定为[16,20]。

第三部分推断过程，test_maxboxes_per_image设定为100，NMS阈值设定为0.5

### Results

训练时，total loss一直下降，至epoch 39时，total loss约为0.16左右。
10 epoch时，得到的网络测试结果为：

mAP@0.5-0.95 = 0.032，AR@0.5-0.95 = 0.173

23 epoch时，得到的网络测试结果为：

mAP@0.5-0.95 = 0.047，AR@0.5-0.95 = 0.15

该模型在coco数据集上表现可达到mAP@0.5-0.95 = 0.401，可知因为mini365为小样本情境数据集，模型训练过程中出现过拟合情况，导致泛化能力下降，测试性能显著下降。

## FSDet

依据FSDet论文当中提到的，修改了train process，在微调时将Backbone以及RPN参数freeze，代码见train_fsdet.py。

### Finetune RCNN

首先微调整个RCNN参数，包括卷积头
### Finetune predict layer

