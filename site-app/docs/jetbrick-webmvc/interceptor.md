自定义拦截器 Interceptor
===============================

Interceptor 是 jetbrick webmvc 用来实现对 Action 的预处理和后处理功能（AOP）。

jetbrick 采用了类似于 HTTP Filter 的责任链模式实现 Interceptor chain。

所有 Interceptor 都是单例的，非线程安全的。


Interceptor 例子
--------------------------------------------------

用户自定义的 Interceptor 需要实现 `jetbrick.web.mvc.intercept.Interceptor` 接口。

```java
package jetbrick.docs.samples;

import jetbrick.web.mvc.RequestContext;
import jetbrick.web.mvc.intercept.Interceptor;
import jetbrick.web.mvc.intercept.InterceptorChain;

public class LogInterceptor implements Interceptor {

    @Override
    public void initialize() {
    }

    @Override
    public void intercept(RequestContext ctx, InterceptorChain chain) throws Throwable {
        System.out.println("Before invoking");
        chain.invoke();
        System.out.println("After invoking");
    }

    @Override
    public void destory() {
    }
}
```

正如上面的代码所示，Interceptor 可以很方便地在 action 调用前后插入切面代码来实现 AOP。

其中 `chain.invoke()` 方法将调用下一个 Interceptor 或者 Action 方法。

> [warn] **注意**: Interceptor 只能拦截 Action，不能拦截 View。


Interceptor 配置 
--------------------------------------------------

jetbrick 总共下面支持 3 种级别的 Interceptor

* Global 级别 - 对所有的 Action 进行拦截
* Controller 级别 - 对 Controller 中定义的 Action 进行拦截 (当前版本暂未实现)
* Action 级别 - 对单个 Action 方法进行拦截 (当前版本暂未实现)


### Global 级别

在全局配置文件中 jetbrick-webmvc.properties 进行配置。

```
$LogInterceptor = jetbrick.docs.samples.LogInterceptor
$DbTransactionInterceptor = jetbrick.docs.samples.DbTransactionInterceptor

web.interceptors = $LogInterceptor, $DbTransactionInterceptor
```

### Controller 级别 (当前版本暂未实现)

在 Controller 类上面添加 @InterceptedWith 标注

```java
@InterceptedWith(AuthInterceptor.class)
@Controller
public class UserController {
    ...
}
```


### Action 级别 (当前版本暂未实现)

在 Action 方法上面添加 @InterceptedWith 标注

```java
@Controller
public class UserController {

    @InterceptedWith(AuthInterceptor.class)
    @Action
    public String save() {
        ...
    }
}
```

> [warn] **注意**：拦截器调用的顺序如下：
> 
> 1. Action 级别
> 2. Controller 级别
> 3. Global 级别
> 同级的 Interceptor 和定义的顺序保持一致。


