## 动态Sql

请求参数为列表

```xml
	<select id="queryByIds" parameterType="java.util.List" resultType="User">
		SELECT * FROM user WHERE id in
		<foreach collection="list"  item="item" separator="," open="(" close=")" index="" >
			#{item, jdbcType=INTEGER}	
		</foreach>
	</select>
```

collection标签可以填（'list','array','map'）

item表示集合中每一个元素进行迭代时的别名；

index指 定一个名字，用于表示在迭代过程中，每次迭代到的位置；

open表示该语句以什么开始，

separator表示在每次进行迭代之间以什么符号作为分隔符；

close表示以什么结束。

mybatis trim标签的使用
　　trim 属性
　　prefix：前缀
　　suffix：后缀
　　prefixOverrides：忽略第一个指定分隔符
　　suffixOverrides：会略最后一个分隔符

```xml
  	<select id="user" parameterType="user" resultType="User">
　　　　　　select * from user 
　　　　　　　　<trim prefix="WHERE" prefixoverride="and | or">
　　　　　　　　　　<if test="id!=null and id!=''">
　　　　　　　　　　　　id=#{id}
　　　　　　　　　　</if>
　　　　　　　　　　<if test="name!=null and name!=''">
　　　　　　　　　　　　and name=#{name}
　　　　　　　　　　</if>
　　　　　　　　　　<if test="gender!=null and gender!=''">
　　　　　　　　　　　　and gender=#{gender}
　　　　　　　　　　</if>
　　　　　　　</trim>
　　　</select>
```

mybatis sql标签的使用

```xml
	<sql id="user_content">
		SELECT 
		user_name as userName,
		password as password,
		age as age
	</sql>

    <select id="queryAll" resultType="User">
		<include refid="user_content"></include>
		FROM user
	</select>
```

## Mybatis原理

参考：<https://www.cnblogs.com/luoxn28/p/6417892.html>

Mybatis缓存：
一级缓存：是SqlSession级别的缓存，用Hash表存储，同一个SqlSession两次执行同一个Sql语句触发，默认开启，

二级缓存：Mapper级别缓存，跨session，默认不开启二级缓存