---
layout: post
title: python kafka 生产者发送数据的三种方式
categories: [kafka]
description: python kafka 生产者发送数据的三种方式

keywords: kafka 
---


python kafka 生产者发送数据的三种方式

## 发送方式
### 同步发送

- 发送数据耗时最长

- 有发送数据的状态，不会丢失数据，数据可靠性高

以同步的方式发送消息时，一条一条的发送，对每条消息返回的结果判断， 可以明确地知道每条消息的发送情况，但是由于同步的方式会阻塞，只有当消息通过get返回future对象时，才会继续下一条消息的发送

### 异步发送
- 发送数据数据耗时最短

- 可能会丢失数据，数据可靠性低

因为不会获取消息发送的返回结果，这种方式的吞吐量是最高的，但是无法保证消息的可靠性，所以可能会丢失数据。

### 异步发送+回调处理
- 发送数据耗时速度较快

- 有发送数据的状态，不会丢失数据，数据可靠性较高

在调用send方法发送消息的同时，指定一个回调函数，服务器在返回响应时会调用该回调函数，通过回调函数能够对异常情况进行处理，当调用了回调函数时，只有回调函数执行完毕生产者才会结束，否则一直会阻塞。


## 其他说明


三种方式虽然在时间上有所差别，但并不是说时间越快的越好，具体要看业务的应用场景

```
场景1：如果业务要求消息必须是按顺序发送的，那么可以使用同步的方式，并且只能在一个partation上，结合参数设置retries的值让发送失败时重试，设置max_in_flight_requests_per_connection=1，可以控制生产者在收到服务器晌应之前只能发送1个消息，从而控制消息顺序发送；
```


```
场景2：如果业务只关心消息的吞吐量，容许少量消息发送失败，也不关注消息的发送顺序，那么可以使用发送并忘记的方式，并配合参数acks=0，这样生产者不需要等待服务器的响应，以网络能支持的最大速度发送消息；
```

```
场景3：如果业务需要知道消息发送是否成功，并且对消息的顺序不关心，那么可以用异步+回调的方式来发送消息，配合参数retries=0，并将发送失败的消息记录到日志文件中；
```

## 示例代码

```

# -*- coding:utf-8 -*-
# @FileName  :KProducer.py
# @Time      :2020/12/16
# @Author    :pylemon
import json
 
from kafka import KafkaConsumer, KafkaProducer
 
 
class KProducer:
    def __init__(self, bootstrap_servers, topic):
        """
        kafka 生产者
        :param bootstrap_servers: 地址
        :param topic:  topic
        """
        self.producer = KafkaProducer(
            bootstrap_servers=bootstrap_servers,
            value_serializer=lambda m: json.dumps(m).encode('ascii'), )  # json 格式化发送的内容
        self.topic = topic
 
    def sync_producer(self, data_li: list):
        """
        同步发送 数据
        :param data_li:  发送数据
        :return:
        """
        for data in data_li:
            future = self.producer.send(self.topic, data)
            record_metadata = future.get(timeout=10)  # 同步确认消费
            partition = record_metadata.partition  # 数据所在的分区
            offset = record_metadata.offset  # 数据所在分区的位置
            print('save success, partition: {}, offset: {}'.format(partition, offset))
 
    def asyn_producer(self,  data_li: list):
        """
        异步发送数据
        :param data_li:发送数据
        :return:
        """
        for data in data_li:
            self.producer.send(self.topic, data)
        self.producer.flush()  # 批量提交
 
    def asyn_producer_callback(self,  data_li: list):
        """
        异步发送数据 + 发送状态处理
        :param data_li:发送数据
        :return:
        """
        for data in data_li:
            self.producer.send(self.topic, data).add_callback(self.send_success).add_errback(self.send_error)
        self.producer.flush()  # 批量提交
 
    def send_success(self, *args, **kwargs):
        """异步发送成功回调函数"""
        print('save success')
        return
 
    def send_error(self, *args, **kwargs):
        """异步发送错误回调函数"""
        print('save error')
        return
 
    def close_producer(self):
        try:
            self.producer.close()
        except:
            pass
 
if __name__ == '__main__':
 
    send_data_li = [{"test": 1}, {"test": 2}]
    kp = KProducer(topic='topic', bootstrap_servers='127.0.0.1:9001,127.0.0.1:9002')
 
    # 同步发送
    kp.sync_producer(send_data_li)
 
    # 异步发送
    # kp.asyn_producer(send_data_li)
 
    # 异步+回调
    # kp.asyn_producer_callback(send_data_li)
    
    kp.close_producer()

```

## 转载
https://blog.csdn.net/qq_27648991/article/details/111622222