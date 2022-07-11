# Lecture 16 Big Data

- 1. Big Data Concept
    - 1.概念层
        - 1.最底层，distribute file system. HBase 现在用的特别少，剔除掉了，用的是HDFS. 底层文件要么是raw要么是parquet文件，用parquet 储存是比较好的。
            
            ![https://api2.mubu.com/v3/document_image/f186f005-78e1-4c47-a837-eec9c1a9bbf3-14086676.jpg](https://api2.mubu.com/v3/document_image/f186f005-78e1-4c47-a837-eec9c1a9bbf3-14086676.jpg)
            
        - 2. 第二层，资源管理层，Yarn控制query优先级
        - 3. 第三层，计算核心层。原生的spark core 完全基于内存的，快但贵，Hadoop MapReduce是基于硬盘的，IO 比较小。两项技术基本混合应用，business department用简单的selection可以Hadoop
        - 4. 第四层，service APIs。spark streaming
            - 1. spark SQL 和Hive 是hybrid的状态，这两个混着用
                
                ![https://api2.mubu.com/v3/document_image/27846669-c6c9-40aa-b298-39f7948770bb-14086676.jpg](https://api2.mubu.com/v3/document_image/27846669-c6c9-40aa-b298-39f7948770bb-14086676.jpg)
                
            - 2. 有了Hive 才好用SQL。首先需要一个储存，然后模拟SQL，将SQL转化成底层文件可以识别的语言，与DW的SQL是不一样的，DW是有专利的。
    - 2. HDFS (重要！）
        - 1. 3个major components
            - 1. Name node
                - 信息先进入到name node中，告诉去哪里, 相当于系统里的大脑，有文件系统处理的能力，例如open，close，rename，还能决定mapping of blocks。name node 坏了就麻烦了，找不到了。
                    
                    ![https://api2.mubu.com/v3/document_image/4f27a6a5-07d7-4e50-8984-4fe2e9f31919-14086676.jpg](https://api2.mubu.com/v3/document_image/4f27a6a5-07d7-4e50-8984-4fe2e9f31919-14086676.jpg)
                    
            - 2. data node
                - 执行，实际的操作（creation，deletion, replication ) 由data node来做
                - 相当于人的手和脚
            - 3. blocks
                - 逻辑上的存在，它决定了辅助文件的储存和读取的具体效率是怎么样的，在系统查阅的连续性，例如514MB的文件分成如下图，多出2MB，这就是small file，small file会影响hive。
                    
                    ![https://api2.mubu.com/v3/document_image/d953aaae-5de8-453d-8465-011fbb31b455-14086676.jpg](https://api2.mubu.com/v3/document_image/d953aaae-5de8-453d-8465-011fbb31b455-14086676.jpg)
                    
                - 最小的逻辑储存单元，一个文件尽量储存成128MB，by default 128MB 和256MB是最受欢迎的储存，分成5个blocks，尽量把每个block用满，小文件越多，meta block就越多，当meta block 占满后，就会系统死掉，尽量把储存的文件调整成大文件，不要用小文件
        - 2. HDFS 架构
            - 中心化，弊端是，一旦Namecode 蹦了，整个系统就蹦了
                
                ![https://api2.mubu.com/v3/document_image/f36ee334-4579-49aa-bcdd-701370cf946f-14086676.jpg](https://api2.mubu.com/v3/document_image/f36ee334-4579-49aa-bcdd-701370cf946f-14086676.jpg)
                
    - 3. Yarn
        - 1. 一个task manager and scheduling manager。客户发送一个请求query，都会被发送到Resource manager （Yarn）
            - 不是一个必须要的component
                
                ![https://api2.mubu.com/v3/document_image/c10cb396-3289-4ef4-adba-3cab17ac4d04-14086676.jpg](https://api2.mubu.com/v3/document_image/c10cb396-3289-4ef4-adba-3cab17ac4d04-14086676.jpg)
                
        - 2. 三种分配方式
            - 0.
                
                ![https://api2.mubu.com/v3/document_image/54dfacb6-588e-4333-b817-ef7d21f86d0b-14086676.jpg](https://api2.mubu.com/v3/document_image/54dfacb6-588e-4333-b817-ef7d21f86d0b-14086676.jpg)
                
            - 1. FIFO，先处理优先级最高的queue
            - 2.Capacity Scheduler。系统determine大的processing和小的processing，分配的资源不同。根据系统分配的资源来决定跑的次序，工业中用的比较多
            - 3. Fair Scheduler。 同时处理，所有的process一起跑，哪个跑完了就让出空间。大部分场景用的很少，不科学。
    - 4. Hive metastore
        - 1. hive 可以理解成Fake DW ,通过hive实现某些data warehouse的操作.
            
            ![https://api2.mubu.com/v3/document_image/4b4c52ab-30da-48ef-ae8b-e8741a31c37e-14086676.jpg](https://api2.mubu.com/v3/document_image/4b4c52ab-30da-48ef-ae8b-e8741a31c37e-14086676.jpg)
            
            - 通过hive 以ANSI SQL的方式处理HDFS 以列储存的parquet文件
                
                ![https://api2.mubu.com/v3/document_image/fb17d945-5c4e-496a-a643-315f9dc9115c-14086676.jpg](https://api2.mubu.com/v3/document_image/fb17d945-5c4e-496a-a643-315f9dc9115c-14086676.jpg)
                
            - hive 只能做到insert，和datawarehouse 是不一样的， 做不到delete等操作。
            - 有table也有view， hive table/view 也只是逻辑上的存在
            - Hive 建起来的目的是给non-technique 的人使用的，通过interface来连接底层的HDFS 信息。
        - 2.可以用不同的database system ，包括MySql database
        - 3. Hive Internal Table VS External Table
            - 0.
                
                ![https://api2.mubu.com/v3/document_image/a3f37889-5eca-4389-b0c7-2d78eeb69cb2-14086676.jpg](https://api2.mubu.com/v3/document_image/a3f37889-5eca-4389-b0c7-2d78eeb69cb2-14086676.jpg)
                
            - Internal table 是default table in Hive.
                - By default, an internal table will be created in a folder path similar to /user/hive/warehouse directory of HDFS.
                - 如果外面drop the internal table or partition, 与那个table相关的 table data and metadata 将会在HDFS中被删除
            - External Table 与Internal Table最大的不一样是： External Table是outside the Hive的users 使用的Table， stored outside the warehouse directory.
                - 能够access data stored in sources such as remote HDFS locations or Azure storage volumes.
                - 用在建data pipeline中
                - External table 是由system ID 来跑的
- 2. Big Data Case Study1 （00：50）
    - 1. 环境（GCP，Intellij, Spark)
        - 前期把components 安装完毕
            
            ![https://api2.mubu.com/v3/document_image/48d92f92-a5a0-43b3-a677-8bded4d7979c-14086676.jpg](https://api2.mubu.com/v3/document_image/48d92f92-a5a0-43b3-a677-8bded4d7979c-14086676.jpg)
            
        - Mac 就不用安装WSL了
            
            ![https://api2.mubu.com/v3/document_image/92e2b404-c5b3-4045-8157-8b9e65040dc3-14086676.jpg](https://api2.mubu.com/v3/document_image/92e2b404-c5b3-4045-8157-8b9e65040dc3-14086676.jpg)
            
        - 安装完成后，启动服务
            
            ![https://api2.mubu.com/v3/document_image/ec09520c-8eff-4083-8390-0806e3098c30-14086676.jpg](https://api2.mubu.com/v3/document_image/ec09520c-8eff-4083-8390-0806e3098c30-14086676.jpg)
            
        - 实验注重理解框架，不用太在意代码
            
            ![https://api2.mubu.com/v3/document_image/6cf19a2d-2899-454c-bb5d-4603e8d2e218-14086676.jpg](https://api2.mubu.com/v3/document_image/6cf19a2d-2899-454c-bb5d-4603e8d2e218-14086676.jpg)