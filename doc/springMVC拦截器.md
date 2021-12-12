## preHandle（） 在控制器执行之前执行
```java
default boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler)
			throws Exception {

		return true;//返回true则放行
	}
```
多个preHandle（）返回值都为true，则按spring mvc配置顺序执行
![图 4](../../images/3423762ff9d2c33f8dba8ab3325636410d3d69a906e5ce2575723c3cf550adfd.png)  

## postHandle() 在控制器执行之后执行
```java
default void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler,
			@Nullable ModelAndView modelAndView) throws Exception {
	}
```
多个postHandle（）返回值都为true，则按spring mvc配置倒序执行
![图 2](../../images/370ce9be9df7ba085bf23a6e13fa51051129aa3bd035196cbfdc610d36b37f49.png)  

## afterCompletion 在视图渲染后执行
```java
default void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler,
			@Nullable Exception ex) throws Exception {
	}
```
多个afterCompletion（）返回值都为true，则按spring mvc配置倒序执行
![图 3](../../images/7a7ea76ab7f3fbb7e815e05c6b979d135676c428148b750f225102ad21d3e107.png)  

<!--
Workflow interface that allows for customized handler execution chains. Applications can register any number of existing or custom interceptors for certain groups of handlers, to add common preprocessing behavior without needing to modify each handler implementation.
A HandlerInterceptor gets called before the appropriate HandlerAdapter triggers the execution of the handler itself. This mechanism can be used for a large field of preprocessing aspects, e.g. for authorization checks, or common handler behavior like locale or theme changes. Its main purpose is to allow for factoring out repetitive handler code.
In an asynchronous processing scenario, the handler may be executed in a separate thread while the main thread exits without rendering or invoking the postHandle and afterCompletion callbacks. When concurrent handler execution completes, the request is dispatched back in order to proceed with rendering the model and all methods of this contract are invoked again. For further options and details see org.springframework.web.servlet.AsyncHandlerInterceptor
Typically an interceptor chain is defined per HandlerMapping bean, sharing its granularity. To be able to apply a certain interceptor chain to a group of handlers, one needs to map the desired handlers via one HandlerMapping bean. The interceptors themselves are defined as beans in the application context, referenced by the mapping bean definition via its "interceptors" property (in XML: a <list> of <ref>).
HandlerInterceptor is basically similar to a Servlet Filter, but in contrast to the latter it just allows custom pre-processing with the option of prohibiting the execution of the handler itself, and custom post-processing. Filters are more powerful, for example they allow for exchanging the request and response objects that are handed down the chain. Note that a filter gets configured in web.xml, a HandlerInterceptor in the application context.
As a basic guideline, fine-grained handler-related preprocessing tasks are candidates for HandlerInterceptor implementations, especially factored-out common handler code and authorization checks. On the other hand, a Filter is well-suited for request content and view content handling, like multipart forms and GZIP compression. This typically shows when one needs to map the filter to certain content types (e.g. images), or to all requests.
自:
20.06.2003
请参阅:
HandlerExecutionChain.getInterceptors, org.springframework.web.servlet.handler.AbstractHandlerMapping.setInterceptors, org.springframework.web.servlet.handler.UserRoleAuthorizationInterceptor, org.springframework.web.servlet.i18n.LocaleChangeInterceptor, org.springframework.web.servlet.theme.ThemeChangeInterceptor, javax.servlet.Filter
作者:
Juergen Hoeller
-->
