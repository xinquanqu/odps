# PyODPS条件查询 {#task_1545721 .task}

本文为您介绍如何使用PyODPS进行条件查询。

请提前开通MaxCompute和DataWorks服务。本例使用DataWorks简单模式。

1.  准备测试数据。 
    1.  单击[此处](http://t.cn/Rf8GeUq)下载鸢尾花数据集iris.data。
    2.  登录Dataworks控制台，以**DDL模式**创建表pyodps\_iris。![DDL模式](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1227015/156498942754311_zh-CN.jpg)


    3.  单击**提交到生产环境**。![提交到生产环境](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1227015/156498942854313_zh-CN.jpg)


    4.  将iris.csv中的数据导入到表pyodps.iris。![数据导入](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1227015/156498942854317_zh-CN.jpg)


2.  新建PyODPS节点，并将节点命名为PyODPS条件查询。![新建节点](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1227015/156498942954319_zh-CN.jpg)

 代码如下。

    ``` {#codeblock_6u9_7uu_woy}
    import sys
    reload(sys)
    #修改系统默认编码。
    sys.setdefaultencoding('utf8')
    
    iris = DataFrame(o.get_table('pyodps_iris'))
    #方法一：使用条件方式输出。
    with o.execute_sql('select * from pyodps_iris WHERE sepallength > 5 ').open_reader() as reader4:
        print reader4.raw
        for record in reader4:
            print record["sepallength"],record["sepalwidth"],record["petallength"],record["petalwidth"],record["name"]
    
    #方法二：使用ODPS的DataFrame的过滤条件得出数据结果。
    print iris[iris.sepallength > 5].head(5)
    
    #方法三：使用query的方式输出。
    print iris.query("(sepallength < 5) and (petallength > 1.5)").head(5)
    ```

3.  单击运行按钮。![单击运行按钮](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1227015/156498942954321_zh-CN.jpg)


4.  在**运行日志**中查看结果。 

    ``` {#codeblock_vft_174_8n6}
    Executing user script with PyODPS 0.8.0
    
    "sepallength","sepalwidth","petallength","petalwidth","name"
    5.1,3.5,1.4,0.2,"Iris-setosa"
    5.4,3.9,1.7,0.4,"Iris-setosa"
    5.4,3.7,1.5,0.2,"Iris-setosa"
    5.8,4.0,1.2,0.2,"Iris-setosa"
    5.7,4.4,1.5,0.4,"Iris-setosa"
    5.4,3.9,1.3,0.4,"Iris-setosa"
    5.1,3.5,1.4,0.3,"Iris-setosa"
    5.7,3.8,1.7,0.3,"Iris-setosa"
    5.1,3.8,1.5,0.3,"Iris-setosa"
    5.4,3.4,1.7,0.2,"Iris-setosa"
    5.1,3.7,1.5,0.4,"Iris-setosa"
    5.1,3.3,1.7,0.5,"Iris-setosa"
    5.2,3.5,1.5,0.2,"Iris-setosa"
    5.2,3.4,1.4,0.2,"Iris-setosa"
    5.4,3.4,1.5,0.4,"Iris-setosa"
    5.2,4.1,1.5,0.1,"Iris-setosa"
    5.5,4.2,1.4,0.2,"Iris-setosa"
    5.5,3.5,1.3,0.2,"Iris-setosa"
    5.1,3.4,1.5,0.2,"Iris-setosa"
    5.1,3.8,1.9,0.4,"Iris-setosa"
    5.1,3.8,1.6,0.2,"Iris-setosa"
    5.3,3.7,1.5,0.2,"Iris-setosa"
    7.0,3.2,4.7,1.4,"Iris-versicolor"
    6.4,3.2,4.5,1.5,"Iris-versicolor"
    6.9,3.1,4.9,1.5,"Iris-versicolor"
    5.5,2.3,4.0,1.3,"Iris-versicolor"
    6.5,2.8,4.6,1.5,"Iris-versicolor"
    5.7,2.8,4.5,1.3,"Iris-versicolor"
    6.3,3.3,4.7,1.6,"Iris-versicolor"
    6.6,2.9,4.6,1.3,"Iris-versicolor"
    5.2,2.7,3.9,1.4,"Iris-versicolor"
    5.9,3.0,4.2,1.5,"Iris-versicolor"
    6.0,2.2,4.0,1.0,"Iris-versicolor"
    6.1,2.9,4.7,1.4,"Iris-versicolor"
    5.6,2.9,3.6,1.3,"Iris-versicolor"
    6.7,3.1,4.4,1.4,"Iris-versicolor"
    5.6,3.0,4.5,1.5,"Iris-versicolor"
    5.8,2.7,4.1,1.0,"Iris-versicolor"
    6.2,2.2,4.5,1.5,"Iris-versicolor"
    5.6,2.5,3.9,1.1,"Iris-versicolor"
    5.9,3.2,4.8,1.8,"Iris-versicolor"
    6.1,2.8,4.0,1.3,"Iris-versicolor"
    6.3,2.5,4.9,1.5,"Iris-versicolor"
    6.1,2.8,4.7,1.2,"Iris-versicolor"
    6.4,2.9,4.3,1.3,"Iris-versicolor"
    6.6,3.0,4.4,1.4,"Iris-versicolor"
    6.8,2.8,4.8,1.4,"Iris-versicolor"
    6.7,3.0,5.0,1.7,"Iris-versicolor"
    6.0,2.9,4.5,1.5,"Iris-versicolor"
    5.7,2.6,3.5,1.0,"Iris-versicolor"
    5.5,2.4,3.8,1.1,"Iris-versicolor"
    5.5,2.4,3.7,1.0,"Iris-versicolor"
    5.8,2.7,3.9,1.2,"Iris-versicolor"
    6.0,2.7,5.1,1.6,"Iris-versicolor"
    5.4,3.0,4.5,1.5,"Iris-versicolor"
    6.0,3.4,4.5,1.6,"Iris-versicolor"
    6.7,3.1,4.7,1.5,"Iris-versicolor"
    6.3,2.3,4.4,1.3,"Iris-versicolor"
    5.6,3.0,4.1,1.3,"Iris-versicolor"
    5.5,2.5,4.0,1.3,"Iris-versicolor"
    5.5,2.6,4.4,1.2,"Iris-versicolor"
    6.1,3.0,4.6,1.4,"Iris-versicolor"
    5.8,2.6,4.0,1.2,"Iris-versicolor"
    5.6,2.7,4.2,1.3,"Iris-versicolor"
    5.7,3.0,4.2,1.2,"Iris-versicolor"
    5.7,2.9,4.2,1.3,"Iris-versicolor"
    6.2,2.9,4.3,1.3,"Iris-versicolor"
    5.1,2.5,3.0,1.1,"Iris-versicolor"
    5.7,2.8,4.1,1.3,"Iris-versicolor"
    6.3,3.3,6.0,2.5,"Iris-virginica"
    5.8,2.7,5.1,1.9,"Iris-virginica"
    7.1,3.0,5.9,2.1,"Iris-virginica"
    6.3,2.9,5.6,1.8,"Iris-virginica"
    6.5,3.0,5.8,2.2,"Iris-virginica"
    7.6,3.0,6.6,2.1,"Iris-virginica"
    7.3,2.9,6.3,1.8,"Iris-virginica"
    6.7,2.5,5.8,1.8,"Iris-virginica"
    7.2,3.6,6.1,2.5,"Iris-virginica"
    6.5,3.2,5.1,2.0,"Iris-virginica"
    6.4,2.7,5.3,1.9,"Iris-virginica"
    6.8,3.0,5.5,2.1,"Iris-virginica"
    5.7,2.5,5.0,2.0,"Iris-virginica"
    5.8,2.8,5.1,2.4,"Iris-virginica"
    6.4,3.2,5.3,2.3,"Iris-virginica"
    6.5,3.0,5.5,1.8,"Iris-virginica"
    7.7,3.8,6.7,2.2,"Iris-virginica"
    7.7,2.6,6.9,2.3,"Iris-virginica"
    6.0,2.2,5.0,1.5,"Iris-virginica"
    6.9,3.2,5.7,2.3,"Iris-virginica"
    5.6,2.8,4.9,2.0,"Iris-virginica"
    7.7,2.8,6.7,2.0,"Iris-virginica"
    6.3,2.7,4.9,1.8,"Iris-virginica"
    6.7,3.3,5.7,2.1,"Iris-virginica"
    7.2,3.2,6.0,1.8,"Iris-virginica"
    6.2,2.8,4.8,1.8,"Iris-virginica"
    6.1,3.0,4.9,1.8,"Iris-virginica"
    6.4,2.8,5.6,2.1,"Iris-virginica"
    7.2,3.0,5.8,1.6,"Iris-virginica"
    7.4,2.8,6.1,1.9,"Iris-virginica"
    7.9,3.8,6.4,2.0,"Iris-virginica"
    6.4,2.8,5.6,2.2,"Iris-virginica"
    6.3,2.8,5.1,1.5,"Iris-virginica"
    6.1,2.6,5.6,1.4,"Iris-virginica"
    7.7,3.0,6.1,2.3,"Iris-virginica"
    6.3,3.4,5.6,2.4,"Iris-virginica"
    6.4,3.1,5.5,1.8,"Iris-virginica"
    6.0,3.0,4.8,1.8,"Iris-virginica"
    6.9,3.1,5.4,2.1,"Iris-virginica"
    6.7,3.1,5.6,2.4,"Iris-virginica"
    6.9,3.1,5.1,2.3,"Iris-virginica"
    5.8,2.7,5.1,1.9,"Iris-virginica"
    6.8,3.2,5.9,2.3,"Iris-virginica"
    6.7,3.3,5.7,2.5,"Iris-virginica"
    6.7,3.0,5.2,2.3,"Iris-virginica"
    6.3,2.5,5.0,1.9,"Iris-virginica"
    6.5,3.0,5.2,2.0,"Iris-virginica"
    6.2,3.4,5.4,2.3,"Iris-virginica"
    5.9,3.0,5.1,1.8,"Iris-virginica"
    5.1 3.5 1.4 0.2 Iris-setosa
    5.4 3.9 1.7 0.4 Iris-setosa
    5.4 3.7 1.5 0.2 Iris-setosa
    5.8 4.0 1.2 0.2 Iris-setosa
    5.7 4.4 1.5 0.4 Iris-setosa
    5.4 3.9 1.3 0.4 Iris-setosa
    5.1 3.5 1.4 0.3 Iris-setosa
    5.7 3.8 1.7 0.3 Iris-setosa
    5.1 3.8 1.5 0.3 Iris-setosa
    5.4 3.4 1.7 0.2 Iris-setosa
    5.1 3.7 1.5 0.4 Iris-setosa
    5.1 3.3 1.7 0.5 Iris-setosa
    5.2 3.5 1.5 0.2 Iris-setosa
    5.2 3.4 1.4 0.2 Iris-setosa
    5.4 3.4 1.5 0.4 Iris-setosa
    5.2 4.1 1.5 0.1 Iris-setosa
    5.5 4.2 1.4 0.2 Iris-setosa
    5.5 3.5 1.3 0.2 Iris-setosa
    5.1 3.4 1.5 0.2 Iris-setosa
    5.1 3.8 1.9 0.4 Iris-setosa
    5.1 3.8 1.6 0.2 Iris-setosa
    5.3 3.7 1.5 0.2 Iris-setosa
    7.0 3.2 4.7 1.4 Iris-versicolor
    6.4 3.2 4.5 1.5 Iris-versicolor
    6.9 3.1 4.9 1.5 Iris-versicolor
    5.5 2.3 4.0 1.3 Iris-versicolor
    6.5 2.8 4.6 1.5 Iris-versicolor
    5.7 2.8 4.5 1.3 Iris-versicolor
    6.3 3.3 4.7 1.6 Iris-versicolor
    6.6 2.9 4.6 1.3 Iris-versicolor
    5.2 2.7 3.9 1.4 Iris-versicolor
    5.9 3.0 4.2 1.5 Iris-versicolor
    6.0 2.2 4.0 1.0 Iris-versicolor
    6.1 2.9 4.7 1.4 Iris-versicolor
    5.6 2.9 3.6 1.3 Iris-versicolor
    6.7 3.1 4.4 1.4 Iris-versicolor
    5.6 3.0 4.5 1.5 Iris-versicolor
    5.8 2.7 4.1 1.0 Iris-versicolor
    6.2 2.2 4.5 1.5 Iris-versicolor
    5.6 2.5 3.9 1.1 Iris-versicolor
    5.9 3.2 4.8 1.8 Iris-versicolor
    6.1 2.8 4.0 1.3 Iris-versicolor
    6.3 2.5 4.9 1.5 Iris-versicolor
    6.1 2.8 4.7 1.2 Iris-versicolor
    6.4 2.9 4.3 1.3 Iris-versicolor
    6.6 3.0 4.4 1.4 Iris-versicolor
    6.8 2.8 4.8 1.4 Iris-versicolor
    6.7 3.0 5.0 1.7 Iris-versicolor
    6.0 2.9 4.5 1.5 Iris-versicolor
    5.7 2.6 3.5 1.0 Iris-versicolor
    5.5 2.4 3.8 1.1 Iris-versicolor
    5.5 2.4 3.7 1.0 Iris-versicolor
    5.8 2.7 3.9 1.2 Iris-versicolor
    6.0 2.7 5.1 1.6 Iris-versicolor
    5.4 3.0 4.5 1.5 Iris-versicolor
    6.0 3.4 4.5 1.6 Iris-versicolor
    6.7 3.1 4.7 1.5 Iris-versicolor
    6.3 2.3 4.4 1.3 Iris-versicolor
    5.6 3.0 4.1 1.3 Iris-versicolor
    5.5 2.5 4.0 1.3 Iris-versicolor
    5.5 2.6 4.4 1.2 Iris-versicolor
    6.1 3.0 4.6 1.4 Iris-versicolor
    5.8 2.6 4.0 1.2 Iris-versicolor
    5.6 2.7 4.2 1.3 Iris-versicolor
    5.7 3.0 4.2 1.2 Iris-versicolor
    5.7 2.9 4.2 1.3 Iris-versicolor
    6.2 2.9 4.3 1.3 Iris-versicolor
    5.1 2.5 3.0 1.1 Iris-versicolor
    5.7 2.8 4.1 1.3 Iris-versicolor
    6.3 3.3 6.0 2.5 Iris-virginica
    5.8 2.7 5.1 1.9 Iris-virginica
    7.1 3.0 5.9 2.1 Iris-virginica
    6.3 2.9 5.6 1.8 Iris-virginica
    6.5 3.0 5.8 2.2 Iris-virginica
    7.6 3.0 6.6 2.1 Iris-virginica
    7.3 2.9 6.3 1.8 Iris-virginica
    6.7 2.5 5.8 1.8 Iris-virginica
    7.2 3.6 6.1 2.5 Iris-virginica
    6.5 3.2 5.1 2.0 Iris-virginica
    6.4 2.7 5.3 1.9 Iris-virginica
    6.8 3.0 5.5 2.1 Iris-virginica
    5.7 2.5 5.0 2.0 Iris-virginica
    5.8 2.8 5.1 2.4 Iris-virginica
    6.4 3.2 5.3 2.3 Iris-virginica
    6.5 3.0 5.5 1.8 Iris-virginica
    7.7 3.8 6.7 2.2 Iris-virginica
    7.7 2.6 6.9 2.3 Iris-virginica
    6.0 2.2 5.0 1.5 Iris-virginica
    6.9 3.2 5.7 2.3 Iris-virginica
    5.6 2.8 4.9 2.0 Iris-virginica
    7.7 2.8 6.7 2.0 Iris-virginica
    6.3 2.7 4.9 1.8 Iris-virginica
    6.7 3.3 5.7 2.1 Iris-virginica
    7.2 3.2 6.0 1.8 Iris-virginica
    6.2 2.8 4.8 1.8 Iris-virginica
    6.1 3.0 4.9 1.8 Iris-virginica
    6.4 2.8 5.6 2.1 Iris-virginica
    7.2 3.0 5.8 1.6 Iris-virginica
    7.4 2.8 6.1 1.9 Iris-virginica
    7.9 3.8 6.4 2.0 Iris-virginica
    6.4 2.8 5.6 2.2 Iris-virginica
    6.3 2.8 5.1 1.5 Iris-virginica
    6.1 2.6 5.6 1.4 Iris-virginica
    7.7 3.0 6.1 2.3 Iris-virginica
    6.3 3.4 5.6 2.4 Iris-virginica
    6.4 3.1 5.5 1.8 Iris-virginica
    6.0 3.0 4.8 1.8 Iris-virginica
    6.9 3.1 5.4 2.1 Iris-virginica
    6.7 3.1 5.6 2.4 Iris-virginica
    6.9 3.1 5.1 2.3 Iris-virginica
    5.8 2.7 5.1 1.9 Iris-virginica
    6.8 3.2 5.9 2.3 Iris-virginica
    6.7 3.3 5.7 2.5 Iris-virginica
    6.7 3.0 5.2 2.3 Iris-virginica
    6.3 2.5 5.0 1.9 Iris-virginica
    6.5 3.0 5.2 2.0 Iris-virginica
    6.2 3.4 5.4 2.3 Iris-virginica
    5.9 3.0 5.1 1.8 Iris-virginica
    Sql compiled:
    CREATE TABLE tmp_pyodps_xxxx LIFECYCLE 1 AS
    SELECT *
    FROM xxx.`pyodps_iris` t1
    WHERE t1.`sepallength` > 5
    Instance ID: 2019xxxx
      Log view: http://logview.odps.aliyun.com/logview/?h=http://service.cn.maxcompute.aliyun.com/api&p=xxxx&i=2019xxxx&token=xxxx
    
       sepallength  sepalwidth  petallength  petalwidth         name
    0          5.1         3.5          1.4         0.2  Iris-setosa
    1          5.4         3.9          1.7         0.4  Iris-setosa
    2          5.4         3.7          1.5         0.2  Iris-setosa
    3          5.8         4.0          1.2         0.2  Iris-setosa
    4          5.7         4.4          1.5         0.4  Iris-setosa
    Sql compiled:
    CREATE TABLE tmp_pyodps_xxxx LIFECYCLE 1 AS
    SELECT *
    FROM xxxx.`pyodps_iris` t1
    WHERE (t1.`sepallength` < 5) AND (t1.`petallength` > 1.5)
    Instance ID: 2019xxxx
      Log view: http://logview.odps.aliyun.com/logview/?h=http://service.cn.maxcompute.aliyun.com/api&p=xxxx&i=2019xxxx&token=xxxx
    
       sepallength  sepalwidth  petallength  petalwidth             name
    0          4.8         3.4          1.6         0.2      Iris-setosa
    1          4.8         3.4          1.9         0.2      Iris-setosa
    2          4.7         3.2          1.6         0.2      Iris-setosa
    3          4.8         3.1          1.6         0.2      Iris-setosa
    4          4.9         2.4          3.3         1.0  Iris-versicolor
    ```


