参考：<https://juejin.im/entry/598da7d16fb9a03c42431ed3>

<https://my.oschina.net/hosee/blog/615269>

AIO：异步非阻塞

BIO：同步阻塞IO

NIO：同步非阻塞IO，AIO的异步特性并不是Java实现的伪异步，而是使用了系统底层API的支持，在Unix系统下，采用了epoll IO模型，而windows便是使用了IOCP模型。

## NIO

> - NIO是基于块（Block）的，它以块为基本单位处理数据 （硬盘上存储的单位也是按Block来存储，这样性能上比基于流的方式要好一些）
> - 为所有的原始类型提供（Buffer）缓存支持 
> - 增加通道（Channel）对象，作为新的原始 I/O 抽象
> - 支持锁（我们在平时使用时经常能看到会出现一些.lock的文件，这说明有线程正在使用这把锁，当线程释放锁时，会把这个文件删除掉，这样其他线程才能继续拿到这把锁）和内存映射文件的文件访问接口 
> - 提供了基于Selector的异步网络I/O