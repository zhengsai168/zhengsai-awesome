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

2. **FEATURE-LEVEL-BASED**



3. **SEMANTIC MEANING-BASED**

