# lecture 19 Data engineering parts 1&2

- 思维导读：
    - 
        
        ![https://api2.mubu.com/v3/document_image/7e1e0cd3-5601-4823-b0b0-175ad6142070-14086676.jpg](https://api2.mubu.com/v3/document_image/7e1e0cd3-5601-4823-b0b0-175ad6142070-14086676.jpg)
        
- 1. Batch processing -----接上节课，第一点，放在一起好复习----
    - 1. 什么是batch processing？
        - 例如最近一周或最近一个月的数据
            
            ![https://api2.mubu.com/v3/document_image/e4be9798-8d77-4e38-930d-85d3fb51dd94-14086676.jpg](https://api2.mubu.com/v3/document_image/e4be9798-8d77-4e38-930d-85d3fb51dd94-14086676.jpg)
            
    - 2. 什么时候用batch processing ?
        - 不需要实时分析的时候用，根据公司数据分析的频率来设置batch processing的频率，weekly，monthly， etc.
            
            ![https://api2.mubu.com/v3/document_image/d1f2938f-7fb3-44af-8e7e-c665c8859d2f-14086676.jpg](https://api2.mubu.com/v3/document_image/d1f2938f-7fb3-44af-8e7e-c665c8859d2f-14086676.jpg)
            
        - 适合不需要实时数据分析的情况
        - 海量数据进行机器学习
        - 海量数据进行整合，便于数据分析及可视化
    - 3. 例子
        - 拿出对我们有用的信息
            
            ![https://api2.mubu.com/v3/document_image/1f1bafc7-447a-41dd-91a9-ca8d8b6920da-14086676.jpg](https://api2.mubu.com/v3/document_image/1f1bafc7-447a-41dd-91a9-ca8d8b6920da-14086676.jpg)
            
        - SMS， 通过大数据对我们进行分析。campaign，不需要实时，法律只能一天一次邮件，batch会成为很好的选择
            
            ![https://api2.mubu.com/v3/document_image/388da9a1-36ec-4bbf-a5d5-da66bd3de276-14086676.jpg](https://api2.mubu.com/v3/document_image/388da9a1-36ec-4bbf-a5d5-da66bd3de276-14086676.jpg)
            
    - 4. challenges
        - 1. Data format and encoding
            - 是UTF -16 还是UTF -8？by default，我们都喜欢UTF-8.在设计data loading的时候，需要考虑到商业需求是不是会遇到这种多编码，多种data format的情况，所有需要设计一种process，有一定的ability去处理多编码多data format的issue。
                
                ![https://api2.mubu.com/v3/document_image/36356be8-c19b-43b6-992e-efa6b7c7b58e-14086676.jpg](https://api2.mubu.com/v3/document_image/36356be8-c19b-43b6-992e-efa6b7c7b58e-14086676.jpg)
                
        - 2. Orchestrating time slices
            - ETL 跑多久，先跑什么再跑什么，如果有些data 晚来了，或数据来的顺序不对，该怎么处理。
                
                ![https://api2.mubu.com/v3/document_image/3e2cfae6-b8e7-4a9a-b99d-d870e07206e6-14086676.jpg](https://api2.mubu.com/v3/document_image/3e2cfae6-b8e7-4a9a-b99d-d870e07206e6-14086676.jpg)
                
    - 5. Architecture
        - 需要理解思考：
            
            ![https://api2.mubu.com/v3/document_image/1bd131aa-513a-4c4b-9169-3df1dd564f34-14086676.jpg](https://api2.mubu.com/v3/document_image/1bd131aa-513a-4c4b-9169-3df1dd564f34-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/33847eed-fb3c-49d6-ae7a-2a145bd8c832-14086676.jpg](https://api2.mubu.com/v3/document_image/33847eed-fb3c-49d6-ae7a-2a145bd8c832-14086676.jpg)
            
        - 1. 需要怎样的data storage
            - 1. S3
                - 能保证很好的durability，
                    
                    ![https://api2.mubu.com/v3/document_image/29ad854d-2400-477e-b152-a549d0b15cd6-14086676.jpg](https://api2.mubu.com/v3/document_image/29ad854d-2400-477e-b152-a549d0b15cd6-14086676.jpg)
                    
            - 2. EBS
                - 可以attach到instance上，直接计算完保留在磁盘上读写速度快
                    
                    ![https://api2.mubu.com/v3/document_image/80546389-8c25-4ecd-90ed-59602b96c373-14086676.jpg](https://api2.mubu.com/v3/document_image/80546389-8c25-4ecd-90ed-59602b96c373-14086676.jpg)
                    
        - 2. 需要怎样的batch processing。能不能让运行的时间更短。
            - 1. Spark
                - 做大数据，考虑spark，支持多种program language，能做分布式计算，提高我们processing的performance。
                    
                    ![https://api2.mubu.com/v3/document_image/83279b1a-3233-424a-9c9a-3b8ef2e2f990-14086676.jpg](https://api2.mubu.com/v3/document_image/83279b1a-3233-424a-9c9a-3b8ef2e2f990-14086676.jpg)
                    
            - 2. ETL/ELT tools
                - 不想用大数据处理，snowflake 本身的performance很高，我们通过生产很多SQL statement，让它们在snowflake等数据库中去运行。可以prebuid 的一些connector ，不需要再去code，只要做些config就可以去跟别人打 交道了。
                    
                    ![https://api2.mubu.com/v3/document_image/f86b3093-dad6-43d3-bf73-ecee01327e94-14086676.jpg](https://api2.mubu.com/v3/document_image/f86b3093-dad6-43d3-bf73-ecee01327e94-14086676.jpg)
                    
        - 3. 需要怎样的analytical data store
            - 0.选取怎样的数据库呢?olap?oltp?
            - 1. Data warehouse -- 对数据进行优化存储，之后做数据分析会非常快
            - 2. Spark SQL
            - 3. HBase
                
                ![https://api2.mubu.com/v3/document_image/88bbc370-b8dd-4a0d-acd3-14fb9ace3b21-14086676.jpg](https://api2.mubu.com/v3/document_image/88bbc370-b8dd-4a0d-acd3-14fb9ace3b21-14086676.jpg)
                
        - 4. 需要怎样的Analysis and reporting
            - 0.传统的分析？机器学习？
            - 1. Power BI
            - 2. Tableau
            - 3. Amazon QuickSight
                
                ![https://api2.mubu.com/v3/document_image/40411dc0-ff8a-4186-b929-292187fbcf32-14086676.jpg](https://api2.mubu.com/v3/document_image/40411dc0-ff8a-4186-b929-292187fbcf32-14086676.jpg)
                
        - 5. 需要怎样的Orchestration
            - 0.整个pipeline怎么串联起来，什么时间跑什么job
            - 1. Oozie and Sqoop
            - 2. Amazon ClouldWatch
                
                ![https://api2.mubu.com/v3/document_image/ec6dd7d0-bf5b-4d8f-8a0b-6553b5c7439c-14086676.jpg](https://api2.mubu.com/v3/document_image/ec6dd7d0-bf5b-4d8f-8a0b-6553b5c7439c-14086676.jpg)
                
- 2. Real time processing (streaming, 数据一直在进入系统）
    - 1.要实时capture data， 时间延迟越少越好
        - 
            
            ![https://api2.mubu.com/v3/document_image/2fe9d10c-8621-48de-96ec-3a3ddbaaddfa-14086676.jpg](https://api2.mubu.com/v3/document_image/2fe9d10c-8621-48de-96ec-3a3ddbaaddfa-14086676.jpg)
            
    - 2. example
        - 例如，1.Google map 就是实时的，batch processing一点意义都没有。
            
            ![https://api2.mubu.com/v3/document_image/b560a1b7-c49a-42ba-8a4d-c292676f84c4-14086676.jpg](https://api2.mubu.com/v3/document_image/b560a1b7-c49a-42ba-8a4d-c292676f84c4-14086676.jpg)
            
        - 2.网购实时推荐
            
            ![https://api2.mubu.com/v3/document_image/4e0f840e-9cf4-44b7-98c4-b58d7ef9569f-14086676.jpg](https://api2.mubu.com/v3/document_image/4e0f840e-9cf4-44b7-98c4-b58d7ef9569f-14086676.jpg)
            
    - 3. challenges
        - 
            
            ![https://api2.mubu.com/v3/document_image/c7257511-65b1-41f3-8a40-2345f193f3c2-14086676.jpg](https://api2.mubu.com/v3/document_image/c7257511-65b1-41f3-8a40-2345f193f3c2-14086676.jpg)
            
    - 4. Architecture
        - 1. arichitecture: real-time message ingestion > streaming processing > analytical data store > analysis and reporting
            - 
                
                ![https://api2.mubu.com/v3/document_image/c261ad89-79a2-4198-8486-5b6cf85ba085-14086676.jpg](https://api2.mubu.com/v3/document_image/c261ad89-79a2-4198-8486-5b6cf85ba085-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/66b4fd03-806a-4ac0-8c75-d87cccbbf589-14086676.jpg](https://api2.mubu.com/v3/document_image/66b4fd03-806a-4ac0-8c75-d87cccbbf589-14086676.jpg)
                
        - 2. real time message Ingestion
            - apasche kafka 可以将message 暂时存到一个地方，可以建provider，也可以建consumer到里面去拿数据
                
                ![https://api2.mubu.com/v3/document_image/ab0539d7-a333-4f51-961a-b8ebf74fdfc4-14086676.jpg](https://api2.mubu.com/v3/document_image/ab0539d7-a333-4f51-961a-b8ebf74fdfc4-14086676.jpg)
                
        - 3. Data Storage
            - 
                
                ![https://api2.mubu.com/v3/document_image/e5ad6e24-db1f-41d3-ba51-ca4af0b30cf1-14086676.jpg](https://api2.mubu.com/v3/document_image/e5ad6e24-db1f-41d3-ba51-ca4af0b30cf1-14086676.jpg)
                
        - 4. Stream processing
            - 1. Apache Spark
                - 
                    
                    ![https://api2.mubu.com/v3/document_image/50dc9f0f-e3ef-42ee-be63-db2b89fa4612-14086676.jpg](https://api2.mubu.com/v3/document_image/50dc9f0f-e3ef-42ee-be63-db2b89fa4612-14086676.jpg)
                    
            - 2. Apache Flink
                - 
                    
                    ![https://api2.mubu.com/v3/document_image/8d01b6f0-5d54-44c6-9a8e-a28d8f37f178-14086676.jpg](https://api2.mubu.com/v3/document_image/8d01b6f0-5d54-44c6-9a8e-a28d8f37f178-14086676.jpg)
                    
            - 3. Apache kafka
                - 提供各种API
                    
                    ![https://api2.mubu.com/v3/document_image/d300d1b2-801b-43d0-bfc8-b4afe0390a10-14086676.jpg](https://api2.mubu.com/v3/document_image/d300d1b2-801b-43d0-bfc8-b4afe0390a10-14086676.jpg)
                    
        - 5. Analytical data store
            - 
                
                ![https://api2.mubu.com/v3/document_image/14d2d4e5-e9a5-446f-a4a7-c864ebe1bf95-14086676.jpg](https://api2.mubu.com/v3/document_image/14d2d4e5-e9a5-446f-a4a7-c864ebe1bf95-14086676.jpg)
                
        - 6. Analytics and reporting
            - reporting tool 不会主动refresh data。但可以通过写一个网站，将实时数据发布出来。
                
                ![https://api2.mubu.com/v3/document_image/052be3f3-2f3f-4d20-8cf0-464845c7f0cb-14086676.jpg](https://api2.mubu.com/v3/document_image/052be3f3-2f3f-4d20-8cf0-464845c7f0cb-14086676.jpg)
                
- 3. Data Extraction/Ingestion
    - 1. 有两种形式提取数据
        - 1. push : 数据被推送到我们的server上
            
            ![https://api2.mubu.com/v3/document_image/9781de9a-3ba7-44bf-a410-c95ddd4a7cb7-14086676.jpg](https://api2.mubu.com/v3/document_image/9781de9a-3ba7-44bf-a410-c95ddd4a7cb7-14086676.jpg)
            
        - 2. pull： 我们去server上主动拿数据
        - 3. 图例
            - 
                
                ![https://api2.mubu.com/v3/document_image/1d80995d-8712-4533-8167-81d2fe59afbf-14086676.jpg](https://api2.mubu.com/v3/document_image/1d80995d-8712-4533-8167-81d2fe59afbf-14086676.jpg)
                
    - 2. landing server mechanism
        - 1.概念
            - 
                
                ![https://api2.mubu.com/v3/document_image/9b9f3007-b6ec-45d7-aa14-4b56590bffd0-14086676.jpg](https://api2.mubu.com/v3/document_image/9b9f3007-b6ec-45d7-aa14-4b56590bffd0-14086676.jpg)
                
        - 2.图例解释 （Lecture19 00:39:00）
            - 好处：管理员直接在landing server上管理data与server的connection，不必维护大量的ingestion pipeline. 2.更安全
                
                ![https://api2.mubu.com/v3/document_image/cdac970d-8c16-4959-9806-f528ca3aa280-14086676.jpg](https://api2.mubu.com/v3/document_image/cdac970d-8c16-4959-9806-f528ca3aa280-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/0ba01c4a-bfa7-4428-aaca-38087affe28d-14086676.jpg](https://api2.mubu.com/v3/document_image/0ba01c4a-bfa7-4428-aaca-38087affe28d-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/9ee0dc11-6958-493d-a0cd-1a10cf7771c0-14086676.jpg](https://api2.mubu.com/v3/document_image/9ee0dc11-6958-493d-a0cd-1a10cf7771c0-14086676.jpg)
                
    - 3. Data extraction/ingestion 的一些操作
        - 1. Basic data information check
            - 1.check 数据的一些基本信息
                - 例如: 来的信息是什么format，CSV？JSON？TXT？什么header file（name, age, address...)？ Footer file(多少条记录）？EOT？
                    
                    ![https://api2.mubu.com/v3/document_image/8af680bd-5296-4a0f-8a71-93d4703bffbc-14086676.jpg](https://api2.mubu.com/v3/document_image/8af680bd-5296-4a0f-8a71-93d4703bffbc-14086676.jpg)
                    
                - EOT， end of transferring file（检查文件是否真正传输完整，不然不执行ETL）
                    - 没有EOT，传文件是渐进的，当我们看到有文件名的时候，整个文件其实还没有传完，ETL是有问题的还不可以跑ETL
                        
                        ![https://api2.mubu.com/v3/document_image/dda531e2-55a4-4a9b-bceb-f584e8e4314d-14086676.jpg](https://api2.mubu.com/v3/document_image/dda531e2-55a4-4a9b-bceb-f584e8e4314d-14086676.jpg)
                        
                    - ETL需要EOT文件才会执行
                        
                        ![https://api2.mubu.com/v3/document_image/b4976311-dbd4-40f6-86f4-0a52f2e1bb9e-14086676.jpg](https://api2.mubu.com/v3/document_image/b4976311-dbd4-40f6-86f4-0a52f2e1bb9e-14086676.jpg)
                        
                        ![https://api2.mubu.com/v3/document_image/49f085d3-cde9-408f-a09a-00f735eca7c2-14086676.jpg](https://api2.mubu.com/v3/document_image/49f085d3-cde9-408f-a09a-00f735eca7c2-14086676.jpg)
                        
        - 2.Key points
            - 
                
                ![https://api2.mubu.com/v3/document_image/4151a0fe-8640-49db-b5e3-15d56bcb2f3d-14086676.jpg](https://api2.mubu.com/v3/document_image/4151a0fe-8640-49db-b5e3-15d56bcb2f3d-14086676.jpg)
                
- 4. Data Pre-processing
    - 0.error 要尽早的处理掉，越早处理掉这些issue，越好。
    - 1. Format modification
        - 几个步骤: （很多不同的做法，截图展示的是老师的方法）
        - 1. Encoding change
            - 例如用Linux，改变encoding： iconv -f ascii -t UTF-16 test.txt -o test_new.txt
                
                ![https://api2.mubu.com/v3/document_image/5585a67c-76c0-444a-bd53-73a4c473d5c4-14086676.jpg](https://api2.mubu.com/v3/document_image/5585a67c-76c0-444a-bd53-73a4c473d5c4-14086676.jpg)
                
        - 2. Formalize the letter case
            - 存储的数据是sensitive 的，join是分大小写的，所以要做字母大小写转换 : tr 'A-Z' 'a-z'
                
                ![https://api2.mubu.com/v3/document_image/2050258f-9bd8-450e-83ad-7301ae33f313-14086676.jpg](https://api2.mubu.com/v3/document_image/2050258f-9bd8-450e-83ad-7301ae33f313-14086676.jpg)
                
        - 3. End of line change
            - 现在可以不用特意改。unix 操作系统改Windows操作系统的line ending: unix2dos text.txt
                
                ![https://api2.mubu.com/v3/document_image/3fa5dba3-a3f6-4d73-b17b-e8dc63efa1d5-14086676.jpg](https://api2.mubu.com/v3/document_image/3fa5dba3-a3f6-4d73-b17b-e8dc63efa1d5-14086676.jpg)
                
            - dos2unix text.txt
        - 4. space trimming
            - join对于 空格也是sensitive的，所以要去除space
                
                ![https://api2.mubu.com/v3/document_image/79d31b15-e0b5-4d0b-915a-713584d5650f-14086676.jpg](https://api2.mubu.com/v3/document_image/79d31b15-e0b5-4d0b-915a-713584d5650f-14086676.jpg)
                
            - sed(重要高阶DE Linux指令）sed -e 's/ |/|/g' : s代表start， g 代表global，替换所有遇到的这种‘/ ’成‘/’。
        - 5.Format standardization
            - awk 也是比较重要的指令
                
                ![https://api2.mubu.com/v3/document_image/50e50553-e13e-4f92-a0d0-1303a77c9b04-14086676.jpg](https://api2.mubu.com/v3/document_image/50e50553-e13e-4f92-a0d0-1303a77c9b04-14086676.jpg)
                
            - cat test.txt | awk -F '|' 'BEGIN { OFS = "|" } {gsub("null", "0000-01-01", $3); print $3); print $0} '
            - awk (也是很重要的指令)
            - 做pattern replace要非常小心, 不希望影响其它value， 这个时候就不方便用sed了。
        - 6. Delimiter change
            - 例如： ， 换成 |。
                
                ![https://api2.mubu.com/v3/document_image/cd214bc9-cd8d-402a-b2d6-bc056650d168-14086676.jpg](https://api2.mubu.com/v3/document_image/cd214bc9-cd8d-402a-b2d6-bc056650d168-14086676.jpg)
                
            - sed
        - 7. Footer removing
            - remove掉最后一行： cat test.txt |head -n -1
                
                ![https://api2.mubu.com/v3/document_image/0e6d3055-798a-4e22-b13e-5c9fa43d2d67-14086676.jpg](https://api2.mubu.com/v3/document_image/0e6d3055-798a-4e22-b13e-5c9fa43d2d67-14086676.jpg)
                
        - 最后的 Format modification result
            - 完整的操作步骤从 cat
                
                ![https://api2.mubu.com/v3/document_image/58fd6d20-808b-4f72-ba1d-97e43af0c35f-14086676.jpg](https://api2.mubu.com/v3/document_image/58fd6d20-808b-4f72-ba1d-97e43af0c35f-14086676.jpg)
                
    - 2. Flattening
        - 0.与数据库的flattening 是不一样的
        - 1.将semi-structure data变成structure data.
            - 
                
                ![https://api2.mubu.com/v3/document_image/bc341fd1-a1e2-4a6f-b4ee-fdc441d17347-14086676.jpg](https://api2.mubu.com/v3/document_image/bc341fd1-a1e2-4a6f-b4ee-fdc441d17347-14086676.jpg)
                
        - 2.例如将JSON data， 变成structure data.
            - 
                
                ![https://api2.mubu.com/v3/document_image/c4417b5a-6424-4bda-8903-7e9c902f46b0-14086676.jpg](https://api2.mubu.com/v3/document_image/c4417b5a-6424-4bda-8903-7e9c902f46b0-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/03aa88b5-49e3-4e72-896b-2287746aeca4-14086676.jpg](https://api2.mubu.com/v3/document_image/03aa88b5-49e3-4e72-896b-2287746aeca4-14086676.jpg)
                
        - 3.我们为什么需要flattening
            - 
                
                ![https://api2.mubu.com/v3/document_image/7c425628-3993-495d-bd32-17f6508a6316-14086676.jpg](https://api2.mubu.com/v3/document_image/7c425628-3993-495d-bd32-17f6508a6316-14086676.jpg)
                
        - 4. 怎么做flattening
            - how to do
                
                ![https://api2.mubu.com/v3/document_image/d83d2c0c-3f62-411a-94c8-8b7bddd6471d-14086676.jpg](https://api2.mubu.com/v3/document_image/d83d2c0c-3f62-411a-94c8-8b7bddd6471d-14086676.jpg)
                
            - Pyspark example
                
                ![https://api2.mubu.com/v3/document_image/8c44ebf0-ac56-4503-8e6b-45005a248316-14086676.jpg](https://api2.mubu.com/v3/document_image/8c44ebf0-ac56-4503-8e6b-45005a248316-14086676.jpg)
                
    - 3. Validation
        - 1. why need validation?
            - 因为多个来源的数据，不一定准确，还有bad data, data exception. meaningless data.
                
                ![https://api2.mubu.com/v3/document_image/5ed91108-82cf-4779-9ac8-a7516f01adef-14086676.jpg](https://api2.mubu.com/v3/document_image/5ed91108-82cf-4779-9ac8-a7516f01adef-14086676.jpg)
                
        - 2. Validation example
            - 客户手填
                
                ![https://api2.mubu.com/v3/document_image/f0614d0d-e819-44ce-bf10-e2da45e0886d-14086676.jpg](https://api2.mubu.com/v3/document_image/f0614d0d-e819-44ce-bf10-e2da45e0886d-14086676.jpg)
                
        - 3. How do we do validation
            - 1. data-type check
                - 1. Numerical Value check
                    - 
                        
                        ![https://api2.mubu.com/v3/document_image/7d81ddef-b14f-411e-8e51-5f7587c628d3-14086676.jpg](https://api2.mubu.com/v3/document_image/7d81ddef-b14f-411e-8e51-5f7587c628d3-14086676.jpg)
                        
                - 2.String length check
                    - 
                        
                        ![https://api2.mubu.com/v3/document_image/dfa47817-7ddb-4a0f-a7af-e551fc1d2dc8-14086676.jpg](https://api2.mubu.com/v3/document_image/dfa47817-7ddb-4a0f-a7af-e551fc1d2dc8-14086676.jpg)
                        
                - 3. Data value check
                    - 
                        
                        ![https://api2.mubu.com/v3/document_image/12ca3abb-6534-4af2-8d99-fefc3123d37a-14086676.jpg](https://api2.mubu.com/v3/document_image/12ca3abb-6534-4af2-8d99-fefc3123d37a-14086676.jpg)
                        
                - 4. Boolean value check
                    - 
                        
                        ![https://api2.mubu.com/v3/document_image/7b4e94d7-6ea6-47db-a4ef-7300e06488a6-14086676.jpg](https://api2.mubu.com/v3/document_image/7b4e94d7-6ea6-47db-a4ef-7300e06488a6-14086676.jpg)
                        
            - 2. Constraint check
                - 5点：
                    
                    ![https://api2.mubu.com/v3/document_image/b43e24a7-7b7e-41f1-9e8a-d53d919dfda8-14086676.jpg](https://api2.mubu.com/v3/document_image/b43e24a7-7b7e-41f1-9e8a-d53d919dfda8-14086676.jpg)
                    
            - 3. Consistency check
                - 
                    
                    ![https://api2.mubu.com/v3/document_image/ed90f902-caad-4eba-982c-cb48d72bae29-14086676.jpg](https://api2.mubu.com/v3/document_image/ed90f902-caad-4eba-982c-cb48d72bae29-14086676.jpg)
                    
            - 4. Cross-reference check
                - 1.例如，一种transaction table中的 ID在production table中找不到。
                    
                    ![https://api2.mubu.com/v3/document_image/3f652155-4510-4f98-a605-46c7e934b211-14086676.jpg](https://api2.mubu.com/v3/document_image/3f652155-4510-4f98-a605-46c7e934b211-14086676.jpg)
                    
                - 2.为什么会出现这种情况?
                    - 1. P table 的ETL 还没做
                        
                        ![https://api2.mubu.com/v3/document_image/b2796e63-af7d-4a68-b4f7-116ae7605ce3-14086676.jpg](https://api2.mubu.com/v3/document_image/b2796e63-af7d-4a68-b4f7-116ae7605ce3-14086676.jpg)
                        
                    - 2. some data extraction , T not in P .
                - 3.应该怎么处理它？
                    - 第一种方法： raise exception
                    - 第二种方法：比较通用的，建一个orphan table
                        - 
                            
                            ![https://api2.mubu.com/v3/document_image/cb3e51bc-9d21-48c3-8369-4ab45e061370-14086676.jpg](https://api2.mubu.com/v3/document_image/cb3e51bc-9d21-48c3-8369-4ab45e061370-14086676.jpg)
                            
- 5. Data Transformation
    - 1. why we need to do data transformation
        - 
            
            ![https://api2.mubu.com/v3/document_image/40c35801-07cf-4c95-a8e7-306e1aa57d1a-14086676.jpg](https://api2.mubu.com/v3/document_image/40c35801-07cf-4c95-a8e7-306e1aa57d1a-14086676.jpg)
            
    - 2. General transformation processes
        - 1.
            
            ![https://api2.mubu.com/v3/document_image/511327a9-4b3a-4182-adb9-8927842b3c54-14086676.jpg](https://api2.mubu.com/v3/document_image/511327a9-4b3a-4182-adb9-8927842b3c54-14086676.jpg)
            
        - 2.
            
            ![https://api2.mubu.com/v3/document_image/7ab1445e-b404-4a15-83aa-c19915d5eee4-14086676.jpg](https://api2.mubu.com/v3/document_image/7ab1445e-b404-4a15-83aa-c19915d5eee4-14086676.jpg)
            
        - 3.
            
            ![https://api2.mubu.com/v3/document_image/cec6c434-8630-4ed2-b8fb-ad1a2456ecc0-14086676.jpg](https://api2.mubu.com/v3/document_image/cec6c434-8630-4ed2-b8fb-ad1a2456ecc0-14086676.jpg)
            
        - 4. 计算
            
            ![https://api2.mubu.com/v3/document_image/142c4cca-b4ad-4f28-8baf-7633bb5dae3f-14086676.jpg](https://api2.mubu.com/v3/document_image/142c4cca-b4ad-4f28-8baf-7633bb5dae3f-14086676.jpg)
            
        - 5.排序，增加performance
            
            ![https://api2.mubu.com/v3/document_image/3ebd4cc6-cb55-4e77-b449-0677e20bdbf5-14086676.jpg](https://api2.mubu.com/v3/document_image/3ebd4cc6-cb55-4e77-b449-0677e20bdbf5-14086676.jpg)
            
        - 6.join
            
            ![https://api2.mubu.com/v3/document_image/fd5c4e6f-9907-4d9d-bcf1-bc321a856603-14086676.jpg](https://api2.mubu.com/v3/document_image/fd5c4e6f-9907-4d9d-bcf1-bc321a856603-14086676.jpg)
            
        - 7.整合计算
            
            ![https://api2.mubu.com/v3/document_image/7258760d-d166-4e4a-8eea-554e807a5610-14086676.jpg](https://api2.mubu.com/v3/document_image/7258760d-d166-4e4a-8eea-554e807a5610-14086676.jpg)
            
        - 8.生成SK
            
            ![https://api2.mubu.com/v3/document_image/7dd5523d-a898-40f8-9b20-d2a9058ec644-14086676.jpg](https://api2.mubu.com/v3/document_image/7dd5523d-a898-40f8-9b20-d2a9058ec644-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/5207c4d6-2528-4f36-866d-8e1f3d65e3e9-14086676.jpg](https://api2.mubu.com/v3/document_image/5207c4d6-2528-4f36-866d-8e1f3d65e3e9-14086676.jpg)
            
        - 9.行变列，列 变行
            
            ![https://api2.mubu.com/v3/document_image/3f3d5cc7-735a-4c56-a0a0-bff54ab5de71-14086676.jpg](https://api2.mubu.com/v3/document_image/3f3d5cc7-735a-4c56-a0a0-bff54ab5de71-14086676.jpg)
            
        - 10. 一个列变多个列
            
            ![https://api2.mubu.com/v3/document_image/682fcb95-fe92-494c-8dc5-766df8ac1394-14086676.jpg](https://api2.mubu.com/v3/document_image/682fcb95-fe92-494c-8dc5-766df8ac1394-14086676.jpg)
            
    - 3. Staging the processed data
        - 1. Refresh
        - 2.Append
        - 3.Upsert
            
            ![https://api2.mubu.com/v3/document_image/0ec00223-d2aa-40c4-8e5d-fe100883b24b-14086676.jpg](https://api2.mubu.com/v3/document_image/0ec00223-d2aa-40c4-8e5d-fe100883b24b-14086676.jpg)
            
    - 4. Example in Matillion
        - 有很多的components, 方便connect 其它服务，例如S3
            
            ![https://api2.mubu.com/v3/document_image/2fcb28af-2ff8-47a9-a83d-36af49aec827-14086676.jpg](https://api2.mubu.com/v3/document_image/2fcb28af-2ff8-47a9-a83d-36af49aec827-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/d12d4dba-291e-4c94-8fd3-4dab6adabd4f-14086676.jpg](https://api2.mubu.com/v3/document_image/d12d4dba-291e-4c94-8fd3-4dab6adabd4f-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/a3ee035c-e1da-4dc7-8bc9-b9db06f75282-14086676.jpg](https://api2.mubu.com/v3/document_image/a3ee035c-e1da-4dc7-8bc9-b9db06f75282-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/13367a01-96e1-4cbf-9045-e15340d91fd6-14086676.jpg](https://api2.mubu.com/v3/document_image/13367a01-96e1-4cbf-9045-e15340d91fd6-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/76c57624-1bbb-4196-b094-e43105831938-14086676.jpg](https://api2.mubu.com/v3/document_image/76c57624-1bbb-4196-b094-e43105831938-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/047facf4-110f-43f7-83f7-5f9b71d175de-14086676.jpg](https://api2.mubu.com/v3/document_image/047facf4-110f-43f7-83f7-5f9b71d175de-14086676.jpg)
            
- 6. Data Loading
    - 1、why we need to do load data
        - 
            
            ![https://api2.mubu.com/v3/document_image/9b819a49-b446-412f-a5e8-e15fd0018693-14086676.jpg](https://api2.mubu.com/v3/document_image/9b819a49-b446-412f-a5e8-e15fd0018693-14086676.jpg)
            
    - 2. loading type
        - 1. insert
            - 
                
                ![https://api2.mubu.com/v3/document_image/04105ab8-5db7-443a-a75e-c0b7fdebeb5c-14086676.jpg](https://api2.mubu.com/v3/document_image/04105ab8-5db7-443a-a75e-c0b7fdebeb5c-14086676.jpg)
                
        - 2.update
            - 
                
                ![https://api2.mubu.com/v3/document_image/79db8253-bc4c-409f-a55d-2890edd2cbc0-14086676.jpg](https://api2.mubu.com/v3/document_image/79db8253-bc4c-409f-a55d-2890edd2cbc0-14086676.jpg)
                
        - 3.append
            - 
                
                ![https://api2.mubu.com/v3/document_image/d7b4804a-b1fd-4998-a42f-def079c4a9a5-14086676.jpg](https://api2.mubu.com/v3/document_image/d7b4804a-b1fd-4998-a42f-def079c4a9a5-14086676.jpg)
                
        - 4. truncate & insert (overwrite)
            - 
                
                ![https://api2.mubu.com/v3/document_image/705c04ed-6400-4842-9571-1c7d11e022e4-14086676.jpg](https://api2.mubu.com/v3/document_image/705c04ed-6400-4842-9571-1c7d11e022e4-14086676.jpg)
                
    - 3. Load destination
        - 
            
            ![https://api2.mubu.com/v3/document_image/04d9bbee-5dea-46dc-9d55-797da8db0511-14086676.jpg](https://api2.mubu.com/v3/document_image/04d9bbee-5dea-46dc-9d55-797da8db0511-14086676.jpg)
            
- 6.9 Summary
    - 
        
        ![https://api2.mubu.com/v3/document_image/448894e7-3428-43ec-930c-9fef2411fda7-14086676.jpg](https://api2.mubu.com/v3/document_image/448894e7-3428-43ec-930c-9fef2411fda7-14086676.jpg)
        
- 7. Data Visualization
    - 1. why need to visualize
        - 我们怎样让我们运行的job变得有意义，告诉我点什么，需要data visualize
            
            ![https://api2.mubu.com/v3/document_image/3c17a1bd-9d5c-441e-8bc8-ea50a332e930-14086676.jpg](https://api2.mubu.com/v3/document_image/3c17a1bd-9d5c-441e-8bc8-ea50a332e930-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/0cd42319-b931-4710-9887-46867f1cb76a-14086676.jpg](https://api2.mubu.com/v3/document_image/0cd42319-b931-4710-9887-46867f1cb76a-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/7dc25e60-e9a3-40dc-8091-da2e620d0eb8-14086676.jpg](https://api2.mubu.com/v3/document_image/7dc25e60-e9a3-40dc-8091-da2e620d0eb8-14086676.jpg)
            
        - 2. 成功的job和失败的job， visual出来，更好看到程序运行状态，例如，运行的时长平时处理十分钟的，这次只处理了1分钟，发现这样的异常，就可以考虑是否是数据少造成还是code bug。
            
            ![https://api2.mubu.com/v3/document_image/cece9dde-a443-403c-97cb-18ed29439b39-14086676.jpg](https://api2.mubu.com/v3/document_image/cece9dde-a443-403c-97cb-18ed29439b39-14086676.jpg)
            
- 8. Data pipeline and automation
    - 1. data pipeline
        - 1. 什么是data pipeline？
            - 
                
                ![https://api2.mubu.com/v3/document_image/bee7e195-5400-4a6e-8721-0ed398c20638-14086676.jpg](https://api2.mubu.com/v3/document_image/bee7e195-5400-4a6e-8721-0ed398c20638-14086676.jpg)
                
        - 2. 图例例子1-AWS （lecture 19 2：18）batch load
            - data auditing： 因为不知道当前的数据能不能支持自己建立数据模型，需要样本数据. data auditing 就是一个assessment of data for quality.
                
                ![https://api2.mubu.com/v3/document_image/1ab00599-6dcb-41de-ae7a-389393550000-14086676.jpg](https://api2.mubu.com/v3/document_image/1ab00599-6dcb-41de-ae7a-389393550000-14086676.jpg)
                
            - Databricks develops a web-based platform for working with Spark, that provides automated cluster management and IPython-style notebooks.
        - 3. 图例例子2 --streaming load
            - 
                
                ![https://api2.mubu.com/v3/document_image/8914c62c-4e96-4a70-80b1-fa5fa326342d-14086676.jpg](https://api2.mubu.com/v3/document_image/8914c62c-4e96-4a70-80b1-fa5fa326342d-14086676.jpg)
                
    - 2. Process automation
        - 1.Benefits of Automation
            - 1. cost reduction
                - 
                    
                    ![https://api2.mubu.com/v3/document_image/00a38ab8-ad01-4cf6-a5e6-4e899f33c2b8-14086676.jpg](https://api2.mubu.com/v3/document_image/00a38ab8-ad01-4cf6-a5e6-4e899f33c2b8-14086676.jpg)
                    
            - 2. productivity
                - 
                    
                    ![https://api2.mubu.com/v3/document_image/d9dcc233-b924-4580-b530-629919a2a7e0-14086676.jpg](https://api2.mubu.com/v3/document_image/d9dcc233-b924-4580-b530-629919a2a7e0-14086676.jpg)
                    
            - 3. availability
                - 
                    
                    ![https://api2.mubu.com/v3/document_image/5b0b2795-203e-4606-b98d-f5fa0a325aad-14086676.jpg](https://api2.mubu.com/v3/document_image/5b0b2795-203e-4606-b98d-f5fa0a325aad-14086676.jpg)
                    
            - 4. reliability
                - 
                    
                    ![https://api2.mubu.com/v3/document_image/c56af5f1-f160-4a2e-9601-15114dd0e282-14086676.jpg](https://api2.mubu.com/v3/document_image/c56af5f1-f160-4a2e-9601-15114dd0e282-14086676.jpg)
                    
        - 2.Crontabe introduction
            - 1. introduction
                - 
                    
                    ![https://api2.mubu.com/v3/document_image/72d501a7-979f-4dfe-851b-d492df49aef4-14086676.jpg](https://api2.mubu.com/v3/document_image/72d501a7-979f-4dfe-851b-d492df49aef4-14086676.jpg)
                    
                    ![https://api2.mubu.com/v3/document_image/1b4e04d3-3db2-4d5b-a954-8e681042c9cf-14086676.jpg](https://api2.mubu.com/v3/document_image/1b4e04d3-3db2-4d5b-a954-8e681042c9cf-14086676.jpg)
                    
                    ![https://api2.mubu.com/v3/document_image/5ce28fa2-77ba-49a6-b5dd-bd53972299f5-14086676.jpg](https://api2.mubu.com/v3/document_image/5ce28fa2-77ba-49a6-b5dd-bd53972299f5-14086676.jpg)
                    
                    ![https://api2.mubu.com/v3/document_image/6a0b7d69-699b-4d21-a858-0eb2579e9b70-14086676.jpg](https://api2.mubu.com/v3/document_image/6a0b7d69-699b-4d21-a858-0eb2579e9b70-14086676.jpg)
                    
                    - 
            - 2. crontab commands
                - 
                    
                    ![https://api2.mubu.com/v3/document_image/117865e6-4969-4ded-9cd0-025f64048785-14086676.jpg](https://api2.mubu.com/v3/document_image/117865e6-4969-4ded-9cd0-025f64048785-14086676.jpg)
                    
            - 3. Disable Email
                - 
                    
                    ![https://api2.mubu.com/v3/document_image/763b130d-0031-4ba8-8986-06ef44a01a88-14086676.jpg](https://api2.mubu.com/v3/document_image/763b130d-0031-4ba8-8986-06ef44a01a88-14086676.jpg)
                    
    - 3.AWS case study (2:45)
        - 1.流程图
            - 如果需要建模，那放回到S3中，Amazon segamaker, 预测模型，再拿回Snowflake。如果不需要建模，直接ETL 后放到datawarehouse 让Snowflake 去拿。
                
                ![https://api2.mubu.com/v3/document_image/1ffc3880-5448-4042-84fb-174279a7cff2-14086676.jpg](https://api2.mubu.com/v3/document_image/1ffc3880-5448-4042-84fb-174279a7cff2-14086676.jpg)
                
        - 2. lambda Extractor 代码
            - 
                
                ![https://api2.mubu.com/v3/document_image/0329d5eb-e1e0-4351-b830-1968c6674193-14086676.jpg](https://api2.mubu.com/v3/document_image/0329d5eb-e1e0-4351-b830-1968c6674193-14086676.jpg)
                
        - 3. ELT Matillion
            - 1.
                - 1
                    
                    ![https://api2.mubu.com/v3/document_image/13ef862e-e740-43a4-bfd9-add3be48a268-14086676.jpg](https://api2.mubu.com/v3/document_image/13ef862e-e740-43a4-bfd9-add3be48a268-14086676.jpg)
                    
                    ![https://api2.mubu.com/v3/document_image/9cbe1447-7bb1-4c26-aafa-a25d72f6b8a0-14086676.jpg](https://api2.mubu.com/v3/document_image/9cbe1447-7bb1-4c26-aafa-a25d72f6b8a0-14086676.jpg)
                    
                    ![https://api2.mubu.com/v3/document_image/2a055e0f-d6fc-45c2-bf29-6cdf5f27d4b0-14086676.jpg](https://api2.mubu.com/v3/document_image/2a055e0f-d6fc-45c2-bf29-6cdf5f27d4b0-14086676.jpg)
                    
                    ![https://api2.mubu.com/v3/document_image/53420fb3-f2d7-49ba-9a26-602ea9c65f3b-14086676.jpg](https://api2.mubu.com/v3/document_image/53420fb3-f2d7-49ba-9a26-602ea9c65f3b-14086676.jpg)
                    
                    ![https://api2.mubu.com/v3/document_image/c3c0833b-5562-4d52-a39d-84cee9276e37-14086676.jpg](https://api2.mubu.com/v3/document_image/c3c0833b-5562-4d52-a39d-84cee9276e37-14086676.jpg)
                    
                    ![https://api2.mubu.com/v3/document_image/bf31f89b-4a24-4b69-9320-dd96af7c84e1-14086676.jpg](https://api2.mubu.com/v3/document_image/bf31f89b-4a24-4b69-9320-dd96af7c84e1-14086676.jpg)
                    
                    ![https://api2.mubu.com/v3/document_image/2be212ca-210e-4bb7-a62f-62417063a2dc-14086676.jpg](https://api2.mubu.com/v3/document_image/2be212ca-210e-4bb7-a62f-62417063a2dc-14086676.jpg)
                    
            - 2. fact update
                - 
                    
                    ![https://api2.mubu.com/v3/document_image/57242da0-e4d2-47a4-9b3f-c7abd5ae0e06-14086676.jpg](https://api2.mubu.com/v3/document_image/57242da0-e4d2-47a4-9b3f-c7abd5ae0e06-14086676.jpg)
                    
                    ![https://api2.mubu.com/v3/document_image/936ee013-0b5e-48dc-8779-a6f0cb5d647a-14086676.jpg](https://api2.mubu.com/v3/document_image/936ee013-0b5e-48dc-8779-a6f0cb5d647a-14086676.jpg)
                    
            - 3. generate summary table for data modeling
                - 
                    
                    ![https://api2.mubu.com/v3/document_image/67d70db6-f9dd-43a8-b891-16aceb0d1449-14086676.jpg](https://api2.mubu.com/v3/document_image/67d70db6-f9dd-43a8-b891-16aceb0d1449-14086676.jpg)
                    
        - 4. summary order 进行一个计算
            - 计算，计算完了，将这些数据写进一个table里
                
                ![https://api2.mubu.com/v3/document_image/54064ee2-0a77-4f4d-9909-e9024b197cab-14086676.jpg](https://api2.mubu.com/v3/document_image/54064ee2-0a77-4f4d-9909-e9024b197cab-14086676.jpg)
                
            - Job status update
                
                ![https://api2.mubu.com/v3/document_image/3aeb114c-ba1c-43bc-87cb-1967b6b73dde-14086676.jpg](https://api2.mubu.com/v3/document_image/3aeb114c-ba1c-43bc-87cb-1967b6b73dde-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/2540be62-6d13-4c59-b926-8dd078511e72-14086676.jpg](https://api2.mubu.com/v3/document_image/2540be62-6d13-4c59-b926-8dd078511e72-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/8777d8f3-5c7f-4dda-93dd-56e10fc21a4a-14086676.jpg](https://api2.mubu.com/v3/document_image/8777d8f3-5c7f-4dda-93dd-56e10fc21a4a-14086676.jpg)
                
        - 5. data visualization
            - 
                
                ![https://api2.mubu.com/v3/document_image/75f60481-5ff4-4ea3-a6d9-6e30262f1664-14086676.jpg](https://api2.mubu.com/v3/document_image/75f60481-5ff4-4ea3-a6d9-6e30262f1664-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/2d379d06-b5e3-49cc-bf92-aff824a52855-14086676.jpg](https://api2.mubu.com/v3/document_image/2d379d06-b5e3-49cc-bf92-aff824a52855-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/e885583c-1d4f-4b02-8fb6-f038da5b6857-14086676.jpg](https://api2.mubu.com/v3/document_image/e885583c-1d4f-4b02-8fb6-f038da5b6857-14086676.jpg)
                
        - 6. machine learning --> prediction
            - 
                
                ![https://api2.mubu.com/v3/document_image/1cc24699-f244-40b3-8878-19452e67bf28-14086676.jpg](https://api2.mubu.com/v3/document_image/1cc24699-f244-40b3-8878-19452e67bf28-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/900f8142-692f-49b5-affb-8935fc6d3827-14086676.jpg](https://api2.mubu.com/v3/document_image/900f8142-692f-49b5-affb-8935fc6d3827-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/ca7de48b-1d19-4335-9401-abe6ea5e4173-14086676.jpg](https://api2.mubu.com/v3/document_image/ca7de48b-1d19-4335-9401-abe6ea5e4173-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/05e13293-c08e-4e77-8ea8-ca539f154c9f-14086676.jpg](https://api2.mubu.com/v3/document_image/05e13293-c08e-4e77-8ea8-ca539f154c9f-14086676.jpg)
                
- 10. 重要概念图
    - 1. data pipeline图例（lecture 19 2：18）
        - 
            
            ![https://api2.mubu.com/v3/document_image/afe12d32-8bd7-4645-a4ff-f34dcc03a5f8-14086676.jpg](https://api2.mubu.com/v3/document_image/afe12d32-8bd7-4645-a4ff-f34dcc03a5f8-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/140bc901-f4e3-4e4b-bb61-1b633fe55b67-14086676.jpg](https://api2.mubu.com/v3/document_image/140bc901-f4e3-4e4b-bb61-1b633fe55b67-14086676.jpg)