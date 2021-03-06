Spring webmvc 集成
==============================

`jetbrick-template` 可以和 `Spring webmvc` 进行集成。


Maven 依赖
------------------

```xml
<dependency>
    <groupId>com.github.subchen</groupId>
    <artifactId>jetbrick-template-springmvc</artifactId>
    <version>{{TEMPLATE-VERSION}}</version>
</dependency>
```

application-context.xml 配置
----------------------------------------------

```xml
<bean id="viewResolver" class="jetbrick.template.web.springmvc.JetTemplateViewResolver">
    <property name="order" value="1" />
    <property name="contentType" value="text/html; charset=utf-8" />
    <property name="suffix" value=".jetx" />
    
    <!-- 指定配置文件 -->
    <property name="configLocation" value="/WEB-INF/jetbrick-template.properties" />
    
    <!-- 直接配置属性 -->
    <property name="configProperties">
        <props>
            <prop key="jetx.input.encoding">utf-8</prop>
            <prop key="jetx.output.encoding">utf-8</prop>
        </props>
    </property>
</bean>
```

> [warn] **小心**：
> * 如果你同时指定 `configLocation` 和 `configProperties` 属性，那么 `configLocation` 文件中的属性优先级高。
> * 请不应该在使用 `viewResolver` 的 `prefix` 属性，用模板的 `$loader.root` 代替


Spring-boot 集成
----------------------------------------------

范例请参考： https://github.com/yingzhuo/springboot-jetx2-examples


范例源码
--------------------------------

具体例子代码参考： https://github.com/subchen/jetbrick-template-2x-samples/


