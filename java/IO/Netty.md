[Netty in Action](https://waylau.gitbooks.io/essential-netty-in-action/GETTING%20STARTED/Introducing%20Netty.html)

ChannelPipeline, Channel, ChannelHandler 和 ChannelHandlerContext 的关系

![1559129731566](image\pipeline.png)

> 1. Channel 绑定到 ChannelPipeline
> 2. ChannelPipeline 绑定到 包含 ChannelHandler 的 Channel
> 3. ChannelHandler
> 4. 当添加 ChannelHandler 到 ChannelPipeline 时，ChannelHandlerContext 被创建

事件传播

![1559129952548](image\pipelin2.png)

>1. 事件传递给 ChannelPipeline 的第一个 ChannelHandler
>2. ChannelHandler 通过关联的 ChannelHandlerContext 传递事件给 ChannelPipeline 中的 下一个
>3. ChannelHandler 通过关联的 ChannelHandlerContext 传递事件给 ChannelPipeline 中的 下一个



```
ChannelHandlerContext ctx = context;
ctx.write(Unpooled.copiedBuffer("Netty in Action",              CharsetUtil.UTF_8));
```



![1559130213589](image\pipeline3.png)

> ChannelHandlerContext事件传递
>
> 1. ChannelHandlerContext 方法调用
> 2. 事件发送到了下一个 ChannelHandler
> 3. 经过最后一个ChannelHandler后，事件从 ChannelPipeline 移除