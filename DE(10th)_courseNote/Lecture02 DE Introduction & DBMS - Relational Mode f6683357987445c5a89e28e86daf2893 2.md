# Lecture02 DE Introduction & DBMS - Relational Model

- 0. 内容导读
    - 
        
        ![https://api2.mubu.com/v3/document_image/1d775983-da48-45b6-ad5f-0c3b31166b7a-14086676.jpg](https://api2.mubu.com/v3/document_image/1d775983-da48-45b6-ad5f-0c3b31166b7a-14086676.jpg)
        
- 1.SQL （DE必须要 掌握非常好）
    - 1.Why SQL ?
        - 无论是传统RDBMS，MPP database， IMDB 还是BIG Data都需要SQL
    - 2. SQL 面试级别：
        - 
            
            ![https://api2.mubu.com/v3/document_image/ee02e14b-f104-4d26-a9df-e7ca4c58284f-14086676.jpg](https://api2.mubu.com/v3/document_image/ee02e14b-f104-4d26-a9df-e7ca4c58284f-14086676.jpg)
            
- 2. Data Warehouse
    - 1. DW 结构
        - 一个滞后的平台，需要把transaction的信息extract出来，放到DW中才能去做分析、数据产品和reporting。
            
            ![https://api2.mubu.com/v3/document_image/53ebb09d-c855-4f10-a8bb-c6d36fb952c7-14086676.jpg](https://api2.mubu.com/v3/document_image/53ebb09d-c855-4f10-a8bb-c6d36fb952c7-14086676.jpg)
            
        - 从transaction system 到DW的过程，两者之间倒过来倒过去的过程就叫Data pipeline, DE 在一开始时的大多数工作都是在做pipeline
    - 1. Inmon Model VS Kimball Model
        - 1. Inmon 与Kimball的结构图
            
            ![https://api2.mubu.com/v3/document_image/caed118d-69b4-4896-8f8a-4350f9bdfda3-14086676.jpg](https://api2.mubu.com/v3/document_image/caed118d-69b4-4896-8f8a-4350f9bdfda3-14086676.jpg)
            
        - 2.Inmon 难点在于design，适合比较大的公司，有足够的预算，业务成熟，需要花1到2年时间去建立一个centralized 的DW（需要符合3NF），但做出来后缺点就很少，没有信息差，产品成熟
        - 3. Kimball 反过来，适合中小公司，需要时间短，主需要要把与自身业务相关性比较强的resource抓取过来，把source变成dimension的模式（不需要3NF要求），不同的部门可以同时进行开发。
        - 知识补充：An OLAP cube is a data structure that overcomes the limitations of relational databases by providing rapid analysis of data. Cubes can display and sum large amounts of data while also providing users with searchable access to any data points.
            - example: An OLAP Cube is a data structure that allows fast analysis of data according to the multiple Dimensions that define a business problem. A multidimensional cube for reporting sales might be, for example, composed of 7 Dimensions: Salesperson, Sales Amount, Region, Product, Region, Month, Year.
    - 2.Data Vault 2.0
        - 周期3-5年，特别复杂，只有少数大型企业使用
            
            ![https://api2.mubu.com/v3/document_image/f5f1f821-3b8c-4386-ba65-dc2a8b6e24be-14086676.jpg](https://api2.mubu.com/v3/document_image/f5f1f821-3b8c-4386-ba65-dc2a8b6e24be-14086676.jpg)
            
    - 3. DW VS Data Lake
        - DW 与DL 的最基础的差别在于，DL储存的是raw文件，原始数据是什么样的，存进来就是什么样的，为了未来潜在的运用做准备。而DW 经过ETL 原始数据会发生改变。例如DW中储存的是table，而DL储存的是files。
            
            ![https://api2.mubu.com/v3/document_image/3713eb0d-9c1b-4514-a4a4-3b2991029961-14086676.jpg](https://api2.mubu.com/v3/document_image/3713eb0d-9c1b-4514-a4a4-3b2991029961-14086676.jpg)
            
        - 类比：DW 做前菜处理，根据顾客诉求做菜做产品。DL把菜放到冰箱里，存起来，为未来需求做准备。
    - 4. what is data
        - byte = 8 bits， 文件大小是以byte来计数的
            
            ![https://api2.mubu.com/v3/document_image/3df86fd9-d2e1-40b3-b344-ebc51680c0cf-14086676.jpg](https://api2.mubu.com/v3/document_image/3df86fd9-d2e1-40b3-b344-ebc51680c0cf-14086676.jpg)
            
        - ACSII & UTF8 & UTF16
            - 
                
             ![https://api2.mubu.com/v3/document_image/2d7b3713-5b16-45d0-8175-f62c109bb961-14086676.jpg](https://api2.mubu.com/v3/document_image/2d7b3713-5b16-45d0-8175-f62c109bb961-14086676.jpg)
                
        - Data Storage Measurements
            - 
                
             ![https://api2.mubu.com/v3/document_image/933446f7-0b55-4008-b001-3c4877bc8e1f-14086676.jpg](https://api2.mubu.com/v3/document_image/933446f7-0b55-4008-b001-3c4877bc8e1f-14086676.jpg)
                
- 3. DBMS
    - 1、什么是DBMS？
        - is a software that storing and retrieving user's data by considering appropriate security measures.
        - It consists of a group of programs which manipulate the database and provide an interface between the database. It includes the user of the database and other application programs.
        - The DBMS accepts the request for data from an application and instructs the operating system to provide the specific data. In large systems, a DBMS helps users and other third-party software to store and retrieve data.
    - 2、DBMS有什么特征？
        - 1.represent some aspects of real world applications
            - A database represents some features of real world applications. Any change in the real world is reflected in the database. For example, let us take railway reservation system; we have in our mind some certain applications of maintaining records of attendance, waiting list, train arrival and departure time, certain day etc. related to each train.
            - 现实中的事物是可以被量化表达的，才可以被储存在数据库中
        - 2.self describing nature
            - A database is of self describing nature; it always describes and narrates itself. It contains the description of the whole data structure, the constraints and the variables. It makes it different from traditional file management system in which definition was not the part of application program. These definitions are used by the users and DBMS software when needed. it not only contains the database itself, but also metadata which defines and describes the data and relationships between tables in the database.
            - 自己表达自己，例如用metadata来定义和表述数据库之间数据与table的关系
        - 3.logical relationship between records and data
            - A database gives a logical relationship between its records and data. So a user can access various records depending upon the logical conditions by a single query from the database.
            - 例如foreign key的使用，讲两个表通过一定的逻辑关系联系在一起
        - 4. Control Data Redundancy
            - DBMS follows the rules of normalization, which splits a relation when any of its attributes is having redundancy in values. Normalization is a mathematically rich and scientific process that reduces data redundancy.
            - 软性标准，完整储存信息，又不破坏数据结构
        - 5. Query Language
            - DBMS is equipped with query language, which makes it more efficient to retrieve and manipulate data. A user can apply as many and as different filtering options as required to retrieve a set of data. Traditionally it was not possible where file-processing system was used.
        - 6. Multiuser and Concurrent Access
            - DBMS supports multi-user environment and allows them to access and manipulate data in parallel. Though there are restrictions on transactions when users attempt to handle the same data item, but users are always unaware of them.
            - 允许很多users，并且允许很多users同时访问系统
        - 7. Multiple views of database
            - Basically, a view is a subset of the database. A view is defined and devoted for a particular user of the system.Different users of the system may have different views of the same system. Every view contains only the data of interest to a user or a group of users. It is the responsibility of users to be aware of how and where the data of their interest is stored.
            - View是一个logical expression。把view删了不会影响数据库
        - 8. Security
            - Features like multiple views offer security to some extent where users are unable to access data of other users and departments. DBMS offers methods to impose constraints while entering data into the database and retrieving the same at a later stage. DBMS offers many different levels of security features, which enables multiple users to have different views with different features. For example, a user in the Sales department cannot see the data that belongs to the Purchase department. Additionally, it can also be managed how much data of the Sales department should be displayed to the user. Since a DBMS is not saved on the disk as traditional file systems, it is very hard for miscreants to break the code.
            - column security (让特殊的列unable to access)和row security，row security很难达到
        - 9. ACID Properties
            - DBMS follows the concepts of Atomicity(Abort/commit), Consistency, Isolation, and Durability (normally shortened as ACID) in order to ensure accuracy, completeness, and data integrity. These concepts are applied on transactions, which manipulate data in a database.
            - Atomicity 原子性：不可以有两种状态，要么完成要么不完成，不可以是中间模棱两可的状态
            - Consistency 一致性： 数据库一个改变，相关的table都要发生改变，这个transaction是完整的。例如转账，主账户转了20块到子账户，那主账户要减少20，子账户相应要增加20.
            - Isolation 绝缘性：multiple users 使用接入到数据库时，用户与用户之间是隔断的，一个用户的session不会影响别人的访问。
            - Durability 持续性：分software和hardware两部分，软件出现问题，对底层的数据是没有影响的。
    - 3、Advantages of DBMS
        -  
            ![https://api2.mubu.com/v3/document_image/80733c87-58a2-4518-b72a-72be299ec577-14086676.jpg](https://api2.mubu.com/v3/document_image/80733c87-58a2-4518-b72a-72be299ec577-14086676.jpg)
            
    - 4、Disadvantages of DBMS
        - 贵！！
            
            ![https://api2.mubu.com/v3/document_image/c70d9bef-fd58-4d63-b6d6-9149337edcaf-14086676.jpg](https://api2.mubu.com/v3/document_image/c70d9bef-fd58-4d63-b6d6-9149337edcaf-14086676.jpg)
            
    - 5、Components of DBMS
        - 
            
            ![https://api2.mubu.com/v3/document_image/793ab2b0-9222-4316-8f38-55c7d7f519f9-14086676.jpg](https://api2.mubu.com/v3/document_image/793ab2b0-9222-4316-8f38-55c7d7f519f9-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/38c3ca37-1e64-4585-a9f1-3b175aa7b627-14086676.jpg](https://api2.mubu.com/v3/document_image/38c3ca37-1e64-4585-a9f1-3b175aa7b627-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/9a6b3958-d03e-436b-9f67-6771149f82fb-14086676.jpg](https://api2.mubu.com/v3/document_image/9a6b3958-d03e-436b-9f67-6771149f82fb-14086676.jpg)
            
    - 6、3种database DBMS architecture
        - 1-tier DBMS architecture
            - 一台机器完成全部工作：eg个人电脑
                
             ![https://api2.mubu.com/v3/document_image/403b686e-2e1b-4b6d-a1c1-bb0873dbf3b4-14086676.jpg](https://api2.mubu.com/v3/document_image/403b686e-2e1b-4b6d-a1c1-bb0873dbf3b4-14086676.jpg)
                
            - 很少用于production中
        - 2-tier DBMS architecture
            - business 中用的最多，有client 端和server端
            - 结构图
                
                ![https://api2.mubu.com/v3/document_image/d3243d05-ef7c-4267-8224-58705ca89e90-14086676.jpg](https://api2.mubu.com/v3/document_image/d3243d05-ef7c-4267-8224-58705ca89e90-14086676.jpg)
                
            - presentation layers runs on a client(PC, Mobile, Tablet, etc)
            - Data is store on a server.
            - An application interface which is called ODBC(Open Database Connectivity) an API which allows the client-side program to call theDBMS. Today most of the DBMS offers ODBC drivers for their DBMS. 2 tier architecture provides added security to the DBMS as it is not exposed to the end user directly.Example Enterprise Intranet Access with Teradata SQL Assistant.
        - 3-tier DBMS architecture
            - 增加了一个database layer， 分的更仔细，更方便我们现在使用的服务，例如online shopping
            - 每一层万一出问题时，我们可以在对应的层上fix， 也运用到big data上面了
            - 结构图
                
             ![https://api2.mubu.com/v3/document_image/746b4939-59ae-4ced-9f3c-2fda5beba603-14086676.jpg](https://api2.mubu.com/v3/document_image/746b4939-59ae-4ced-9f3c-2fda5beba603-14086676.jpg)
                
            - 3-tier schema is an extension of the 2-tier architecture. 3-tier architecture has following
                - layersPresentation layer (your PC, Tablet, Mobile, etc.)
                - Application layer (server)
                - Database Server
            - E.g. Online Shopping Website (Amazon), BI service(Tableau/Power BI )...
            - This DBMS architecture contains an Application layer between the user and the DBMS, which is responsible for communicating the user's request to theDBMS system and send the response from the DBMS to the user. The application layer(business logic layer) also processes functional logic, constraint, and rules before passing data to the user or down to the DBMS. Three tier architecture is the most popular DBMS architecture.
            - The goal of Three-tier architecture is:
                - To separate the user applications and physical database
                - Proposed to support DBMS characteristics
                - Program-data independence
                - Support of multiple views of the data
- 3. Big data ecosystem
    - 1. Hadoop 数据仓库架构
        - 
            
            ![https://api2.mubu.com/v3/document_image/6f014cdd-189f-47d6-b808-4c67f84b69e3-14086676.jpg](https://api2.mubu.com/v3/document_image/6f014cdd-189f-47d6-b808-4c67f84b69e3-14086676.jpg)
            
        - 1. 以batch的方式录入数据（以主动的方式），例如业务数据、外部数据是sqoop. ELk 是一个打包服务，监控功能
        - 2. streaming （passive的方式），kafka队列传到Spark streaming处理
            - End2End 在各大企业里不是很通用，因为成本大大增加
        - 3. Cassandra/Redis/MySQL 视图储存数据库
            - 数据安全管理等，都是辅助处理， inhouse 服务
        - 4. Hbase基本不使用，直接使用HDFS文本系统，通过伪数据层Hive给user SQL
        - 5. 应用部分，eg. PowerBI
    - 2. Super Lite
        - 1. system 偏技术层面
            
            ![https://api2.mubu.com/v3/document_image/7a487766-fe94-41c9-9c94-85bdc194422e-14086676.jpg](https://api2.mubu.com/v3/document_image/7a487766-fe94-41c9-9c94-85bdc194422e-14086676.jpg)
            
            - Yarn是一种 resource management system，做好traffic control
            - spark 做searching engine, 给技术人员使用，但贵；一般人员用MapReduce， 用普通硬盘就可以实现，但慢
        - 2. data flow 更偏架构方面
            
            ![https://api2.mubu.com/v3/document_image/3f62960d-8b2f-4f68-9bb4-6331dc01a454-14086676.jpg](https://api2.mubu.com/v3/document_image/3f62960d-8b2f-4f68-9bb4-6331dc01a454-14086676.jpg)
            
            - source layer = date lake， 1:1， 根据公司需求而定
            - silver layer 做了一些数据的transformation，对应到了一定的data map
            - gold layer 更精简，数据降级最多，aggregation
- 4. Types of Database Model
    - 1. Flat-File Database Model
        - FF 是独立的，中间没有可编辑的relationship
            
            ![https://api2.mubu.com/v3/document_image/10c27cbd-9f00-42e2-aec2-50e83520a353-14086676.jpg](https://api2.mubu.com/v3/document_image/10c27cbd-9f00-42e2-aec2-50e83520a353-14086676.jpg)
            
    - 2. Hierarchical Database Model
        - 父子级关系， 可以变成1-1， 也可以1-many
            
            ![https://api2.mubu.com/v3/document_image/6861b3dd-8e44-44d9-812c-d545190acb4d-14086676.jpg](https://api2.mubu.com/v3/document_image/6861b3dd-8e44-44d9-812c-d545190acb4d-14086676.jpg)
            
    - 3. Network Database Model
        - 还是一个root， 可以实现many-many
            
            ![https://api2.mubu.com/v3/document_image/17031c0f-ae06-42a1-a80f-06f13535dc53-14086676.jpg](https://api2.mubu.com/v3/document_image/17031c0f-ae06-42a1-a80f-06f13535dc53-14086676.jpg)
            
    - 4. Entity-relationship Model
        - RDBMS 出现以后，有了ER model
            
            ![https://api2.mubu.com/v3/document_image/3bcf23fc-7372-46f9-a616-ff285cddfa6a-14086676.jpg](https://api2.mubu.com/v3/document_image/3bcf23fc-7372-46f9-a616-ff285cddfa6a-14086676.jpg)
            
    - 5. Relational Model
        - 表示ER diagram怎么操作的，eg. star schema
            
            ![https://api2.mubu.com/v3/document_image/29166b40-de5c-4038-b16b-1d3648a0ac86-14086676.jpg](https://api2.mubu.com/v3/document_image/29166b40-de5c-4038-b16b-1d3648a0ac86-14086676.jpg)
            
- 5. Data Modelling
    - 0.在设计DW 很重要的部分
        - 
            
            ![https://api2.mubu.com/v3/document_image/0fe2dbdd-31ce-445f-a6b3-c80151f0de68-14086676.jpg](https://api2.mubu.com/v3/document_image/0fe2dbdd-31ce-445f-a6b3-c80151f0de68-14086676.jpg)
            
    - 1. Three kinds of data model instance
        - 1. Conceptual schema， 最high level的，是很rough的design
            - 
                
             ![https://api2.mubu.com/v3/document_image/446008a7-db71-4441-9fe0-deb4261645d7-14086676.jpg](https://api2.mubu.com/v3/document_image/446008a7-db71-4441-9fe0-deb4261645d7-14086676.jpg)
                
        - 2. Logical schema， 做完了Conceptual schema, relationship具象化出来
            - 
                
             ![https://api2.mubu.com/v3/document_image/f1929b2f-3413-4358-8a7e-088c7b020b8b-14086676.jpg](https://api2.mubu.com/v3/document_image/f1929b2f-3413-4358-8a7e-088c7b020b8b-14086676.jpg)
                
        - 3. Physical schema， 完整版表达，给Developer使用
            - 
                
             ![https://api2.mubu.com/v3/document_image/8c870103-19be-48d9-9669-beca17a4782b-14086676.jpg](https://api2.mubu.com/v3/document_image/8c870103-19be-48d9-9669-beca17a4782b-14086676.jpg)
                
             ![https://api2.mubu.com/v3/document_image/e91f71a2-9769-40be-a5e9-39f9e51e5714-14086676.jpg](https://api2.mubu.com/v3/document_image/e91f71a2-9769-40be-a5e9-39f9e51e5714-14086676.jpg)
                
- 6. ER Model:
    - 1.Basic concept
        - 1. Entity and Entity Set
            - eg. 学生 --》entity；所用
                
                ![https://api2.mubu.com/v3/document_image/37526e74-05ef-4fcf-89de-c7122b78d081-14086676.jpg](https://api2.mubu.com/v3/document_image/37526e74-05ef-4fcf-89de-c7122b78d081-14086676.jpg)
                
        - 2. Attributes
            - simple attributes不可再被分割的。
                
                ![https://api2.mubu.com/v3/document_image/1e108d9d-6fcd-43a4-8eeb-0615b4a2f0e0-14086676.jpg](https://api2.mubu.com/v3/document_image/1e108d9d-6fcd-43a4-8eeb-0615b4a2f0e0-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/8652c3af-aec7-4273-8d30-bfb766df453e-14086676.jpg](https://api2.mubu.com/v3/document_image/8652c3af-aec7-4273-8d30-bfb766df453e-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/7c19b06d-1b62-4f9b-98e5-286a010fefdf-14086676.jpg](https://api2.mubu.com/v3/document_image/7c19b06d-1b62-4f9b-98e5-286a010fefdf-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/bdc635aa-1431-46a9-bb8f-9154239eabc0-14086676.jpg](https://api2.mubu.com/v3/document_image/bdc635aa-1431-46a9-bb8f-9154239eabc0-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/06e4c57d-f37d-4003-bf21-2cc45f0f846d-14086676.jpg](https://api2.mubu.com/v3/document_image/06e4c57d-f37d-4003-bf21-2cc45f0f846d-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/2be25596-ea12-4646-8873-6c662f586d24-14086676.jpg](https://api2.mubu.com/v3/document_image/2be25596-ea12-4646-8873-6c662f586d24-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/e664ce6d-314c-48b1-aebc-0856455fbf38-14086676.jpg](https://api2.mubu.com/v3/document_image/e664ce6d-314c-48b1-aebc-0856455fbf38-14086676.jpg)
                
            - Derived attributes, eg. age
            - single value attribute , eg. 西方人生日
            - Multi value att , eg. phone, home phone, work phone
        - 3. keys
            - 所有能代表唯一性的key 都叫 SK。CK在SK中选，PK又在CK中选
                
                ![https://api2.mubu.com/v3/document_image/0aa7527a-3035-4442-b129-5de99d33e7dc-14086676.jpg](https://api2.mubu.com/v3/document_image/0aa7527a-3035-4442-b129-5de99d33e7dc-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/76d7ea83-6649-4949-92ef-24221d27b960-14086676.jpg](https://api2.mubu.com/v3/document_image/76d7ea83-6649-4949-92ef-24221d27b960-14086676.jpg)
                
            - 备选key : secondary key
            - FK
                
                ![https://api2.mubu.com/v3/document_image/04025a36-4f11-4baa-a2c7-05198b9b6ca6-14086676.jpg](https://api2.mubu.com/v3/document_image/04025a36-4f11-4baa-a2c7-05198b9b6ca6-14086676.jpg)
                
            - relationships
                
                ![https://api2.mubu.com/v3/document_image/806f344c-249e-48ed-b160-bd1cbda201b8-14086676.jpg](https://api2.mubu.com/v3/document_image/806f344c-249e-48ed-b160-bd1cbda201b8-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/9a45e230-e921-4afe-8409-5c59e5cafa2f-14086676.jpg](https://api2.mubu.com/v3/document_image/9a45e230-e921-4afe-8409-5c59e5cafa2f-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/fc564d85-7e29-4d8a-8d9c-61796a41247d-14086676.jpg](https://api2.mubu.com/v3/document_image/fc564d85-7e29-4d8a-8d9c-61796a41247d-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/f6bb79f7-8889-4dcf-a89d-2a0152ddb5f5-14086676.jpg](https://api2.mubu.com/v3/document_image/f6bb79f7-8889-4dcf-a89d-2a0152ddb5f5-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/ac8a5856-0649-40e9-a485-85f831fa486d-14086676.jpg](https://api2.mubu.com/v3/document_image/ac8a5856-0649-40e9-a485-85f831fa486d-14086676.jpg)
                
    - 2. Creating ER Diagram
        - 0. preview
            - 
                
                ![https://api2.mubu.com/v3/document_image/dcdf4dff-aebb-424e-ada8-6bbc1179157b-14086676.jpg](https://api2.mubu.com/v3/document_image/dcdf4dff-aebb-424e-ada8-6bbc1179157b-14086676.jpg)
                
        - 1. Components of ER Diagram
            - 
                
                ![https://api2.mubu.com/v3/document_image/b4f23c86-0e20-4608-95c0-9462ee24d2ed-14086676.jpg](https://api2.mubu.com/v3/document_image/b4f23c86-0e20-4608-95c0-9462ee24d2ed-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/af1d0672-4add-4e91-9754-1300f4abfd86-14086676.jpg](https://api2.mubu.com/v3/document_image/af1d0672-4add-4e91-9754-1300f4abfd86-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/21e8e5cb-b95a-49c7-a7b6-ffecec989189-14086676.jpg](https://api2.mubu.com/v3/document_image/21e8e5cb-b95a-49c7-a7b6-ffecec989189-14086676.jpg)
                
        - 2.Entity
            - 
                
                ![https://api2.mubu.com/v3/document_image/29ae2ffe-0504-4cfa-9b8d-4fbd9e98018d-14086676.jpg](https://api2.mubu.com/v3/document_image/29ae2ffe-0504-4cfa-9b8d-4fbd9e98018d-14086676.jpg)
                
        - 3.Week Entity
            - 不能单独存在的entity，eg. a apartment room => building
                
                ![https://api2.mubu.com/v3/document_image/4d1a0900-aab4-4438-9d0a-0e388e8a525a-14086676.jpg](https://api2.mubu.com/v3/document_image/4d1a0900-aab4-4438-9d0a-0e388e8a525a-14086676.jpg)
                
        - 4.Relationship
            - 
                
                ![https://api2.mubu.com/v3/document_image/9d71631b-c770-45a4-b57e-b272e7fab17b-14086676.jpg](https://api2.mubu.com/v3/document_image/9d71631b-c770-45a4-b57e-b272e7fab17b-14086676.jpg)
                
        - 5. Binary Relationship
            - 
                
                ![https://api2.mubu.com/v3/document_image/b7cb3db6-8404-4cc9-83fc-8e09eb363cbd-14086676.jpg](https://api2.mubu.com/v3/document_image/b7cb3db6-8404-4cc9-83fc-8e09eb363cbd-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/78a40544-1aea-41bb-9438-4214c9905416-14086676.jpg](https://api2.mubu.com/v3/document_image/78a40544-1aea-41bb-9438-4214c9905416-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/e420ac42-2686-4571-9f95-df8e094077c9-14086676.jpg](https://api2.mubu.com/v3/document_image/e420ac42-2686-4571-9f95-df8e094077c9-14086676.jpg)
                
        - 6. Recursive Relationship
            - 一个entity有两个属性，极端表达的存在，如
                
                ![https://api2.mubu.com/v3/document_image/6429f880-ff1b-4b29-b320-7a5585a4b2e1-14086676.jpg](https://api2.mubu.com/v3/document_image/6429f880-ff1b-4b29-b320-7a5585a4b2e1-14086676.jpg)
                
        - 7. Total/Partial Participation
            - eg. Total participation : 1 , 一定会enroll一个course，Partial Participation : 0 , 不是所有的course都能被enroll
                
                ![https://api2.mubu.com/v3/document_image/3a51a624-ec15-4696-b166-1500ae946275-14086676.jpg](https://api2.mubu.com/v3/document_image/3a51a624-ec15-4696-b166-1500ae946275-14086676.jpg)
                
        - 8. Ternary Relationship
            - 
                
                ![https://api2.mubu.com/v3/document_image/8a389d4f-1581-4600-8a5d-99482bf2ee6d-14086676.jpg](https://api2.mubu.com/v3/document_image/8a389d4f-1581-4600-8a5d-99482bf2ee6d-14086676.jpg)
                
        - 9. Generalization and Specialization
            - Generalization
                - 将两个low level的entities 合并成一个higher level 的entity。用的多
                    
                    ![https://api2.mubu.com/v3/document_image/3d32df5a-5bb8-439f-8031-1a3e6455b9bb-14086676.jpg](https://api2.mubu.com/v3/document_image/3d32df5a-5bb8-439f-8031-1a3e6455b9bb-14086676.jpg)
                    
            - Specialization
                - 将一个high level的entity拆分成两个lower level 的entities。少用，工作量会大大加大，double工作量。
                    
                    ![https://api2.mubu.com/v3/document_image/db71cd62-f3db-4ce3-a489-c99cf547789c-14086676.jpg](https://api2.mubu.com/v3/document_image/db71cd62-f3db-4ce3-a489-c99cf547789c-14086676.jpg)
                    
            - Aggregation
                - 将两个entities看成一个entity。eg. UNI和course合起来做单独的处理
                    
                    ![https://api2.mubu.com/v3/document_image/2f313533-a24e-4c39-9d50-3490b8f3e031-14086676.jpg](https://api2.mubu.com/v3/document_image/2f313533-a24e-4c39-9d50-3490b8f3e031-14086676.jpg)
                    
            - Inheritance
                - 有点像Python中的子类继承父类的属性
                    
                    ![https://api2.mubu.com/v3/document_image/54c4f040-baac-4164-90cb-971ff889371b-14086676.jpg](https://api2.mubu.com/v3/document_image/54c4f040-baac-4164-90cb-971ff889371b-14086676.jpg)
