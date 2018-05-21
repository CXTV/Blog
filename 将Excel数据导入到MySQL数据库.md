# 将Excel数据导入到MySQL数据库



```
#coding:utf-8


import pandas as pd
import xlrd
"""
功能：将Excel数据导入到MySQL数据库
"""
import xlrd
import pymssql
# Open the workbook and define the worksheet
book = xlrd.open_workbook("1.xls")
sheet = book.sheet_by_name("Sheet1")

conn = pymssql.connect(host='127.0.0.1:1433', user='sa', password='shangxi', database='sycm')


cursor = conn.cursor()

# 创建插入SQL语句
query = """INSERT INTO trace_test1 (source,sourcedet,uv,uv2,mon) VALUES (%s,%s,%s,%s,%s)"""

mon = '2017-01-10'
for r in range(7,sheet.nrows):

      item = sheet.row_values(r)
      source = item[1]
      sourcedet = item[2]
      uv = item[3]
      uv2 = item[4]
      values = (source, sourcedet, uv, uv2, mon)
      cursor.execute(query, values)




# 关闭游标
cursor.close()
# 提交
conn.commit()
# 关闭数据库连接
conn.close()
```

## 将PC数据保存至数据库

```
#coding:utf-8


import pandas as pd
import xlrd
"""
功能：将Excel数据导入到MySQL数据库
"""
import xlrd
import pymssql
# Open the workbook and define the worksheet
book = xlrd.open_workbook("pcdata.xls")
sheet = book.sheet_by_name("PC流量来源")
#
conn = pymssql.connect(host='127.0.0.1:1433', user='sa', password='shangxi', database='sycm')
#
#
cursor = conn.cursor()
#
# # 创建插入SQL语句
query = """INSERT INTO trace_all(port,shopname,mon,source, sourcedet, uv, uv2,newUv,newUv2,pv,pv2,avgPv,avgPv2,cltCnt,cltCnt2,cartByrCnt,cartByrCnt2,bounceRate,bounceRate2,
                                    crtVldAmt,crtVldAmt2,crtByrCnt,crtByrCnt2,crtRate,crtRate2,payAmt,payAmt2,payByrCnt,payByrCnt2,payRate,payRate2,payPct,payPct2,uvValue,uvValue2) VALUES (%s,%s,
                                    %s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s)"""
#

port = '1'
shopname = '健足乐'
mon = '2017-05-1'
for r in range(6,sheet.nrows):

      item = sheet.row_values(r)
      source = item[0]
      sourcedet = item[1]
      uv = item[2]
      uv2 = item[3]
      newUv = item[4]
      newUv2 = item[5]
      pv = item[6]
      pv2 = item[7]
      avgPv = item[8]
      avgPv2 = item[9]
      cltCnt = item[10]
      cltCnt2 = item[11]
      cartByrCnt = item[12]
      cartByrCnt2 = item[13]
      bounceRate = item[14]
      bounceRate2 = item[15]
      crtVldAmt = item[16]
      crtVldAmt2 = item[17]
      crtByrCnt = item[18]
      crtByrCnt2 = item[19]
      crtRate = item[20]
      crtRate2 = item[21]
      payAmt = item[22]
      payAmt2 = item[23]
      payByrCnt = item[24]
      payByrCnt2 = item[25]
      payRate = item[26]
      payRate2 = item[27]
      payPct = item[28]
      payPct2 = item[29]
      uvValue = item[30]
      uvValue2 = item[31]
      payByrCnt, payByrCnt2,

      # print(payBryCnt)
      values = (port,shopname,mon,source, sourcedet, uv, uv2,newUv,newUv2,pv,pv2,avgPv,avgPv2,cltCnt,cltCnt2,cartByrCnt,
                cartByrCnt,bounceRate,bounceRate2,crtVldAmt,crtVldAmt2,crtByrCnt,crtByrCnt2,crtRate,crtRate2,payAmt,payAmt2,
                payByrCnt, payByrCnt2,payRate,payRate2,payPct,payPct2,uvValue,uvValue2)

      cursor.execute(query, values)




# 关闭游标
cursor.close()
# 提交
conn.commit()
# 关闭数据库连接
conn.close()
```
## 将mob数据保存到数据库

```
#coding:utf-8


import pandas as pd
import xlrd
"""
功能：将Excel数据导入到MySQL数据库
"""
import xlrd
import pymssql
# Open the workbook and define the worksheet
book = xlrd.open_workbook("mobdata.xls")
sheet = book.sheet_by_name("无线流量来源")
#
conn = pymssql.connect(host='127.0.0.1:1433', user='sa', password='shangxi', database='sycm')
#
#
cursor = conn.cursor()
#

# # 创建插入SQL语句
query = """INSERT INTO trace_all2(port,shopname,mon,source, sourcedet, uv, uv2,crtVldAmt,crtVldAmt2,crtByrCnt,crtByrCnt2,crtRate,crtRate2,
                                    payAmt,payAmt2,payByrCnt,payByrCnt2,payRate,payRate2,payPct,payPct2,uvValue,uvValue2,shopCltByrCnt,shopCltByrCnt2,
                                    cltItmCnt,cltItmCnt2,cartByrCnt,cartByrCnt2,newUv,newUv2) VALUES (%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s)"""
#


port = '2'
shopname = '健足乐'
mon = '2017-05-1'
for r in range(6,sheet.nrows):

    item = sheet.row_values(r)
    source = item[0]
    sourcedet = item[1]
    uv = item[2]
    uv2 = item[3]
    crtVldAmt = item[4]
    crtVldAmt2 = item[5]
    crtByrCnt = item[6]
    crtByrCnt2 = item[7]
    crtRate = item[8]
    crtRate2 = item[9]
    payAmt = item[10]
    payAmt2 = item[11]
    payByrCnt = item[12]
    payByrCnt2 = item[13]
    payRate = item[14]
    payRate2 = item[15]
    payPct = item[16]
    payPct2 = item[17]
    uvValue = item[18]
    uvValue2 = item[19]
    shopCltByrCnt = item[20]
    shopCltByrCnt2 = item[21]
    cltItmCnt = item[22]
    cltItmCnt2 = item[23]
    cartByrCnt = item[24]
    cartByrCnt2 = item[25]
    newUv = item[26]
    newUv2 = item[27]


#
    values = (port,shopname,mon,source, sourcedet, uv, uv2,crtVldAmt,crtVldAmt2,crtByrCnt,crtByrCnt2,crtRate,crtRate2,
            payAmt,payAmt2,payByrCnt,payByrCnt2,payRate,payRate2,payPct,payPct2,uvValue,uvValue2,shopCltByrCnt,shopCltByrCnt2,
            cltItmCnt,cltItmCnt2,cartByrCnt,cartByrCnt2,newUv,newUv2)

    cursor.execute(query, values)



# 关闭游标
cursor.close()
# 提交
conn.commit()
# 关闭数据库连接
conn.close()
```

## 两张表数据合并（未判断是否存在）

```
#coding:utf-8

import logging

"""
将pc_excel存入到数据库
"""
import xlrd
import pymssql

# HOST = '127.0.0.1:1433'
# USER = 'sa'
# PWD = 'shangxi'
# DB = 'sycm'


logging.basicConfig(datefmt='%Y-%m-%d %H:%M:%S', format='[%(asctime)s] %(levelname)s:%(message)s', level=logging.DEBUG,
                    filename="sycmtrace.log")



def save2excel(xls_name,port,shopname,mon):

    conn = pymssql.connect(host='127.0.0.1:1433', user='sa', password='shangxi', database='sycm')

    cursor = conn.cursor()
    
    #插入pc流量数据
    if port == '1':
        book = xlrd.open_workbook(xls_name)
        sheet = book.sheet_by_name("PC流量来源")

        query = """INSERT INTO trace_all2(port,shopname,mon,source, sourcedet, uv, uv2,newUv,newUv2,pv,pv2,avgPv,avgPv2,cltCnt,cltCnt2,cartByrCnt,cartByrCnt2,bounceRate,bounceRate2,
                                            crtVldAmt,crtVldAmt2,crtByrCnt,crtByrCnt2,crtRate,crtRate2,payAmt,payAmt2,payByrCnt,payByrCnt2,payRate,payRate2,payPct,payPct2,uvValue,uvValue2) VALUES (%s,%s,
                                            %s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s)"""
        for r in range(6,sheet.nrows):

            item = sheet.row_values(r)
            source = item[0]
            sourcedet = item[1]
            uv = item[2]
            uv2 = item[3]
            newUv = item[4]
            newUv2 = item[5]
            pv = item[6]
            pv2 = item[7]
            avgPv = item[8]
            avgPv2 = item[9]
            cltCnt = item[10]
            cltCnt2 = item[11]
            cartByrCnt = item[12]
            cartByrCnt2 = item[13]
            bounceRate = item[14]
            bounceRate2 = item[15]
            crtVldAmt = item[16]
            crtVldAmt2 = item[17]
            crtByrCnt = item[18]
            crtByrCnt2 = item[19]
            crtRate = item[20]
            crtRate2 = item[21]
            payAmt = item[22]
            payAmt2 = item[23]
            payByrCnt = item[24]
            payByrCnt2 = item[25]
            payRate = item[26]
            payRate2 = item[27]
            payPct = item[28]
            payPct2 = item[29]
            uvValue = item[30]
            uvValue2 = item[31]

            values = (port,shopname,mon,source, sourcedet, uv, uv2,newUv,newUv2,pv,pv2,avgPv,avgPv2,cltCnt,cltCnt2,cartByrCnt,
                    cartByrCnt2,bounceRate,bounceRate2,crtVldAmt,crtVldAmt2,crtByrCnt,crtByrCnt2,crtRate,crtRate2,payAmt,payAmt2,
                    payByrCnt, payByrCnt2,payRate,payRate2,payPct,payPct2,uvValue,uvValue2)

            cursor.execute(query, values)
            logging.info('pc端数据插入')
    elif port == '2':
        #插入mob端数据
        book = xlrd.open_workbook(xls_name)
        sheet = book.sheet_by_name("无线流量来源")

        query = """INSERT INTO trace_all2(port,shopname,mon,source, sourcedet, uv, uv2,crtVldAmt,crtVldAmt2,crtByrCnt,crtByrCnt2,crtRate,crtRate2,
                                        payAmt,payAmt2,payByrCnt,payByrCnt2,payRate,payRate2,payPct,payPct2,uvValue,uvValue2,shopCltByrCnt,shopCltByrCnt2,
                                        cltItmCnt,cltItmCnt2,cartByrCnt,cartByrCnt2,newUv,newUv2) VALUES (%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s)"""
        for r in range(6, sheet.nrows):
            item = sheet.row_values(r)
            source = item[0]
            sourcedet = item[1]
            uv = item[2]
            uv2 = item[3]
            crtVldAmt = item[4]
            crtVldAmt2 = item[5]
            crtByrCnt = item[6]
            crtByrCnt2 = item[7]
            crtRate = item[8]
            crtRate2 = item[9]
            payAmt = item[10]
            payAmt2 = item[11]
            payByrCnt = item[12]
            payByrCnt2 = item[13]
            payRate = item[14]
            payRate2 = item[15]
            payPct = item[16]
            payPct2 = item[17]
            uvValue = item[18]
            uvValue2 = item[19]
            shopCltByrCnt = item[20]
            shopCltByrCnt2 = item[21]
            cltItmCnt = item[22]
            cltItmCnt2 = item[23]
            cartByrCnt = item[24]
            cartByrCnt2 = item[25]
            newUv = item[26]
            newUv2 = item[27]


            values = (port, shopname, mon, source, sourcedet, uv, uv2, crtVldAmt, crtVldAmt2, crtByrCnt, crtByrCnt2, crtRate, crtRate2,
                        payAmt, payAmt2, payByrCnt, payByrCnt2, payRate, payRate2, payPct, payPct2, uvValue, uvValue2, shopCltByrCnt,
                         shopCltByrCnt2,cltItmCnt, cltItmCnt2, cartByrCnt, cartByrCnt2, newUv, newUv2)

            cursor.execute(query, values)
            logging.info('无线端数据插入成功')

    # 关闭游标
    cursor.close()
    # 提交
    conn.commit()
    # 关闭数据库连接
    conn.close()
```