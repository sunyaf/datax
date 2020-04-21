## datax parquet hdfswriter

> 背景
> 为什么我要开发这个工具呢？我之前安装的cdh集群版本是5.14，里面的impala支持parquet,不支持orc，但是偏偏呀，datax不支持直接写到hdfs的parquet。虽说datax和impala同时还支持txt格式，但是查询速度比较慢，问了很多，见别人有开发datax parquet reader的，就是没有writer，于是就有了我这个datax parquet hdfswriter。

## 使用方式
**1、很简单，只需要将我的文件夹替换掉你的datax里面的hdfswriter文件夹即可
2、设置"fileType":"parquet",其他的参照datax 阿里官方即可**
## 例子
```bash
{
    "job":{
        "content":[
            {
                "writer":{
                    "parameter":{
                        "writeMode":"append",
                        "column":[
                            {
                                "type":"bigint",
                                "name":"user_id"
                            },
                            {
                                "type":"string",
                                "name":"mobile"
                            }
                        ],
                        "fieldDelimiter":" ",
                        "fileType":"parquet",
                        "hadoopConfig":{
                            "dfs.nameservices":"nameservice1",
                            "dfs.ha.namenodes.nameservice1":"namenode128,namenode113",
                            "dfs.client.failover.proxy.provider.nameservice1":"org.apache.hadoop.hdfs.server.namenode.ha.ConfiguredFailoverProxyProvider",
                            "dfs.namenode.rpc-address.nameservice1.namenode113":"*****:8020",
                            "dfs.namenode.rpc-address.nameservice1.namenode128":"*****:8020"
                        },
                        "fileName":"rw_user_login",
                        "path":"/user/hive/warehouse/ods_test.db/rw_user_login/20200420",
                        "defaultFS":"hdfs://nameservice1"
                    },
                    "name":"hdfswriter"
                },
                "reader":{
                    "parameter":{
                        "username":"bigdata",
                        "column":[
                            "user_id",
                            "mobile"
                        ],
                        "connection":[
                            {
                                "table":[
                                    "rw_user_login"
                                ],
                                "jdbcUrl":[
                                    "jdbc:mysql://********:3306/***?zeroDateTimeBehavior=convertToNull&useUnicode=true&characterEncoding=utf8"
                                ]
                            }
                        ],
                        "password":"****",
                        "splitPk":"user_id"
                    },
                    "name":"mysqlreader"
                }
            }
        ],
        "setting":{
            "speed":{
                "channel":8
            }
        }
    },
    "setting":{

    }
}
```
**有疑问可以入微信群咨询我，源码可以私下给你们，做二次开发**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200421174402880.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM0NzQ4NTY5,size_16,color_FFFFFF,t_70)

