# FATE特征工程

- FederatedSample

上采样/下采样，分层采样

上采样：新建一个Table

下采样：.join（）操作

参数：

```python

```



- FeatureScale



- HeteroFeatureBinning



- OneHotEncoder



- HeteroFeatureSelection





# 2020

## 9-14 ~ 9-18

- 数字网关项目
  - 阅读FATE中纵向LR模型的部分代码，结合之前看的gRPC通信，FATE中的federation模块的代码，构思了一个数据拆包再重新打包的方案。
  - 写出了初步的数据拆包打包的代码，部署在了FATE的源代码中。
  - 以不通过fate_flow进行提交任务的方式进行了纵向LR的测试，10轮测试左右都没报错。
  - 通过fate_flow，进行了secure_boost的几轮测试，发现部分类型在本地序列化和反序列成功的情况下，通过网关sdk传输后，反序列化失败，推测是网关发送字节码的时候有损。
  - 通过改写网关sdk代码，将字节码导出，本地写脚本对比后发现。丢失了一个空格，将此错误报给了@李英达，@吕长彬
  - 再次经过测试，发现如果不将数据进行分片发送，是不会出问题的。
  - 导出出错的分片，发现其特点是开头有个空格，推测java后端发送开头有空格的数据时出了问题，@吕长彬
  - 确认java端没有问题后，仔细阅读网关sdk代码，发现了空格丢失的原因：对接受到的字符串类型的data做了strip()操作。
  - 修改代码后，通过fateflow测试sdk替换后的结果，10多轮secure_boost，均正常。

## 9-21 ~ 9-25

- 数字网关项目
  - SDK通信替换FATE通信
    - 目前采用直接传输RollPair所指向的数据的方案
    - 在secure_boost模型上测试正常

- 时空自动机器学习
  - 看书《深入理解AutoML和AutoDL》，大致了解了下现有的一些AutoML的方法和一些开源框架。
  - 在KuAI上学习了创建了自定义的docker镜像并上传和使用，且阅读了KuAI的使用文档

- 时空多源数据融合
  - 阅读论文并做了简单的笔记和ppt：《Methodologies for Cross-Domain Data Fusion: An Overview》。

## 10-12 ~ 10-6

- 数字网关项目
  - 调研了开源FL库：FedML并做了分享，其特点为灵活，主要用于FL科研。
  - 协助@王若兰，@杜师帅进行3.0版本的FATE和网关的迁移，DataIO组件。