**终于看完尚硅谷杨博超老师的mybatis辣 理论+实践 断断续续的 今天把主要内容整理了下 实践项目想要的姐妹可以私我分享！！
有写的不对的地方欢迎大家指出~~~**

## 一、MyBatis简介



## 二、搭建MyBatis

### 1.打包方式(pom.xml)

```pom.xml
<packaging>jar</packaging>
```

### 2.导入依赖(pom.xml)

```pom.xml
<!--   MyBatis核心     -->
      <dependency>
          <groupId>org.mybatis</groupId>
          <artifactId>mybatis</artifactId>
          <version>3.5.7</version>
      </dependency>
      <!--  测试      -->
      <dependency>
          <groupId>junit</groupId>
          <artifactId>junit</artifactId>
          <version>4.12</version>
          <scope>test</scope>
      </dependency>
      <!--    MySQL驱动    -->
      <dependency>
          <groupId>mysql</groupId>
          <artifactId>mysql-connector-java</artifactId>
          <version>5.1.3</version>
      </dependency>
12345678910111213141516171819
```

### 3.创建核心依赖文件(习惯上命名为mybatis-config.xml)

```mybatis-config.xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <!--  配置连接数据库的环境  -->
    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql://localhost:3306/mybatis"/>
                <property name="username" value="root"/>
                <property name="password" value="123456"/>
            </dataSource>
        </environment>
    </environments>
    <!--    引入映射文件     -->
    <mappers>
        <mapper resource="mappers/UserMapper.xml"/>
    </mappers>
</configuration>
12345678910111213141516171819202122
```

### 4.创建mapper接口

```UserMapper.java
public interface UserMapper {
    /**
     * MyBatis面向接口编程的两个一致：
     * 1.映射文件的namespace要和mapper接口的全类名保持一致
     * 2.映射文件中的SQL语句的id要和mapper接口中的方法名一致
     *
     * 表--实体类--mapper接口--映射文件
     */
    /**
     * 添加用户信息
     */
    int insertUser();
}
12345678910111213
```

### 5.创建MyBatis的映射文件

ORM：Object Relationship Mapping 对象关系映射

对象：Java的实体类对象

关系：关系型数据库

映射：二者之间的对应关系

| java概念 | 数据库概念 |
| -------- | ---------- |
| 类       | 表         |
| 属性     | 字段/行    |
| 对象     | 记录/行    |

①映射文件的命名规则:

表所对应的实体类的类名+Mapper.xml

### 6.测试

```MyBatisTest.java
/**
     * SqlSession默认不自动提交事务，若需要自动提交事务
     * 可以使用SqlSessionFactory.openSession(true);
     */

    @Test
    public void TestMyBatis() throws IOException {
        //加载核心配置文件
        InputStream is=Resources.getResourceAsStream("mybatis-config.xml");
        //获取SqlSessionFactoryBuilder
        SqlSessionFactoryBuilder sqlSessionFactoryBuilder=new SqlSessionFactoryBuilder();
        //获取SqlSessionFactory
        SqlSessionFactory sqlSessionFactory=sqlSessionFactoryBuilder.build(is);
        //获取SqlSession
        SqlSession sqlSession=sqlSessionFactory.openSession(true);
        //获取Mapper接口对象
        UserMapper mapper=sqlSession.getMapper(UserMapper.class);
        //测试功能
        int result=mapper.insertUser();
        //提交事务
//        sqlSession.commit();
        System.out.println("result:"+result);
    }
1234567891011121314151617181920212223
```

SqlSession：代表Java程序和数据库之间的会话。(HttpSession是Java程序和浏览器之间的会话)

SqlSessionFactory:是“生产”SqlSession的“工厂”

工厂模式：如果创建某一个对象，使用的过程基本固定，那么我们就可以把创建这个对象的相关代码封装到一个工厂类中，以后都使用这个工厂类来生产我们需要的对象。

### 7.加入log4j日志功能

加入依赖

```pom.xml
<!--    log4j日志    -->
        <dependency>
            <groupId>log4j</groupId>
            <artifactId>log4j</artifactId>
            <version>1.2.17</version>
        </dependency>
```

配置log4j.xml

```log4j.xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE log4j:configuration SYSTEM "log4j.dtd">

<log4j:configuration xmlns:log4j="http://jakarta.apache.org/log4j/">

    <appender name="STDOUT" class="org.apache.log4j.ConsoleAppender">
        <param name="Encoding" value="UTF-8"/>
        <layout class="org.apache.log4j.PatternLayout">
            <param name="ConversionPattern" value="%-5p %d{MM-dd HH:mm:ss,SSS} %m
(%F:%L) \n"/>
        </layout>
    </appender>
    <logger name="java.sql">
        <level value="debug"/>
    </logger>
    <logger name="org.apache.ibatis">
        <level value="info"/>
    </logger>
    <root>
        <level value="debug"/>
        <appender-ref ref="STDOUT"/>
    </root>
</log4j:configuration>
```

日志的级别

FATAL(致命)>ERROR(错误)>WARN(警告)>INFO(信息)>DEBUG(调试)

从左到右打印的内容越来越详细

## 三、核心配置文件详解

MyBatis核心配置文件中，标签的顺序：
“(properties?,settings?,typeAliases?,typeHandlers?,objectFactory?,
objectWrapperFactory?,reflectorFactory?,plugins?,environments?,
databaseIdProvider?,mappers?)”.

```mybatis-config.xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <!--  MyBatis核心配置文件中，标签的顺序：
     "(properties?,settings?,typeAliases?,typeHandlers?,objectFactory?,
     objectWrapperFactory?,reflectorFactory?,plugins?,environments?,
     databaseIdProvider?,mappers?)".  -->

    <!--  引入properties文件  -->
    <properties resource="jdbc.properties"/>

    <!--  设置类型别名  -->
    <typeAliases>
        <!--  typeAlias:设置某个类型的别名
              属性：
              type:设置需要设置别名的类型
              alia：设置某个类型的别名，若不设置该属性，
              那么该类型拥有默认的别名，即类名且不区分大小写
              -->
<!--        <typeAlias type="com.jxxy.mybatis.pojo.User" alias="user"/>-->
        <!--   以包为单位，将包下所有的类型设置默认的别名,即类名且不区分大小写     -->
        <package name="com.jxxy.mybatis.pojo"/>
    </typeAliases>
    <!--
    environments:配置多个连接数据库的环境
    属性：
        default:设置默认使用的环境的id
      -->
    <environments default="development">
        <!--
        environment:配置某个具体的环境
         属性：
            id:表示连接数据库的环境的唯一标识，不能重复
     -->
        <environment id="development">
            <!--
             TransactionManager:设置事务管理方式
                 属性：
                  type="JDBC/MANAGED"
                  JDBC：表示当前环境中，执行sql时，使用的是JDBC中原生的事务管理方式，事务的提交或回滚需要手动处理
                  MANAGED：被管理，例如Spring
                        -->
            <transactionManager type="JDBC"/>
            <!--     dataSource：配置数据源
                   属性：
                   type：设置数据源的类型
                   type="POOLED|UNPOOLED|JNDI"
                   POOLED:表示使用数据库连接池缓存数据库连接
                   UNPOOLED:表示不使用数据库连接池
                   JNDI:表示使用上下文中的数据源
                   -->
            <dataSource type="POOLED">
                <!--     设置连接数据库的驱动           -->
                <property name="driver" value="${jdbc.driver}"/>
                <!--     设置连接数据库的连接地址           -->
                <property name="url" value="${jdbc.url}"/>
                <!--     设置连接数据库的用户名           -->
                <property name="username" value="${jdbc.username}"/>
                <!--     设置连接数据库的密码           -->
                <property name="password" value="${jdbc.password}"/>
            </dataSource>
        </environment>
    </environments>
    <!--    引入映射文件     -->
    <mappers>
<!--        <mapper resource="mappers/UserMapper.xml"/>-->
        <!--   以包为单位引入映射文件：
             要求:
             1.mapper接口所在的包要和映射文件所在的包一致
             2.mapper接口要和映射文件的名字一致
             -->
        <package name="com.jxxy.mybatis.mapper"/>
    </mappers>
</configuration>
```

## 四.MyBatis的增删查改

### 1.添加

```UserMapper.xml
<!--  int insertUser()  -->
    <insert id="insertUser">
        insert into t_user values(null,'admin','123456',23,'男','123456@qq.com')
    </insert>
1234
```

### 2.删除

```UserMapper.xml
 <!-- void deleteUser();   -->
    <delete id="deleteUser">
        delete from t_user where username = '张三'
    </delete>
1234
```

### 3.修改

```UserMapper.xml
<!-- void updateUser();-->
    <update id="updateUser">
        update t_user
        set username = '张三'
        where id=10;
    </update>
123456
```

### 4.查询一个实体类对象

```UserMapper.xml
 <!--   User getUserById(); -->
    <!--  查询功能的标签必须设置resultType或resultMap
           resultType:设置默认的映射关系
           resultMap:设置自定义的映射关系
    -->
    <select id="getUserById" resultType="com.jxxy.mybatis.pojo.User">
        select * from t_user where id =11
    </select>
12345678
```

### 5.查询集合

```UserMapper.xml
<!--  List<User> getAllUser();   -->
    <select id="getAllUser" resultType="user">
        select *
        from t_user;
    </select>
12345
```

注意：

①查询的标签select必须设置属性resultType或resultMap,用于设置实体类和数据库表的映射关系

resultType:自动映射，用于属性名和表中字段名一致的情况

resultMap：自定义映射，用于一对多或多对一或字段名和属性名不一致的情况

②当查询的数据过多时，不能使用实体类作为返回值，只能使用集合，否则会抛出异常TooManyResultException;但是若查询的数据只有一条，可以使用实体类或集合作为返回值

## 五.MyBatis获取参数值的两种方式(重点)

MyBatis获取参数值的两种方式，${}和#{}

${}的本质就是字符串拼接，#{}的本质就是占位符赋值

${}使用字符串拼接的方式拼接sql，若为字符串类型或日期类型的字段进行赋值时，需要手动加单引号；但是#{}使用占位符赋值的方式拼接sql，此时为字符串类型或日期类型的字段进行赋值时，可以自动添加单引号

web工程：

browser–>Server–>service–>dao–>mapper

### 1.单个字面量类型的参数（可以知道有这样）

若mapper接口中的方法参数为单个的字面量类型，此时可以使用KaTeX parse error: Expected 'EOF', got '#' at position 5: {} 和#̲{}以任意的名称获取参数的值，…{}需要手动加单引号,比如：

```ParameterMapper.xml
 <!--     List<User> gerUserByUsername(String username);   -->
    <select id="gerUserByUsername" resultType="User">
        <!--select * from t_user where username = #{username}-->
        select * from t_user where username = '${username}'
    </select>
12345
```

### 2.多个字面量类型的参数（不要用）

若mapper接口中的方法参数为多个时，此时MyBatis会将这些参数放在一个map集合中，以两种方式进行存储

①以arg0,arg1…为键，以参数为值
②以param1,param2…为键，以参数为值

因此只需要通过以#{}和以 键 的 方 式 访 问 值 即 可 ， 但 是 要 注 意 {}以键的方式访问值即可，但是要注意以键的方式访问值即可，但是要注意{}的单引号问题
比如：#{arg0},#{arg1}…或者’a r g 0 ′ , ′ {arg0}','arg0′,′{arg1}'…比如：

```ParameterMapper.xml
 <!--   List<User> checkLogin(String username, String password);  -->
    <select id="checkLogin" resultType="User">
        <!--select * from t_user where username=#{arg0} and password=#{arg1}-->
        select * from t_user where username='${arg0}' and password='${arg1}'
    </select>
```

### 3.map集合类型的参数（不要用）

若mapper接口方法的参数有多个时，可以手动将这些参数放在一个map中存储(由2演变来)，只需要通过以#{}和以 键 的 方 式 访 问 值 即 可 ， 但 是 要 注 意 {}以键的方式访问值即可，但是要注意以键的方式访问值即可，但是要注意{}的单引号问题,比如

```ParameterMapper.xml
<!--  List<User> checkLoginByMap(Map<String,Object> map);  -->
    <select id="checkLoginByMap" resultType="User">
        select * from t_user where username='${username}' and password='${password}'
    </select>
1234
```

### 4.实体类类型的参数（经常用）

mapper接口方法的参数是实体类型的参数(用的最多)，只需要通过以#{}和以 键 的 方 式 访 问 值 即 可 ， 但 是 要 注 意 {}以键的方式访问值即可，但是要注意以键的方式访问值即可，但是要注意{}的单引号问题,比如

```ParameterMapper.xml
<!--    int insertUser(User user);-->
    <insert id="insertUser">
        insert into t_user
        values (null,#{username},#{password},#{age},#{sex},#{email});
    </insert>
12345
```

### 5.使用@Param标识参数（经常用）

此时MyBatis会将这些参数放在一个map集合中，以两种方式进行存储:
a>以@Param注解的值为键，以参数为值
b>以param1,param2…为键，以参数为值
因此只需要通过#{}和以 键 的 方 式 访 问 值 即 可 ， 但 是 要 注 意 {}以键的方式访问值即可，但是要注意以键的方式访问值即可，但是要注意{}的单引号问题,比如：

```ParameterMapper.xml
<!--      List<User> checkLoginByParam(@Param("username") String username, @Param("password") String password);  -->
    <select id="checkLoginByParam" resultType="User">
        select * from t_user where username='${param1}' and password='${param2}'
    </select>
```

## 六.MyBatis的各种查询功能

- MyBatis的各种查询功能：
  - 1.若查询出的数据只有一条
    - a>可以通过实体类对象
    - b>可以通过list集合接收
    - c>可以通过map集合接收 结果：{password=123456, sex=男, id=7, age=23, email=123456@qq.com, username=admin}
  - 2.若查询出的数据有多条
    - a>可以通过实体类类型的list集合接收
    - b>可以通过map类型的list接收
    - c>可以在mapper接口的方法上添加@Mapkey注解，此时就可以将每条数据转换的map集合作为值

以某个字段的值作为键，放在同一个map中

注意：一定不能通过实体类对象接收，此时会抛异常TooManyResultsException,

MyBatis中设置了默认的类型别名
Java.lang.Integer–>int,integer

int–>_int,_integer

Map–>map

String–>string

### 1.查询一个实体类对象

```SelectMapper.xml
  <!--User getUserById(@Param("id") Integer id);通过实体类对象接收-->
    <select id="getUserById" resultType="User">
        select * from t_user where id = #{id}
    </select>
   
12345
```

### 2.查询一个list集合

```SelectMapper.xml
  <!--  List<User> getAllUser();  -->
    <select id="getAllUser" resultType="User">
        select * from t_user
    </select>
1234
```

### 3.查询单个数据

```SelectMapper.java
/**
 *查询总用户信息数
 */
Integer getCount();
1234
<!--  Integer getCount();  -->
<select id="getCount" resultType="java.lang.Integer">
    select count(*) from t_user
</select>
1234
```

### 4.查询一条数据为map集合(Vue中会很常用)

```SelectMapper.java
/**
 *根据id查询用户信息为一个map集合
 */
Map<String, Object> getUserByIdToMap(@Param("id") Integer id);

<select id="getUserByIdToMap" resultType="map">
    select * from t_user where id = #{id}
</select>
```

### 5.查询多条数据为map集合（Vue中会很常用）

```java
/*
 *查询所有用户信息为map集合
 */
//List<Map<String,Object>> getAllUserToMap();,这个方式可以用
@MapKey("id")
Map<String,Object> getAllUserToMap();
```

```xml
<select id="getAllUserToMap" resultType="map">
    select * from t_user
</select>
```

## 七.特殊SQL的执行

### 1.模糊查询（解决方法要熟记）

1. 解决方法1：不要用#{},用${}
2. 解决方法2：concat('%',#{username},'%')
3. 解决方法3："%"#{username}"%"（这个最常用，最推荐！）



```SQLMapper.xml
/**
 * 模糊查询
 * 根据用户名模糊查询用户信息
 */
List<User> getUserByLike(@Param("username") String username);
12345
<!--   List<User> getUserByLike(@Param("username") String username);  -->
<select id="getUserByLike" resultType="User">
 <!--   select * from t_user where username like '%${username}%'  -->
 <!--   select * from t_user where username like concat('%', #{username},'%')  字符串拼接-->
    select * from t_user where username like "%"#{username}"%"
</select>
123456
```

### 2.批量删除（只要是批量处理）

- 解决方法：用${}

这里批量删除是指，把id拼成一个字符串，这个字符串里面全是为要删除的内容的id

比如我要批量删除id为1,2,3的记录，我这里的String ids 就应该等于 "1,2,3"

这里的sql关键词是IN

```SQLMapper.java
/**
 * 批量删除
 */
int deleteMore(@Param("ids") String ids);
1234
<!--    int deleteMore(@Param("ids") String ids);  -->
<delete id="deleteMore">
    delete from t_user where id in (${ids})
</delete>
1234
```

### 3.动态设置表名（不常用）

这个是因为，有的时候一个表特别大，不太好。

所以把一个表拆成多个表，如果我要查找的话，我就要查询这多个表。

所以查询的表名字是不固定的。

- 只能用${}

```SelectMapper.java
/**
 *查询指定表中的数据
 */
List<User> getUserByTableName(@Param("tableName") String tableName);
1234
<!--  List<User> getUserByTableName(@Param("tableName") String tableName);  -->
<select id="getUserByTableName" resultType="User">
    select * from ${tableName}
</select>
1234
```

### 4.添加功能获取自增的主键（！！给一对多的表插入数据）

假如有clazz表（clazz_id，clazz_name）

student表（student_id，student_name，clazz_id）

很显然一个clazz有多个Student。

先添加班级后，再添加学生，所以需要用到上次插入数据的id

- 解决方法：用`prepareStatement`的两个参数的接口，传入`Statement.RETURN_GENERATED_KEYS`。再到对应的`Mapper.xml`中设置`useGeneratedKey=true keyProperty="自己设置"`

```SQLMapper.java
/**
 * 添加用户信息
 */
void insertUser(User user);
1234
<!--  void insertUser(User user);
        useGenerateKeys:设置当前标签中的sql使用了自增的主键
        keyProperty：将自增的主键的值赋值给传输到映射文件中参数的某个属性
-->
<insert id="insertUser" useGeneratedKeys="true" keyProperty="id">
    insert into t_user values (null,#{username},#{password},#{age},#{sex},#{email})
</insert>
123456
```

## 八.自定义映射resultMap

除了resultMap的方法解决查询有字段为NULL的问题

1. 在sql语句中其别名SELECT emp_name AS empName FROM emp;（不好）
2. 在`mybatis-config.xml`中加入`<settings><setting name="mapUnderscoreToCamelCase" value="true"/></settings>`这一堆标签（还行，可用可不用）

### 1.resultMap处理字段和属性的映射关系（必须全部设置）

若字段名和实体类中的属性名不一样，可以通过resultMap设置自定义映射

```DeptMapper.xml
<!--
  resultMap：设置自定义映射关系
  id:唯一标识，不能重复
  type: 设置映射关系中的实体类类型
  子标签:
  id:设置主键的元素关系
  result:设置普通字段的映射关系
  属性：
  property:设置映射关系中的属性名，必须是type属性所设置的实体类类型中的属性名
  column:设置映射关系中的字段名，必须是sql语句查询出的字段名
  -->
<resultMap id="empResultMap" type="Emp">
    <id property="eid" column="eid"></id>
    <result property="empName" column="emp_name"></result>
    <result property="age" column="age"></result>
    <result property="sex" column="sex"></result>
    <result property="email" column="email"></result>
</resultMap>

<!--   List<Emp> getAllEmp();  -->
<select id="getAllEmp" resultMap="empResultMap">
    select * from t_emp
</select>
1234567891011121314151617181920212223
```

### 2.多对一映射处理

#### a>级联方式处理映射关系（简单）（用的并不多哈）（所以不要用）

```EmpMapper.xml
<!--  处理多对一映射关系方式一：级联属性赋值 -->
    <resultMap id="empAndDeptResultMapOne" type="Emp">
        <id property="eid" column="eid"/>
        <result property="empName" column="emp_name"/>
        <result property="age" column="age"/>
        <result property="sex" column="sex"/>
        <result property="email" column="email"/>
        <result property="dept.did" column="did"/>
        <result property="dept.deptName" column="dept_name"/>
123456789
```

#### b >使用association处理映射关系

```EmpMapper.xml
<!--  处理多对一映射关系方式二：association -->
<resultMap id="empAndDeptResultMapTwo" type="com.jxxy.mybatis.pojo.Emp">
    <id property="eid" column="eid"/>
    <result property="empName" column="emp_name"/>
    <result property="age" column="age"/>
    <result property="sex" column="sex"/>
    <result property="email" column="email"/>
    <!--
         association:处理多对一的映射关系
         property:需要处理多对一的映射关系的属性名
         javaType:该属性的类型
         -->
    <association property="dept" javaType="Dept">
        <id property="did" column="did"/>
        <result property="deptName" column="dept_name"/>
    </association>
</resultMap>
1234567891011121314151617
```

#### c>分步查询（也是用assocation）（最常用）（麻烦）

```EmpMapper.java
/**
* 分步查询员工以及员工所对应的部门信息
* 分步查询第一步:根据eid查询员工信息
*/
Emp getEmpAndDeptByStepOne(@Param("eid") Integer eid);
```
```xml
<!--   Emp getEmpAndDeptByStepOne(@Param("eid") Integer eid); -->
<select id="getEmpAndDeptByStepOne" resultMap="getEmpAndDeptByStepResultMap">
    select * from t_emp where eid = #{eid}
</select>
```
```xml
<!--  处理多对一映射关系方式三：分步查询(延时加载) -->
<resultMap id="getEmpAndDeptByStepResultMap" type="Emp">
    <id property="eid" column="eid"/>
    <result property="empName" column="emp_name"/>
    <result property="age" column="age"/>
    <result property="sex" column="sex"/>
    <result property="email" column="email"/>
    <!--
        select:设置分步查询的sql的唯一标识(namespace.SQLId或mapper接口的全类名.方法名)
        column:设置分步查询的条件
        fetchType:当开启了全局的延迟加载之后，可通过此属性手动控制延迟加载的效果
        fetchType="lazy|eager":lazy表示延迟加载，eager表示立即加载
        -->
    <association property="dept"
                 select="com.jxxy.mybatis.mapper.DeptMapper.getEmpAndDeptByStepTwo"
                 column="did"
                fetchType="eager">
    </association>
</resultMap>
```
1234567891011121314151617181920212223
```java
/**
 * 分步查询员工以及员工所对应的部门信息
 * 分步查询第二步:通过did查询员工所对对应的部门
 */
Dept getEmpAndDeptByStepTwo(@Param("did") Integer did);
```
```xml
12345
<!--   Dept getEmpAndDeptByStepTwo(@Param("did") Integer did);  -->
<select id="getEmpAndDeptByStepTwo" resultType="Dept">
    select * from t_dept where did = #{did}
</select>
1234
```

### 3.一对多映射处理

#### a>collection

```DeptMapper.xml
<!--
        collection:处理一对多的映射关系
        ofType:表示该属性所对应的集合中存储数据的类型
-->
<resultMap id="deptAndEmpResultMap" type="Dept">
    <id property="did" column="did"></id>
    <result property="deptName" column="dept_name"></result>
    <!--
    1.目的：设置字段和属性的映射关系
    2.通过ofType获取集合里存储的数据的类型
    3.然后根据这个类型获取相应的属性(mybatis内部操作)
    4.映射关系建立后，创建该类型的对象(此处是emp)
    5.最后把每一个对象放在集合(emps)中
    -->
    <collection property="empList" ofType="Emp">
        <id property="eid" column="eid"></id>
        <result property="empName" column="emp_name"></result>
        <result property="age" column="age"></result>
        <result property="sex" column="sex"></result>
        <result property="email" column="email"></result>
    </collection>
</resultMap>

 <!-- Dept getDeptAndEmp(@Param("did") Integer did);//获取部门以及部门中所有的员工信息   -->
<select id="getDeptAndEmp" resultMap="deptAndEmpResultMap">
    select *
    from t_dept left  join t_emp on t_dept.did = t_emp.did where  t_dept.did = #{did};
</select>
12345678910111213141516171819202122232425262728
```

#### b>分步查询

```DeptMapper.java
/**
     * 通过分步查询查询部门以及部门中所有的员工信息
     * 分布查询第一步：查询部门信息
     */
    Dept getDeptAndEmpByStepOne(@Param("did") Integer did);
12345
 <!--   Dept getDeptAndEmpByStepOne(@Param("did") Integer did);  -->
    <select id="getDeptAndEmpByStepOne" resultMap="deptAndEmpByStepResultMap">
        select * from t_dept where did = #{did}
    </select>
<!--  处理多对一映射关系方式三：分步查询(延时加载) -->
    <resultMap id="getEmpAndDeptByStepResultMap" type="Emp">
        <id property="eid" column="eid"/>
        <result property="empName" column="emp_name"/>
        <result property="age" column="age"/>
        <result property="sex" column="sex"/>
        <result property="email" column="email"/>
        <!--
            select:设置分步查询的sql的唯一标识(namespace.SQLId或mapper接口的全类名.方法名)
            column:设置分步查询的条件
            fetchType:当开启了全局的延迟加载之后，可通过此属性手动控制延迟加载的效果
            fetchType="lazy|eager":lazy表示延迟加载，eager表示立即加载
            -->
        <association property="dept"
                     select="com.jxxy.mybatis.mapper.DeptMapper.getEmpAndDeptByStepTwo"
                     column="did"
                    fetchType="eager"></association>
    </resultMap>
12345678910111213141516171819202122
/**
     * 通过分步查询查询部门以及部门中所有的员工信息
     * 分布查询第二步：根据did查询员工信息
     */
    List<Emp> getDeptAndEmpByStepTwo(@Param("did") Integer did);
12345
  <!--   List<Emp> getDeptAndEmpByStepTwo(@Param("did") Integer did);  -->
    <select id="getDeptAndEmpByStepTwo" resultType="Emp">
        select *
        from t_emp where did = #{did};
    </select>
12345
```

> 分步查询的优点：可以实现延迟加载，但是必须在核心配置文件中设置全局配置信息：
>
> lazyLoadingEnabled:延迟加载的全局开关。当开启时，所有关联对象都会延迟加载
>
> aggressiveLazyLoading:当开启时，任何方法的调用都会加载该对象的所有属性。否则，每个属性会按需加载
>
> 此时就可以实现按需加载，获取的数据是什么，就只会执行相应的sql。此时可通过association和collection中的fetchType属性设置当前的分步查询是否适用延迟加载，fetchType=“lazy(延迟加载)|eager(立即加载)”
>

## 九.动态SQL（建议去官方中文文档直接拷贝即可）

MyBatis框架的动态SQL技术是一种根据特定条件动态拼装SQL语句的功能，它存在的意义是为了解决拼接SQL语句字符串时的痛点问题。

### 1.if

```DynamicMapper.xml
<!--  List<Emp> getEmpByCondition(Emp emp);  -->
<select id="getEmpByConditionOne" resultType="Emp">
    select <include refid="empColumns"/> from t_emp where 1=1
    <if test="empName != null and empName != ''">
        emp_name = #{empName}
    </if>
    <if test="age != null and age != ''">
        and age = #{age}
    </if>
    <if test="sex != null and sex != ''">
        and sex = #{sex}
    </if>
    <if test="email != null and email != ''">
        and email = #{email}
    </if>
</select>
12345678910111213141516
```

if标签可通过test属性的表达式进行判断，若表达式的结果为true，则标签中的内容会执行；反之标签中的内容不会执行。

### 2.where

```DynamicMapper.xml
<!--  List<Emp> getEmpByCondition(Emp emp);  -->
<select id="getEmpByCondition11" resultType="Emp">
    select * from t_emp
        <where>
            <if test="empName != null and empName != ''">
                and  emp_name = #{empName}
            </if>
            <if test="age != null and age != ''">
                and  age = #{age}
            </if>
            <if test="sex != null and sex != ''">
                and sex = #{sex}
            </if>
            <if test="email != null and email != ''">
                and email = #{email}
            </if>
        </where>
</select>
123456789101112131415161718
```

### 3.trim

```DynamicMapper.xml
<!--  List<Emp> getEmpByCondition(Emp emp);  -->
<select id="getEmpByCondition" resultType="Emp">
    select * from t_emp
    <trim prefix="where" suffixOverrides="and|or">
        <if test="empName != null and empName != ''">
            emp_name = #{empName} and
        </if>
        <if test="age != null and age != ''">
            age = #{age} or
        </if>
        <if test="sex != null and sex != ''">
            sex = #{sex} and
        </if>
        <if test="email != null and email != ''">
            email = #{email}
        </if>
    </trim>
</select>
123456789101112131415161718
//动态SQL：
*  1.if:根据标签中test属性所对应的表达式决定标签中的内容是否需要拼接到SQL中
*  2.where:
*  当where标签中有内容时，会自动生成where关键字，并且将内容前多余的 and 或 or去掉
*  当where标签中没有内容时，此时where标签没有任何效果
*  注意：where标签不能将其中内容后面多余的and或or去掉
*  3.trim:
*  若标签中有内容时：
*  prefix/suffix:将trim标签中内容前面或后面添加指定内容
*  suffixOverrides/prefixOverrides:将trim标签中内容前面或后面去掉指定内容
*  若标签中没有内容时，trim标签也没有任何效果
*  4.choose,when,otherwise,相当于if ... else if ...else
*  when至少要有一个，otherwise最多只能有一个
*  5.foreach
*  collection:设置需要循环的数组或集合
*  item:表示数组或集合中的每一个数据
*  separator:循环体之间的分割符
*  open:foreach标签所循环的所有内容的开始符
*  close:foreach标签所循环的所有内容的结束符
*  6.sql标签
*  设置SQL片段  <sql id="empColumns">eid,emp_name,age,sex,email</sql>
*  引用SQL片段 select <include refid="empColumns"/> from t_emp where 1=1
*
1234567891011121314151617181920212223
```

## 十、MyBatis的缓存

### 1.MyBatis的一级缓存

一级缓存是SqlSession级别的，通过同一个SqlSession查询的数据会被缓存，下次查询相同的数据，就会从缓存中直接获取，不会从数据库重新访问

使一级缓存失效的四种情况：

1）不同的SqlSession对应不同的一级缓存

2）同一个SqlSession但是查询条件不同

3）同一个SqlSession两次查询期间执行了任何一次增删改操作

4）同一个SqlSession两次查询期间手动清空了缓存

### 2.MyBatis的二级缓存

二级缓存使SqlSessionFactory级别，通过同一个SqlSessionFactory创建的SqlSession查询的结果会被缓存；此后若再次执行相同的查询语句，结果就会从缓存中获取

二级缓存开启的条件

a>在核心配置文件中，设置全局配置属性cacheEnabled=“true”，默认为true，不需要设置

b>在映射文件中设置标签

c>二级缓存必须在SqlSession关闭或提交之后有效

d>查询的数据所转换的实体类型必须实现序列化的接口

使二级缓存失效的情况：

两次查询之间执行了任意的增删改，会使一级和二级缓存同时失效

### 3.二级缓存的相关配置

在mapper配置文件中添加的cache标签可以设置一些属性：

**·eviction**属性：缓存回收策略

LRU（Least Recently Used）- 最近最少使用的：移除最长时间不被使用的对象。

FIFO（First in First out）- 先进先出：按对象进入缓存的顺序来移除它们。

SOFT - 软引用：移除基于垃圾回收器状态和软引用规则的对象。

WEAK - 弱引用：更积极地移除基于垃圾收集器状态和弱引用规则的对象

默认的是LRU。

**·fulshInterval**属性：刷新间隔，单位毫秒

默认情况是不设置，也就是没有刷新间隔，缓存仅仅调用语句时刷新

**·size**属性：引用数目，正整数

代表缓存最多可以存储多少个对象，太大容易导致内存溢出

**·readOnly**属性：只读，true/false

true：只读缓存，会给所有调用者返回缓存对象的相同实例。因此这些对象不能被修改。这提供了很多重要的性能优势。

false：读写缓存，会返回缓存对象的拷贝（通过序列化）。这会慢一些，但是安全，因此默认是false。

### 4.MyBatis缓存查询的循序

**·**先查询二级缓存，因为二级缓存中可能会有其他程序已经查出来的数据，可以拿来直接使用。

**·**如果二级缓存没有命中，再查询一级缓存

**·**如果一级缓存也没有命中，则查询数据库

**·**SqlSession关闭之后，一级缓存中的数据会写入二级缓存

### 5.整合第三方缓存EHCache

**a> 添加依赖**

```pom.xml
<!--   MyBatis EHCache整合包     -->
        <dependency>
            <groupId>org.mybatis.caches</groupId>
            <artifactId>mybatis-ehcache</artifactId>
            <version>1.2.1</version>
        </dependency>
        <!--    slf4j日志门面的一个具体实现    -->
        <dependency>
            <groupId>ch.qos.logback</groupId>
            <artifactId>logback-classic</artifactId>
            <version>1.2.3</version>
        </dependency>
123456789101112
```

**b> 各jar包功能**

| jar包名称       | 作用                            |
| --------------- | ------------------------------- |
| mybatis-ehcache | Mybatis和EHCache的整合包        |
| ehcache         | EHCache核心包                   |
| slf4j-api       | SLF4J日志门面包                 |
| logback-classic | 支持SLF4J门面接口的一个具体实现 |

**c> 创建EHCache的配置文件ehcache.xml**

```ehcache.xml
<?xml version="1.0" encoding="UTF-8" ?>
<ehcache xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="../config/ehcahe.xsd">
    <!--        磁盘保存路径   -->
    <diskStore path="D:/"/>

    <defaultCache maxElementsInMemory="1000"
                  maxElementsOnDisk="10000000"
                  eternal="false"
                  overflowToDisk="true"
                  timeToIdleSeconds="120"
                  timeToLiveSeconds="120"
                  diskExpiryThreadIntervalSeconds="120"
                  memoryStoreEvictionPolicy="LRU">

    </defaultCache>
</ehcache>
1234567891011121314151617
```

**d> 设置二级缓存的类型**

```CacheMapper.xml
<cache type="org.mybatis.caches.ehcache.EhcacheCache"/>
1
```

**e>加入logback日志**

存在SLF4J时，作为简易日志的log4j讲失效，此时我们需要借助SLF4J的具体实现logback来打印日志。创建logback的配置文件logback.xml

```logback.xml
<?xml version="1.0" encoding="UTF-8" ?>
<configuration debug="true">
    <!--  指定日志输出的位置  -->
    <appender name="STDOUT"
              class="ch.qos.logback.core.ConsoleAppender">
        <encoder>
            <!--     日志输出的格式       -->
            <!--      按照顺序分别是：时间、日志级别、线程名称、打印日志的类、日志主体内容、换行      -->
            <pattern>[%d{HH:mm:ss.SSS}] [%-5level] [%thread] [%logger] [%msg]%n</pattern>
        </encoder>
    </appender>

    <!-- 设置全局日志级别。日志级别按顺序分别是：DEBUG、INFO、WARN、ERROR   -->
    <!-- 指定任何一个日志级别都只打印当前级别和后面级别的日志。   -->
    <root level="DEBUG">
        <!--   指定打印日志的appender，这里通过"STDOUT"引用了前面配置的appender     -->
        <appender-ref ref="STDOUT"/>
    </root>

    <!--  根据特殊需求指定局部日志级别  -->
    <logger name="com.jxxy.mybatis.mapper" level="DEBUG"/>

</configuration>
1234567891011121314151617181920212223
```

**f> EHCache配置文件说明**

| 属性名                          | 是否必须 | 作用                                                         |
| ------------------------------- | -------- | ------------------------------------------------------------ |
| maxElementsInMemory             | 是       | 在内存中缓存的element的最大数目                              |
| maxElementsOnDisk               | 是       | 在磁盘上缓存的element的最大数目，若是0表示无穷大             |
| eternal                         | 是       | 设定缓存的elements是否永远不过期。如果为true，则缓存的数据始终有效，如果为false那么还要根据timeToIdleSeconds、timeToLiveSeconds判断 |
| overflowToDisk                  | 是       | 设定当内存缓存溢出的时候是否将国企的element缓存到磁盘上      |
| timeToldleSeconds               | 否       | 当缓存在EhCache中的数据前后两次访问的时间超过timeToldleSeconds的属性取值时，这些数据便会删除，默认值是0，也就是可闲置时间无穷大 |
| timeToLiveSeconds               | 否       | 缓存element的有效生命期，默认是0，也就是element存活时间无穷大 |
| diskSpoolBufferSizeMB           | 否       | DiskStore（磁盘缓存）的缓存区大小。默认是30MB，每个Cache都应该有自己的一个缓冲区 |
| diskPersistent                  | 否       | 在VM重启的时候是否用磁盘保存EhCache中的数据，默认是false     |
| diskExpiryThreadIntervalSeconds | 否       | 磁盘缓存的清理线程运行间隔，默认是120秒。每个120s，相应的线程会进行一词EhCache中数据的清理工作 |
| memoryStoreEvictionPolicy       | 否       | 当内存缓存达到最大，有新的element加入的时候，移除缓存中element的策略。默认是LRU（最近最少使用），可选的有LFU（最不常使用）和FIFO（先进先出） |

## 十一、MyBatis的逆向工程（单表查询有用）（工作上实际不用）（不能多表连查）

·正向工程：先创建Java实体类，由框架负责根据实体类生成数据库表。Hibernate是支持正向工程的。

·逆向工程：先创建数据库表，由框架负责根据数据库表，反向生成如下资源：

 ·java实体类

 ·Mapper接口

 ·Mapper映射文件

### 1.创建逆向工程的步骤

**a>添加依赖和插件**

```pom.xml
 <!--  控制maven在构建过程中相关配置  -->
    <build>
        <!--   构建过程中用到的插件     -->
        <plugins>
            <!--   具体插件，逆向工程的操作是以构建过程中插件形式出现的         -->
            <plugin>
                <groupId>org.mybatis.generator</groupId>
                <artifactId>mybatis-generator-maven-plugin</artifactId>
                <version>1.3.6</version>
                <dependencies>
                    <!--      逆向工程的核心依赖              -->
                    <dependency>
                        <groupId>org.mybatis.generator</groupId>
                        <artifactId>mybatis-generator-core</artifactId>
                        <version>1.3.2</version>
                    </dependency>

                    <!--      数据库连接池              -->
                    <dependency>
                        <groupId>com.mchange</groupId>
                        <artifactId>c3p0</artifactId>
                        <version>0.9.2</version>
                    </dependency>
                    <dependency>
                        <groupId>mysql</groupId>
                        <artifactId>mysql-connector-java</artifactId>
                        <version>5.1.3</version>
                    </dependency>
                </dependencies>
            </plugin>

        </plugins>
    </build>
123456789101112131415161718192021222324252627282930313233
```

**b>创建MyBatis的核心配置文件**

**c>创建逆向工程的配置文件**

文件名必须是generatorConfig.xml

```generatorConfig.xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE generatorConfiguration
        PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN"
        "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd">
<generatorConfiguration>

    <!--  targetRuntime:执行生成的逆向工程的版本
            MyBatis3Simple:生成基本的CRUD（清新简洁版）
            Mybatis3：生成带条件的CRUD（奢华尊享版）-->
    <context id="DB2Tables" targetRuntime="MyBatis3">
        <!--   数据库的连接信息     -->
        <jdbcConnection driverClass="com.mysql.jdbc.Driver"
                        connectionURL="jdbc:mysql://localhost:3306/mybatis?characterEncoding=UTF-8"
                        userId="root"
                        password="123456">
        </jdbcConnection>
        <!--   javaBean的生成策略     -->
        <javaModelGenerator targetPackage="com.jxxy.mybatis.pojo"
                            targetProject=".\src\main\java">
            <property name="enableSubPackages" value="true"/>
            <property name="trimStrings" value="true"/>
        </javaModelGenerator>
        <!--   SQL映射文件的生成策略     -->
        <sqlMapGenerator targetPackage="com.jxxy.mybatis.mapper"
                         targetProject=".\src\main\resources">
            <property name="enableSubPackages" value="true"/>
        </sqlMapGenerator>
        <!--  Mapper接口的生成策略      -->
        <javaClientGenerator targetPackage="com.jxxy.mybatis.mapper"
                             targetProject=".\src\main\java"
                                type="XMLMAPPER">
            <property name="enableSubPackages" value="true"/>
        </javaClientGenerator>
        <!--   逆向分析的表     -->
        <table tableName="t_emp" domainObjectName="Emp"/>
        <table tableName="t_dept" domainObjectName="Dept"/>
    </context>
</generatorConfiguration>
1234567891011121314151617181920212223242526272829303132333435363738
```

**d>执行MBG插件的generate目标**

会生成相关的目录和文件

## 十二、分页插件（做导航栏）（好用）

### 1.分页插件使用步骤

**a> 添加依赖**

```POM.XML
<!--分页插件依赖-->
        <dependency>
            <groupId>com.github.pagehelper</groupId>
            <artifactId>pagehelper</artifactId>
            <version>5.3.0</version>
        </dependency>
```

**b> 配置分页插件**

在MyBatis的核心配置文件`mybatis-config,xml`中配置插件

```mybatis-config.xml
<plugins>
        <!--设置分页插件-->
        <plugin interceptor="com.github.pagehelper.PageInterceptor"></plugin>
</plugins>
```

### 2.分页插件的使用

a> 在查询功能之前使用`PageHelper.startPage(int pageNum, int pageSize)`开启分页功能

```java
PageHelper.startPage(int pageNum, int pageSize);
//pageNum:当前页的页码
//pageSize:每页显示的条数
```

b>在查询获取list集合之后，使用`PageInfo pageInfo = new PageInfo<>(List list,int navigatePages)`获取分页相关数据

```java
PageInfo pageInfo = new PageInfo<>(List list,int navigatePages);
//list:分页之后的数据，是调用mapper查询出来的结果list
//navigatePages:导航分页的页码数
```

c>分页相关数据（看看里面会用到那些？)

```java
PageInfo{pageNum=2, pageSize=4, size=4, startRow=5, endRow=8, total=26, pages=7, 
list=Page{count=true, pageNum=2, pageSize=4, startRow=4, endRow=8, total=26, pages=7, reasonable=false, pageSizeZero=false}
[Emp{eid=5, empName='田七', age=43, sex='女', email='90@gmail.com', did=1}, 
Emp{eid=11, empName='a', age=34, sex='男', email='911@gmail.com', did=null}, 
Emp{eid=12, empName='a', age=34, sex='男', email='911@gmail.com', did=null},
Emp{eid=13, empName='a', age=34, sex='男', email='911@gmail.com', did=null}], 
prePage=1, nextPage=3, isFirstPage=false, isLastPage=false, hasPreviousPage=true, hasNextPage=true, navigatePages=5, navigateFirstPage=1, navigateLastPage=5, navigatepageNums=[1, 2, 3, 4, 5]}

常用数据：
pageNum:当前页的页码
pageSize:每页显示的条数
size:当前页显示的真实条数
total:总记录数
pages:总页数
prePage:上一页的页码
nextPage:下一页的页码
isFirstPage/isLastPage:是否为第一页/最后一页
hasPreviousPage/hasNextPage:是否存在上一页/下一页
navigatePages:导航分页的页码数
navigatepaeNums:导航分页的页码
```



# 常见报错

## 多表查询用了Collection

```
org.apache.ibatis.exceptions.PersistenceException
Object key is [null]..... 
```

是因为

```xml
没有写ofType
<collection property="flavors" ofType="com.sky.entity.DishFlavor">
    <id column="df.id" property="id"/>
    <result column="dish_id" property="dishId"/>
    <result column="df.name" property="name"/>
    <result column="value" property="value"/>
</collection>
```

