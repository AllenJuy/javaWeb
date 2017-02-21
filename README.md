# Spring

javaWeb

**web.xml加载过程：**

. 启动容器（tomcat）加载web项目时，容器读取配置文件web.xml:&lt;listener/&gt;和&lt;context-param/&gt;

. 容器创建一个ServletContext，整个web项目都将共享这个上下文

. 容器将&lt;context-param/&gt;转化为键值对，并交给ServletContext

. 容器创建&lt;listener/&gt;中的实例（创建监听）

. 在监听中会有contextInitialized\(ServletContextEvent args\)初始化方法，在这个方法中获得：

ServletContext = ServletContextEvent.getServletContext\(\);

context-param\(value\) = ServletContext.getInitParameter\("context-parm 的 key"\);

（ 得到context-param的值之后，可以做一些操作，注意：这个时候web项目还没有完全启动完成，这个动作比所有的Servlet都要早。所以在对context-param中的键值对做操作时会在项目启动完成前被执行）

**web.xml节点加载顺序：**

. context-param &gt; listener &gt; filter &gt; servlet\(不会因为编写的顺序而有影响\)

**Spring的加载：**

. &lt;listener&gt;&lt;listener-class&gt;org.springframework.web.context.ContextLoaderListener &lt;/listerner-class&gt;&lt;/listener&gt;

总结：web.xml的加载顺序是context-param &gt; listener &gt; filter &gt; servlet &gt; Spring。同类型节点之间的实际程序调用的时候是根据对应的mapping的顺序进行调用的。

引申：Spring的配置（下一篇）

