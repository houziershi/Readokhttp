### 源码阅读知识点
-  拦截器的设计模式--责任链模式
   *  RealCall类中的getResponseWithInterceptorChain方法和RealInterceptorChain管理拦截器的调用，调用顺序？；
   *  应用拦截器和网络拦截器的区别？
   
-  RetryAndFollowUpInterceptor--请求失败重试请求和重定向
   *  核心方法recover和followUpRequest；recover方法判断是否继续重试，followUpRequest方法进行重定向;
   ```   
   *  创建StreamAllocation对象；
   *  调用realChain.proceed(request, streamAllocation, null, null)进行网络请求；
   *  根据异常结果或者响应结果判断是否进行重新请求；
   *  调用下一个拦截器，对responese进行处理，返回给上一个拦截器；
   ```
   *  问题？StreamAllocation和Route  
- BridgeInterceptor--处理请求头，Gzip，以及cookie的处理

- CacheInterceptor--缓存逻辑，见intercept方法分析
    ```
    * 读取候选缓存；
    * 创建缓存策略（根据头信息，判断强制缓存，对比缓存等策略)；
    * 根据策略，不使用网络，缓存又没有直接报错；
    * 根据策略，不使用网络，有缓存就直接返回；
    * 前面个都没有返回，读取网络结果（跑下一个拦截器）；
    * 接收到的网络结果，如果是code 304, 使用缓存，返回缓存结果（对比缓存）
    * 读取网络结果；
    * 对数据进行缓存；删除无效缓存；
    * 返回网络读取的结果。
    ```
- ConnectInterceptor--启动一个连接，调用下一个拦截器

- StreamAllocation    

- ConnectionPool
```
    * 连接池：connections默认可以有5个请求，5分钟的活跃度(超过时间被踢出)
    * get方法获取一个connection：
```
 