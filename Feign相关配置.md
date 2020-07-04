```yaml
feign:
  client:
    config:
      # 全局配置 如果需要单个配置指定Feign-name
      default:
        # 连接超时时间
        connectTimeout: 6000
        # 读取超时时间
        readTimeout: 6000
        # 日志级别
        loggerLevel: full
        # 错误解码器
        errorDecoder: com.example.SimpleErrorDecoder
        # 重试策略
        retryer: com.example.SimpleRetryer
        # 拦截器
        requestinterceptors:
          - com.example.FooRequestInterceptor
        # 是否对404错误解码
        decode404: false
        encoder: com.example.SimpleEncoder   #编码器 
        decoder: com.example.SimpleDecoder   #解码器
        contract: com.example.SimpleContract #契约
```

