# python连接hive，并通过pandas进行分析



## python连接

- 开始之前还要装一些依赖

```python
pip install sasl
pip install thrift
pip install thrift-sasl
pip install PyHive
```



```python
from pyhive import presto
conn = presto.connect(protocol='https', host="~.com", port=~, username="你的账号", password="你的密码")
cursor = conn.cursor()
sql = "select * from hive.tmp.adjust_adid0408 limit 10"
cursor.execute(sql)
res = cursor.fetchall()
print(res)
for i in res:
    print(i)

# 转为DataFrame
df = pd.DataFrame(res)
# 列名还要自己写，100多个字段难搞
```



> 使用python虽然可以连接，但是再数据分析上还是pandas用起来爽



## pandas连接

```python
from pyhive import presto
import pandas as pd
conn = presto.connect(protocol='https', host="~.com", port=~, username="#", password="#")
df = pd.read_sql_query("select * from hrder_detail limit 20", conn)
# df = pd.read_sql("select * from hrder_detail limit 20", conn)
df
```

![image](https://user-images.githubusercontent.com/26622879/69540519-be0f4d00-0fc1-11ea-98bb-bb9621e84d94.png)

