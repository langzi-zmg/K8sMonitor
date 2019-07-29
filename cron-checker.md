# 定期检测
自定义监控项目，开发或业务人员可以自由添加需要监控的对象，设置检测指标以及报警对象。

## 概念
* 任务(task)  
用户自定义任务，执行指定类型任务，并拉取返回数据。

* 断言(assertion)  
用户定义的断言，根据用户任务返回数据，执行用户定义的数据校验。  
如API任务返回的status为200，则通过断言，否则失败。

* 变量(variable)  
通过任务的返回数据声明变量，在下一次任务中可以使用。

## 示例
访问[后台](https://juicy.wallstreetcn.com/sre/apitest/create)创建检测任务，以检测wallstreetcn.com主页为例，确认http返回码为200。

![cron-image](monitor/cron-checker.jpg)

### 字段解释
1. API检测字段  
    * 名称  
    检测项目名称
    * 描述  
    描述
    * cron  
    检测的周期，使用cron语法，详情可参考[cron.guru](http://crontab.guru)
1. 检测任务
    * 名称  
    任务名称，如http请求wscn首页
    * 断言  
    添加对任务执行结果的确认，此示例中校验header与status code
        * source  
        数据源，在任务类型为http时，source可用值为header,status,body
        * key  
        若source为header时，key为header名，通过key取出数据源的指定字段。  
        若source为body时，key为body字段名。
        * operator  
        断言操作符
        * expected  
        期望值
        * source_encoding  
        数据源的编码类型，当数据源为body，目前只支持JSON编码，可以将json body解析，便于之后字段选取。
    * 变量  
    声明变量，下一个任务可以获取改值，如一些场景测试，如任务A: 拉取首页信息流，任务B: 访问首页信息流中第一篇内容。
        * source  
        数据源，在任务类型为http时，source可用值为header,status,body
        * key  
        若source为header时，key为header名，通过key取出数据源的指定字段。  
        若source为body时，key为body字段名。
        * source_encoding  
        数据源的编码类型，当数据源为body，目前只支持JSON编码，可以将json body解析，便于之后字段选取。
