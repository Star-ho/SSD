DispatcherServlet의 doDispatch는 핸들러로 실제로 디스패치 하는 메서드입니다
request를 가지고 getHandler메서드에서 매핑된 핸들러를 가져옵니다
```java
protected void doDispatch(HttpServletRequest request, HttpServletResponse response) throws Exception {  
    HttpServletRequest processedRequest = request;  
    HandlerExecutionChain mappedHandler = null;  
    boolean multipartRequestParsed = false;  
  
    WebAsyncManager asyncManager = WebAsyncUtils.getAsyncManager(request);  
  
    try {  
       ModelAndView mv = null;  
       Exception dispatchException = null;  
  
       try {  
          processedRequest = checkMultipart(request);  
          multipartRequestParsed = (processedRequest != request);  
  
          // Determine handler for the current request.  
          mappedHandler = getHandler(processedRequest);  
          if (mappedHandler == null) {  
             noHandlerFound(processedRequest, response);  
             return;  
          }  
  
          // Determine handler adapter for the current request.  
          HandlerAdapter ha = getHandlerAdapter(mappedHandler.getHandler());  
  
          // Process last-modified header, if supported by the handler.  
          String method = request.getMethod();  
          boolean isGet = HttpMethod.GET.matches(method);  
          if (isGet || HttpMethod.HEAD.matches(method)) {  
             long lastModified = ha.getLastModified(request, mappedHandler.getHandler());  
             if (new ServletWebRequest(request, response).checkNotModified(lastModified) && isGet) {  
                return;  
             }  
          }  
  
          if (!mappedHandler.applyPreHandle(processedRequest, response)) {  
             return;  
          }  
  
          // Actually invoke the handler.  
          mv = ha.handle(processedRequest, response, mappedHandler.getHandler());  
  
          if (asyncManager.isConcurrentHandlingStarted()) {  
             return;  
          }  
  
          applyDefaultViewName(processedRequest, mv);  
          mappedHandler.applyPostHandle(processedRequest, response, mv);  
       }  
       catch (Exception ex) {  
          dispatchException = ex;  
       }  
       catch (Throwable err) {  
          // As of 4.3, we're processing Errors thrown from handler methods as well,  
          // making them available for @ExceptionHandler methods and other scenarios.          dispatchException = new NestedServletException("Handler dispatch failed", err);  
       }  
       processDispatchResult(processedRequest, response, mappedHandler, mv, dispatchException);  
    }  
    catch (Exception ex) {  
       triggerAfterCompletion(processedRequest, response, mappedHandler, ex);  
    }  
    catch (Throwable err) {  
       triggerAfterCompletion(processedRequest, response, mappedHandler,  
             new NestedServletException("Handler processing failed", err));  
    }  
    finally {  
       if (asyncManager.isConcurrentHandlingStarted()) {  
          // Instead of postHandle and afterCompletion  
          if (mappedHandler != null) {  
             mappedHandler.applyAfterConcurrentHandlingStarted(processedRequest, response);  
          }  
       }  
       else {  
          // Clean up any resources used by a multipart request.  
          if (multipartRequestParsed) {  
             cleanupMultipart(processedRequest);  
          }  
       }  
    }  
}
```


getHander메서드에서는 현재 인스턴스의 handlerMappings에있는 mapping에서 현재 request를 인자로 getHandler요청을 호출합니다
mapping의 getHandler는 AbstractHandlerMapping의 getHandler를 사용합니다
```java
protected HandlerExecutionChain getHandler(HttpServletRequest request) throws Exception {  
    if (this.handlerMappings != null) {  
       for (HandlerMapping mapping : this.handlerMappings) {  
          HandlerExecutionChain handler = mapping.getHandler(request);  
          if (handler != null) {  
             return handler;  
          }  
       }  
    }  
    return null;  
}
```

HandlerMapping의 getHandler는 getHandlerInternal을 호출합니다
```java
public final HandlerExecutionChain getHandler(HttpServletRequest request) throws Exception {  
    Object handler = getHandlerInternal(request);  
    if (handler == null) {  
       handler = getDefaultHandler();  
    }  
    if (handler == null) {  
       return null;  
    }  
    // Bean name or resolved handler?  
    if (handler instanceof String) {  
       String handlerName = (String) handler;  
       handler = obtainApplicationContext().getBean(handlerName);  
    }  
  
    // Ensure presence of cached lookupPath for interceptors and others  
    if (!ServletRequestPathUtils.hasCachedPath(request)) {  
       initLookupPath(request);  
    }  
  
    HandlerExecutionChain executionChain = getHandlerExecutionChain(handler, request);  
  
    if (logger.isTraceEnabled()) {  
       logger.trace("Mapped to " + handler);  
    }  
    else if (logger.isDebugEnabled() && !DispatcherType.ASYNC.equals(request.getDispatcherType())) {  
       logger.debug("Mapped to " + executionChain.getHandler());  
    }  
  
    if (hasCorsConfigurationSource(handler) || CorsUtils.isPreFlightRequest(request)) {  
       CorsConfiguration config = getCorsConfiguration(handler, request);  
       if (getCorsConfigurationSource() != null) {  
          CorsConfiguration globalConfig = getCorsConfigurationSource().getCorsConfiguration(request);  
          config = (globalConfig != null ? globalConfig.combine(config) : config);  
       }  
       if (config != null) {  
          config.validateAllowCredentials();  
       }  
       executionChain = getCorsHandlerExecutionChain(request, executionChain, config);  
    }  
  
    return executionChain;  
}
```

getHandlerInternal에서는 
```java
protected HandlerMethod getHandlerInternal(HttpServletRequest request) throws Exception {  
    String lookupPath = initLookupPath(request);  
    this.mappingRegistry.acquireReadLock();  
    try {  
       HandlerMethod handlerMethod = lookupHandlerMethod(lookupPath, request);  
       return (handlerMethod != null ? handlerMethod.createWithResolvedBean() : null);  
    }  
    finally {  
       this.mappingRegistry.releaseReadLock();  
    }  
}
```