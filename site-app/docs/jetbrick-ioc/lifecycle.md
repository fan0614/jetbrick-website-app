IoC 对象生命周期
============================

在对象注入完成之后，我们提供了一些方法来监控对象的生命周期。


注入完成之后调用的方法 @IocInit
----------------------------------------

```java
@IocBean
public class Test {
    @Inject Foo foo;

    @IocInit
    private void initialize() {
        System.out.println("foo is ready: " + foo);
    }
}
```

> [info] 提示：`@IocInit` 标注的方法必须是没有任何参数，并且返回值是 `void`，非 `static` 的方法。


被 IoC 容器删除时调用的方法 @IocFree
------------------------------------------

注意：如果你的对象是 `singleton=false`，那么 IoC 容器创建了对象实例的时候，并不会记录该对象实例。所以在对象被 IoC 容器移除的时候，并不会触发该方法调用。

> [warn] Sorry！该功能当前版本暂未实现！

