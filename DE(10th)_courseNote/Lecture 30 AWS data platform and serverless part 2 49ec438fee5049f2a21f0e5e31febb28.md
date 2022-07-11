# Lecture 30 AWS data platform and serverless part 2 & snowpipe

- 1.serverless 操作复习
- 2. snowflake pipe
    - 1. 直接在snowflake中做data ingestion 类似data streaming
        - 
            
            ![https://api2.mubu.com/v3/document_image/40ac06bf-85e5-459b-92d8-241b620d4340-14086676.jpg](https://api2.mubu.com/v3/document_image/40ac06bf-85e5-459b-92d8-241b620d4340-14086676.jpg)
            
    - 2. snowpipe 代码讲解（00：37）
- 3. Kinesis
    - 1. 什么是kinesis
        - 每个shard
            
            ![https://api2.mubu.com/v3/document_image/f60a7c83-ffda-4260-81e8-dd5b0bd07aa8-14086676.jpg](https://api2.mubu.com/v3/document_image/f60a7c83-ffda-4260-81e8-dd5b0bd07aa8-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/2f60ab13-79e5-4d7b-94a7-89cd149a5374-14086676.jpg](https://api2.mubu.com/v3/document_image/2f60ab13-79e5-4d7b-94a7-89cd149a5374-14086676.jpg)
            
        - shard的容量就是data Steam容量
    - 2. 在建stream 的时候，很重要的是在建之前要想清楚stream的容量有多大。
        - 0
            
            ![https://api2.mubu.com/v3/document_image/1ba23932-309a-40e8-a44c-8ea07823d4d0-14086676.jpg](https://api2.mubu.com/v3/document_image/1ba23932-309a-40e8-a44c-8ea07823d4d0-14086676.jpg)
            
        - 1.需要知道多少个consumers
            
            ![https://api2.mubu.com/v3/document_image/eee1951e-1635-41c2-bc1f-3311a8833edb-14086676.jpg](https://api2.mubu.com/v3/document_image/eee1951e-1635-41c2-bc1f-3311a8833edb-14086676.jpg)
            
        - number of shards 很重要，通过取最大值
            
            ![https://api2.mubu.com/v3/document_image/45b0998f-2e9a-4f88-b024-ba9eecb20ff2-14086676.jpg](https://api2.mubu.com/v3/document_image/45b0998f-2e9a-4f88-b024-ba9eecb20ff2-14086676.jpg)
            
    - 3. 怎么创建kinesis, kinesis 能用什么？
        - 0
            
            ![https://api2.mubu.com/v3/document_image/c7884220-9edf-4ce0-9f25-78c86719424c-14086676.jpg](https://api2.mubu.com/v3/document_image/c7884220-9edf-4ce0-9f25-78c86719424c-14086676.jpg)
            
        - 1. firehose 直接将stream data 放到 AWS store中，例如S3
            
            ![https://api2.mubu.com/v3/document_image/ff275bca-7536-4ef3-8247-226136d02b81-14086676.jpg](https://api2.mubu.com/v3/document_image/ff275bca-7536-4ef3-8247-226136d02b81-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/e695cbcd-3792-4846-a4b5-56ca2b4402d0-14086676.jpg](https://api2.mubu.com/v3/document_image/e695cbcd-3792-4846-a4b5-56ca2b4402d0-14086676.jpg)
            
        - 2.
            
            ![https://api2.mubu.com/v3/document_image/a6d59f88-c2db-44b7-9f05-05de9b3005bc-14086676.jpg](https://api2.mubu.com/v3/document_image/a6d59f88-c2db-44b7-9f05-05de9b3005bc-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/c8a1ce18-85a5-42c2-903f-49b03edf00a0-14086676.jpg](https://api2.mubu.com/v3/document_image/c8a1ce18-85a5-42c2-903f-49b03edf00a0-14086676.jpg)
            
    - 4. kinesis 实验（2：00）
        - 0.收费不便宜，实验注意操作
- 4. Elastic MapReduce (EMR)
    - 对大数据做数据处理和分析
        
        ![https://api2.mubu.com/v3/document_image/f8ebdbbf-b672-4a22-8999-aa36027ed76e-14086676.jpg](https://api2.mubu.com/v3/document_image/f8ebdbbf-b672-4a22-8999-aa36027ed76e-14086676.jpg)
        
    - 还可以把data从database拿出来，分布式系统，速度快
    - masternode 管理，core node既存储数据又计算， task node 是option的，不存数据
        
        ![https://api2.mubu.com/v3/document_image/c26dc17f-f4f2-4edd-b879-b138b5acb840-14086676.jpg](https://api2.mubu.com/v3/document_image/c26dc17f-f4f2-4edd-b879-b138b5acb840-14086676.jpg)
        
        ![https://api2.mubu.com/v3/document_image/9322578e-1bca-4a11-81cc-beb0ed0d8502-14086676.jpg](https://api2.mubu.com/v3/document_image/9322578e-1bca-4a11-81cc-beb0ed0d8502-14086676.jpg)
        
- 5.Athena
    - 1. what is Athena
        - 交互查询式
            
            ![https://api2.mubu.com/v3/document_image/0871292a-9f81-4a6c-96bd-323e7612b8b3-14086676.jpg](https://api2.mubu.com/v3/document_image/0871292a-9f81-4a6c-96bd-323e7612b8b3-14086676.jpg)
            
        - 好处是可以直接在dataset上做query做数据分析，不需要做太多ETL处理
    - 2. Athena is serverless
        - 
            
            ![https://api2.mubu.com/v3/document_image/9409c592-51f1-4adb-9f75-ef09da0e61a2-14086676.jpg](https://api2.mubu.com/v3/document_image/9409c592-51f1-4adb-9f75-ef09da0e61a2-14086676.jpg)
            
    - 3. Pay per query
        - 可以通过压缩query提高query的performance来节省cost
            
            ![https://api2.mubu.com/v3/document_image/3cab7d0a-0cac-41e1-a466-a766e2f145e9-14086676.jpg](https://api2.mubu.com/v3/document_image/3cab7d0a-0cac-41e1-a466-a766e2f145e9-14086676.jpg)
            
    - 4. Open. powerful. standard
        - 
            
            ![https://api2.mubu.com/v3/document_image/3e5f8a22-2d5e-4e8c-8a24-460ed8b68e14-14086676.jpg](https://api2.mubu.com/v3/document_image/3e5f8a22-2d5e-4e8c-8a24-460ed8b68e14-14086676.jpg)
            
    - athena 的优点
        
        ![https://api2.mubu.com/v3/document_image/d3f94e8a-2aee-44fd-abff-49d594323daf-14086676.jpg](https://api2.mubu.com/v3/document_image/d3f94e8a-2aee-44fd-abff-49d594323daf-14086676.jpg)
        
- 6. Redshift Spectrum
    - 1. what is Redshift spectrum
        - 可以同时存取structure and semi-structure data from s3；multiple cluster 能query the same datasetl
            
            ![https://api2.mubu.com/v3/document_image/615bcd1a-ad91-44ec-a630-7a33c105624a-14086676.jpg](https://api2.mubu.com/v3/document_image/615bcd1a-ad91-44ec-a630-7a33c105624a-14086676.jpg)
            
        - 可以直接访问S3
    - 2. considerations
        - 1.与S3必须在同一个region.
        - 2. 需要做vpc config ，可能做不了，在设计的时候需要知道
            
            ![https://api2.mubu.com/v3/document_image/a9b35459-c69b-49d9-b142-c5bfc8140673-14086676.jpg](https://api2.mubu.com/v3/document_image/a9b35459-c69b-49d9-b142-c5bfc8140673-14086676.jpg)
            
    - 3. Benefits
        - 1. 可以在S3中query大量数据
            
            ![https://api2.mubu.com/v3/document_image/7a1935e8-b9a1-4d59-97ed-bf4a99a0b6eb-14086676.jpg](https://api2.mubu.com/v3/document_image/7a1935e8-b9a1-4d59-97ed-bf4a99a0b6eb-14086676.jpg)
            
        - 2. 不需要把数据录进 database中
        - 3. 可以把热的data 放在spectrum中 ，而不放在数据库中，可以减少cost（snowflake也有这个好处）
- 7. SageMaker
    - [1.AI](http://1.ai/) machine learning 的一个service
        - 好处：
        - 1. 用jupyter notebook 形式做开发
            
            ![https://api2.mubu.com/v3/document_image/b4aaf6ed-bcf2-467a-b699-9f915c7ca229-14086676.jpg](https://api2.mubu.com/v3/document_image/b4aaf6ed-bcf2-467a-b699-9f915c7ca229-14086676.jpg)
            
        - 2. 有很多prebuild的算法，直接用这些sample
    - 2.cost 按每分钟的使用花费， Pay as you go
    - 3.机器模型建立过程
        - 
            
            ![https://api2.mubu.com/v3/document_image/06f99b68-68a1-4042-b662-3a700a7c46ff-14086676.jpg](https://api2.mubu.com/v3/document_image/06f99b68-68a1-4042-b662-3a700a7c46ff-14086676.jpg)
            
- 8. AWS batch和stream pipeline 流程讲解 (3:00)
    - 1. Enterprise data warehouse
        
        ![https://api2.mubu.com/v3/document_image/c4b4af17-f5c1-4366-8702-49ae072577fe-14086676.jpg](https://api2.mubu.com/v3/document_image/c4b4af17-f5c1-4366-8702-49ae072577fe-14086676.jpg)
        
    - 2. streaming pipeline
        
        ![https://api2.mubu.com/v3/document_image/9a1c59bc-92ec-4f04-b86f-ee4ad3d73109-14086676.jpg](https://api2.mubu.com/v3/document_image/9a1c59bc-92ec-4f04-b86f-ee4ad3d73109-14086676.jpg)