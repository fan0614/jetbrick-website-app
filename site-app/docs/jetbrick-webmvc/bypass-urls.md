资源过滤器 BypassRequestUrls
==================================


在 `web.xml` 中，我们通常将 URL 映射成 `/*`，也就是将所有请求的 URL 都交给 `DispatcherFilter` 来进行处理。

这其中包括了 js, css, jpg 等静态资源，也包括像 jsp 这样的等动态页面。而像这样的 URL 通常是由默认的 Servlet 来处理的，我们的 `DispatcherFilter` 是无法直接处理这样的 URL 资源的。如此就会造成这些 URL 将无法得到正确的处理。

所以，这里我们需要对这些静态/动态资源进行 URL 过滤，让这些 URL 交给其他的 Servlet 来处理。

URL 过滤匹配算法
-------------------------------

jetbrick 提供了 2 种资源过滤器，使用的不同的匹配算法。用户也可以实现自己的资源过滤器。

1. 前缀/后缀匹配: [PrefixSuffixBypassRequestUrls](#-prefixsuffixbypassrequesturls)（默认）
2. 正则表达式匹配: [RegexBypassRequestUrls](#-regexbypassrequesturls)


### 前缀/后缀匹配: PrefixSuffixBypassRequestUrls（默认）

匹配方式和常见的通配符匹配类似，但是只能使用 `*`, 并且 `*` 只能放在最前面或者最后面。

```
$bypassUrls = jetbrick.web.mvc.router.PrefixSuffixBypassRequestUrls
$bypassUrls.patterns = *.jsp, *.html, /assets/*

web.urls.bypass = $bypassUrls
```

### 正则表达式匹配: RegexBypassRequestUrls

```
$bypassUrls = jetbrick.web.mvc.router.RegexBypassRequestUrls
$bypassUrls.patterns = \
	^(.+[.])(jsp|html)$, \
	^(/assets/|/static/).+$

web.urls.bypass = $bypassUrls
```

## 自定义资源过滤器
-----------------------------

如果用户想要自定义自己的过滤器，只要实现 `jetbrick.web.mvc.BypassRequestUrls` 接口即可。

```java
public interface BypassRequestUrls {

    public boolean accept(HttpServletRequest request, String path);

}
```

