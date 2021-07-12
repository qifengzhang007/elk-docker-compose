###  elk-docker-compose

#### 前言
docker-compose.yml 只为快速创建 `elasticsearch+logstash+kibana`  集成环境，主要为项目所产生的日志文件，提供顶级解决方案。  


#### 配置介绍

- elasticsearch 配置
```code   
# 配置文件目录 
 elasticsearch > config 
 # 如果服务器配置比较高，建议将 jvm.options 配置文件中的内存使用设置大一点，例如 默认为 1g，可以设置为 2g 
    -Xms1g
    -Xmx1g
    
```

- kibana 配置
> kibana 主要提供界面展示系统，他需要连接 elasticsearch 获取数据，默认配置使用即可，不需要修改.  
```code   

# 配置文件目录 , 可以在这里查询具体配置，默认即可
 kibana > config 
    
```

- logstash 配置
> logstash 可以分布在任何服务器，负责采集日志，向 elasticsearch 服务器发送日志.如果你的应用程序产生的日志是独立的服务器，那么就需要在每台应用服务器安装。  
```code   

# 配置文件目录 ,
 logstash > config 
          > pipeline   
          
  # 其中 config 目录主要配置 logstash 本身的参数
   1.  logstash > config  > jvm.options 可以限制内存使用 ，默认为 512M ,如果服务器配置高，可以设置为 1g  
     -Xms512m
     -Xmx512m
   2.  logstash > config  > logstash.yml 可以配置数据对接的 elasticsearch 服务器ip等参数，默认即可
   
   # 本配置项定义 logstash 需要采集的目标日志文件路径、名称以及发送到 elasticsearch 服务器时的文件名等，相对比较复杂。
   # 请参考我们提供的格式修改即可，这样是最简单的办法.  
   3.  logstash > pipeline  > logstash.conf 配置采集的日志对象处理逻辑，请参考默认的格式配置即可
```


#### 注意事项  
- 1.本仓库提供的是 elk 集成环境,如果是中大型项目,可能 logstash 分布在多台服务器，那么服务器只需要安装 elasticsearch+kibana 即可.  
- 2.请自行在 docker-compose.yml 文件屏蔽 logstash 相关项即可。
- 3.独立安装 logstash ,请屏蔽 elasticsearch+kibana  项即可。  
- 4.以上操作都只是基于我们提供的docker-compose.yml 文件，您进行合适的选择即可.  