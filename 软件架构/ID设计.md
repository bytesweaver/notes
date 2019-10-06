



分布式唯一ID生成器

```
private static synchronized long nextId(long epochSecond) {
    if (epochSecond < lastEpoch) {
        // warning: clock is turn back:
        logger.warn("clock is back: " + epochSecond + " from previous:" + lastEpoch);
        epochSecond = lastEpoch;
    }
    if (lastEpoch != epochSecond) {
        lastEpoch = epochSecond;
        reset();
    }
    offset++;
    long next = offset & MAX_NEXT;
    if (next == 0) {
        logger.warn("maximum id reached in 1 second in epoch: " + epochSecond);
        return nextId(epochSecond + 1);
    }
    return generateId(epochSecond, next, SHARD_ID);
}
```



https://www.liaoxuefeng.com/article/1280526512029729

参考文章

https://tech.meituan.com/2017/04/21/mt-leaf.html