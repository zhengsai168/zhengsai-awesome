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

# FATE-1.5

```
两张表
01机器：
hetero_breast_host
experiment
02机器：
hetero_breast_guest
experiment
```

上传数据

命令：
`python /data/projects/fate/python/fate_flow/fate_flow_client.py -f upload -c upload_data_breast_hetero_guest.json`

json文件： `upload_data_breast_hetero_guest.json`

```json
{
  "file": "/data/projects/fate/examples/data/breast_hetero_guest.csv",  #文件
  "table_name": "hetero_breast_guest",   # 表名
  "namespace": "experiment",   # 命名空间
  "head": 1,
  "partition": 8,
  "work_mode": 1,    # 注意设置 0 为单机， 1 为集群
  "backend": 0     # 0为eggroll ， 1位spark
}
```

提交任务

命令

`python /data/projects/fate/python/fate_flow/fate_flow_client.py -f submit_job -d lr_with_feature_engineering_dsl.json -c lr_with_feature_engineering_job_conf.json`

DSL 文件

`lr_with_feature_engineering_dsl.json`

```json
{
    "components" : {
        "dataio_0": {
            "module": "DataIO",
            "input": {
                "data": {
                    "data": [
                        "args.train_data"
                    ]
                }
            },
            "output": {
                "data": ["train"],
                "model": ["dataio"]
            }
         },
         "intersection_0": {
             "module": "Intersection",
             "input": {
                 "data": {
                     "data": [
                         "dataio_0.train"
                     ]
                 }
             },
             "output": {
                 "data": ["train"]
             }
         },
        "feature_scale_0": {
            "module": "FeatureScale",
            "input": {
                "data": {
                    "data": [
                        "intersection_0.train"
                    ]
                }
            },
            "output": {
                "data": ["train"],
                "model": ["feature_scale"]
            }
        },
        "hetero_feature_binning_0": {
            "module": "HeteroFeatureBinning",
            "input": {
                "data": {
                    "data": [
                        "feature_scale_0.train"
                    ]
                }
            },
            "output": {
                "data": ["transform_data"],
                "model": ["binning_model"]
            }
        },
        "hetero_feature_selection_0": {
            "module": "HeteroFeatureSelection",
            "input": {
                "data": {
                    "data": [
                        "hetero_feature_binning_0.transform_data"
                    ]
                },
                "isometric_model": [
                    "hetero_feature_binning_0.binning_model"
                ]
            },
            "output": {
                "data": ["train"],
                "model": ["selected"]
            }
        },
        "one_hot_encoder_0": {
            "module": "OneHotEncoder",
            "input": {
                "data": {
                    "data": [
                        "hetero_feature_selection_0.train"
                    ]
                }
            },
            "output": {
                "data": ["train"],
                "model": ["model"]
            }
        },
        "hetero_lr_0": {
            "module": "HeteroLR",
            "input": {
                "data": {
                    "train_data": ["one_hot_encoder_0.train"]
                }
            },
            "output": {
                "data": ["train"],
                "model": ["hetero_lr"]
            }
        },
        "evaluation_0": {
            "module": "Evaluation",
            "input": {
                "data": {
                    "data": ["hetero_lr_0.train"]
                }
            }
        }
    }
}

```

job_conf文件

`lr_with_feature_engineering_job_conf.json`

```json
{
    "initiator": {
        "role": "host",
        "party_id": 10000
    },
    "job_parameters": {
        "work_mode": 1
    }, 
    "role": {
        "guest": [
            9999
        ],
        "host": [
            10000
        ],
        "arbiter": [
            10000
        ]
    },
    "role_parameters": {
        "guest": {
            "args": {
                "data": {
                    "train_data": [
                        {
                            "name": "hetero_breast_guest",
                            "namespace": "experiment"
                        }
                    ]
                }
            },
            "dataio_0": {
                "with_label": [
                    true
                ],
                "label_name": [
                    "y"
                ],
                "label_type": [
                    "int"
                ],
                "output_format": [
                    "dense"
                ],
                "missing_fill": [
                    true
                ],
                "outlier_replace": [
                    true
                ]
            },
            "evaluation_0": {
                "eval_type": [
                    "binary"
                ],
                "pos_label": [
                    1
                ]
            }
        },
        "host": {
            "args": {
                "data": {
                    "train_data": [
                        {
                            "name": "hetero_breast_host",
                            "namespace": "experiment"
                        }
                    ]
                }
            },
            "dataio_0": {
                "with_label": [
                    false
                ],
                "output_format": [
                    "dense"
                ],
                "outlier_replace": [
                    true
                ]
            },
            "evaluation_0": {
                "need_run": [
                    false
                ]
            }
        }
    },
    "algorithm_parameters": {
        "feature_scale_0": {
            "method": "standard_scale",
            "need_run": true
        },
        "hetero_feature_binning_0": {
            "method": "quantile",
            "compress_thres": 10000,
            "head_size": 10000,
            "error": 0.001,
            "bin_num": 10,
            "bin_indexes": -1,
            "adjustment_factor": 0.5,
            "local_only": false,
            "need_run": true,
            "transform_param": {
                "transform_cols": -1,
                "transform_type": "bin_num"
            }
        },
        "hetero_feature_selection_0": {
            "select_col_indexes": -1,
            "filter_methods": [
                "manually",
                "iv_value_thres",
                "iv_percentile"
            ],
            "manually_param": {
                "filter_out_indexes": null
            },
            "iv_value_param": {
                "value_threshold": 1.0
            },
            "iv_percentile_param": {
                "percentile_threshold": 0.9
            },
            "need_run": true
        },
        "one_hot_encoder_0": {
            "transform_col_indexes": -1,
            "transform_col_names": null,
            "need_run": true
        },
        "hetero_lr_0": {
            "penalty": "L2",
            "optimizer": "rmsprop",
            "tol": 1e-05,
            "alpha": 0.01,
            "max_iter": 10,
            "early_stop": "diff",
            "batch_size": -1,
            "learning_rate": 0.15,
            "init_param": {
                "init_method": "random_uniform"
            },
            "cv_param": {
                "n_splits": 5,
                "shuffle": false,
                "random_seed": 103,
                "need_cv": false
            }
        }
    }
}

```



git pull origin dev_3.1



密码：

08.04

10.28



网关和城操的融合：

postman起任务需要把cookie写进去



开发环境的表：

01 - arbiter

02 - guest  无标签 

03 -host  有标签

`namespace：  `

zhengsai

`table_name：`

hetero_breast_guest_with_empty_int

hetero_breast_host_with_empty_int

```
handled_hetero_breast_guest_with_empty_int
```

```
handled_hetero_breast_host_with_empty_int
```

`hadleData`下

"withLabel":true,  //有label为true，无label为false

"labelColumns": "",  // 无label 为 空字符串，

 "labelType": ""  //  int, or float  无label为空





DataIO 要指定数据类型（oneHot必须为int类型的）



如何在无label 的情况下分配guest和host？



```python
import _init_path
from arch.api import session
import uuid
session.init(str(uuid.uuid1()),1,0)


data = session.table(name="handled_hetero_breast_host_with_empty_int", namespace="zhengsai")
data = session.table(name="handled_hetero_breast_guest_with_empty_int", namespace="zhengsai")

data = session.table(name="hetero_breast_host_with_empty_int", namespace="zhengsai")
data = session.table(name="hetero_breast_guest_with_empty_int", namespace="zhengsai")
```

IO 之后有了schema

正常保存可以用get_metas得到schema



