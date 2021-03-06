Controller 和 Action
==================================

Controller 是一个普通的 Java POJO 类。

每个 Controller 类包含一个或者多个 Action 方法。每一个 Action 方法对应一个 Action URL。

jetbrick 使用 `@Controller` 来标注 Controller 类，使用 `@Action` 来标注一个 Action 方法。

一个最简单的 Controller 类
----------------------------------

```java
@Controller("/hello")
public class HelloController {

    @Action("/world")
    public void world() {
    }
}
```

这个 Action 方法将会被映射到 `/hello/world` 这样的 URL 上面。

Action URL 映射
-------------------------------

一个 Action URL 由 `controller_path` 和 `action_path` 组合而成。 规则如下：

```
Action URL = /<controller_path>/<action_path>
```

### 范例 1

```java
@Controller("/users")
public class UsersController {

    @Action("/list")
    public void list() {
    }
}
```

其中：
* controller_path = /users
* action_path = /list

那么组合在一起的 Action URL 就是 `/users/list`


### 范例 2 （默认 path）

```java
@Controller
public class UsersController {

    @Action
    public void list() {
    }
}
```

缺省默认 path 的规则如下：

* controller_path - 默认为空。
* action_path - 默认为方法名。

根据默认规则，这样我们的 Action URL 就是 `/list`

### URL 映射表格

下面的表格有助于对如何生成对于的 Action URL 有更直观的了解。

controller_path | action_path   | URL                     |
----------------|---------------|-------------------------|
默认(空 or `/`)   | 默认          | /&lt;method>            |
默认(空 or `/`)   | /             | /                       |
默认(空 or `/`)   | /foo          | /foo                    |
默认(空 or `/`)   | foo           | /foo                    |
/boo            | 默认          | /boo/&lt;method>        |
/boo            | /             | /boo/                   |
/boo            | /foo          | /boo/foo                |
/boo            | foo           | /boo/foo                |


Controller 单例？
-----------------------------

默认，我们的 Controller 是单例的，如果你的 Controller 是有状态的，那么你可以将 Controller 设为非单例的。如下：

```java
@Controller(singleton=false)
public class HelloController {

}
```

> [info] **最佳实践**：
>
> * 单例的 Controller 有助于提高响应速度，IoC 注入只发生一次。
> * 单例的 Controller 是线程不安全的，所以应该是无状态的，或者是无关 Request/Session 的。


HTTP request methods
----------------------------

默认的 Action 将会匹配 GET 和 POST 方法，用户可以使用 `@Action` 进行重载。

```java
@Controller
public class FormController {

    @Action(method=HttpMethod.POST)
    public void save() {
    }
}
```

这个 Action 方法将会匹配一个 `POST` 请求， URL为 `/save`。如果是 `GET` 或者其他的请求，那么将会得到一个 `404 (Page not found)`.

我们也支持一个 Action 对应多个 Http Method，可以如下配置：

```java
@Action(method={HttpMethod.GET, HttpMethod.POST})
public void save() {
}
```

