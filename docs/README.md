 ### 1.����
```
 <!-- Spring Boot Redis���� -->
        <!-- ע�⣺1.5�汾��������2.0��������һ����ע�⿴Ŷ 1.5�Ҽǵ���������Ӧ��û�С�data��, 2.0�����ǡ�spring-boot-starter-data-redis�� �������-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-redis</artifactId>
            <!-- 1.5�İ汾Ĭ�ϲ��õ����ӳؼ�����jedis  2.0���ϰ汾Ĭ�����ӳ���lettuce, ���������jedis��������Ҫ�ų�lettuce��jar -->
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
        
        <!-- ���jedis�ͻ��� -->
        <dependency>
            <groupId>redis.clients</groupId>
            <artifactId>jedis</artifactId>
        </dependency>

        <!--spring2.0����redis����common-pool2-->
        <!-- ������ϣ�jedis������  -->
        <!-- spring boot 2.0 �Ĳ����ֲ��б�ע ��ҿ���ȥ���� ��ַ�ǣ�https://docs.spring.io/spring-boot/docs/2.0.3.RELEASE/reference/htmlsingle/-->
        <dependency>
            <groupId>org.apache.commons</groupId>
            <artifactId>commons-pool2</artifactId>
            <version>2.5.0</version>
        </dependency>

        <!-- ����ΪRedis�������л��� -->
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>fastjson</artifactId>
            <version>1.2.47</version>
        </dependency>
        
```
### 2.application.properties����
```
#Redis������������ַ
spring.redis.host=192.168.119.132
#Redis������������
spring.redis.password=football
spring.redis.database=0
#Redis�������˿�
spring.redis.port=6379
```

### 3.����ʹ��RedisTemplate
```
//ע��
@Autowired
    private RedisTemplate<Object,Object> redisTemplate;

//����
	@Test
	public void testSet(){
        //���¶����ַ���ϵ�л�
        RedisSerializer redisSerializer=new StringRedisSerializer();
        //���ַ������л��ӵ�ģ��key��
        redisTemplate.setKeySerializer(redisSerializer);
		this.redisTemplate.opsForValue().set("redis","javaredis");
	}
```
