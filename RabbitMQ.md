# RabbitMQ

我的环境是Ubuntu 14.04.1 LTS

## 安装erlang

```
sudo apt-get install build-essential   
sudo apt-get install libncurses5-dev   
sudo apt-get install libssl-dev
sudo apt-get install erlang

```

## 安装rabbitMQ

```
sudo apt-get install rabbitmq-server

```

## 安装管理插件rabbitMQweb

```
sudo rabbitmq-plugins enable rabbitmq_management
```

登录密码是:guest/guest

## 安装RabbitMQ libraries

RabbitMQ遵循AMQP协议，为了使用rabbitmq，你需要一个库来解读这个协议，对于python来说，你需要安装下面库函数中的任意一个即可：

```
>py-amqplib
>txAMQP
>pika
```

这里选择pika

```
sudo pip install pika
```

## 简单理解

RabbitMQ相当于一个消息代理，他完成接收和转发消息的功能，你可以把它想成一个邮局，起到中转作用

1. Producer:用来发送消息的程序被称为一个producer
2. Queue: 队列，相当于邮箱的作用，他在创建后一直存活与RabbitMQ中，虽然消息可以在你的程序之间流动，但是在这中间的过程中，消息必须存在queue中，一下queue没有大小限制，你可以存无数的消息，（前提你必须预留1GB的硬盘空间），他就相当于一个没有限制的缓存。多个Producer可以发送消息到同一个queue，多个Consumer也可以从同一个queue中接收消息
3. Consumer: 一个用来接收消息的程序称之为Consumer

## 点对点通信

我们实现一个helloword的一对一的通信,一个发送方,一个接收方

### 客户端 client.py

```
#导入pika
import pika

#建立与rabbitMQ-server的连接
connection = pika.BlockingConnection(pika.ConnectionParameters(host = 'localhost'))
channel = connection.channel()
#确定queue是否存在,不存在则建立
channel.queue_declare(queue = 'hello')
#消息不直接发送给queue, 要经过一个exchange
channel.basic_publish(exchange='', routing_key='hello', body='Hello World!')
print "[x] send 'Hello World!'"
#关闭连接
connection.close()
```

### 服务端server.py

```
import pika

connection = pika.BlockingConnection(pika.ConnectionParameters(host='localhost'))
channel = connection.channel()

channel.queue_declare(queue='hello')

print ' [*] Waiting for messages. To exit press CTRL+C'

#我们要定义一个callback函数，在我们接受到消息的时候，pika库会调用callback函数，在我们的程序里，callback函数就是将接收到的消息打印在屏幕上
def callback(ch, method, properties, body):
    print " [x] Received %r" % (body,)

#接下来我们需要告诉Rabbitmq，这个特殊的函数callback（）的功能，就是从hello的queue中接收消息
channel.basic_consume(callback, queue='hello', no_ack=True)
开启一个永不停止的线程来等待消息，在需要的时候运行callback（）函数
channel.start_consuming()
```

### 运行

1. 运行server.py

   ```
   python server.py
   ```

2. 运行client.py

   ```
   python client.py
   ```

3. 查看web界面
   web界面对各个元素都有记录, 我们能看到刚才的操作
   [![img](http://maqiangthunder.github.io/2016/04/03/rabbitMQ/rabbitMQ%E5%AD%A6%E4%B9%A01/QQ%E6%88%AA%E5%9B%BE20160403231352.png)](http://maqiangthunder.github.io/2016/04/03/rabbitMQ/rabbitMQ%E5%AD%A6%E4%B9%A01/QQ%E6%88%AA%E5%9B%BE20160403231352.png)

## 命令

```
sudo rabbitmqctl list_queues
sudo rabbitmqctl list_exchanges
sudo rabbitmqctl list_bindings
```