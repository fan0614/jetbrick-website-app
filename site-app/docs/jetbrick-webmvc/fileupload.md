文件上传支持 FileUpload
==============================

jetbrick-webmvc 可以使用 [commons-fileupload](http://commons.apache.org/fileupload) 来处理文件上传。

```xml
<dependency>
    <groupId>com.github.subchen</groupId>
    <artifactId>jetbrick-webmvc-fileupload</artifactId>
    <version>{{WEBMVC-VERSION}}</version>
</dependency>
```

jetbrick-webmvc 会自动判断 Request 请求时候是否是文件上传(multipart/form-data)，然后会将上传文件内容解析出来，将文件内容储存在临时文件中（由 `web.upload.dir` 配置），并封装成 FilePart 对象给用户使用。

看代码学习
-----------------------

```java
@Controller
public class FileController {

    @Action
    public String upload(FilePart[] files) {
        for (FilePart file: files) {
            file.moveTo(new File("/uploads/" + file.getOriginalFileName()));
        }
        return "ok.jsp";
    }
}
```

API 接口
----------------------

我们可以通过 `RequestContext` 对象获取上传的文件：

* **List&lt;FilePart> getFileParts()** - 获取所有的文件对象
* **FilePart getFilePart(String name)** - 按照名称获取文件对象
* **FilePart getFilePart()** - 获取第一个文件对象

同样的，我们可以通过 Action 参数注入获取 FilePart 对象。

* **FilePart[] files** - 获取所有的文件对象(按类型注入)
* **FilePart file** - 获取第一个文件对象(按类型注入)
* **@RequestParam("name") FilePart file** - 按照名称获取文件对象


文件上传和其他参数混合
----------------------------

jetbrick-webmvc 已经在内部处理的该情况，其他参数我们依旧可以通过 `request.getParameter(...)` 来访问。

```java
@Controller
public class PhotoController {

    @Action("/upload/photo")
    public String upload(
            @RequestParam("userid") int userid, 
            FilePart photo
        ) {
        String file = "/user/photos/" + userid +  '.jpg';
        photo.moveTo(new File(file));
        return "ok.jsp";
    }
}
```

我们的 jsp 页面如下：

```html
<form action="/upload/photo" method="post" enctype="multipart/form-data">
    UserId: <br/>
    <input type="text" name="userid" value="123" size="30" /><br/>
    Photo: <br/>
    <input type="file" name="photo" size="30" /><br/>
    <input type="submit" value="Submit" />
</form>
```

