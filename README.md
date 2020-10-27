# [论文笔记](paper-note)

# [Linux笔记](Linux-note)

# [Python笔记](python-note)

# [Torch](python-note/torch)

### [Python标准库](python-note)

### [jupyter notebook](python-note/jupyter)

### [numpy](python-note/numpy-note)

### [pandas](python-note/pandas)

# [算法题笔记](algorithm-note)

## [C++模板](algorithm-note)

## [LeetCode题目分类+模板(python)](algorithm-note/LeetCode)

# [周报](work-note)

# [简历](resume)



# tmp

- Python由于GIL（Global Interpreter Lock，全局解释锁）的存在，使得一个核在同一时间只能运行一个线程，所以多线程反而变慢了（对于cpu密集型任务）。推荐使用multi

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





git pull origin dev_3.0_distributed