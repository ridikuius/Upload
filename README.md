# Upload-master
### 上传文件（测试Jetty文件占用无法修改删除的解决方法）
#### 经测试有效
* 文件被锁定是由于在使用windows系统时，jetty默认在内存中映射了这些文件，而windows会锁定内存映射的文件。解决的办法就是修改jetty的配置，让其在启动server时将useFileMappedBuffer标志位设置为false。
* 修改项目中的`WEB-INF/web.xml`文件，在其中加入这个节点。

```xml
<servlet>
    <!-- Override init parameter to avoid nasty -->
    <!-- file locking issue on windows.         -->
    <servlet-name>default</servlet-name>
        <init-param>
            <param-name>useFileMappedBuffer</param-name>
            <param-value>false</param-value>
        </init-param>
</servlet>

```

