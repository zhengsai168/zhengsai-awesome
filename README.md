# [设计模式](design-pattern)

# [论文笔记](paper-note)

# [Linux笔记](Linux-note)

# [Python笔记](python-note)

# [Torch](python-note/torch)

### [Python标准库](python-note)

### [Python规范](python-note/python-rule)

### [jupyter notebook](python-note/jupyter)

### [numpy](python-note/numpy-note)

### [pandas](python-note/pandas)

# [算法题笔记](algorithm-note)

## [C++模板](algorithm-note)

## [LeetCode题目分类+模板(python)](algorithm-note/LeetCode)

# [周报](work-note)

# [简历](resume)



# tmp

- Python由于GIL（Global Interpreter Lock，全局解释锁）的存在，使得一个核在同一时间只能运行一个线程，所以多线程反而变慢了（对于cpu密集型任务）。推荐使用多进程。
- pycharm 一键规范化代码  ctrl + alt + L

# FATE代码改动

```python
/data/projects/fate/python/federatedml/feature/sampler.py   line 131
# callback
\python\federatedml\param\sample_param.py 
和
\python\federatedml\feature\sampler.py
多处修改 为了 添加按数量 采样的功能
```

开发 目录

/export/icity/eggroll

/export/icity/model

# 开发环境配置

```shell
/export/icity/model/federated_learning_models/config.properties

[tmp_var]
SDK_TAG = 10000 # 保证每次起任务tag不一样，之后删除

run_train.sh 中的params参数 3台机器上不一样

新装的包
Deprecated 1.2.10
把fate_flow 装回到 distributed_fml_lib

eggroll  
有进程残留的问题 和 session 有关
```

# 网关 后端服务

```shell
---------先切换用户-----
用户
gateway-azkaban 
密码
TMoo0bhMe8ggYJkeQGqxmgWx

10.241.241.7  和 10.241.241.6
/export/icity/model-gateway/bin

/10.241.241.8
/export/icity/gw-service-center/bin

url  (str)
http://gw.sdk.host:8288/sdk/api/dest

param  (str)
{"sessionId": "", "taskId": "P61-T10-I1", "source": "a4c64803b9a74f29953873ebf2204b35", "destCode": null, "op": null, "destSource": null, "type": null}

headers  (dict)
{'Content-Type': 'application/json'}

response_json = requests.post(url=url, data=param, headers=headers).json()
```

# FATE 集群环境

```
两张表
01机器：
breast_host
dev
03机器：
breast_guest
dev

```



git pull origin dev_3.0_distributed



密码：

08.04

10.28

