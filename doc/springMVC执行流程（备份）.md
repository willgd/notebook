# springMVC的执行
***
## 1、SpringMVC常用组件
* DispatcherServlet:
前端控制器,不需要工程师开发，由框架提供  
作用：统一处理请求和响应，整个流程控制的中心,由它调用其它组件处理用户的请求
* HandlerMapping:
处理器映射器，不需要工程师开发，由框架提供  
作用：根据请求的url、method等信息查找Handler，即控制器方法
* Handler：处理器,需要工程师开发  
作用：在DispatcherServlet的控制下Handler对具体的用户请求进行处理
* HandlerAdapter:
处理器适配器，不需要工程师开发，由框架提供.  
作用：通过HandlerAdapter对处理器
(控制器方法) 进行执行
* ViewResolver：视图解析器，不需要工程师开发，由框架提供  
作用：进行视图解析，得到相应的视图，例如：ThymeleafView、InternalResourceView、RedirectView
* View：视图
作用：将模型数据通过页面展示给用户
***
## 2、DispatcherServlet初始化过程 
`DispatcherServlet` 本质上是一个`Servlet`，所以天然的遵循`Servlet`的生命周期。所以宏观上是`Servlet`生命周期来进行调度。  
* a>初始化WebApplicationContext
所在类：`org.springframework.web.servlet.FrameworkServlet`  
* b>创建`WebApplicationContext`
所在类：
`org.springframework.web.servlet.FrameworkServlet`
* c>`DispatcherServlet`初始化策略
`FrameworkServlet`创建`WebApplicationContext`后，刷新容器，调用`onRefresh(wac)`，此方法在
`DispatcherServlet`中进行了重写，调用了`initStrategies(context)`方法，初始化策略，即初始化`DispatcherServlet`
的各个组件
所在类：`org.springframework.web.servlet.DispatcherServlet`
## 3、DispatcherServlet调用组件处理请求
a>**processRequest()**  
FrameworkServlet重写HttpServlet中的service()和doXxx()，这些方法中调用了processRequest(request,
response)
所在类：`org.springframework.web.servlet.FrameworkServlet`

processRequest(request,response)-->doService(request,response)-->**doDispatch(request,response)**-->processDispatchResult()

***
* doDispatch(request,response):
```java
new HttpServletRequest processedRequest  = request;  
new HandlerExecutionChain mappedHandler = null;
                   ↓
mappedHandler = getHandler(processedRequest);
                   ↓
HandlerAdapter ha = getHandlerAdapter(mappedHandler.getHandler());
                   ↓
if(!mappedHandler.applyPreHandler(processedRequest,response)){return;}
                   ↓
mv = ha.handler(processedRequest,response,mappedHandler.getHandler());
                   ↓
mappedHandler.applyPostHandler(processedRequest,response,mv);
                   ↓
dispatchException = new ...;
processDispatchResult(processedRequest,response,mappedHandler,mv,dispatchException);

```
* processDispatchResult()
```java
render(mv,request,response);
                   ↓
mappedHandler.triggerAfterCompletion(request,response,null);
```
