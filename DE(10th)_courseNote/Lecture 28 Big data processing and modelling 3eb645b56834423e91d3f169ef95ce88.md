# Lecture 28 Big data processing and modelling

- 0.课前老师建议：
    - 0.1 把code都放在GitHub 里，方便maintain和查看
    - 0.2 自己Google一些文章看看，因为老师讲的都是精华，还有细节需要自己完善
- 1. Data Lake 的使用目的等等
    - 1、什么是Data Lake（DL)？
        - DL是一个目录
        - data warehouse数据格式是非常严格，非常相关的数据才会放进数据库进行处理，而DL与DW相反，包括所有类型的数据
            
            ![https://api2.mubu.com/v3/document_image/24c99f3b-bf11-4924-a482-2128e43d7f15-14086676.jpg](https://api2.mubu.com/v3/document_image/24c99f3b-bf11-4924-a482-2128e43d7f15-14086676.jpg)
            
    - 2、Objectives of a Data Lake
        - 1.前期effort非常简单
        - 2.使得获取数据很简单
        - 3.将multi-structured保持native format，保持源数据格式方便做Auditing
        - 4.公司不需要在初期（requirements不是很清楚时）花很多精力把schema定义的很好
        - 5.处理速度更快
        - 6.可以储存更多中的数据格式，例如image，video也能储存（DW就不能储存），在S3中数据以object格式储存，格式与原格式一模一样。
        - 7.作为staging area，减少DW的storage
        - 8.拥有更活跃的archiving, 有多种可以query的手段，如Athena，EMR等等
            
            ![https://api2.mubu.com/v3/document_image/2452664e-1d7f-493f-ace8-0ec55b9402ce-14086676.jpg](https://api2.mubu.com/v3/document_image/2452664e-1d7f-493f-ace8-0ec55b9402ce-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/c6f58467-9f4b-4476-9058-09220e42a948-14086676.jpg](https://api2.mubu.com/v3/document_image/c6f58467-9f4b-4476-9058-09220e42a948-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/b2200c35-1b44-4610-859a-ec3989d79b9e-14086676.jpg](https://api2.mubu.com/v3/document_image/b2200c35-1b44-4610-859a-ec3989d79b9e-14086676.jpg)
            
    - 3、Iterative Data Lake Pattern
        - 1.ingest
        - 2.分析下数据有什么value，因为很多时候拿了数据不知道它有什么用，我们要分析这个数据到底能干嘛，对我们有什么用。
        - 3. integrate data with DW or use data virtualization(data 的乌托邦，所有的有用的数据都可以在一个common layer中获取，很难做，一般情况下公司都做不到这一步）
            
            ![https://api2.mubu.com/v3/document_image/e2b7de05-10dc-4cc5-923a-dfca0ccc0cc4-14086676.jpg](https://api2.mubu.com/v3/document_image/e2b7de05-10dc-4cc5-923a-dfca0ccc0cc4-14086676.jpg)
            
    - 4、Data lake implementation
        - data lake是一个conceptual idea，有很多的flexibility 在里面，去implement with one or more technologies
        - HDFS 可以很方便更改数据（如删除，rename等），而S3中改数据就比较麻烦了，但是S3还是用的多因为好处太大，S3是object store，速度快。HDFS是disk储存方式，会比较慢
            
            ![https://api2.mubu.com/v3/document_image/b3625297-4e5e-4df7-8998-ffe592c1a6b7-14086676.jpg](https://api2.mubu.com/v3/document_image/b3625297-4e5e-4df7-8998-ffe592c1a6b7-14086676.jpg)
            
    - 5、Coexistence of Data Lake & Data Warehouse
        - 
            
            ![https://api2.mubu.com/v3/document_image/6c3ab0c4-3e46-441d-a881-583499040272-14086676.jpg](https://api2.mubu.com/v3/document_image/6c3ab0c4-3e46-441d-a881-583499040272-14086676.jpg)
            
    - 6、zones in a data lake （00:28）
        - 重点要背：4个zone，数据根据purpose选择放在哪个zone里
            - 0.
                
                ![https://api2.mubu.com/v3/document_image/cc1ae806-0a29-4c38-a8ed-6da71cdda326-14086676.jpg](https://api2.mubu.com/v3/document_image/cc1ae806-0a29-4c38-a8ed-6da71cdda326-14086676.jpg)
                
            - 1.Transient/ Temp Zone
                - 0.有些公司可能不需要temp zone，
                    
                    ![https://api2.mubu.com/v3/document_image/9f00b7cc-c381-46ae-a4e2-b4ca5e13966f-14086676.jpg](https://api2.mubu.com/v3/document_image/9f00b7cc-c381-46ae-a4e2-b4ca5e13966f-14086676.jpg)
                    
                - 1. 有些数据可能是脏数据，传到到Raw data zone可能会污染数据，起到缓冲作用，所以要放到Temp zone了，当Temp zone里的数据是完全没问题的，再放到raw data zone
                - 2.highly limited access, 源数据几乎是不给user的，除非一些特殊部门的人，如市场部，data analyst.
            - 2. Raw Data/ Staging Zone
                - 0、overview， 放在S3 Bucket中
                    
                    ![https://api2.mubu.com/v3/document_image/cf6af764-385f-4419-ab90-295b6b916ea1-14086676.jpg](https://api2.mubu.com/v3/document_image/cf6af764-385f-4419-ab90-295b6b916ea1-14086676.jpg)
                    
                - 1、Immutable，不能改变格式，保持源数据原始格式
                - 2、History is retained 预留给未来需求
            - 3.Curated Data Zone
                - 0.
                    
                    ![https://api2.mubu.com/v3/document_image/67c766de-520d-4c86-8dc3-d46f9dd5645c-14086676.jpg](https://api2.mubu.com/v3/document_image/67c766de-520d-4c86-8dc3-d46f9dd5645c-14086676.jpg)
                    
                - 1.存放了精细化处理过的数据，可以给down users 使用了，是确定有value的数据
                - 2.self-service, 不是给自己用的，而是给别人用的，建好后就不会过多的去干预
                - 3. standard governance & security
            - 4. Analytics Sandbox
                - 0.
                    
                    ![https://api2.mubu.com/v3/document_image/71fa38e9-537c-4b00-878a-49fa4c614ac6-14086676.jpg](https://api2.mubu.com/v3/document_image/71fa38e9-537c-4b00-878a-49fa4c614ac6-14086676.jpg)
                    
                - 1. DE能够provide给 DA 和DS 分析区域，给他们探索用，比较杂乱，各种各样的DA和DS分析的数据，
                - 2. Minimal governance
                - 3. 一些production，valuable efforts， 比较好的数据会promote到Curated Data Zone 中
    - 7、Sandbox Solutions:
        - 1、Sandbox Solutions: Develop
            - 0. 一个typical的在真实业务中该如何处理数据的一个architacture
                
                ![https://api2.mubu.com/v3/document_image/37f8b147-9e62-463c-adbf-629d46063b64-14086676.jpg](https://api2.mubu.com/v3/document_image/37f8b147-9e62-463c-adbf-629d46063b64-14086676.jpg)
                
        - 2、Sandbox Solutions: Operationalize
            - 0.
                
                ![https://api2.mubu.com/v3/document_image/9abaaa17-665b-4342-89c0-3ba45d0135ca-14086676.jpg](https://api2.mubu.com/v3/document_image/9abaaa17-665b-4342-89c0-3ba45d0135ca-14086676.jpg)
                
            - 1.现在不用R server 用的是AWS的SegeMakerM
    - 8、Organizing the Data Lake
        - 0.如何把数据存放成一个efficient format，让DA、DS 使用
            
            ![https://api2.mubu.com/v3/document_image/bd8c459d-de82-448d-b6f9-b85bb037a5c9-14086676.jpg](https://api2.mubu.com/v3/document_image/bd8c459d-de82-448d-b6f9-b85bb037a5c9-14086676.jpg)
            
        - 1.Subject area：按类别划分，如sale部门就放sale数据，生产部就放生产数据。
        - 2.Time Partitioning：按时间序列，如年份月份存放
        - 3.Security Boundaries: high confidencial 的数据需要特定的 boundaries organize 起来
        - 4. Downstream app/purpose: 根据数据最后的用法organize起来
        - 目的是避免data swamp。
    - 9、Challenges of a Data Lake
        - 不像DW有一个执行计划，DL需要更好的design
            
            ![https://api2.mubu.com/v3/document_image/7ab17151-7881-484c-b706-c0e929beca84-14086676.jpg](https://api2.mubu.com/v3/document_image/7ab17151-7881-484c-b706-c0e929beca84-14086676.jpg)
            
    - 10、Ways to Get Started with a Data Lake
        - 0
            
            ![https://api2.mubu.com/v3/document_image/193f2e9a-1397-418b-8366-1704178d9d22-14086676.jpg](https://api2.mubu.com/v3/document_image/193f2e9a-1397-418b-8366-1704178d9d22-14086676.jpg)
            
    - 11、Getting real value from the Data Lake
        - 0.
            
            ![https://api2.mubu.com/v3/document_image/37ea8ada-61ce-45de-ba27-70f5631f917d-14086676.jpg](https://api2.mubu.com/v3/document_image/37ea8ada-61ce-45de-ba27-70f5631f917d-14086676.jpg)
            
    - 12、The Logical Data warehouse & data virtualization
        - 0. 实现非常困难，知道就好，基本所有公司都做不到，因为太难了
            
            ![https://api2.mubu.com/v3/document_image/13c77d30-abc7-451c-9f06-2c9787657ff0-14086676.jpg](https://api2.mubu.com/v3/document_image/13c77d30-abc7-451c-9f06-2c9787657ff0-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/d5415426-8c8f-48ba-b24a-e17b1ce1db29-14086676.jpg](https://api2.mubu.com/v3/document_image/d5415426-8c8f-48ba-b24a-e17b1ce1db29-14086676.jpg)
            
        - 1。困难很多
            
            ![https://api2.mubu.com/v3/document_image/ed8745e4-a54f-4c01-89c9-eb34545502af-14086676.jpg](https://api2.mubu.com/v3/document_image/ed8745e4-a54f-4c01-89c9-eb34545502af-14086676.jpg)
            
    - 推荐书籍
        - 
            
            ![https://api2.mubu.com/v3/document_image/af94c981-313e-4b33-894a-3034b7d0470b-14086676.jpg](https://api2.mubu.com/v3/document_image/af94c981-313e-4b33-894a-3034b7d0470b-14086676.jpg)
            
- 2. AWS glue
    - 1. 主要做ETL的集大成service
        - 
            
            ![https://api2.mubu.com/v3/document_image/684d2941-2382-414a-b7df-7da5af00e450-14086676.jpg](https://api2.mubu.com/v3/document_image/684d2941-2382-414a-b7df-7da5af00e450-14086676.jpg)
            
    - 2. Glue ETL
        - 
            
            ![https://api2.mubu.com/v3/document_image/2b6db631-ad1a-41ac-a8c7-bf020b718f47-14086676.jpg](https://api2.mubu.com/v3/document_image/2b6db631-ad1a-41ac-a8c7-bf020b718f47-14086676.jpg)
            
- 3.有监督学习和无监督学习
- 4.R k-mean practice (2:38:00)
    - kmean cluster 和hirach clustering 工业用的多，简单高效
        
        ![https://api2.mubu.com/v3/document_image/faf4e6e5-c253-4fd2-a3f0-4882a75aaa2b-14086676.jpg](https://api2.mubu.com/v3/document_image/faf4e6e5-c253-4fd2-a3f0-4882a75aaa2b-14086676.jpg)