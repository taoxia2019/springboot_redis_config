 ### 1.依赖
```
 <!-- Spring Boot Redis依赖 -->
        <!-- 注意：1.5版本的依赖和2.0的依赖不一样，注意看哦 1.5我记得名字里面应该没有“data”, 2.0必须是“spring-boot-starter-data-redis” 这个才行-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-redis</artifactId>
            <!-- 1.5的版本默认采用的连接池技术是jedis  2.0以上版本默认连接池是lettuce, 在这里采用jedis，所以需要排除lettuce的jar -->
            <exclusions>
                <exclusion>
                    <groupId>redis.clients</groupId>
                    <artifactId>jedis</artifactId>
                </exclusion>
                <exclusion>
                    <groupId>io.lettuce</groupId>
                    <artifactId>lettuce-core</artifactId>
                </exclusion>
            </exclusions>
        </dependency>
        
        <!-- 添加jedis客户端 -->
        <dependency>
            <groupId>redis.clients</groupId>
            <artifactId>jedis</artifactId>
        </dependency>

        <!--spring2.0集成redis所需common-pool2-->
        <!-- 必须加上，jedis依赖此  -->
        <!-- spring boot 2.0 的操作手册有标注 大家可以去看看 地址是：https://docs.spring.io/spring-boot/docs/2.0.3.RELEASE/reference/htmlsingle/-->
        <dependency>
            <groupId>org.apache.commons</groupId>
            <artifactId>commons-pool2</artifactId>
            <version>2.5.0</version>
        </dependency>

        <!-- 将作为Redis对象序列化器 -->
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>fastjson</artifactId>
            <version>1.2.47</version>
        </dependency>
        
```
### 2.application.properties设置
```
#Redis服务器主机地址
spring.redis.host=192.168.119.132
#Redis服务连接密码
spring.redis.password=football
spring.redis.database=0
#Redis对外服务端口
spring.redis.port=6379
```

### 3.测试使用RedisTemplate
```
//注入
@Autowired
    private RedisTemplate<Object,Object> redisTemplate;

//测试
	@Test
	public void testSet(){
        //重新定义字符串系列化
        RedisSerializer redisSerializer=new StringRedisSerializer();
        //将字符串序列化加到模板key中
        redisTemplate.setKeySerializer(redisSerializer);
		this.redisTemplate.opsForValue().set("redis","javaredis");
	}
```
