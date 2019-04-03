###源码阅读知识点
-  拦截器的设计模式--责任链模式
   *  RealCall类中的getResponseWithInterceptorChain方法和RealInterceptorChain管理拦截器的调用，调用顺序？；
   *  应用拦截器和网络拦截器的区别？
   
-  RetryAndFollowUpInterceptor--请求失败重试请求和重定向
   *  核心方法recover和followUpRequest；recover方法判断是否继续重试，followUpRequest方法进行重定向，
   *  问题？StreamAllocation和Route
   
- BridgeInterceptor--处理请求头，Gzip，以及cookie的处理

- CacheInterceptor--缓存逻辑，见intercept方法分析
