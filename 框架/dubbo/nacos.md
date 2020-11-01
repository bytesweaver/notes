| 任务         | 计划开始日期 | 计划完成日期 |
| ------------ | ------------ | ------------ |
| nacos        |              |              |
| elastic job  |              |              |
| rabitmq      |              |              |
| mongo        |              |              |
| pgsql        |              |              |
| 异步通信架构 |              |              |

@RabbitListener(containerFactory = "rabbitListenerContainerFactory", bindings = @QueueBinding(
        value = @Queue(value = "${mq.config.queue}", durable = "true"),
        exchange = @Exchange(value = "${mq.config.exchange}", type = ExchangeTypes.TOPIC),
        key = "${mq.config.key}"), admin = "rabbitAdmin")