## RedisConfig

![image-20260415154621751](笔记2.assets/image-20260415154621751.png)

```
package com.lzk.redisdemo.config;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.data.redis.connection.RedisConnectionFactory;
import org.springframework.data.redis.core.RedisTemplate;
import org.springframework.data.redis.serializer.StringRedisSerializer;

@Configuration
public class RedisConfig {
    @Bean
    public RedisTemplate<Object, Object> redisTemplate(RedisConnectionFactory redisConnectionFactory) {
        // 1. 创建RedisTemplate对象
        RedisTemplate<Object, Object> template = new RedisTemplate<>();

        // 2. 设置key的序列化方式
        template.setKeySerializer(new StringRedisSerializer());
        template.setHashKeySerializer(new StringRedisSerializer());

        // 3. 设置value的序列化方式
        template.setValueSerializer(new StringRedisSerializer());
        template.setHashValueSerializer(new StringRedisSerializer());

        // 4. 设置Redis连接工厂
        template.setConnectionFactory(redisConnectionFactory);

        return template;
    }
}
```



## **RedisdemoApplication**

```
package com.lzk.redisdemo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
//springboot启动类
@SpringBootApplication
//@SpringBootApplication 是springboot提供
//普通类加这个 这个类是启动类或 引导类
//启动类在项目启动时会自动创建spring 的ioc容器并扫描当前类的包和子包，使当前包和子包的所有注解生效
public class RedisdemoApplication {
    /**
     *
     * srpingboot 的入口 所有代码的开口
     * @param args
     */
    public static void main(String[] args) {
        /**
         * 启动sprigboot程序 调用application
         */
        SpringApplication.run(RedisdemoApplication.class, args);
    }

}
```

 

## **RedisdemoApplicationTests**

```
package com.lzk.redisdemo;

import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.data.redis.connection.DataType;
import org.springframework.data.redis.core.*;

import java.util.List;
import java.util.Map;
import java.util.Set;
import java.util.concurrent.TimeUnit;

@SpringBootTest
//由springboot提供
    //作用：给哪个类加这个注解，哪个类就继承springboot测试，集成后可以调用ioc容器
class RedisdemoApplicationTests {
    @Autowired//依赖注入 从springboot ioc容器获取对象

    private RedisTemplate redisTemplate;
    @Test//加了@Test的是测试方法 返回值为空 方法名 一般为xxxxTest testxxx
    //测试类的命名规则一般为 xxxxTestx 或
    void contextLoads() {
        //1获取spring的方法名
        ValueOperations valueOperations = redisTemplate.opsForValue();
        //4.操作redis存值
        valueOperations.set("code","123",10, TimeUnit.SECONDS);
        //5.key不存在时设置
        Boolean b=valueOperations.setIfAbsent("code1","123");
        System.out.println(b);
    }
    @Test
    void hashTest(){
        //1.获取hash操作对象
        HashOperations hashOperations = redisTemplate.opsForHash();
        //2.操作redis存值
        hashOperations.put("user","name","zhangsan");
        hashOperations.put("user","age","18");
        hashOperations.put("user","sex","男");
        //3.取值
        String name=(String)hashOperations.get("user","name");
        System.out.println(name);
        //4.获取hash所有字段
        Set keys=hashOperations.keys("user");
        System.out.println(keys);
        //5.获取hash所有字段值
        List values=hashOperations.values("user");
        System.out.println(values);
        //6.获取hash所有字段和值
        Map user=hashOperations.entries("user");
        System.out.println(user);
    }
    @Test
    void setTest(){
        //1.获取操作对象
        SetOperations setOperations = redisTemplate.opsForSet();
        //2.存值
        setOperations.add("set","1","2","3");
        //3.取值
        Set set=setOperations.members("set");
        System.out.println(set);
        //4.删除某个
        setOperations.remove("set","1");
    }
    @Test
    void zsetTest(){
        //1.获取zset
        ZSetOperations zsetOperations = redisTemplate.opsForZSet();
        //2.存值
        zsetOperations.add("zset","1",1.1);
        zsetOperations.add("zset","2",2.2);
        zsetOperations.add("zset","3",3.3);
        //3.取值
        Set zset=zsetOperations.range("zset",0,-1);
        System.out.println(zset);
        //4.修改
        Double zset2=zsetOperations.incrementScore("zset","2",1);
        System.out.println(zset2);
        //5.删除
        zsetOperations.remove("zset","1");

    }
    @Test
    void bitTest(){
        //1.查询符合给定模式的key
        Set keys=redisTemplate.keys("*");
        System.out.println(keys);
        //2.检查是否存在
        Boolean b=redisTemplate.hasKey("code");
        System.out.println(b);
        //3.删除指定
        Boolean delete=redisTemplate.delete("code1");
        System.out.println(delete);
        //4.获取过期时间
        Long code=redisTemplate.getExpire("code");
        System.out.println(code);
        //5.获取制定key的类型
        DataType code1=redisTemplate.type("List");
        System.out.println(code1);
    }
}
```

