# lecture 9 Databases on AWS & Git

- 1. SQS LAMBDA作业讲解
    - 代码光能运行是不够的，还要考虑exceptions, 工业生产中exceptions要在代码中解决
    - 写代码的建议，考量的几个点：（0:50）
        - 1.效率
        - 2.exception 在工业中，随处可见
- 2. Database Overview
    - o。overview
        - 
            
            ![https://api2.mubu.com/v3/document_image/a4c97b33-84aa-4c27-84e7-7afbd7ae5078-14086676.jpg](https://api2.mubu.com/v3/document_image/a4c97b33-84aa-4c27-84e7-7afbd7ae5078-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/73af280c-34e0-4856-ac03-a4ec02dffce2-14086676.jpg](https://api2.mubu.com/v3/document_image/73af280c-34e0-4856-ac03-a4ec02dffce2-14086676.jpg)
            
    - 1.non relational database
        - non relational database好处：1. schema less的，指表的definition，不是数据库里的schema. 只用建立collection或document就可以了，往里面塞row，塞document
            - 
                
                ![https://api2.mubu.com/v3/document_image/068dae09-1a53-447b-8b42-082901847a74-14086676.jpg](https://api2.mubu.com/v3/document_image/068dae09-1a53-447b-8b42-082901847a74-14086676.jpg)
                
            - 知识补充：So while a supposed Schema-less NoSQL data-store will in theory allow you to store any data you like (typically key value pairs, in a document) without prior knowledge of the keys, or data types, it will be pointless unless you have some mechanism to retrieve and use the data. 来源[https://stackoverflow.com/questions/15589184/what-does-being-schema-less-mean-for-a-nosql-database](https://stackoverflow.com/questions/15589184/what-does-being-schema-less-mean-for-a-nosql-database)
        - 2.flexible
        - 3. 减少数据的冗余，但并不一定会减少储存量
            - 在某一项里面有100个item，在DW 里面就要存储100次相应的信息（如姓名，年龄），而JSON只存一次
                
                ![https://api2.mubu.com/v3/document_image/4e602b68-dd44-41e4-8c89-b6778db529a6-14086676.jpg](https://api2.mubu.com/v3/document_image/4e602b68-dd44-41e4-8c89-b6778db529a6-14086676.jpg)
                
            - 由于JSON需要定义attributes , 如name，age等，就会增加储存量，DW定义好了，直接塞数据就行，所以JSON减少数据的冗余，但并不一定会减少储存量
    - 2. data warehousing
        - 为了BI，query方便
            
            ![https://api2.mubu.com/v3/document_image/0efd834b-e700-4810-99dc-0168f909332d-14086676.jpg](https://api2.mubu.com/v3/document_image/0efd834b-e700-4810-99dc-0168f909332d-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/bf2b1e06-39be-4ae1-9c06-d8933a79b206-14086676.jpg](https://api2.mubu.com/v3/document_image/bf2b1e06-39be-4ae1-9c06-d8933a79b206-14086676.jpg)
            
    - 3.Elasticache:
        - AWS 缓存，in-memory的而非disk based的， 提高web application performance。把一定时间内，不怎么变化的数据放在Elasticache caches 中，提高速率。
            
            ![https://api2.mubu.com/v3/document_image/6fab94ac-cf78-4c33-8bf5-38f97c91360c-14086676.jpg](https://api2.mubu.com/v3/document_image/6fab94ac-cf78-4c33-8bf5-38f97c91360c-14086676.jpg)
            
        - in-memory caching system, 例如，web top 5的销售产品，放在caching system里，可以不用到data system里去query耽误时间，caching system可以直接取出储存的结果。
- 2. RDS
    - 1.create RDS 及MySQL branch 连接RDS 实验
    - 2.什么是RDS？
        - Amazon Relational Database Service (RDS) is a managed SQL database service provided by Amazon Web Services (AWS). Amazon RDS supports an array of database engines to store and organize data. It also helps with relational database management tasks, such as data migration, backup, recovery and patching.
        - RDS就是一个管理SQL数据库的一个AWS服务，不用去管maintain。
            
            ![https://api2.mubu.com/v3/document_image/c8c7fb1e-3f6f-4327-85ba-69e7d52118a4-14086676.jpg](https://api2.mubu.com/v3/document_image/c8c7fb1e-3f6f-4327-85ba-69e7d52118a4-14086676.jpg)
            
    - 3. backup
        - 数据自动backup，可以Multi-AZ deployment ，放在多个AZ中备份，防止数据丢失。
            - 
                
                ![https://api2.mubu.com/v3/document_image/39c189d2-a589-49e2-a505-2ed1c94fec1b-14086676.jpg](https://api2.mubu.com/v3/document_image/39c189d2-a589-49e2-a505-2ed1c94fec1b-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/3a3f6374-9fc1-4c54-b962-90cadff65141-14086676.jpg](https://api2.mubu.com/v3/document_image/3a3f6374-9fc1-4c54-b962-90cadff65141-14086676.jpg)
                
    - 4. Snapshot，在删掉 RDS instance后不会像Auto backup一样被删掉，会产生一定的费用。
        - 
            
            ![https://api2.mubu.com/v3/document_image/f9c26c64-725c-488e-ad5b-185017f83e83-14086676.jpg](https://api2.mubu.com/v3/document_image/f9c26c64-725c-488e-ad5b-185017f83e83-14086676.jpg)
            
    - 5. Encryption(面试很多人会问)
        - 有两种加密方式
            - 1.数据传输中加密
            - 2.数据存储时加密
                - KMS 服务进行加密
                    
                    ![https://api2.mubu.com/v3/document_image/dbc1cb58-1394-490e-96de-e28c08e01bcc-14086676.jpg](https://api2.mubu.com/v3/document_image/dbc1cb58-1394-490e-96de-e28c08e01bcc-14086676.jpg)
                    
                    ![https://api2.mubu.com/v3/document_image/c0189889-d783-42f6-8557-e07a6da6c398-14086676.jpg](https://api2.mubu.com/v3/document_image/c0189889-d783-42f6-8557-e07a6da6c398-14086676.jpg)
                    
    - 6.Restoring Backups
        - restore 后所有的数据库都会指向新的endpoint , 企业中会把Endpoint 变成一个DNS（一个AWS 服务），新的endpoint通过DNS使得application或者程序每次访问的database 都是一个unique name
            
            ![https://api2.mubu.com/v3/document_image/d948cd9e-8ec7-4002-8a33-3ad70a886011-14086676.jpg](https://api2.mubu.com/v3/document_image/d948cd9e-8ec7-4002-8a33-3ad70a886011-14086676.jpg)
            
    - 7.RDS-multi-az
        - 数据库 deploy到不同的AZ里，主要用于防止disaster recovery.
            
            ![https://api2.mubu.com/v3/document_image/36470e1b-c7d6-4451-afe3-19086c5f6829-14086676.jpg](https://api2.mubu.com/v3/document_image/36470e1b-c7d6-4451-afe3-19086c5f6829-14086676.jpg)
            
        - 
            
            ![https://api2.mubu.com/v3/document_image/b7ef29a0-8586-4a7d-9ab7-b926946894ed-14086676.jpg](https://api2.mubu.com/v3/document_image/b7ef29a0-8586-4a7d-9ab7-b926946894ed-14086676.jpg)
            
    - 8. RDS-read - replicas
        - 用于提高效率，允许read ONLY的database
            
            ![https://api2.mubu.com/v3/document_image/7a0e06ee-e590-4c77-88bb-0e11696d3d89-14086676.jpg](https://api2.mubu.com/v3/document_image/7a0e06ee-e590-4c77-88bb-0e11696d3d89-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/1c994a06-b9a0-4eac-b09b-b211b8d80f19-14086676.jpg](https://api2.mubu.com/v3/document_image/1c994a06-b9a0-4eac-b09b-b211b8d80f19-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/0fb2090b-c6fb-4457-beda-1adb6a4a3cd5-14086676.jpg](https://api2.mubu.com/v3/document_image/0fb2090b-c6fb-4457-beda-1adb6a4a3cd5-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/9e8df79d-fe34-491f-800f-978c0a6978be-14086676.jpg](https://api2.mubu.com/v3/document_image/9e8df79d-fe34-491f-800f-978c0a6978be-14086676.jpg)
            
        - 比较
            
            ![https://api2.mubu.com/v3/document_image/76c36c78-f846-440a-9549-42f0eece5d68-14086676.jpg](https://api2.mubu.com/v3/document_image/76c36c78-f846-440a-9549-42f0eece5d68-14086676.jpg)
            
    - 9. RDS structure
        - 每个instance都有一个endpoint, master database 和standby database 都有自己的volume 自己的磁盘，synchronous 同步，replicas 可以在相同的AZ也可以在不同的AZ 。
            
            ![https://api2.mubu.com/v3/document_image/3831148f-8710-442f-ab7c-19d7e822c4d5-14086676.jpg](https://api2.mubu.com/v3/document_image/3831148f-8710-442f-ab7c-19d7e822c4d5-14086676.jpg)
            
        - backup 有一个daily snapshot 和transaction log（会记录backup的情况）
        - read replica 可以有自己的replica， 它是asynchronous的，可能会有small latency
- 3. DynamoDB
    - 1. 什么是DynamoDB？
        - dynamoDB 是NoSQL database 不同于RDS SQL database，相比于relational database 速度很快，因为不需要maintain 很多relationship，内部存储速度快的特性，可以让数据读写速度很快。
            
            ![https://api2.mubu.com/v3/document_image/6c437208-99b4-4c0f-9c88-6c2c9dd6860d-14086676.jpg](https://api2.mubu.com/v3/document_image/6c437208-99b4-4c0f-9c88-6c2c9dd6860d-14086676.jpg)
            
        - Nosql database 多应用与IOT，web ， application 这种读写速度需要很快的场景中。
        - 可以存configuration，存log
    - 2. 优点
        - Schemaless
        - 在三个不同的AZ中备份
            
            ![https://api2.mubu.com/v3/document_image/06e6392c-d8f9-4ccc-a172-3d4d3ac65a16-14086676.jpg](https://api2.mubu.com/v3/document_image/06e6392c-d8f9-4ccc-a172-3d4d3ac65a16-14086676.jpg)
            
        - 两种consistent read.
            - 1.Eventual consistent reads(default), 快速拿到结果，不用等到所有的copy的数据都更新
                - 
            - 2.strongly consistent reads, 要确保之前的操作所有copy的数据都apply了，才会拿到数据。
                
                ![https://api2.mubu.com/v3/document_image/9c49f3ff-4733-40b4-aab8-bc36a83adc4b-14086676.jpg](https://api2.mubu.com/v3/document_image/9c49f3ff-4733-40b4-aab8-bc36a83adc4b-14086676.jpg)
                
            - 3.新的版本还有 transaction consistent read/write
            - 作业：3种 consistent reads 在什么情况下工作的？
                - 不同部门数据不互相影响时，用eventual consistent, A 的操作不会B 的正常使用。
                - 所有数据都是联动的时候并且要保证准确性的时候，用strong consistent reads ，如 电商平台，存货数量不能在其它节点没有更新完的时候提供给user，不然很可能会造成错误的存货数量，让user以为还有货，结果下单却不能发货。答案来源： [https://dynobase.dev/dynamodb-read-consistency/](https://dynobase.dev/dynamodb-read-consistency/)
                    
                    ![https://api2.mubu.com/v3/document_image/a396821d-680e-4004-87e3-bb2fd55c4b53-14086676.jpg](https://api2.mubu.com/v3/document_image/a396821d-680e-4004-87e3-bb2fd55c4b53-14086676.jpg)
                    
                    ![https://api2.mubu.com/v3/document_image/8bf6a187-f3c7-4a63-b961-04196e20a0bd-14086676.jpg](https://api2.mubu.com/v3/document_image/8bf6a187-f3c7-4a63-b961-04196e20a0bd-14086676.jpg)
                    
        - 强制加密，安全性高
        - 数据NoSQL存储是 semi-structure data
        - 所有的数据都是存在SSD中的，速度快
    - 操作
        - partition key 是primary key的一部分，hash value。如果只用了partition key，那primary key就是partition key。 如果命名了Sort key，那这两个组合成primary key.
            
            ![https://api2.mubu.com/v3/document_image/5449d97d-5ee1-4463-9366-8288846bf864-14086676.jpg](https://api2.mubu.com/v3/document_image/5449d97d-5ee1-4463-9366-8288846bf864-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/5a12e177-2f20-4608-9bdf-7b9cc91c022a-14086676.jpg](https://api2.mubu.com/v3/document_image/5a12e177-2f20-4608-9bdf-7b9cc91c022a-14086676.jpg)
            
        - table 中Item的格式不是固定的，可以以任意形式储存，这就是schemaless。
        - 计算收费
            
            ![https://api2.mubu.com/v3/document_image/b57ff065-402b-44f3-97f8-2e0e1aed2a76-14086676.jpg](https://api2.mubu.com/v3/document_image/b57ff065-402b-44f3-97f8-2e0e1aed2a76-14086676.jpg)
            
        - provisioned：auto scaling。 On-demand，用多少，交多少钱
            
            ![https://api2.mubu.com/v3/document_image/975db4b9-849c-4258-a31d-d5b93948011c-14086676.jpg](https://api2.mubu.com/v3/document_image/975db4b9-849c-4258-a31d-d5b93948011c-14086676.jpg)
            
        - encryption 可以由Amazon加密，也可以由自己加密
            
            ![https://api2.mubu.com/v3/document_image/bde72fd5-03d0-4d22-b347-25c7f018b4cf-14086676.jpg](https://api2.mubu.com/v3/document_image/bde72fd5-03d0-4d22-b347-25c7f018b4cf-14086676.jpg)
            
        - scan: scan整个table。Query：只选特定的数据。在以后项目尽量用query
            
            ![https://api2.mubu.com/v3/document_image/34f43c00-a974-47f8-9cd5-cb5933c81c07-14086676.jpg](https://api2.mubu.com/v3/document_image/34f43c00-a974-47f8-9cd5-cb5933c81c07-14086676.jpg)
            
        - create item, new attribute
            - 可加减attribute，这就是schemaless，不是固定死了的。
                
                ![https://api2.mubu.com/v3/document_image/572c7cda-4a70-429d-8cc0-456c5308f200-14086676.jpg](https://api2.mubu.com/v3/document_image/572c7cda-4a70-429d-8cc0-456c5308f200-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/daac60bd-b6c0-4d04-9184-cf9a20493c09-14086676.jpg](https://api2.mubu.com/v3/document_image/daac60bd-b6c0-4d04-9184-cf9a20493c09-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/d36c79c9-1197-4685-a131-ff9682d8b934-14086676.jpg](https://api2.mubu.com/v3/document_image/d36c79c9-1197-4685-a131-ff9682d8b934-14086676.jpg)
                
- 4. RedShift
    - OLAP 数据库
        - 
            
            ![https://api2.mubu.com/v3/document_image/45337b2d-0a28-4c68-a065-7e6b53effeb4-14086676.jpg](https://api2.mubu.com/v3/document_image/45337b2d-0a28-4c68-a065-7e6b53effeb4-14086676.jpg)
            
    - configuration
        - 分布式计算
            
            ![https://api2.mubu.com/v3/document_image/2beaa988-3249-43ef-9745-7687b26c70af-14086676.jpg](https://api2.mubu.com/v3/document_image/2beaa988-3249-43ef-9745-7687b26c70af-14086676.jpg)
            
        - Leader Node - distribute 计算的一种方式
            
            ![https://api2.mubu.com/v3/document_image/92a10e2d-e447-4d9f-bf24-25ba067e8f52-14086676.jpg](https://api2.mubu.com/v3/document_image/92a10e2d-e447-4d9f-bf24-25ba067e8f52-14086676.jpg)
            
    - RedShift快的原因
        - 1.按列存储数据，不同于传统的OLTP数据库用行储存数据
            - 传统按行储存
                - 
                    
                    ![https://api2.mubu.com/v3/document_image/5c2c6434-d62c-4856-bc34-42773354e673-14086676.jpg](https://api2.mubu.com/v3/document_image/5c2c6434-d62c-4856-bc34-42773354e673-14086676.jpg)
                    
                    ![https://api2.mubu.com/v3/document_image/74ec5b21-f389-4add-b233-df45b2d733f4-14086676.jpg](https://api2.mubu.com/v3/document_image/74ec5b21-f389-4add-b233-df45b2d733f4-14086676.jpg)
                    
            - Redshift按列储存
                - 列数据存储可以减少一些IO的操作
                    
                    ![https://api2.mubu.com/v3/document_image/2e899631-b00d-43b6-a460-8ceb39d57451-14086676.jpg](https://api2.mubu.com/v3/document_image/2e899631-b00d-43b6-a460-8ceb39d57451-14086676.jpg)
                    
                - OLTP传统数据库是将数据分不同的列储存在不同的disk上的，而OLAP数据库一列储存在一个disk中。在进行数据分析例如sum操作时，OLTP需要去不同的disk里面取数据，而列存储就只要在一个disk储存，分析数据更快
                    
                    ![https://api2.mubu.com/v3/document_image/470a43c4-6860-48c4-86d4-1ca3b096b903-14086676.jpg](https://api2.mubu.com/v3/document_image/470a43c4-6860-48c4-86d4-1ca3b096b903-14086676.jpg)
                    
        - 2.Advanced Compression
            - 压缩按列压缩，都是同一类型的数据，压缩储存会更快。不像行储存，需要对不同的数据类型进行压缩。
                
                ![https://api2.mubu.com/v3/document_image/66c009cf-0998-4b48-bd48-410fa51e16ca-14086676.jpg](https://api2.mubu.com/v3/document_image/66c009cf-0998-4b48-bd48-410fa51e16ca-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/3bc190ca-2c7f-41d8-9b37-beacc0f54b4d-14086676.jpg](https://api2.mubu.com/v3/document_image/3bc190ca-2c7f-41d8-9b37-beacc0f54b4d-14086676.jpg)
                
        - 3.sort Key 排序，排序的时间复杂度会更低。
            - 
                
                ![https://api2.mubu.com/v3/document_image/c8de9964-0f03-4d79-96f3-2c73e77a6376-14086676.jpg](https://api2.mubu.com/v3/document_image/c8de9964-0f03-4d79-96f3-2c73e77a6376-14086676.jpg)
                
        - 4.distribute Key
            - 根据key来做distribution, 例如，根据partition key做distribution。
                
                ![https://api2.mubu.com/v3/document_image/72264171-645a-43a7-97a6-9682d308e5cb-14086676.jpg](https://api2.mubu.com/v3/document_image/72264171-645a-43a7-97a6-9682d308e5cb-14086676.jpg)
                
            - 优点：
                - 1.不用SCAN 全部的disks，例如0开头和1开头的PK在disk1中就不用扫后面的disk。
                - 2.可以采用even distribution, 平均分disk
                    - 效率更高，更快
                        
                        ![https://api2.mubu.com/v3/document_image/27650fef-1992-4b49-9f46-4048fab41e17-14086676.jpg](https://api2.mubu.com/v3/document_image/27650fef-1992-4b49-9f46-4048fab41e17-14086676.jpg)
                        
                - 3.可以采用replication distribution
                    - 每个node中有复制一个Dimension table， fact 不用cross node花时间去join，牺牲空间换取时间。
                        
                        ![https://api2.mubu.com/v3/document_image/6d9e227d-bde9-4345-82c1-07885db0475e-14086676.jpg](https://api2.mubu.com/v3/document_image/6d9e227d-bde9-4345-82c1-07885db0475e-14086676.jpg)
                        
        - 5. 并行计算
            - 
                
                ![https://api2.mubu.com/v3/document_image/e677b956-f001-46e6-bbb6-5e25774f856f-14086676.jpg](https://api2.mubu.com/v3/document_image/e677b956-f001-46e6-bbb6-5e25774f856f-14086676.jpg)
                
    - pricing
        - 
            
            ![https://api2.mubu.com/v3/document_image/e1b9bd7a-2551-4031-b4fd-dff8848ce3f0-14086676.jpg](https://api2.mubu.com/v3/document_image/e1b9bd7a-2551-4031-b4fd-dff8848ce3f0-14086676.jpg)
            
    - security
        - 主要体现在加密上
            
            ![https://api2.mubu.com/v3/document_image/04315e67-5b4a-45c6-b88e-dd34d9c62e6a-14086676.jpg](https://api2.mubu.com/v3/document_image/04315e67-5b4a-45c6-b88e-dd34d9c62e6a-14086676.jpg)
            
    - Availability
        - 建立在单个AZ中
            
            ![https://api2.mubu.com/v3/document_image/ecd15f45-c235-4f5a-961e-de0236c884c5-14086676.jpg](https://api2.mubu.com/v3/document_image/ecd15f45-c235-4f5a-961e-de0236c884c5-14086676.jpg)
            
- 5. Elasticache
    - 1. 什么是Elasticache
        - 
            
            ![https://api2.mubu.com/v3/document_image/9e55de3d-d428-4a08-86d2-221a94243230-14086676.jpg](https://api2.mubu.com/v3/document_image/9e55de3d-d428-4a08-86d2-221a94243230-14086676.jpg)
            
    - 2. 主要是提高响应performance
    - recommendation 的引擎，减少query的时间
        - 
            
            ![https://api2.mubu.com/v3/document_image/95a70065-dbb7-4626-844a-2317e96701fc-14086676.jpg](https://api2.mubu.com/v3/document_image/95a70065-dbb7-4626-844a-2317e96701fc-14086676.jpg)
            
    - Types of Elasticache
        - Memcahed, 很容易做migration
            
            ![https://api2.mubu.com/v3/document_image/0a7d5103-adb6-47a0-ae90-4ade5a6fac5e-14086676.jpg](https://api2.mubu.com/v3/document_image/0a7d5103-adb6-47a0-ae90-4ade5a6fac5e-14086676.jpg)
            
        - Redis
            
            ![https://api2.mubu.com/v3/document_image/441d12f0-9c5d-4406-baff-c040a1484493-14086676.jpg](https://api2.mubu.com/v3/document_image/441d12f0-9c5d-4406-baff-c040a1484493-14086676.jpg)
            
    - 何时用Elasticache,何时用Redshift？
        - 数据分析速度要求不快，有时需要做OLAP，Redshift更好；数据分析要求快，数据不怎么变动的用Elasticache 更好。
            
            ![https://api2.mubu.com/v3/document_image/6241a6fe-a392-4d7e-aa84-92ffa1ca6c41-14086676.jpg](https://api2.mubu.com/v3/document_image/6241a6fe-a392-4d7e-aa84-92ffa1ca6c41-14086676.jpg)
            
- 6. Aurora
    - MySql 数据库，在其上面做了更改，但比传统MySQL效率会更高
        - 
            
            ![https://api2.mubu.com/v3/document_image/ba52f0ff-5574-43f5-85a8-9724d9772741-14086676.jpg](https://api2.mubu.com/v3/document_image/ba52f0ff-5574-43f5-85a8-9724d9772741-14086676.jpg)
            
    - Scaling
        - 数据非常可靠
            
            ![https://api2.mubu.com/v3/document_image/3c4b678a-b835-44c7-acf9-e674b1403325-14086676.jpg](https://api2.mubu.com/v3/document_image/3c4b678a-b835-44c7-acf9-e674b1403325-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/5321141e-3413-47af-b463-189dbba7ff59-14086676.jpg](https://api2.mubu.com/v3/document_image/5321141e-3413-47af-b463-189dbba7ff59-14086676.jpg)
            
    - 有15个 replicas
        - Replicas
            
            ![https://api2.mubu.com/v3/document_image/e2ee6784-65c7-4dd2-9a20-afcebb2b8a17-14086676.jpg](https://api2.mubu.com/v3/document_image/e2ee6784-65c7-4dd2-9a20-afcebb2b8a17-14086676.jpg)
            
        - 有15个不同的等级，如果main database挂了，直接用tier-0的replica promote成main database
            - 
                
                ![https://api2.mubu.com/v3/document_image/1b2fb607-f468-4588-bfe2-8310edf5dc06-14086676.jpg](https://api2.mubu.com/v3/document_image/1b2fb607-f468-4588-bfe2-8310edf5dc06-14086676.jpg)
                
    - 运行资源可选有弹性
        - 
            
            ![https://api2.mubu.com/v3/document_image/5326d572-7015-4867-89bc-c84a439cc5b3-14086676.jpg](https://api2.mubu.com/v3/document_image/5326d572-7015-4867-89bc-c84a439cc5b3-14086676.jpg)
            
    - Aurora Structure （与RDS的区别）
        - 1.通过endpoint 来决定是只能读，还是读写都可以。read和write的endpoint是可以分开的。
            
            ![https://api2.mubu.com/v3/document_image/6d5a9541-5dd9-4829-bfaa-878d80af629d-14086676.jpg](https://api2.mubu.com/v3/document_image/6d5a9541-5dd9-4829-bfaa-878d80af629d-14086676.jpg)
            
        - 2.每个不同的data copies 不基于comput resource的，不是通过comput resource挂接起来的，能够独立存在，不同的AZ的人读到的6个 data copies都是最新的（这是与RDS的区别）
        - 3.同过transaction log缩短wait的时间
            - user wait的时间大大缩短
                
                ![https://api2.mubu.com/v3/document_image/49296f3c-7304-48a9-8968-1e33859edbf8-14086676.jpg](https://api2.mubu.com/v3/document_image/49296f3c-7304-48a9-8968-1e33859edbf8-14086676.jpg)
                
            - disk 访问也是一样（灰色小人）
                
                ![https://api2.mubu.com/v3/document_image/0f4c29f8-0aba-4d6c-b01a-6f2df45665dc-14086676.jpg](https://api2.mubu.com/v3/document_image/0f4c29f8-0aba-4d6c-b01a-6f2df45665dc-14086676.jpg)
                
            - 到底什么时候apply transaction log由AWS快
- Disaster Recorvery
    - 3个概念
        - 
            
            ![https://api2.mubu.com/v3/document_image/2fbdfc8f-ba8b-4226-ab77-740f47350852-14086676.jpg](https://api2.mubu.com/v3/document_image/2fbdfc8f-ba8b-4226-ab77-740f47350852-14086676.jpg)
            
        - 模型图
            
            ![https://api2.mubu.com/v3/document_image/e312f722-ae19-4eba-93cf-1670e339c536-14086676.jpg](https://api2.mubu.com/v3/document_image/e312f722-ae19-4eba-93cf-1670e339c536-14086676.jpg)
            
        - RPO
        - RTO： downtime
        - Transaction Log: sequencial 的record，记录了所有的database的一些改变，例如upgrade，insert等等