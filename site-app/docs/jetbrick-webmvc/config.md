配置 jetbrick-webmvc.properties
========================================

在 web.xml 中，我们配置了 jetbrick-webmvc 用到的全局配置文件，默认位于如下的路径： `/WEB-INF/jetbrick-webmvc.properties`。

这里提供一个完整的可配置项列表，以供参考。


名称                    | 默认值        | 说明
------------------------|---------------|---------------------------------
web.development         | true          | 是否属于开发模式
web.http.encoding       | utf-8         | 默认编码
web.http.cache          | false         | 是否启用 HTTP 协议的 Cache 功能
web.scan.packages       |               | 默认 Annotation 扫描的 packages
web.urls.bypass         |               | 静态资源过滤器
web.urls.router         | RestfulRouter | URL 路由方式
web.view.default        | jetx          | 默认视图处理器别名


web.development
---------------------------

是否属于开发模式。默认为 `true`

何为开发模式？即框架中专门为了开发、调试方便，提供了额外的调试日志，并且禁用了部分 cache，以便能及时发现部分 Resource 的变更，做到热加载。

web.http.encoding
---------------------------

HTTP Request/Response 的编码方式，默认为 `utf-8`

```java
request.setCharacterEncoding(encoding);
response.setCharacterEncoding(encoding);
```

web.http.cache
---------------------------

是否启用 HTTP Response 的 cache，默认为 `false`，表示禁用。

```java
// Http 1.0 header
response.setHeader("Buffer", "false");
response.setHeader("Pragma", "no-cache");
response.setDateHeader("Expires", 1L);

// Http 1.1 header
response.setHeader("Cache-Control", "no-cache, no-store, max-age=0");
```

web.scan.packages
---------------------------

jetbrick-webmvc 通过 Annotation 的自动扫描，可以自动发现如下的配置：

* @IocBean
* @Controller
* @Managed ResultHandler
* @Managed ViewResult
* @Managed ArgumentGetter
* @Managed FileUpload

这里，用户需要配置 classpath 下面允许扫描的 package 名称。可以配置多个。

如下：

```
web.scan.packages = jetbrick.docs.demo.controllers, jetbrick.docs.demo.handlers
```

web.urls.bypass
---------------------------

具体可以参考：[资源过滤器 BypassRequestUrls](bypass-urls.html)

通常来讲，只有 web.xml 中将 URL 映射配置成 `/*` 的时候，才需要进行配置。

目前系统提供了 2 种过滤器，用户可以选择一个，或者实现自己的过滤器。

web.urls.router
---------------------------

默认的路由实现：`jetbrick.web.mvc.router.RestfulRouter`

web.view.default
---------------------------

默认的 view 处理器别名： `jsp`

如果用户返回的 View Name 中，无法判断是有那个 View Handler 处理的话，那么将默认使用这里配置的 View Handler 来处理。

更多信息可以看：[View/ViewHandler](view.html)





