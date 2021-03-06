配置 web.xml
===========================

一个典型的 Restful 配置 "/*"
----------------------------------

```xml
<filter>
    <filter-name>jetbrick-webmvc</filter-name>
    <filter-class>jetbrick.web.mvc.DispatcherFilter</filter-class>
    <init-param>
        <param-name>configLocation</param-name>
        <param-value>/WEB-INF/jetbrick-webmvc.properties</param-value>
    </init-param>
</filter>
<filter-mapping>
    <filter-name>jetbrick-webmvc</filter-name>
    <url-pattern>/*</url-pattern>
</filter-mapping>
```

1. 将 URL 映射成 `/*`，将会对所有的资源进行拦截，静态资源的过滤请看：[资源过滤器 BypassRequestUrls](bypass-urls.html)
2. 设置配置文件路径为 `/WEB-INF/jetbrick-webmvc.properties` （默认值）



传统的后缀名映射 "*.do"
-------------------------------------

```xml
<filter>
    <filter-name>jetbrick-webmvc</filter-name>
    <filter-class>jetbrick.web.mvc.DispatcherFilter</filter-class>
    <init-param>
        <param-name>configLocation</param-name>
        <param-value>/WEB-INF/jetbrick-webmvc.properties</param-value>
    </init-param>
</filter>
<filter-mapping>
    <filter-name>jetbrick-webmvc</filter-name>
    <url-pattern>*.do</url-pattern>
</filter-mapping>
```

1. 将 URL 映射成 `*.do`
2. 设置配置文件路径为 `/WEB-INF/jetbrick-webmvc.properties` （默认值）



