# Python连接sql server





```
import pymssql


def insert_db(data_list):

    conn = pymssql.connect(host = '127.0.0.1:1433',user = 'sa',password = 'shangxi',database = 'new_test')  # 链接数据库
    cursor = conn.cursor()
    # 删除当日已插入数据，避免重复插入
    cursor.execute('DELETE FROM lm WHERE update_day=CURRENT_DATE()')

    sql = 'INSERT INTO sycm(id,runAsShopTitle, runAsShopId, cateName,cateId, uv, payAmt, rfdSucAmt) VALUES (%d,%s,%s,%s,%s,%s,%s,%s)'
    print(data_list)
    cursor.executemany(sql, data_list)
    conn.commit()  # 提交
    cursor.close()  # 关闭cursor
    conn.close()  # 关闭连接



a= [{'shopname': '健足乐旗舰', 'shopid': 569771360, 'catename': '女鞋', 'uv': 8599, 'payamt': 33071, 'rfdsucamt': 4258}, {'shopname': '健足乐旗舰', 'shopid': 569771360, 'catename': '流行男鞋', 'uv': 1854, 'payamt': 13745, 'rfdsucamt': 1523}, {'shopname': '健足乐旗舰', 'shopid': 569771360, 'catename': '男装', 'uv': 93, 'payamt': 1120, 'rfdsucamt': 0}]


new_list = [(1,'健足乐旗舰', 569771360, '女鞋', 50006843, 8599, 330711, 4258), (2,'健足乐旗舰', 569771360, '流行男鞋', 50011740, 1854, 13745, 1523)]
insert_db(new_list)
```

```
def insert_data(data_list):

    """
    存储到数据库
    :return:
    """
    try:

        conn = pymssql.connect(host=Host, user=User, password=Password, database=Date_base)
        cursor = conn.cursor()
        cursor.execute('DELETE FROM lm WHERE update_day=CURRENT_DATE()')
        conn.commit()  # 提交
        # 用executemany一次性提交爬取数据，比直接用execute快
        sql = 'INSERT INTO lm values(%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s)'
        cursor.executemany(sql, data_list)
        conn.commit()  # 提交
        cursor.close()  # 关闭cursor
        conn.close()  # 关闭连接
    except Exception as e:
        print
        e
        conn.rollback()


```

