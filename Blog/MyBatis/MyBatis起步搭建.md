## 1 步骤

- 数据库环境
- 创建Maven项目
- 导入依赖
- 编写MyBatis配置文件
- 编写MyBatis工具类
- 编写实体类
- 编写Mapper
- 测试

<br>

## 2 数据库环境

MySQL 8.0版本

```mysql
create database mybatis;

use mybatis;

create table `user`(
	`id` int(20) primary key,
    `name` varchar(30) default null,
    `pwd` varchar(30) default null
) engine=InnoDB default charset=utf8;

insert into user(id,name,pwd) values
(1,'张一','111111'),
(2,'张二','222222'),
(3,'张三','333333')

select * from user;
```

<br>

## 3 创建项目并导入依赖

创建普通的maven项目

导入依赖

```xml
<!-- 导入坐标 -->
<dependencies>
    <!-- mysql -->
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>8.0.11</version>
    </dependency>

    <!-- mybatis -->
    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis</artifactId>
        <version>3.5.5</version>
    </dependency>

    <!-- junit -->
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.13.1</version>
    </dependency>
</dependencies>
```



配置resources，防止资源导出失败

```xml
<build>
    <resources>
        <resource>
            <directory>src/main/resources</directory>
            <includes>
                <include>**/*.properties</include>
                <include>**/*.xml</include>
            </includes>
            <filtering>true</filtering>
        </resource>
        <resource>
            <directory>src/main/java</directory>
            <includes>
                <include>**/*.properties</include>
                <include>**/*.xml</include>
            </includes>
            <filtering>true</filtering>
        </resource>
    </resources>
</build>
```

<br>

## 4 编写MyBatis配置文件

**mybatis-config.xml**

```xml
<?xml version="1.0" encoding="UTF8"?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">

<!-- 核心配置文件 -->
<configuration>
    <!-- 配置环境-->
    <environments default="mysql">
        <environment id="mysql">
            <transactionManager type="JDBC">
            </transactionManager>
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql://127.0.0.1:3306/mybatis?serverTimezone=UTC"/>
                <property name="username" value="root"/>
                <property name="password" value="mysql"/>
            </dataSource>
        </environment>
    </environments>

    <!-- 映射配置文件 -->
    <mappers>
        <mapper resource="com/tanyiqu/mapper/UserMapper.xml"/>
    </mappers>

</configuration>
```

<br>

## 5 编写MyBatis工具类

创建util包并创建MybatisUtil类

**MybatisUtil.java**

```xml
package com.tanyiqu.util;

import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;

import java.io.IOException;
import java.io.InputStream;


/**
 * mybatis工具类
 */
public class MybatisUtil {

    private static SqlSessionFactory sqlSessionFactory;

    static {
        try {
            // 获取SqlSessionFactory对象
            String resource = "mybatis-config.xml";
            InputStream inputStream = Resources.getResourceAsStream(resource);
            sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    public static SqlSession getSqlSession() {
        return sqlSessionFactory.openSession();
    }
}
```

<br>

## 6 编写实体类

创建pojo包并创建User类

**User.java**

```java
package com.tanyiqu.pojo;

public class User {
    private int id;
    private String name;
    private String pwd;

    @Override
    public String toString() {
        return "User{" +
                "id=" + id +
                ", name='" + name + '\'' +
                ", pwd='" + pwd + '\'' +
                '}';
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getPwd() {
        return pwd;
    }

    public void setPwd(String pwd) {
        this.pwd = pwd;
    }
}
```

<br>

## 7 编写Mapper

创建mapper包并创建UserMapper接口

**UserMapper.java**

```java
package com.tanyiqu.mapper;

import com.tanyiqu.pojo.User;

import java.util.List;

public interface UserMapper {
    List<User> getUsers();
}
```

创建UserMapper配置文件，在UserMapper.java同级目录下创建UserMapper.xml文件

**UserMapper.xml**

```xml
<?xml version="1.0"  encoding="UTF8"?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">

<mapper namespace="com.tanyiqu.mapper.UserMapper">
    <select id="getUsers" resultType="com.tanyiqu.pojo.User">
        select * from user
    </select>
</mapper>
```

<br>

## 8 测试

在test文件夹里面创建测试类

**MyTest.java**

```java
public class UserMapperTest {
    @Test
    public void getUsers() {
        SqlSession sqlSession = MybatisUtil.getSqlSession();

        UserMapper userMapper = sqlSession.getMapper(UserMapper.class);

        List<User> users = userMapper.getUsers();

        for (User user : users) {
            System.out.println(user);
        }

        sqlSession.close();
    }
}
```

执行成功！