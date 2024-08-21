---
title: Java Spring Boot
tags:
  - 学些有趣的
categories:
  - Java
top: 1  
cover: 'https://miaomiao-1-1319022947.cos.ap-beijing.myqcloud.com/202406271601.jpg'
abbrlink: da8c2e9e
date: 2024-08-11 21:09:31
---

主要参考视频：https://www.bilibili.com/video/BV1gm411m7i6/?share_source=copy_web&vd_source=23f587301dbedf5d4b482ef5b1d05bf4

其他资料：互联网，ChatGPT

# 基本使用

## maven

- 管理各种jar包
- 构建项目

## Java-组件化-gradle

https://www.cnblogs.com/Im-Victor/p/10901528.html

组件化可以分别打包，不必注释掉其他类的代码。

组件化步骤：

- 创建module，将代码放到各个module中
- setting.gradle 添加module
- 依赖分开管理

# spring boot

初始化：使用pom.xml打开并创建项目（新建/跑已有的项目）。这里pom中写入相关依赖与配置，如是否有数据库。

运行：

查看：浏览器查看，注意端口为8080

## http动词

```
@GetMapping
```

- GET：取出资源（单个或多个）
- POST：新建资源
- PUT：更新资源（客户端提供改变后的完整资源）
- PATCH：在服务器更新(更新)资源（客户端提供改变的属性，比如说某个字段+1）
- DELETE：从服务器删除资源

这里的`getmapping`大概使用了第1个？

## bean

 构成应用程序主干并由Spring IoC容器管理的对象称为bean。







JpaRepository接口同时拥有基本`CRUD`功能以及分页功能。

```
druid包
```

通常指的是 [Alibaba Druid](https://github.com/alibaba/druid)，这是一个高性能、功能强大的数据库连接池库。在 Spring Boot 项目中，`druid` 包可能包含与 Druid 数据库连接池相关的配置和管理类。

**spring-bean 里注册 druid 的datasource：**添加 Druid 依赖；配置 Druid DataSource；注册 Druid DataSource 为 Spring Bean。

## @……

**<font color = blue>为什么要使用@……</font>**

<u>个人回答：</u>让 Spring 框架自动发现和管理这些类，并将它们注册为 Spring 容器中的一个 bean，吗？

以下为GPT的回答。

***

![](https://miaomiao-1-1319022947.cos.ap-beijing.myqcloud.com/image-20240731134701829.png)

1. **组件扫描和注册 Bean**
   - `@Component`：通用的组件注解，表示类是一个 Spring 组件，会被自动扫描和注册为 bean。
   - `@Service`：特定于服务层的注解，表示类是一个服务组件。
   - `@Repository`：特定于数据访问层的注解，表示类是一个数据仓库组件，通常与持久化框架如 JPA 一起使用。
   - `@Controller`：特定于 Spring MVC 的注解，表示类是一个控制器组件，用于处理 HTTP 请求。
2. **配置和管理 Bean**
   - `@Bean`：用于方法上，表示该方法的返回值是一个 bean，通常用于 Java 配置类中。
   - `@Configuration`：用于标记配置类，表示该类包含了一个或多个 `@Bean` 方法，并且可以被 Spring 容器作为 bean 的定义源。
3. **依赖注入**
   - `@Autowired`：用于自动注入依赖，Spring 会自动满足被标记字段、构造函数或方法的依赖。
   - `@Qualifier`：与 `@Autowired` 一起使用，用于在有多个同类型的 bean 时，指定要注入的具体 bean。
   - `@Inject`：JSR-330 标准注解，类似于 `@Autowired`。
4. **生命周期管理**
   - `@PostConstruct`：用于标记方法，表示该方法应在依赖注入完成后立即调用。
   - `@PreDestroy`：用于标记方法，表示该方法应在容器销毁 bean 之前调用。
5. **事务管理**
   - `@Transactional`：用于类或方法上，表示该类或方法应该在事务上下文中执行。
6. **切面编程**
   - `@Aspect`：用于标记切面类，定义横切关注点。
   - `@Before`、`@After`、`@Around` 等：用于定义切入点方法，表示在目标方法执行前、执行后或包围目标方法执行的逻辑。
7. **MVC 和 Web**
   - `@RequestMapping`：用于方法或类上，映射 HTTP 请求到处理方法。
   - `@GetMapping`、`@PostMapping`、`@PutMapping`、`@DeleteMapping` 等：特定于 HTTP 方法的请求映射。
   - `@RestController`：组合了 `@Controller` 和 `@ResponseBody`，用于创建 RESTful web 服务。

这些注解的使用帮助开发者以声明的方式配置和管理 Spring 应用程序的组件、依赖和行为，大大简化了开发过程中的配置工作，同时提高了代码的可读性和维护性。

***

```
@RestController 
```

注解，用于将 Java 类转换为 RESTful API 控制器。

```
@Repository
```

关于DB的接口？做数据库操作的最底层的抽象接口。标记后将此类作为spring bean放在spring容器中操作。

```
@ApiModelProperty
  value：字段说明 
```

用于方法，字段； 表示对model属性的说明或者数据操作更改。

```
@Service
```

配合接口等使用，解耦？

```
@ApiOperation 
```

![](https://miaomiao-1-1319022947.cos.ap-beijing.myqcloud.com/image-20240801144442539.png)

```
@Component
```



## pom.xml文件

<groupId>   存储的包的路径

<artifactId>   模块名

<version>   声明版本号

## 自动配置

似乎是，不需要配置复杂的环境，仅需在pom文件中写入相关依赖的信息。

分析项目中的依赖关系和配置，自动化地配置Spring应用程序的Bean。

## 项目层次

前端：

- 客户端/浏览器

后端：

- API

- service 层

- data access 层
- 数据库

### 项目流程

#### **数据库：**

自行创建-mysql

数据库表主键何时使用自增长：直接自增（@GeneratedValue），<font color = red>雪花算法，分布式数据库id自增</font>

#### **data access层：**

1. pom补充相关依赖
2. reload
3. 新增package-dao
4. 新增接口，里面有注解@Repository，这里有<a href="#first_link">`extends JpaRepository`</a>。把数据库表映射到对象中。

```
@Id
```

创建自增组件。

```
@Column(name="填数据库对应的列名？")
@TableFiled("....")
```

将数据库中的字段映射。

`@Column,@Table注解是JPA提供的，而@TableField，@TableName注解是MyBatis Plus提供的。`

#### service 层：

分为：

- 接口
- impl







## sql注入检测







# Spring Cloud 的服务发现框架——Eureka