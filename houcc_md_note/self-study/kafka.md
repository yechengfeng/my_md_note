# Kafka

### Kafka下载与安装：

[Kafka入门级Windows环境下安装](https://blog.csdn.net/sinat_33236642/article/details/100730462)

### Springboot整合Kafka

###### 1. 引入jar包

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
<!--重点jar包-->
<dependency>
    <groupId>org.springframework.kafka</groupId>
    <artifactId>spring-kafka</artifactId>
    <version>2.3.7.RELEASE</version>
</dependency>
<dependency>
    <groupId>org.apache.logging.log4j</groupId>
    <artifactId>log4j-core</artifactId>
    <version>2.7</version>
</dependency>
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>fastjson</artifactId>
    <version>1.2.69</version>
</dependency>
```

###### 2. 序列化与反序列化文件（以JSONObject格式为例）

**序列化文件JsonSerializer.java **

```java
package com.content.search.kafka.serialization;

import com.alibaba.fastjson.JSON;
import com.alibaba.fastjson.JSONObject;
import org.apache.kafka.common.serialization.Serializer;

import java.util.Map;

/**
 * Created by houchangchang on 2020/7/1 9:20
 */
public class JsonSerializer implements Serializer<JSONObject> {
    @Override
    public void configure(Map<String, ?> configs, boolean isKey) {

    }

    @Override
    public byte[] serialize(String topic, JSONObject data) {
        return JSON.toJSONBytes(data);
    }

    @Override
    public void close() {

    }
}
```

**反序列化文件JsonDeserializer.java**	

```java
package com.content.search.kafka.serialization;

import com.alibaba.fastjson.JSON;
import com.alibaba.fastjson.JSONObject;
import org.apache.kafka.common.serialization.Deserializer;

import java.util.Map;

/**
 * Created by houchangchang on 2020/7/1 9:26
 */
public class JsonDeserializer implements Deserializer<JSONObject> {
    @Override
    public void configure(Map<String, ?> configs, boolean isKey) {

    }

    @Override
    public JSONObject deserialize(String topic, byte[] data) {
        return JSON.parseObject(data, JSONObject.class);
    }

    @Override
    public void close() {

    }
}
```

###### 3. application.properties配置

```properties
spring.kafka.bootstrap-servers=127.0.0.1:9092
#序列化和反序列化方式
spring.kafka.producer.key-serializer=org.apache.kafka.common.serialization.StringSerializer
spring.kafka.producer.value-serializer=com.content.search.kafka.serialization.JsonSerializer
spring.kafka.consumer.key-deserializer=org.apache.kafka.common.serialization.StringDeserializer
spring.kafka.consumer.value-deserializer=com.content.search.kafka.serialization.JsonDeserializer
#批量发送的数据大小
#spring.kafka.producer.batch-size=
#缓冲区大小
#spring.kafka.producer.buffer-memory=
#解决问题：消费监听接口监听的主题不存在时，默认会报错
spring.kafka.listener.missing-topics-fatal=false
```

###### 4. 生产者类与消费者类

**生产者类KafkaProducer.java**

```java
package com.content.search.kafka;

import com.alibaba.fastjson.JSONObject;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.kafka.core.KafkaTemplate;
import org.springframework.stereotype.Component;
import org.springframework.util.concurrent.FailureCallback;
import org.springframework.util.concurrent.ListenableFuture;
import org.springframework.util.concurrent.SuccessCallback;

/**
 * Created by houchangchang on 2020/7/1 18:03
 */
@Component
public class KafkaProducer {
    private static final Logger LOGGER = LoggerFactory.getLogger("KafkaProducer.class");

    @Autowired
    KafkaTemplate kafkaTemplate;

    public void sendMessage(String channel, JSONObject message) {
        ListenableFuture future = kafkaTemplate.send(channel, message);
        future.addCallback(new SuccessCallback() {
            @Override
            public void onSuccess(Object result) {
                LOGGER.info("发送成功，channel：{}, message：{}", channel, message);
            }
        }, new FailureCallback() {
            @Override
            public void onFailure(Throwable ex) {
                LOGGER.info("发送异常：{}", ex);
            }
        });
    }
}
```

**消费者类KafkaConsumer.java**

```java
package com.content.search.kafka;

import com.alibaba.fastjson.JSONObject;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.kafka.annotation.KafkaListener;
import org.springframework.stereotype.Component;

import java.util.Date;
import java.util.List;

/**
 * Created by houchangchang on 2020/7/1 17:56
 */
@Component
public class KafkaConsumer {
    private static final Logger LOGGER = LoggerFactory.getLogger("KafkaConsumer.class");

    @KafkaListener(topics = {"content-libraries-search-watcher"}, groupId = "test")
    public void handleMessage(JSONObject message) {
        LOGGER.info("接受kafka中的信息：{}", message);
        //将JSONObject转化为自己需要的实体
        //KafkaMessageParam kafkaParam = (KafkaMessageParam)JSONObject.toJavaObject(message, KafkaMessageParam.class);
    }
}

```

### Kafka相关参数学习

###### TODO