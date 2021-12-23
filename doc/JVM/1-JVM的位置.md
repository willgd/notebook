操作系统（linux）---> JVM运行在jvm上
.java --->(javac)--->class file ---->Class Loader类加载器
<--->runtime data area运行时数据区
* 方法区（元空间）*堆的一种*
* java栈 stack *不会有垃圾回收*
* 本地方法栈 native method stack*不会有垃圾回收*
* 堆 heap *方法调优主要目标*
* 程序计数器*不会有垃圾回收*

JNI Java本地接口
native method library 本地方法库
excute执行引擎

类是抽象的，new出来的对象是具体的。

# Class Loader类加载器
* 虚拟机自带加载器
* 启动类加载器（根加载器）BootstrapClassLoader
* 扩展类加载器 ExtClassLoader
* 应用程序加载器 AppClassLoader