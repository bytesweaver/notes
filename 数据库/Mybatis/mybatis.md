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

