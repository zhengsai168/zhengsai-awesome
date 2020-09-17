# Series对象

```python
data = pd.Series([0.25,0.5,0.75,1.0])

data.values

data.index

data[1]

data[1:3]

data = pd.Series([0.25,0.5,0.75,1.0],index=['a','b','c','d'])

data

data['b']

test_dict = {'a':1,'b':2,'c':3}

pd.Series(test_dict)
                 
pd.Series(test_dict,index=['a','c'])
```

