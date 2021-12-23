native关键字表示java的作用范围达不到，需要调用本地方法的库。
* 进入本地方法栈
* 调用本地方法接口 JNI java native interface
* 扩展java的使用
* 在内存中专门开辟了一块标记的区域，native method stack，登记native方法，在执行引擎执行的时候加载本地库。
  
pc寄存器
* 程序计数器 每个线程都有一个计数器

方法区
* static方法
* final
* class类
* 常量池