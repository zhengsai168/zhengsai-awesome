# 多源数据融合
## 综述
- Zheng, Y. (2015). Methodologies for Cross-Domain Data Fusion: An Overview. IEEE Transactions on Big Data, 1(1), 16–34. https://doi.org/10.1109/tbdata.2015.2465959

### 多源数据定义

来自不同领域的数据集，例如我们要改善城市规划，可能要用到的数据集有：路网数据，交通流量数据，POI数据，人口数据。
这些数据就是来自不同领域的数据，需要更好地融合这些数据集中知识。

### 方法分类
1. **STAGE-BASED** 

在数据挖掘任务的不同阶段，采用不同的数据集。

**例子1（路网数据和出租车轨迹数据）：**

stage1：通过主干路网将城市划成不同区域

! [1](pic/1.png)

stage2：通过出租车轨迹数据，画出一个graph，点代表stage1中构造的区域，
边代表出租车的移动。

! [2](pic/2.png)

最终通过这个graph可以用来分析很多东西（比如哪两个区域的路规划的不好）

**例子2（用户轨迹和POI数据）**

stage1：通过轨迹数据获取用户的驻留点

stage2：通过驻留点的POI数据，将驻留点描述成一个向量，将向量进行层次聚类，
得到一个树状的结构

stage3：由于不同用户的轨迹最终变成了驻留点向量，在不同的树形结构的不同layer
有不同的图结构。可以通过这个比较用户间的相似度

! [3](pic/3.png)

**例子3（）**

2. **FEATURE-LEVEL-BASED**



3. **SEMANTIC MEANING-BASED**

