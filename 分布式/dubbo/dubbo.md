## dubbo服务的暴露流程和引用流程

![1556149744309](image\provide_a_service.png)
![consumer](..\..\common\consumer.png)

## dubbo通信协议

dubbo支持的通信协议有dubbo（默认），rmi，hession，http

rmi和hession建立的连接是短连接，dubbo建立的连接为长连接

dubbo协议默认采用hession序列化，服务消费者维持一个长连接，后面基于长连接NIO异步通信，可以支持高并发请求

## dubbo 序列化协议

dubbo支持 hession，java，json，soap多种序列化协议

## PB

PB，Protocal Buffer,结构化数据存储格式，1、使用proto编译器，自动进行序列化和反序列化，速度很快，压缩效果好

收藏：[Protocol Buffer 的使用和原理](<https://www.ibm.com/developerworks/cn/linux/l-cn-gpb/index.html>)

## 负载均衡

RandomLoadBalance

```java
 // 下面的 if 分支主要用于获取随机数，并计算随机数落在哪个区间上
        if (totalWeight > 0 && !sameWeight) {
            // 随机获取一个 [0, totalWeight) 区间内的数字
            int offset = random.nextInt(totalWeight);
            // 循环让 offset 数减去服务提供者权重值，当 offset 小于0时，返回相应的 Invoker。
            // 举例说明一下，我们有 servers = [A, B, C]，weights = [5, 3, 2]，offset = 7。
            // 第一次循环，offset - 5 = 2 > 0，即 offset > 5，
            // 表明其不会落在服务器 A 对应的区间上。
            // 第二次循环，offset - 3 = -1 < 0，即 5 < offset < 8，
            // 表明其会落在服务器 B 对应的区间上
            for (int i = 0; i < length; i++) {
                // 让随机值 offset 减去权重值
                offset -= getWeight(invokers.get(i), invocation);
                if (offset < 0) {
                    // 返回相应的 Invoker
                    return invokers.get(i);
                }
            }
        }
```

LeastActiveLoadBalance

ConsistentHashLoadBalance

RoundRobinLoadBalance