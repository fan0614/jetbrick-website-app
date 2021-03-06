@IocBean
=============================

此章节中，我们会详细讲解一下如何通过 Java Annotation 来配置你的 IoC 容器对象。

通常，在 IoC 容器启动的时候，会在用户配置的 classpath 路径下面扫描所有的 Class，然后将所有声明了 `@IocBean` 这个 Annotation 的 Class，自动加入到 IoC 容器中进行管理。


指定对象的名称
----------------------

任何一个 Ioc 容器管理的对象，都必须有一个名字，以便通过 `ioc.getBean(name)` 来获取对象。因此，你可以这样定义你的对象:

```java
package jetbrick.docs.demo;

@IocBean("foo")
public class Foo {
    ...
}
```

我们看到，我们的 Foo 的名字叫 `foo`，然后我们可以通过下面的代码来获取该对象：

```java
Foo foo = (Foo) ioc.getBean("foo");
```


缺省的对象名称
----------------------

如果你的注解 `@IocBean` 省略了名字，那么默认名字为定义类的完整的类名，如下：

```java
package jetbrick.docs.demo;

@IocBean
public class Foo {
    ...
}
```

这里，我们没有手动指定对象在 IoC 容器中的名称，这个时候将会采用默认的名称（类名的全称）。

然后我们可以通过下面 2 种方式来获取该对象：

1. 根据类名的全称

	```java
	Foo foo = (Foo) ioc.getBean("jetbrick.docs.demo.Foo");
	```

2. 直接根据类名

	```java
	Foo foo = ioc.getBean(Foo.class);
	```

> [info] **最佳实践**：我们推荐对象都优先使用这种缺省名称，不容易产生命名冲突，并且代码更优雅。


工厂类 IocFactory
-----------------------------

像 Spring 的 BeanFactory 一样，我们的 IoC 也支持工厂类。看范例代码：

```java
package jetbrick.docs.demo;

@IocBean("product")
public class ProductFactory implements IocFactory<Product> {

    @Override
    public Product getObject() {
        return new Product();
    }
}

public class Product {
    ...
}
```

通过代码我们可以看到，我的工厂类实现了 `IocFactory` 接口。
这样，我们通过 `ioc.getBean("product")`  获得对象将是 `Product`，而不是 `ProductFactory`。


单例？
-----------------------

默认情况下，所有 `@IocBean` 的对象都被认为是单例对象，在 IoC 容器中只会存在一份实例。

如果要将对象设置为非单例模式，那么只需要配置 `@IocBean(singleton=false)` 既可。

```java
package jetbrick.docs.demo;

// 普通对象
@IocBean(singleton=false)
public class Foo {
    ...
}

// 工厂类
@IocBean(value="product", singleton=false)
public class ProductFactory implements IocFactory<Product> {

    @Override
    public Product getObject() {
        return new Product();
    }
}

// 非单例，普通对象
Foo foo1 = ioc.getBean(Foo.class);
Foo foo2 = ioc.getBean(Foo.class);
assertTrue(foo1 != foo2);

// 非单例，工厂类也一样是使用哦
Product product1 = (Product) ioc.getBean("product");
Product product2 = (Product) ioc.getBean("product");
assertTrue(product1 != product2);
```


