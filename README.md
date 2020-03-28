<p align="center">
  <a href="https://github.com/geekidea/spring-boot-plus">
   <img alt="spring-boot-plus logo" src="https://springboot.plus/img/logo.png">
  </a>
</p>
<p align="center">
  Everyone can develop projects independently, quickly and efficiently！
</p>

<p align="center">  
  <a href="https://github.com/geekidea/spring-boot-plus/">
    <img alt="spring-boot-plus version" src="https://img.shields.io/badge/spring--boot--plus-2.0-blue">
  </a>
  <a href="https://github.com/spring-projects/spring-boot">
    <img alt="spring boot version" src="https://img.shields.io/badge/spring%20boot-2.2.5.RELEASE-brightgreen">
  </a>
  <a href="https://www.apache.org/licenses/LICENSE-2.0">
    <img alt="code style" src="https://img.shields.io/badge/license-Apache%202-4EB1BA.svg?style=flat-square">
  </a>
</p>

## What is spring-boot-plus?

### A **easy-to-use**, **high-speed**, **high-efficient**, **feature-rich**, **open source** spring boot scaffolding.
> spring-boot-plus is a background rapid development framework that integrates spring boot common development components.

> Front-end and back-end separation, focusing on back-end services

## Purpose
> Everyone can develop projects independently, quickly and efficiently！

## Repository
#### [GITHUB](https://github.com/geekidea/spring-boot-plus) | [GITEE](https://gitee.com/geekidea/spring-boot-plus)

## Website
#### [springboot.plus](http://springboot.plus)

## Features
- Integrated spring boot common development component set, common configuration, AOP log, etc
- Maven Module Project
- Integrated mybatis-plus fast dao operation
- Quickly generate background code:entity/param/vo/controller/service/mapper/xml
- Integrated swagger2, automatic generation of api documents
- Integrated JWT,Shiro/Spring security permission control
- Integrated Redis Cache
- Integration HikariCP connection pool, A solid, high-performance, JDBC connection pool at last.
- Integrated Spring Boot Admin, real-time detection of project operation
- Integrate maven-assembly-plugin for different environment package deployment, including startup and restart commands, and extract configuration files to external config directory

## Project structure
```text
└── spring-boot-plus
    ├── admin           SpringBootAdmin Server Module          
    ├── bootstrap       Project Bootstrap Module    
    ├── config          Config Module
    ├── distribution    Maven assembly Module        
    ├── docs            Document
    ├── example         Example Module
    ├── framework       Framework Core Module    
    ├── generator       Code Generator Module    
    ├── scheduled       Scheduled Module
    └── system          System Manager Module
```

### Project Environment 
Middleware | Version |  Remark
-|-|-
JDK | 1.8+ | JDK1.8 and above |
MySQL | 5.7+ | 5.7 and above |
Redis | 3.2+ |  |

### Technology stack 
Component| Version |  Remark
-|-|-
Spring Boot | 2.2.5.RELEASE | Latest release stable version |
Spring Framework | 5.2.4.RELEASE | Latest release stable version |
Spring Boot Admin| 2.2.2 | Manage and monitor spring boot applications |
Mybatis | 3.5.3 | DAO Framework |
Mybatis Plus | 3.3.1 | mybatis Enhanced framework |
HikariCP | 3.4.2 | DataSource |
Fastjson | 1.2.67 | JSON processing toolset |
Swagger2 | 2.9.2 | Api document generation tool |
Knife4j | 2.0.2 | Api document generation tool |
commons-lang3 | 3.9 | Apache language toolkit |
commons-io | 2.6 | Apache IO Toolkit |
commons-codec | 1.14 | Apache Toolkit such as encryption and decryption |
commons-collections4 | 4.4 | Apache collections toolkit |
reflections | 0.9.9 | Reflection Toolkit  |
hibernate-validator | 6.0.18.Final | Validator toolkit |
Shiro | 1.5.1 | Permission control |
JWT | 3.10.1 | JSON WEB TOKEN |
hutool-all | 5.2.4 | Common toolset |
lombok | 1.18.12 | Automatically plugs |
mapstruct | 1.3.1.Final | Object property replication tool |

## CHANGELOG
#### [CHANGELOG.md](https://github.com/geekidea/spring-boot-plus/blob/master/CHANGELOG.md)

## Java Docs
#### [Java Api Docs](http://geekidea.io/spring-boot-plus-apidocs/)


## Getting started
### Clone spring-boot-plus
```bash
git clone https://github.com/geekidea/spring-boot-plus.git
cd spring-boot-plus
```

### Maven Build
> dev environment is used by default, The configuration file：application-dev.yml
```bash
mvn clean package -Plocal
```


## 5 Minutes Finish CRUD

### 1. Create Table
```sql
-- ----------------------------
-- Table structure for foo_bar
-- ----------------------------
DROP TABLE IF EXISTS `foo_bar`;
CREATE TABLE `foo_bar`
(
    `id`            bigint(20)  NOT NULL COMMENT 'ID',
    `name`          varchar(20) NOT NULL COMMENT 'Name',
    `foo`           varchar(20)          DEFAULT NULL COMMENT 'Foo',
    `bar`           varchar(20) NOT NULL COMMENT 'Bar',
    `remark`        varchar(200)         DEFAULT NULL COMMENT 'Remark',
    `state`         int(11)     NOT NULL DEFAULT '1' COMMENT 'State，0：Disable，1：Enable',
    `version`       int(11)     NOT NULL DEFAULT '0' COMMENT 'Version',
    `create_time`   timestamp   NULL     DEFAULT CURRENT_TIMESTAMP COMMENT 'Create Time',
    `update_time`   timestamp   NULL     DEFAULT NULL COMMENT 'Update Time',
    PRIMARY KEY (`id`)
) ENGINE = InnoDB
  DEFAULT CHARSET = utf8mb4
  COLLATE = utf8mb4_general_ci COMMENT ='FooBar';

-- ----------------------------
-- Records of foo_bar
-- ----------------------------
INSERT INTO foo_bar (id, name, foo, bar, remark, state, version, create_time, update_time) 
    VALUES (1, 'FooBar', 'foo', 'bar', 'remark...', 1, 0, '2019-11-01 14:05:14', null);
INSERT INTO foo_bar (id, name, foo, bar, remark, state, version, create_time, update_time) 
    VALUES (2, 'HelloWorld', 'hello', 'world', null, 1, 0, '2019-11-01 14:05:14', null);

```

### 2. Generator CRUD CODE
> Modify database info

> Modify module name / author / table name / primary key id

#### generator Module

```text
SpringBootPlusGenerator.java
```

```java
/**
 * spring-boot-plus Code Generator
 *
 * @author geekidea
 * @date 2019-10-22
 **/
public class SpringBootPlusGenerator {

    public static void main(String[] args) {
        CodeGenerator codeGenerator = new CodeGenerator();
        // Common configuration
        // Database configuration
        codeGenerator
                .setUserName("root")
                .setPassword("root")
                .setDriverName("com.mysql.jdbc.Driver")
                .setDriverUrl("jdbc:mysql://localhost:3306/spring_boot_plus?useUnicode=true&characterEncoding=UTF-8&useSSL=false");

        // Configuration package information
        codeGenerator
                .setProjectPackagePath("io/geekidea/springbootplus")
                .setParentPackage("io.geekidea.springbootplus");

        // Configuration of component author, etc.
        codeGenerator
                .setModuleName("foobar")
                .setAuthor("geekidea")
                .setPkIdColumnName("id");

        // Generation strategy
        codeGenerator
                .setGeneratorStrategy(CodeGenerator.GeneratorStrategy.ALL)
                .setPageListOrder(true)
                .setParamValidation(true);

        // Customize which files are generated automatically
        codeGenerator
                .setGeneratorEntity(true)
                .setGeneratorPageParam(true)
                .setGeneratorQueryVo(true);

        // Generate business related codes
        codeGenerator
                .setGeneratorController(true)
                .setGeneratorService(true)
                .setGeneratorServiceImpl(true)
                .setGeneratorMapper(true)
                .setGeneratorMapperXml(true);

        // Generated RequiresPermissions Annotation
        codeGenerator.setRequiresPermissions(false);

        // Overwrite existing file or not
        codeGenerator.setFileOverride(true);

        // Initialize common variables
        codeGenerator.init();

        // Table array to be generated
        String[] tables = {
                "foo_bar"
        };

        // Cycle generation
        for (String table : tables) {
            // Set the name of the table to be generated
            codeGenerator.setTableName(table);
            // Generate code
            codeGenerator.generator();
        }

    }

}
```

```java
/**
 * spring-boot-plus代码生成器入口类
 *
 * @author geekidea
 * @date 2019-10-22
 **/
@Component
public class SpringBootPlusGenerator {

    /**
     * 生成代码
     * @param args
     */
    public static void main(String[] args) {
        GeneratorProperties generatorProperties = new GeneratorProperties();

        // Common configuration
        generatorProperties
                .setMavenModuleName("example")
                .setParentPackage("com.example")
                .setModuleName("foobar")
                .setAuthor("geekidea")
                .setFileOverride(true);

        // generator Table
        generatorProperties.addTable("foo_bar","id");

        // DataSourceConfig
        generatorProperties.getDataSourceConfig()
                .setDbType(DbType.MYSQL)
                .setUsername("root")
                .setPassword("root")
                .setDriverName("com.mysql.jdbc.Driver")
                .setUrl("jdbc:mysql://localhost:3306/spring_boot_plus?useUnicode=true&characterEncoding=UTF-8&useSSL=false");

        // GeneratorConfig
        generatorProperties.getGeneratorConfig()
                .setGeneratorStrategy(GeneratorStrategy.SINGLE)
                .setGeneratorEntity(true)
                .setGeneratorController(true)
                .setGeneratorService(true)
                .setGeneratorServiceImpl(true)
                .setGeneratorMapper(true)
                .setGeneratorMapperXml(true)
                .setGeneratorPageParam(true)
                .setGeneratorQueryVo(true)
                .setRequiresPermissions(true)
                .setPageListOrder(true)
                .setParamValidation(true)
                .setSwaggerTags(true)
                .setOperationLog(true);

        // GlobalConfig
        generatorProperties.getMybatisPlusGeneratorConfig().getGlobalConfig()
                .setOpen(true)
                .setSwagger2(true)
                .setIdType(IdType.AUTO)
                .setDateType(DateType.ONLY_DATE);

        // StrategyConfig
        generatorProperties.getMybatisPlusGeneratorConfig().getStrategyConfig()
                .setNaming(NamingStrategy.underline_to_camel)
                .setColumnNaming(NamingStrategy.underline_to_camel)
                .setEntityLombokModel(true)
                .setRestControllerStyle(true)
                .setControllerMappingHyphenStyle(true)
                .setVersionFieldName(GeneratorConstant.VERSION)
                .setLogicDeleteFieldName(GeneratorConstant.DELETED);

        // Code Generator 
        CodeGenerator codeGenerator = new CodeGenerator();
        codeGenerator.generator(generatorProperties);
    }
}
```

> Generated code structure

```text
└── src
    └── main
        ├── java
        │   └── com
        │       └── example
        │           └── foobar
        │               ├── controller
        │               │   └── FooBarController.java
        │               ├── entity
        │               │   └── FooBar.java
        │               ├── mapper
        │               │   └── FooBarMapper.java
        │               ├── param
        │               │   └── FooBarPageParam.java
        │               ├── service
        │               │   ├── FooBarService.java
        │               │   └── impl
        │               │       └── FooBarServiceImpl.java
        │               └── vo
        │                   └── FooBarQueryVo.java
        └── resources
            └── mapper
                └── foobar
                    └── FooBarMapper.xml
```

### 3. Startup Project
> Project Main Class
```text
src/main/java/io/geekidea/springbootplus/SpringBootPlusApplication.java
```

```java
/**
 * spring-boot-plus Project Main Class
 * @author geekidea
 * @since 2018-11-08
 */
@EnableAsync
@EnableScheduling
@EnableTransactionManagement
@EnableConfigurationProperties
@EnableAdminServer
@MapperScan({"io.geekidea.springbootplus.**.mapper"})
@SpringBootApplication
public class SpringBootPlusApplication {

    public static void main(String[] args) {
        // Run spring-boot-plus
        ConfigurableApplicationContext context = SpringApplication.run(SpringBootPlusApplication.class, args);
        // Print Project Info
        PrintApplicationInfo.print(context);
    }

}


/**
 * spring-boot-plus Project Main Class
 *
 * @author geekidea
 * @since 2018-11-08
 */
@EnableAsync
@EnableScheduling
@EnableTransactionManagement
@EnableConfigurationProperties
@ServletComponentScan
@MapperScan({"io.geekidea.springbootplus.**.mapper", "com.example.**.mapper"})
@SpringBootApplication(scanBasePackages = {"io.geekidea.springbootplus", "com.example"})
public class SpringBootPlusApplication {

    public static void main(String[] args) {
        // Run spring-boot-plus
        ConfigurableApplicationContext context = SpringApplication.run(SpringBootPlusApplication.class, args);
        // Print Project Info
        PrintApplicationInfo.print(context);
        // Print Project Tip
        PrintApplicationInfo.printTip();
    }

}

```

### 4. Access Swagger Docs
[http://47.105.159.10:8888/api/swagger-ui.html](http://47.105.159.10:8888/api/swagger-ui.html)
![swagger-ui.png](https://geekidea.oss-cn-chengdu.aliyuncs.com/spring-boot-plus/img/swagger-ui.png)
![swagger-ui-1.png](https://geekidea.oss-cn-chengdu.aliyuncs.com/spring-boot-plus/img/swagger-ui-1.png)

### 5. Access Knife4j Docs 
[http://47.105.159.10:8888/api/doc.html](http://47.105.159.10:8888/api/doc.html)
![knife4j.png](https://geekidea.oss-cn-chengdu.aliyuncs.com/spring-boot-plus/img/knife4j.png)
![knife4j-1.png](https://geekidea.oss-cn-chengdu.aliyuncs.com/spring-boot-plus/img/knife4j-1.png)


## CentOS Quick Installation Environment / Build / Deploy / Launch Spring-boot-plus Project

### 1. Download the installation script
> Install `jdk`, `git`, `maven`, `redis`, `mysql`

```bash
wget -O download-install-all.sh https://springboot.plus/bin/download-install-all.sh
```

### 2. Run the installation script
```bash
sh download-install-all.sh
```

### 3. Modify MySQL password
```bash
ALTER USER 'root'@'localhost' IDENTIFIED BY 'Springbootplus666!';
exit
mysql -uroot -pSpringbootplus666!
```

### 4. Import MySQL scripts
```bash
create database if not exists spring_boot_plus character set utf8mb4;
use spring_boot_plus;
source /root/mysql_spring_boot_plus.sql;
show tables;
exit
```

### 5. Download deployment script `deploy.sh`
```bash
wget -O deploy.sh https://springboot.plus/bin/deploy.sh
```

### 6. Execution script
```bash
sh deploy.sh
```

### 7. View project run log
```bash
tail -f -n 1000 /spring-boot-plus-server-2.0/logs/spring-boot-plus.log
```


## spring-boot-plus Views

### spring-boot-plus IDEA Sources Views

![spring-boot-plus-idea](https://geekidea.oss-cn-chengdu.aliyuncs.com/spring-boot-plus/img/idea.png)

### [Spring Boot Admin Instances](http://47.105.159.10:8000/instances/11090f218c47/details)
<p>
    <a href="http://47.105.159.10:8000/instances/11090f218c47/details">
        <img src="https://geekidea.oss-cn-chengdu.aliyuncs.com/spring-boot-plus/img/springbootadmin-en.png" alt="spring-boot-admin instances">
    </a>
</p>

### [Spring Boot Admin Statistics](http://47.105.159.10:8000/instances/11090f218c47/details)
<p>
    <a href="http://47.105.159.10:8000/instances/11090f218c47/details">
        <img src="https://geekidea.oss-cn-chengdu.aliyuncs.com/spring-boot-plus/img/springbootadmin-en-1.png" alt="spring-boot-admin statistics">
    </a>
</p>

### [Spring Boot Admin Log](http://47.105.159.10:8000/instances/11090f218c47/logfile)
<p>
    <a href="http://47.105.159.10:8000/instances/11090f218c47/logfile">
        <img src="https://springboot.plus/img/home/spring-boot-admin-log-en.png" alt="spring-boot-admin log">
    </a>
</p>

## spring-boot-plus-vue Front-end Project
### [GITHUB-REPO](https://github.com/geekidea/spring-boot-plus-vue)
### [VUE WebSite](http://47.105.159.10/)
#### VUE HOME
![VUE HOME](https://geekidea.oss-cn-chengdu.aliyuncs.com/spring-boot-plus/img/springbootplusvue.png)
#### System User List
![System User List](https://geekidea.oss-cn-chengdu.aliyuncs.com/spring-boot-plus/img/springbootplusvue-1.png)


## spring-boot-plus Videos  :movie_camera: 
- [5-Minutes-Finish-CRUD](https://www.bilibili.com/video/av67401204)
- [CentOS Quick Installation JDK/Git/Maven/Redis/MySQL](https://www.bilibili.com/video/av67218836/)
- [CentOS Quick Build / Deploy / Launch Spring-boot-plus Project](https://www.bilibili.com/video/av67218970/)


## Contact
- spring-boot-plus QQ Group

![spring-boot-plus QQ Group](https://spring-boot-plus.gitee.io/img/spring-boot-plus-qq-group.png)


## Donate
Ask the author to drink coffee and let the code fly for a while! 

![geekidea-wechat-donate](https://geekidea.oss-cn-chengdu.aliyuncs.com/geekidea/geekidea-wechat-donate.png)

## License
spring-boot-plus is under the Apache 2.0 license. See the [LICENSE](https://github.com/geekidea/spring-boot-plus/blob/master/LICENSE) file for details.

