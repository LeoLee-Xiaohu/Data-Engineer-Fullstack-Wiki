# Lecture03DBMS & SQL Intro

- 0.导读
    - 课间休息的问题都很有意义，可以回看
    - 
        
        ![https://api2.mubu.com/v3/document_image/22894286-1e7c-447d-9b44-5872aeb151bd-14086676.jpg](https://api2.mubu.com/v3/document_image/22894286-1e7c-447d-9b44-5872aeb151bd-14086676.jpg)
        
    - 额外知识补充
        - 1. schema的通俗解释：
            - 我们可以可以把Database看作是一个大仓库，仓库分了很多很多的房间，Schema就是其中的房间，一个Schema代表一个房间，Table可以看作是每个Schema中的床，Table（床）就被放入每个房间中，不能放置在房间之外，那岂不是晚上睡觉无家可归了J。，然后床上可以放置很多物品，就好比Table上可以放置很多列和行一样，数据库中存储数据的基本单元是Table，现实中每个仓库放置物品的基本单位就是床， User就是每个Schema的主人，（所以Schema包含的是Object，而不是User），其实User是对应与数据库的（即User是每个对应数据库的主人），既然有操作数据库（仓库）的权利，就肯定有操作数据库中每个Schema（房间）的权利，就是说每个数据库映射的User有每个Schema（房间）的钥匙，换句话说，如果他是某个仓库的主人，那么这个仓库的使用权和仓库中的所有东西都是他的（包括房间），他有完全的操作权，可以扔掉不用的东西从每个房间，也可以放置一些有用的东西到某一个房间，呵呵，和现实也太相似了吧。我还可以给User分配具体的权限，也就是他到某一个房间能做些什么，是只能看（Read-Only），还是可以像主人一样有所有的控制权（R/W），这个就要看这个User所对应的角色Role了，至于分配权限的问题，我留在以后单独的blog中详述。比喻到这里，相信大家都清楚了吧。来源：[https://www.cnblogs.com/NewPigJack/p/8000904.html](https://www.cnblogs.com/NewPigJack/p/8000904.html)
- 1. Codd's 12 rule of RDBMS
    - 做的系统要符合科德12准则，完整的RDBMS的特性，解释为什么要装hive，spark
    - Rule 1: Information Rule
        - 与self-discribe ability 相似
        - The data stored in a database, may it be user data or metadata, must be a value of some table cell. Everything in a database must be stored in a table format.
        - E.g. show databases; show tables;
    - Rule 2: Guaranteed Access Rule
        - 能有良好的环境允许query去access，尽管这个query很复杂，如万行query。
        - Every single data element (value) is guaranteed to be accessible logically with a combination of table-name, primary-key (row value), and attribute-name (column value).
        - Most RDBMS do not make the definition of the primary key mandatory and are deficient to that extent .
        - E.g. Use very complex SQL to retrieve information.
    - Rule 3: Systematic Treatment of NULL Values
        - 
            
            ![https://api2.mubu.com/v3/document_image/84fe23c0-bbb8-40b7-84ec-29f178253dee-14086676.jpg](https://api2.mubu.com/v3/document_image/84fe23c0-bbb8-40b7-84ec-29f178253dee-14086676.jpg)
            
    - Rule 4: Active Online Catalog
        - The structure description of the entire database must be stored in an online catalog, known as data dictionary, which can be accessed by authorized users. Users can use the same query language to access the catalog which they use to access the database itself.
    - Rule 5: Comprehensive Data Sub-Language Rule
        - 
            
            ![https://api2.mubu.com/v3/document_image/9631c097-8538-4d22-a23c-760ffff5f2a8-14086676.jpg](https://api2.mubu.com/v3/document_image/9631c097-8538-4d22-a23c-760ffff5f2a8-14086676.jpg)
            
    - Rule 6: View Updating Rule
        - table是一个physical existence，view是一个logical existence。
            
            ![https://api2.mubu.com/v3/document_image/f112e4d3-e7f2-47c8-949b-51581595f648-14086676.jpg](https://api2.mubu.com/v3/document_image/f112e4d3-e7f2-47c8-949b-51581595f648-14086676.jpg)
            
    - Rule 7: High-Level Insert, update and delete rule
        - 
            
            ![https://api2.mubu.com/v3/document_image/783e99a8-5a89-4cba-84a8-48d9ff31436a-14086676.jpg](https://api2.mubu.com/v3/document_image/783e99a8-5a89-4cba-84a8-48d9ff31436a-14086676.jpg)
            
    - Rule 8: Physical Data Independence
        - application是application，数据是数据，两者分开
            
            ![https://api2.mubu.com/v3/document_image/9037c546-3f51-4885-8d4e-36bf74c94ff4-14086676.jpg](https://api2.mubu.com/v3/document_image/9037c546-3f51-4885-8d4e-36bf74c94ff4-14086676.jpg)
            
    - Rule 9: Logical Data Independence
        - 改底层逻辑不影响query access，很难
            
            ![https://api2.mubu.com/v3/document_image/93d73b0d-c8c0-42e5-ba8c-6ec993a4cb20-14086676.jpg](https://api2.mubu.com/v3/document_image/93d73b0d-c8c0-42e5-ba8c-6ec993a4cb20-14086676.jpg)
            
    - Rule 10: Integrity Independence
        - 前端修改不影响后端数据的完整性
            
            ![https://api2.mubu.com/v3/document_image/929de830-d8b2-44dd-9867-4ad46e22cddb-14086676.jpg](https://api2.mubu.com/v3/document_image/929de830-d8b2-44dd-9867-4ad46e22cddb-14086676.jpg)
            
    - Rue 11: Distribution Independence
        - 节点备份，Hadoop 1:3，一个节点损坏，还有3个可以备份回数据
            
            ![https://api2.mubu.com/v3/document_image/e1f8af7a-f82d-4a39-92f6-5cf36254249e-14086676.jpg](https://api2.mubu.com/v3/document_image/e1f8af7a-f82d-4a39-92f6-5cf36254249e-14086676.jpg)
            
    - Rule 12: Non-subversion Rule
        - 跟产品相关的rule，重要，要记一下
            
            ![https://api2.mubu.com/v3/document_image/86e66721-2dc0-4c23-83b9-fbbb857d52e6-14086676.jpg](https://api2.mubu.com/v3/document_image/86e66721-2dc0-4c23-83b9-fbbb857d52e6-14086676.jpg)
            
        - 需要输入很大的数据，而insert很慢，所以系统提供Bulk copy会非常快地导入数据。
        - 在输入时，disable constraint，如果不这样做，没插入一下数据都要进行一次效验，这样效率都会特别低
- 2. Basic Concepts of RDBMS
    - 1. 数据库三种储存：
        - 1. table形式储存
            - 
                
                ![https://api2.mubu.com/v3/document_image/a5717810-b4ff-4e82-bb39-294305e9f250-14086676.jpg](https://api2.mubu.com/v3/document_image/a5717810-b4ff-4e82-bb39-294305e9f250-14086676.jpg)
                
        - 2. tuple形式储存（row based）
            - 
                
                ![https://api2.mubu.com/v3/document_image/fcbee848-8804-40e2-a3dc-bb7294f46418-14086676.jpg](https://api2.mubu.com/v3/document_image/fcbee848-8804-40e2-a3dc-bb7294f46418-14086676.jpg)
                
        - 3. Attribute, column based的形式储存
            - 
                
                ![https://api2.mubu.com/v3/document_image/45c21d3f-e6d9-4af5-ba1b-a0c03df89124-14086676.jpg](https://api2.mubu.com/v3/document_image/45c21d3f-e6d9-4af5-ba1b-a0c03df89124-14086676.jpg)
                
    - 2. Relation Schema
        - table schema
            
            ![https://api2.mubu.com/v3/document_image/8075d8f2-60c2-430d-ad75-de8eeb06c246-14086676.jpg](https://api2.mubu.com/v3/document_image/8075d8f2-60c2-430d-ad75-de8eeb06c246-14086676.jpg)
            
        - 要分清楚什么是DB schema，什么是table schema，如图
        - 知识拓展：
            - 介绍relation schema and relation diagram : [https://www.geeksforgeeks.org/relation-schema-in-dbms/](https://www.geeksforgeeks.org/relation-schema-in-dbms/)
                
                ![https://api2.mubu.com/v3/document_image/9147a691-4bab-4a17-bfe1-3a9c4daacd74-14086676.jpg](https://api2.mubu.com/v3/document_image/9147a691-4bab-4a17-bfe1-3a9c4daacd74-14086676.jpg)
                
    - 3. Relation Key
        - 
            
            ![https://api2.mubu.com/v3/document_image/979824fd-0aeb-4845-a3e9-18bd818cbd29-14086676.jpg](https://api2.mubu.com/v3/document_image/979824fd-0aeb-4845-a3e9-18bd818cbd29-14086676.jpg)
            
    - 4. Relational Integrity Constraints
        - 0.
            - 
                
                ![https://api2.mubu.com/v3/document_image/00702c03-4b19-45c6-b53b-3a0d4e5052b7-14086676.jpg](https://api2.mubu.com/v3/document_image/00702c03-4b19-45c6-b53b-3a0d4e5052b7-14086676.jpg)
                
        - 1. The three main Integrity Constraints are:
            - 1. Key Constraints
                - 0.
                    - 在大的层面上，定义constraint
                        
                        ![https://api2.mubu.com/v3/document_image/2551a584-9fb8-4f88-bb5f-2c668202ef08-14086676.jpg](https://api2.mubu.com/v3/document_image/2551a584-9fb8-4f88-bb5f-2c668202ef08-14086676.jpg)
                        
                - NOT NULL Constraint− Ensures that a column cannot have NULL value.
                - DEFAULT Constraint− Provides a default value for a column when none is specified.
                - UNIQUE Constraint− Ensures that all values in a column are different.
                - PRIMARY Key− Uniquely identifies each row/record in a database table.
                - FOREIGN Key− Uniquely identifies a row/record in any of the given database table.
                - CHECK Constraint− The CHECK constraint ensures that all the values in a column satisfies certain conditions.e.g. check(GENDER in ('Male', 'Female', 'Unknown'))
                - INDEX− Used to create and retrieve data from the database very quickly. 在transaction 系统中用的，在DW有可能会用，每一次增加信息，每一次都要更新index。可以在更新的时候，先把index drop掉，在更新完后再添加index
            - 2. Domain Constraints
                - Domain constraints refers to the rules defined for the values that can be stored for a certain attribute.
                - Like we explained above, we cannot store Address of employee in the column for Name.
                - The data type of domain includes string, character, integer, time, date, currency, etc.
                    
                    ![https://api2.mubu.com/v3/document_image/2824028a-5d91-4384-8f35-e1fece3dc222-14086676.jpg](https://api2.mubu.com/v3/document_image/2824028a-5d91-4384-8f35-e1fece3dc222-14086676.jpg)
                    
            - 3. Referential integrity Constraints
                - E.g. if I say XXXXX is my wife, then a lady with name XXXXX should also exist for that relationship to be present.
                    
                    ![https://api2.mubu.com/v3/document_image/901d0dcd-4fbd-4cbc-a9a1-664904b09f56-14086676.jpg](https://api2.mubu.com/v3/document_image/901d0dcd-4fbd-4cbc-a9a1-664904b09f56-14086676.jpg)
                    
                - 绝对不会在transaction system中出现
- 3. Relational Algebra
    - Relational algebra is a procedural query language, which takes instances of relations as input and yields instances of relations as output. It uses operators to perform queries.An operator can be either unary or binary. They accept relations as their input and yield relations as their output. Relational algebra is performed recursively on a relation and intermediate results are also considered relations.
    - Select
        - 
            
            ![https://api2.mubu.com/v3/document_image/4caac808-84de-4f52-89ce-a5b186242ef9-14086676.jpg](https://api2.mubu.com/v3/document_image/4caac808-84de-4f52-89ce-a5b186242ef9-14086676.jpg)
            
    - Project
        - 选择特定的column
        - 
            
            ![https://api2.mubu.com/v3/document_image/7659d0ff-bda2-4b21-9ce3-7b2e6f65eb33-14086676.jpg](https://api2.mubu.com/v3/document_image/7659d0ff-bda2-4b21-9ce3-7b2e6f65eb33-14086676.jpg)
            
    - Union
        - union是deduplication的，去除两者的重复部分
            
            ![https://api2.mubu.com/v3/document_image/ae0cd67b-fee5-4547-a94e-1351d5c36497-14086676.jpg](https://api2.mubu.com/v3/document_image/ae0cd67b-fee5-4547-a94e-1351d5c36497-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/97443c2e-0f6b-4899-a19e-fca944afdbc5-14086676.jpg](https://api2.mubu.com/v3/document_image/97443c2e-0f6b-4899-a19e-fca944afdbc5-14086676.jpg)
            
        - SQL中保留所有信息，不去重，用union all
    - Intersection
        - 有点像inner join
            
            ![https://api2.mubu.com/v3/document_image/d5454ae4-cd19-4425-abc2-737673a0f2ff-14086676.jpg](https://api2.mubu.com/v3/document_image/d5454ae4-cd19-4425-abc2-737673a0f2ff-14086676.jpg)
            
    - Set Different
        - eg.查询没有下单的customer
            
            ![https://api2.mubu.com/v3/document_image/f814073b-8c0e-423a-937f-0f06d019cb43-14086676.jpg](https://api2.mubu.com/v3/document_image/f814073b-8c0e-423a-937f-0f06d019cb43-14086676.jpg)
            
    - Cartesian product 笛卡尔积
        - 所有链接的可能性都表达出来
        - 相当于cross join，cross join数据库系统不一定都有
            
            ![https://api2.mubu.com/v3/document_image/e09655b0-9b92-4595-8773-b92a457f8c67-14086676.jpg](https://api2.mubu.com/v3/document_image/e09655b0-9b92-4595-8773-b92a457f8c67-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/8cd8bc30-a751-4699-b997-5aff7b0890fe-14086676.jpg](https://api2.mubu.com/v3/document_image/8cd8bc30-a751-4699-b997-5aff7b0890fe-14086676.jpg)
            
        - 工业中有，但在特定情况下使用
    - Rename
        - 
            
            ![https://api2.mubu.com/v3/document_image/c0d5fa1f-c4af-4844-a1c3-05df052304c7-14086676.jpg](https://api2.mubu.com/v3/document_image/c0d5fa1f-c4af-4844-a1c3-05df052304c7-14086676.jpg)
            
    - 课外延伸：[https://www.cnblogs.com/clap-of-thunder/p/15332530.html](https://www.cnblogs.com/clap-of-thunder/p/15332530.html)
- 4. ER model to Relational Model (怎么mapping？）
    - 1. Mapping Entity
        - 1. Create table for each entity. 字符太长，超过限制，用简写表达（在knowledge management中储存），table与entity一一对应
        - 2. Entity's attributes should become fields of tables with their respective data types.
        - 3. Declare primary key. DW中尽量避免物理上的PK定义
        - 实例
            - 主要针对transaction database，完整的entity schema中还要有data type
                
                ![https://api2.mubu.com/v3/document_image/e8da9b43-2fd4-4de8-82a8-44c135faa835-14086676.jpg](https://api2.mubu.com/v3/document_image/e8da9b43-2fd4-4de8-82a8-44c135faa835-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/c98d180b-d478-41e5-88fa-b1b8ca12cf6f-14086676.jpg](https://api2.mubu.com/v3/document_image/c98d180b-d478-41e5-88fa-b1b8ca12cf6f-14086676.jpg)
                
    - 2. Mapping Relationship
        - primary key针对transaction database，而不是for data warehouse，不需要将primary key的constraint等信息储存在data warehouse中。如果data warehouse是小规模的，只需要data warehouse的计算功能，即使知道primary key也不用物理标注出来，节省空间，让系统能够更有效运行。
            
            ![https://api2.mubu.com/v3/document_image/135fe2d3-5ea5-47ba-984d-18f7ca6b5423-14086676.jpg](https://api2.mubu.com/v3/document_image/135fe2d3-5ea5-47ba-984d-18f7ca6b5423-14086676.jpg)
            
        - 
            
            ![https://api2.mubu.com/v3/document_image/4c391986-59b8-4925-8f19-5d3071068d4d-14086676.jpg](https://api2.mubu.com/v3/document_image/4c391986-59b8-4925-8f19-5d3071068d4d-14086676.jpg)
            
        - relationship table, 还有n1, n2, n3...（由于位置有限，没放上来），将 AccNo, SSN 拿回原表，都将是primary key. relationship table 要两个Foreign key放到一起才可以表示唯一性。
            
            ![https://api2.mubu.com/v3/document_image/458426e7-e769-4558-9392-276f421eb207-14086676.jpg](https://api2.mubu.com/v3/document_image/458426e7-e769-4558-9392-276f421eb207-14086676.jpg)
            
    - 3. Mapping Weak Entity Sets
        - week entity: 一个entity不能单独的存在，必须依存与另一个entity。
            
            ![https://api2.mubu.com/v3/document_image/fd200acb-e56a-47d0-9fb0-fbe5efeae96f-14086676.jpg](https://api2.mubu.com/v3/document_image/fd200acb-e56a-47d0-9fb0-fbe5efeae96f-14086676.jpg)
            
        - 方法
            - 
                
                ![https://api2.mubu.com/v3/document_image/685801f0-e48b-4d76-a126-6b95c3c5fa72-14086676.jpg](https://api2.mubu.com/v3/document_image/685801f0-e48b-4d76-a126-6b95c3c5fa72-14086676.jpg)
                
        - 一个识别吗BranchNo 和 Bank code 组成一个统一的primary key
            
            ![https://api2.mubu.com/v3/document_image/e146fa57-ae2b-4661-a992-35e9b4768225-14086676.jpg](https://api2.mubu.com/v3/document_image/e146fa57-ae2b-4661-a992-35e9b4768225-14086676.jpg)
            
    - 4. Mapping Hierarchical Entities
        - 了解即可。Hierarchical entities are organized in a tree structure. They are composed of parents and children. The root entity has no parent and is the ancestor of all the other entities.
            
            ![https://api2.mubu.com/v3/document_image/21a1b715-3593-4125-9f6f-b1ac9a4afae9-14086676.jpg](https://api2.mubu.com/v3/document_image/21a1b715-3593-4125-9f6f-b1ac9a4afae9-14086676.jpg)
            
- 5. Type of Database Key
    - Super Key
    - Candidate Key
    - Primary Key
    - Secondary or Alternative key
    - Foreign Key
        - 
            
            ![https://api2.mubu.com/v3/document_image/d3fbb2e0-c8be-4c3c-aece-9d31534cc89e-14086676.jpg](https://api2.mubu.com/v3/document_image/d3fbb2e0-c8be-4c3c-aece-9d31534cc89e-14086676.jpg)
            
    - Compound Key
        - 
            
            ![https://api2.mubu.com/v3/document_image/c23afe69-28db-4f01-9522-0a2d0bf53985-14086676.jpg](https://api2.mubu.com/v3/document_image/c23afe69-28db-4f01-9522-0a2d0bf53985-14086676.jpg)
            
    - Composite Key
        - 和compound key基本一码事，不用纠结定义
            
            ![https://api2.mubu.com/v3/document_image/52d13459-6857-4388-8bc9-90a8c72a9aa3-14086676.jpg](https://api2.mubu.com/v3/document_image/52d13459-6857-4388-8bc9-90a8c72a9aa3-14086676.jpg)
            
    - Nature key
        - 一种primary key拿出database是有实际意义的
            - eg. 身份证ID，drive license
                
                ![https://api2.mubu.com/v3/document_image/60b53b8e-f4cd-446b-859f-9f917e89b28f-14086676.jpg](https://api2.mubu.com/v3/document_image/60b53b8e-f4cd-446b-859f-9f917e89b28f-14086676.jpg)
                
    - Surrogate Key
        - 与Nature Key相反，拿出database没有实际意义，定义：a primary key which is internally generated that does not exist in the real world.
            - eg. ID=1 for Customer A and ID=2 for Customer B serves to uniquely identify the record but has no bearing the customer themselves and is an attribute they will never (need to) be aware of.
            - 表示状态的变化，因为有时PK无法表达数据变迁下的变化，如下图
                
                ![https://api2.mubu.com/v3/document_image/1c734d16-fb02-4107-8d8c-38acf35bc29c-14086676.jpg](https://api2.mubu.com/v3/document_image/1c734d16-fb02-4107-8d8c-38acf35bc29c-14086676.jpg)
                
        - surrogate key 主要应用在data warehouse 中
- 6. Database Normalization (重要！2：10)
    - normalization 合理的把信息储存在DW中，主要解决两个问题，冗余 （data redundancy)和异常(anomaly)。
        - 数据工程操作是正向的过程(normalize)，使用是逆向的过程denormalize，eg. big flat file。例如XIAOLU同学的城市发生改变，如果没有normalize的话得更新很多次（假设有上万条XIAOLU的记录），如果normalize了，只需要更新一次城市信息，就可以更新所有的XIAOLU的记录。
        - data warehouse 只要做到第三层NF就可以了。照顾了原子性就会造成join次数越多，系统负荷越大
        - 但是Transaction database 必须要做到完全原子化，NNF。
        - 以下这张表是denormalization 过了的表，在原始状态下不可能有denormalized 表。
            
            ![https://api2.mubu.com/v3/document_image/3b5eb003-4f38-45c3-9b05-15193d0d400f-14086676.jpg](https://api2.mubu.com/v3/document_image/3b5eb003-4f38-45c3-9b05-15193d0d400f-14086676.jpg)
            
    - Normalization steps:
        - 做到4层，data warehouse 做到第三层。BCNF代表3.5层
            - 
                
                ![https://api2.mubu.com/v3/document_image/20eda612-b087-4ae0-b13c-28a14396f209-14086676.jpg](https://api2.mubu.com/v3/document_image/20eda612-b087-4ae0-b13c-28a14396f209-14086676.jpg)
                
        - 1NF (Normal Form):
            - 第一步拿到的表是未完全原子化的，eg. acccount type 未原子化
                
                ![https://api2.mubu.com/v3/document_image/d66e35ec-fb46-45ee-be9e-875a9a060ba7-14086676.jpg](https://api2.mubu.com/v3/document_image/d66e35ec-fb46-45ee-be9e-875a9a060ba7-14086676.jpg)
                
            - 转化成允许局部的duplication 但是一部分是unique的这种状态。把这种两个数据在同一单元格中的信息，解开就行了。例如以下表格状态，account type原子化。
                - 这一步的output:
                    
                    ![https://api2.mubu.com/v3/document_image/c1535acc-8d78-4fc1-a708-b32e6b054734-14086676.jpg](https://api2.mubu.com/v3/document_image/c1535acc-8d78-4fc1-a708-b32e6b054734-14086676.jpg)
                    
        - 2NF：
            - 第二步相对更严谨，要分清什么是prime attribute 和 non-prime attribute
                - Prime attribute − An attribute, which is a part of the candidate-key, is known as a prime attribute.
                - Non-prime attribute − An attribute, which is not a part of the prime-key, is said to be a non-prime attribute. 不是PK 都属于Non-prime attributes。
                - 图例
                    
                    ![https://api2.mubu.com/v3/document_image/37e82a6d-b7da-4648-80a6-91b0bc7eb03c-14086676.jpg](https://api2.mubu.com/v3/document_image/37e82a6d-b7da-4648-80a6-91b0bc7eb03c-14086676.jpg)
                    
            - 接着1NF中的数据，解决partial dependency.
                - It should be in the First Normal form.
                - It should not have Partial Dependency.
                    - Functional dependency (FD) is a relationship between two attributes, typically between the PK and other non-key attributes within a table. Functional Dependency is when one attribute determines another attribute in a DBMS system.
                        - 知识补充：[https://www.guru99.com/dbms-functional-dependency.html#:~:text=Functional%20Dependency%20(FD)%20is%20a,good%20and%20bad%20database%20design.](https://www.guru99.com/dbms-functional-dependency.html#:~:text=Functional%20Dependency%20(FD)%20is%20a,good%20and%20bad%20database%20design.)
                            - 3 Rules of determine FD:
                                - Reflexive rule –. If X is a set of attributes and Y is_subset_of X, then X holds a value of Y.
                                - Augmentation rule: When x -> y holds, and c is attribute set, then ac -> bc also holds. That is adding attributes which do not change the basic dependencies.
                                - Transitivity rule: This rule is very much similar to the transitive rule in algebra if x -> y holds and y -> z holds, then x -> z also holds. X -> y is called as functionally that determines y.
                            - 4 Types of FD in DBMS:
                                - There are mainly four types of Functional Dependency in DBMS. Following are the types of Functional Dependencies in DBMS:
                                - Multivalued Dependency
                                    - Multivalued dependency occurs in the situation where there are multiple independent multivalued attributes in a single table. A multivalued dependency is a complete constraint between two sets of attributes in a relation. It requires that certain tuples be present in a relation.
                                    - example:
                                        - 
                                            
                                            ![https://api2.mubu.com/v3/document_image/02433ed1-f8e3-4a65-80f9-49cbf80d69d7-14086676.jpg](https://api2.mubu.com/v3/document_image/02433ed1-f8e3-4a65-80f9-49cbf80d69d7-14086676.jpg)
                                            
                                - Trivial Functional Dependency
                                    - The Trivial dependency is a set of attributes which are called a trivial if the set of attributes are included in that attribute.
                                    - So, X -> Y is a trivial functional dependency if Y is a subset of X.是一个数组组合的形式。
                                    - example：
                                        - 
                                            
                                            ![https://api2.mubu.com/v3/document_image/4dafe349-0a4a-41f9-9c73-84549fee2365-14086676.jpg](https://api2.mubu.com/v3/document_image/4dafe349-0a4a-41f9-9c73-84549fee2365-14086676.jpg)
                                            
                                - Non-Trivial Functional Dependency
                                    - Functional dependency which also known as a nontrivial dependency occurs when A->B holds true where B is not a subset of A. In a relationship, if attribute B is not a subset of attribute A, then it is considered as a non-trivial dependency.
                                    - example：
                                        - 
                                            
                                            ![https://api2.mubu.com/v3/document_image/c1811bbb-fb30-4412-b810-65c89d3d0f4b-14086676.jpg](https://api2.mubu.com/v3/document_image/c1811bbb-fb30-4412-b810-65c89d3d0f4b-14086676.jpg)
                                            
                                - Transitive Dependency
                                    - A Transitive Dependency is a type of functional dependency which happens when “t” is indirectly formed by two functional dependencies.
                                    - Example
                                        
                                        ![https://api2.mubu.com/v3/document_image/fd955e5c-8092-4e64-bec8-efe215313191-14086676.jpg](https://api2.mubu.com/v3/document_image/fd955e5c-8092-4e64-bec8-efe215313191-14086676.jpg)
                                        
                            - summary:
                                - Axiom, Decomposition, Dependent, Determinant, Union are key terms for functional dependency
                                - Four types of functional dependency are 1) Multivalued 2) Trivial 3) Non-trivial 4) Transitive
                                - Multivalued dependency occurs in the situation where there are multiple independent multivalued attributes in a single table
                                - The Trivial dependency occurs when a set of attributes which are called a trivial if the set of attributes are included in that attribute
                                - Nontrivial dependency occurs when A->B holds true where B is not a subset of A
                                - A transitive is a type of functional dependency which happens when it is indirectly formed by two functional dependencies
                                - Normalization is a method of organizing the data in the database which helps you to avoid data redundancy
                    - Partial Dependency occurs when a non-prime attribute is functionally dependent on part of a candidate key.
            - 这一步的output：
                - customer table中FK（account ID） 要保留，不然联系不起来account table
                    
                    ![https://api2.mubu.com/v3/document_image/20ee7b60-050e-4a64-ba20-6bd4414919e4-14086676.jpg](https://api2.mubu.com/v3/document_image/20ee7b60-050e-4a64-ba20-6bd4414919e4-14086676.jpg)
                    
        - 3NF：
            - It is in the Second Normal form. Remove Transitive Dependency.
                - Transitive Dependency. When a non-prime attribute depends on other non-prime attributes rather than depending upon the prime attributes or primary key.
            - 要移除Transitive dependancy, 因为Transitive dependency 会变，例如post_code 和City (suburb), post_code 现实世界中会每三个月更新一次。
                
                ![https://api2.mubu.com/v3/document_image/e7472fa2-3ccf-4ade-be3d-744bb1f1d232-14086676.jpg](https://api2.mubu.com/v3/document_image/e7472fa2-3ccf-4ade-be3d-744bb1f1d232-14086676.jpg)
                
            - Output:
                - 将city，country分解出来了，保证了主表的唯一性，当post code, city, country在现实世界中发生了改变时，直接在city表中更新就能更新到主表中了。
                    
                    ![https://api2.mubu.com/v3/document_image/5276afb3-23f0-4724-a160-082faae5134d-14086676.jpg](https://api2.mubu.com/v3/document_image/5276afb3-23f0-4724-a160-082faae5134d-14086676.jpg)
                    
        - BCNF ( Boyce and Codd Normal Form):
            - BCNF is stricter than 3NF.
                - For any dependency A → B, A should be a super key.
                - Namely, for a dependency A → B, A cannot be a non-prime attribute, if B is a prime attribute.
            - account ID 依赖于 client manager（不依赖于customer ID），但是client manager 又不是prime attribute. 这种情况需要BCNF。解决依赖的对象不是prime key, 但又需要key to key 对应的要求。
                
                ![https://api2.mubu.com/v3/document_image/e128e3ce-3646-46ff-b7a3-5bd59fb35977-14086676.jpg](https://api2.mubu.com/v3/document_image/e128e3ce-3646-46ff-b7a3-5bd59fb35977-14086676.jpg)
                
            - output:
                - 将account ID 剥离出来，从而达到原表中，每个attributes都只依赖于 prime attribute。
                    
                    ![https://api2.mubu.com/v3/document_image/4649fb4a-3181-41f3-a626-424c49b47c67-14086676.jpg](https://api2.mubu.com/v3/document_image/4649fb4a-3181-41f3-a626-424c49b47c67-14086676.jpg)
                    
        - 4NF：
            - It should be in the Boyce-Codd Normal Form.
            - The table should not have any Multi-valued Dependency.
            - 这里customer_ID -> property, customer_ID -> vehicle 是multi-valued dependency，需要进一步拆解，因为不拆解的话，每更新一次property或者vehicle都要考虑这两个在同一张表的更新。
                
                ![https://api2.mubu.com/v3/document_image/157ea1ad-1fca-483f-a248-fcb03eca754d-14086676.jpg](https://api2.mubu.com/v3/document_image/157ea1ad-1fca-483f-a248-fcb03eca754d-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/3c025a36-330a-4b34-abac-4749b8d78215-14086676.jpg](https://api2.mubu.com/v3/document_image/3c025a36-330a-4b34-abac-4749b8d78215-14086676.jpg)
                
            - 树形的关系，动任何一个节点都可能破坏原有的意义，所以要把这种逻辑关系进行处理
            - output:
                
                ![https://api2.mubu.com/v3/document_image/e3468b97-ba11-4427-ada8-95672ee368e4-14086676.jpg](https://api2.mubu.com/v3/document_image/e3468b97-ba11-4427-ada8-95672ee368e4-14086676.jpg)
                
- 7. SQL introduction
    - 1. DDL--data definition language
        - CREATE – create the database or its objects (like table, index, function, views, storeprocedure and triggers).
            - DW建立时，可以不用建PK
                
                ![https://api2.mubu.com/v3/document_image/12acd149-0258-43c2-affc-99d92f817afc-14086676.jpg](https://api2.mubu.com/v3/document_image/12acd149-0258-43c2-affc-99d92f817afc-14086676.jpg)
                
        - DROP – delete objects from the database.
            - 
                
                ![https://api2.mubu.com/v3/document_image/509276d2-18d6-4ca0-bc99-9ff30add6a6c-14086676.jpg](https://api2.mubu.com/v3/document_image/509276d2-18d6-4ca0-bc99-9ff30add6a6c-14086676.jpg)
                
        - ALTER – alter the structure of the database.
            - 在实际工业中用不到这个，要考虑版本的变迁，原来的旧的表更改后不是扔掉，而是备份起来。
                
                ![https://api2.mubu.com/v3/document_image/add46aa6-c3c1-41d2-810b-9bb2883792c3-14086676.jpg](https://api2.mubu.com/v3/document_image/add46aa6-c3c1-41d2-810b-9bb2883792c3-14086676.jpg)
                
        - TRUNCATE – remove all records from a table, including all spaces allocated for there cords are removed. 记住这个，属于DDL，不是DML，保持数据原有结构，但是抹除所有信息
        - COMMENT – add comments to the data dictionary.
            - 注释功能，把error可以narrow down到特定区间
                
                ![https://api2.mubu.com/v3/document_image/aba30739-8bc6-4abd-9de1-38a3569fd595-14086676.jpg](https://api2.mubu.com/v3/document_image/aba30739-8bc6-4abd-9de1-38a3569fd595-14086676.jpg)
                
        - RENAME – rename an object existing in the database.
            - 在实际工业中用不到这个
                
                ![https://api2.mubu.com/v3/document_image/cf4e0dc5-8836-4bb4-9312-6c908d55ae46-14086676.jpg](https://api2.mubu.com/v3/document_image/cf4e0dc5-8836-4bb4-9312-6c908d55ae46-14086676.jpg)
                
    - 2. DML（重要！）
        - SELECT
            - 
                
                ![https://api2.mubu.com/v3/document_image/3ef7ff31-5e33-4f1c-94fe-ba126f3067fa-14086676.jpg](https://api2.mubu.com/v3/document_image/3ef7ff31-5e33-4f1c-94fe-ba126f3067fa-14086676.jpg)
                
        - INSERT
            - 
                
                ![https://api2.mubu.com/v3/document_image/eb0098d0-34fb-449f-84a7-307884ee2e56-14086676.jpg](https://api2.mubu.com/v3/document_image/eb0098d0-34fb-449f-84a7-307884ee2e56-14086676.jpg)
                
        - UPDATE
            - 要慎用，一定要记得带WHERE
                
                ![https://api2.mubu.com/v3/document_image/44c953b8-e087-4188-908a-d0ca952a30c2-14086676.jpg](https://api2.mubu.com/v3/document_image/44c953b8-e087-4188-908a-d0ca952a30c2-14086676.jpg)
                
        - DELETE
            - 要慎用，一定要记得带WHERE
                
                ![https://api2.mubu.com/v3/document_image/37bfc40b-11c6-4086-a4fd-13286b307a40-14086676.jpg](https://api2.mubu.com/v3/document_image/37bfc40b-11c6-4086-a4fd-13286b307a40-14086676.jpg)
                
    - 3. DCL(Data Control Language)
        - 给特定user特定的权限，大部分Data Engineer遇不到。。。。。
            
            ![https://api2.mubu.com/v3/document_image/bfb06071-fd43-4707-bff0-60ee4ea476c0-14086676.jpg](https://api2.mubu.com/v3/document_image/bfb06071-fd43-4707-bff0-60ee4ea476c0-14086676.jpg)
            
        - GRANT 赋予权限
            - 
                
                ![https://api2.mubu.com/v3/document_image/607487d2-37bf-4342-b471-09bebe6a69b8-14086676.jpg](https://api2.mubu.com/v3/document_image/607487d2-37bf-4342-b471-09bebe6a69b8-14086676.jpg)
                
        - REVOKE 取消权限
            - 
                
                ![https://api2.mubu.com/v3/document_image/c52bc591-f6db-44bc-bebf-97570ef4ce9c-14086676.jpg](https://api2.mubu.com/v3/document_image/c52bc591-f6db-44bc-bebf-97570ef4ce9c-14086676.jpg)
                
    - 4. TCL (transaction Control Language)
        - 0.对提交的过程也有一些管控
            - 
                
                ![https://api2.mubu.com/v3/document_image/6ddf6dc7-cbdd-451a-9303-78e0c09fe9f0-14086676.jpg](https://api2.mubu.com/v3/document_image/6ddf6dc7-cbdd-451a-9303-78e0c09fe9f0-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/87d3bfc6-ad89-4ab3-8eee-e17646a7a584-14086676.jpg](https://api2.mubu.com/v3/document_image/87d3bfc6-ad89-4ab3-8eee-e17646a7a584-14086676.jpg)
                
        - COMMIT– commits a Transaction.提交session，完成系统中的修改。
            - 建议把auto commit关闭掉
        - ROLLBACK– rollbacks a transaction in case of any error occurs.