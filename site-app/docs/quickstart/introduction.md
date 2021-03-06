jetbrick 介绍
==========================

jetbrick 是什么？
-------------------------

jetbrick 是一个用 Java 开发的轻量级框架。追求快速上手和高效开发。用少量的代码来实现强大的功能。极大的提高用户的开发效率，节约宝贵的时间。


jetbrick 的组成部分
-------------------------

组件                      | 说明
--------------------------|-------------------------------
[jetbrick-commons][]      | 常用 Utils 类库
[jetbrick-webmvc][]       | 灵活的 MVC 框架
[jetbrick-template][]     | 高性能的 Java 模板引擎
[jetbrick-ioc][]          | 小巧的 IoC 容器
[jetbrick-orm][]          | 一个 轻量级的 O/R Mapping 框架
[jetbrick-schema-app][]   | 基于 Schema 的自动代码生成器


jetbrick-commons
-------------------------

jetbrick-commons 提供了常用的 utils 类库，类似于 apache-commons 类库。无第三方 jars 依赖，其中部分源代码来源于第三方开源类库。

* StringUtils, ArrayUtils, ...
* ClassDescriptor, MethodDescriptor, ...
* ClassLoaderUtils, ClassUtils, ...
* FileResource, ClasspathResource, ...
* FastByteArrayOutputStream, ...
* FileFinder, ClassFinder, ...
* ConfigLoader, Configuration, ...
* Logger, LoggerFactory, ...
* TypeCast
* ...

jetbrick-webmvc 的特点
-------------------------

类似于 Struts, Spring MVC 等经典 MVC 框架，jetbrick-webmvc 通过大量的经验总结，提供小巧、强大，更灵活的 webmvc。

- 小巧，轻量，易上手
- 支持 Restful
- IoC 注入，易管理，易测试
- Interceptor 机制，功能强大
- Plugin 机制，易扩展
- 完全自定义的 Annotation，灵活定制
- 内置文件上传，下载支持
- 内置 JSON 支持
- 内置多种 Result
- 内置多种 View


jetbrick-template 的特点
-------------------------

jetbrick-template 是一个新一代 Java 模板引擎，具有高性能和高扩展性。 适合于动态 HTML 页面输出或者代码生成，可替代 JSP 页面或者 Velocity 等模板。 指令和 Velocity 相似，表达式和 Java 保持一致，易学易用。

- 支持类似于 Velocity 的多种指令
- 支持静态编译
- 支持编译缓存
- 支持热加载
- 支持类型推导
- 支持泛型
- 支持可变参数方法调用
- 支持方法重载
- 支持类似于 Groovy 的方法扩展
- 支持函数扩展
- 支持自定义标签 #tag
- 支持宏定义 #macro
- 支持布局 Layout


jetbrick-ioc 的特点
-------------------------

简单，小巧的 IoC 容器，Bean 自动发现，自动注册。

- 小巧，轻量，易上手
- Properties 配置文件配置 Bean
- Annotation 自动扫描获取 Bean
- 支持字段注入
- 支持构造函数注入
- 支持 Bean 工厂模式
- 支持 Bean 初始化方法
- 支持自定义的 Annotation 注入


jetbrick-orm 的特点
-------------------------

JDBC 的轻量级封装，面向对象的 API 接口。简单，高效。

- 无反射，高性能
- API 接口易使用
- 支持 one-to-one, one-to-many
- 支持 CRUD Cache
- 支持编程事务+声明事务
- 支持嵌入式事务
- 支持数据库方言 Dialect
- 支持 JSR303 Validator
- 支持运行期自动升降级数据库
- 配合 [jetbrick-schema-app][] 自动生成 pojo, dao

jetbrick-schema-app 的特点
-------------------------

借助于 XML Schema 文件，自动为 jetbrick-orm 生成相应的 POJO, DAO 等相关代码。

- 自动生成 [jetbrick-orm][] 用的 pojo, dao
- 独立的数据类型（和数据库产品无关）
- 支持多种数据库
- 支持 one-to-one, one-to-many
- 支持不同类型的主键（String, int, Long)


[jetbrick-commons]: 	#jetbrick-commons
[jetbrick-webmvc]: 		#jetbrick-webmvc
[jetbrick-template]: 	#jetbrick-template
[jetbrick-ioc]: 		#jetbrick-ioc
[jetbrick-orm]: 		#jetbrick-orm
[jetbrick-schema-app]: 	#jetbrick-schema-app

