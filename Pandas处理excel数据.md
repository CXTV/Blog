# Pandas处理excel数据

[TOC]



## 1.处理表上面的不符合表结构的中文

示例表：trace2

```
# coding: utf-8

import numpy as np
import pandas as pd


data = pd.read_excel('trace2.xls')   #读取成为dataframe格式
b = data.drop(np.arange(0,4))        #
c = b[0:1].T
d = c.values

liebiao=[]
for i in d:
    for x in i:
        liebiao.append(x)

b.columns=liebiao
e = b.drop([4])
e.index=range(len(e))

# print(e)

e.to_excel('1.xls')
```

## 2. 向 DataFrame 添加一列，该列为同一值



```

```

## 3.pandas处理excel并且存入数据库sqlserver

```
# coding: utf-8

import numpy as np
import pandas as pd
from sqlalchemy import create_engine
import pymssql



data = pd.read_excel('trace2.xls')
b = data.drop(np.arange(0,4))
c = b[0:1].T
d = c.values

liebiao=[]
for i in d:
    for x in i:
        liebiao.append(x)

b.columns=liebiao
e = b.drop([4])
e.index=range(len(e))



e['mon'] = '2017-05-01'
e['shopName'] = '健足乐'
e['port'] = '无线端'

# print(e)
# e.to_excel('1.xls')

e.rename(columns={'来源':'source','来源明细':'sourceDet','访客数':'uv','访客数变化':'uv2','下单金额':'crtVldAmt','下单金额变化':'crtVldAmt2','下单买家数':'crtByrCnt','下单买家数变化':'crtByrCnt2','下单转化率':'crtRate','下单转化率变化':'crtRate2','支付金额':'payAmt','支付金额变化':'payAmt2','支付买家数':'payByrCnt ','支付买家数变化':'payByrCnt2','支付转化率':'payRate','支付转化率变化':'payRate2','客单价':'payPct','客单价变化':'payPct2','UV价值':'uvValue','uv价值变化':'uvValue2','关注店铺买家数':'shopCltByrCnt','关注店铺买家数变化':'shopCltByrCnt2','收藏商品买家数':'cltItmCnt','收藏商品买家数变化':'cltItmCnt2','加购人数':'cartByrCnt','加购人数变化':'cartByrCnt2','新访客':'newUv','新访客变化':'newUv2'}, inplace = True)
# print(e)
# e.to_excel('2.xls')

user='sa'
passwd='shangxi'
host='127.0.0.1'
port = '1433'
db_name='sycm'
engine = create_engine('mssql+pymssql://{0}:{1}@{2}:{3}/{4}?charset=utf8'.format(user,passwd,host,port,db_name))

e.to_sql('trace_data2',con =engine,if_exists='append',index=False)

```

## 4.pandas合并两个表填补空白数据



```
# coding: utf-8

import numpy as np
import pandas as pd
from sqlalchemy import create_engine

#清洗表结构
data = pd.read_excel('pc_trace.xls')

b = data.drop(np.arange(0,4))
c = b[0:1].T
d = c.values

liebiao=[]
for i in d:
    for x in i:
        liebiao.append(x)

b.columns=liebiao
e = b.drop([4])

e.index=range(len(e))


#mob
e.rename(columns={'来源':'source','来源明细':'sourcedet','访客数':'uv','访客数变化':'uv2','下单金额':'crtvldamt',
                  '下单金额变化':'crtvldamt2','下单买家数':'crtbyrcnt','下单买家数变化':'crtbyrcnt2','下单转化率':'crtrate',
                  '下单转化率变化':'crtrate2','支付金额':'payamt','支付金额变化':'payamt2','支付买家数':'paybyrcnt ',
                  '支付买家数变化':'paybyrcnt2','支付转化率':'payrate','支付转化率变化':'payrate2','客单价':'paypct',
                  '客单价变化':'paypct2','UV价值':'uvvalue','uv价值变化':'uvvalue2','关注店铺买家数':'shopcltbyrcnt',
                  '关注店铺买家数变化':'shopcltbyrcnt2','收藏商品买家数':'cltitmcnt','收藏商品买家数变化':'cltitmcnt2',
                  '加购人数':'cartbyrcnt','加购人数变化':'cartbyrcnt2','新访客':'newuv','新访客变化':'newuv2'}, inplace = True)

# e.to_excel('2.xls')

#pc
e.rename(columns={'来源': 'source', '来源明细': 'sourcedet', '访客数': 'uv', '访客数变化': 'uv2', '新访客': 'newuv', '新访客变化': 'newuv2',
                  '浏览量':'pv','浏览量变化':'pv2','人均浏览量':'avgpv ','人均浏览量变化':'avgpv2','收藏人数':'cltcnt','收藏人数变化':'cltcnt2',
                  '加购人数': 'cartByrcnt', '加购人数变化': 'cartByrcnt2','跳失率':'bouncerate','跳失率变化':'bouncerate2','下单金额': 'crtvldamt',
                  '下单金额变化': 'crtvldamt2','下单买家数': 'crtbyrcnt', '下单买家数变化': 'crtbyrcnt2','下单转化率': 'crtrate', '下单转化率变化': 'crtrate2',
                  '支付金额': 'payamt', '支付金额变化': 'payamt2','支付买家数': 'paybyrcnt', '支付买家数变化': 'paybyrcnt2', '支付转化率': 'payrate',
                  '支付转化率变化': 'payrate2', '客单价': 'paypct', '客单价变化': 'paypct2','UV价值': 'uvvalue', 'uv价值变化': 'uvvalue2'}, inplace=True)




# #处理pc表结构添加字段
# col_name = e.columns.tolist()
# # print(col_name)
# col_name.insert(0,'shopName')
# col_name.insert(1,'port')
# col_name.insert(2,'mon')
# pc = e.reindex(columns=col_name)
#
# pc['mon'] = '2017-05-01'
# pc['shopName'] = '健足乐'
# a['port'] = 'pc端'

#保存处理好的pc excel
# a.to_excel('change_pc.xls')



# 读取mob表
datamob = pd.read_excel('2.xls')

datapc = pd.read_excel('pcxls.xls')

df_new = pd.merge(datamob,datapc,
                  on=['source', 'shopName', 'mon', 'sourcedet', 'uv', 'uv2', 'crtbyrCnt', 'crtbyrcnt2',
                      'crtrate', 'crtrate2', 'payamt', 'payamt2','paybyrcnt', 'paybyrcnt2','payrate', 'payrate2',
                      'paypct', 'paypct2','uvvalue','uvvalue2', 'newuv', 'newuv2', 'port', 'crtvldamt', 'crtvldamt2'], how='outer')

a = df_new
# a= df_new.fillna('NaN')

# print(a)
# a.to_excel('pcandmob22.xls')
# col_name = e.columns.tolist()
# # print(col_name)
# col_name.insert(0,'shopName')
# col_name.insert(1,'port')
# col_name.insert(2,'mon')
# a = e.reindex(columns=col_name)
#
# a['mon'] = '2017-05-01'
# a['shopName'] = '健足乐'
# a['port'] = 'pc端'

#保存pc数据
# print(a)
# a.to_excel('change_pc.xls')



# b = pd.read_excel('pcandmob22.xls')
# # print(e)
# # print(datamod)
# # a.to_excel('all_xls77.xls')
# # print(df_new)
user='sa'
passwd='shangxi'
host='127.0.0.1'
port = '1433'
db_name='sycm'
engine = create_engine('mssql+pymssql://{0}:{1}@{2}:{3}/{4}?charset=utf8'.format(user,passwd,host,port,db_name))
a.to_sql('trace_data2',con =engine, if_exists='replace',index=False)





```



## 5.更改表位置

```
#处理pc表结构添加字段
col_name = e.columns.tolist()
# print(col_name)
col_name.insert(0,'shopName')
col_name.insert(1,'port')
col_name.insert(2,'mon')
pc = e.reindex(columns=col_name)

pc['mon'] = '2017-05-01'
pc['shopName'] = '健足乐'
pc['port'] = 'pc端'
```