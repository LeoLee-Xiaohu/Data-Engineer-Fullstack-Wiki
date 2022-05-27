# Lecture 14  Data warehouse1

- 0.导读
    - CTE recursive 也是在lecture15 讲的
    - 2，3，5是重点，必须要很好的掌握
        - 
            
            ![https://api2.mubu.com/v3/document_image/68c72105-0c86-4ab5-b38f-e390172fad70-14086676.jpg](https://api2.mubu.com/v3/document_image/68c72105-0c86-4ab5-b38f-e390172fad70-14086676.jpg)
            
    - 这节课的data warehouse 是泛Kimball类的
        - 现在几乎没有Data Marts了，直接user 到warehouse中取数
            
            ![https://api2.mubu.com/v3/document_image/2a5fd6cf-2607-4f4e-b0d1-dba99ce97549-14086676.jpg](https://api2.mubu.com/v3/document_image/2a5fd6cf-2607-4f4e-b0d1-dba99ce97549-14086676.jpg)
            
        - data warehouse主要用于报表，BI互动式报表，和做一些产品，挖掘对业务有利的潜在价值
        - transaction DB 主要用于日常交易，转账等等
    - 知识延伸：fact table 实例
        - 
            
            ![https://api2.mubu.com/v3/document_image/6d7d1f7a-8def-4e68-8707-b87fc1d79697-14086676.jpg](https://api2.mubu.com/v3/document_image/6d7d1f7a-8def-4e68-8707-b87fc1d79697-14086676.jpg)
            
- 1. Fundamental Concepts
    - 1.Gather business requirements and data realities
        - 在做数据产品之前要综合考虑商业要求和数据现实情况，跟business 的部门谈，将诉求document化
            
            ![https://api2.mubu.com/v3/document_image/321a033b-5e46-4bdd-a789-84dadb4a01a0-14086676.jpg](https://api2.mubu.com/v3/document_image/321a033b-5e46-4bdd-a789-84dadb4a01a0-14086676.jpg)
            
    - 2. Collaborative dimensional modeling workshops
        - 这个workshop 很重要，把ER diagram或data warehouse 的design做成一个demo，去给他们看，告诉他们根据我们现在手上已有的资源，我们能达到哪些哪些（可以预计的功能，Q& A的过程） ，哪些功能能达到，哪些功能不能达到。
            
            ![https://api2.mubu.com/v3/document_image/2025136d-e46c-45db-a621-dafe06d53b56-14086676.jpg](https://api2.mubu.com/v3/document_image/2025136d-e46c-45db-a621-dafe06d53b56-14086676.jpg)
            
    - 3. Four step dimensional design process
        - 套路化4步
            
            ![https://api2.mubu.com/v3/document_image/6bb7b42b-98fd-4f3f-9e9d-d0c5434e770f-14086676.jpg](https://api2.mubu.com/v3/document_image/6bb7b42b-98fd-4f3f-9e9d-d0c5434e770f-14086676.jpg)
            
            - 1. Business process。 明白为什么是这样的商业流程
                - 
                    
                    ![https://api2.mubu.com/v3/document_image/3ed759f7-4d59-49aa-8f24-9b4b5d23821b-14086676.jpg](https://api2.mubu.com/v3/document_image/3ed759f7-4d59-49aa-8f24-9b4b5d23821b-14086676.jpg)
                    
            - 2. 知道并定义grain，最小颗粒度(标准）是多大
                - grain 是apply到dimension上面，保持最低grain，grain越小，表达的信息可能就越全越强。grain必须要在dimension 之前确定。
                    
                    ![https://api2.mubu.com/v3/document_image/88abb477-57cb-40fa-8548-58d9118bf79f-14086676.jpg](https://api2.mubu.com/v3/document_image/88abb477-57cb-40fa-8548-58d9118bf79f-14086676.jpg)
                    
                    ![https://api2.mubu.com/v3/document_image/4d0f4c00-4fa7-4e14-9b17-47a20441707b-14086676.jpg](https://api2.mubu.com/v3/document_image/4d0f4c00-4fa7-4e14-9b17-47a20441707b-14086676.jpg)
                    
            - 3. Dimensions for descriptive context, 确定维度
                - dimension 提供5w1h的context，辅助我们最后fact table的表达
                    
                    ![https://api2.mubu.com/v3/document_image/e34c5a28-1b90-4df6-975a-7b9a2dc3e4e9-14086676.jpg](https://api2.mubu.com/v3/document_image/e34c5a28-1b90-4df6-975a-7b9a2dc3e4e9-14086676.jpg)
                    
            - 4. Facts for measurements
                - facts 很好衡量业务变化的情况，与上一周期的报告相比，是好还是坏，指标是增长了还是降低了。sensitive information 不建议用fact来表达，例如manager's salary.
                    
                    ![https://api2.mubu.com/v3/document_image/65816c06-093f-4558-b0c7-7c65793cbac1-14086676.jpg](https://api2.mubu.com/v3/document_image/65816c06-093f-4558-b0c7-7c65793cbac1-14086676.jpg)
                    
                - fact table 可通过dimension tables 去拓展信息的宽度 ==> star schema。Pk join FK。 注意fact table 里面的信息是可以duplicate的，但dimension table里面的信息是不可以duplicate的，必须unique。
                    
                    ![https://api2.mubu.com/v3/document_image/3e54523c-c3fd-4e0f-9688-e4220e11d09e-14086676.jpg](https://api2.mubu.com/v3/document_image/3e54523c-c3fd-4e0f-9688-e4220e11d09e-14086676.jpg)
                    
    - 4. Star schema and OLAP cubes
        - 一般是3 个dimension， XYZ.
            
            ![https://api2.mubu.com/v3/document_image/951802d6-16de-42c8-a1b8-c8de79c51797-14086676.jpg](https://api2.mubu.com/v3/document_image/951802d6-16de-42c8-a1b8-c8de79c51797-14086676.jpg)
            
        - 现在OLAP cubes 没那么流行了，微软全家桶用的少了
            
            ![https://api2.mubu.com/v3/document_image/e15586ba-5f39-4620-aec9-1a74a490de61-14086676.jpg](https://api2.mubu.com/v3/document_image/e15586ba-5f39-4620-aec9-1a74a490de61-14086676.jpg)
            
    - 5. Graceful Extensions to dimensional models
        - 对工业要求进行修改，需要对数据升级。先看dimension table 再看 fact table
            
            ![https://api2.mubu.com/v3/document_image/68e845da-fe87-49d1-87cb-51bddcf2366c-14086676.jpg](https://api2.mubu.com/v3/document_image/68e845da-fe87-49d1-87cb-51bddcf2366c-14086676.jpg)
            
- 2.Basic Dimension Table Techniques
    - 0. 一定要记住基础技术，高阶操作也就会了。数据操作没有完全正确的标准，只有适不适合。
        - 
            
            ![https://api2.mubu.com/v3/document_image/94f80728-8899-47a3-956c-d026650f9769-14086676.jpg](https://api2.mubu.com/v3/document_image/94f80728-8899-47a3-956c-d026650f9769-14086676.jpg)
            
    - 1. Dimension table structure
        - Primary Key column 是conceptual的，定义的PK是能代表业务需求的。
            
            ![https://api2.mubu.com/v3/document_image/ec822a23-1f27-48ae-b27e-a058544641c3-14086676.jpg](https://api2.mubu.com/v3/document_image/ec822a23-1f27-48ae-b27e-a058544641c3-14086676.jpg)
            
        - flat denormalized, 不需要做到很细
        - low-cardinality text attributes 例如yes/no， 1/0，总结性表述
            - 例如，可以用D01来表示 Lost Job， D02 --》bank currupt,....
                
                ![https://api2.mubu.com/v3/document_image/3e6fba1d-1cb6-460f-a7a8-be11e8706e45-14086676.jpg](https://api2.mubu.com/v3/document_image/3e6fba1d-1cb6-460f-a7a8-be11e8706e45-14086676.jpg)
                
        - PK，FK， SK
            
            ![https://api2.mubu.com/v3/document_image/fbbe4f83-abb0-4f9d-b4b2-2f4ceeab5fe4-14086676.jpg](https://api2.mubu.com/v3/document_image/fbbe4f83-abb0-4f9d-b4b2-2f4ceeab5fe4-14086676.jpg)
            
    - 2.Dimension surrogate keys
        - 从1开始的序列型key。时间维度是例外，处理时间时，不用1，2，3，4...这样的序列表述SK。
            
            ![https://api2.mubu.com/v3/document_image/9b54e33e-6617-4b82-bf6e-eb509f190436-14086676.jpg](https://api2.mubu.com/v3/document_image/9b54e33e-6617-4b82-bf6e-eb509f190436-14086676.jpg)
            
        - 允许多次录入
        - 表示数据的唯一性
            - 通过造一个SK，可以很好的查询dimension table中的信息，这里通过PK可能找不到，因为居住时间发生改变。例如，下面查询某位客户的在进行交易时所居住的城市
                
                ![https://api2.mubu.com/v3/document_image/69a1d896-7b24-4c9e-94be-f867b3ea7f1c-14086676.jpg](https://api2.mubu.com/v3/document_image/69a1d896-7b24-4c9e-94be-f867b3ea7f1c-14086676.jpg)
                
            - 有个区间表达，有状态的变化，如住址改变
                
                ![https://api2.mubu.com/v3/document_image/eaac5fda-2ae2-4ee6-b929-831282906d75-14086676.jpg](https://api2.mubu.com/v3/document_image/eaac5fda-2ae2-4ee6-b929-831282906d75-14086676.jpg)
                
    - 3. Natural, durable and supernatural keys
        - 定义
            
            ![https://api2.mubu.com/v3/document_image/704c70b5-3707-4865-aab8-050b6a026af2-14086676.jpg](https://api2.mubu.com/v3/document_image/704c70b5-3707-4865-aab8-050b6a026af2-14086676.jpg)
            
        - 记录BK和SK，SK会变，Durable key标记第一次ingest的record
            
            ![https://api2.mubu.com/v3/document_image/4fe9ac8b-a5fd-4c14-bc14-b3c132e75f4c-14086676.jpg](https://api2.mubu.com/v3/document_image/4fe9ac8b-a5fd-4c14-bc14-b3c132e75f4c-14086676.jpg)
            
        - 产品升级，BK 跟着升级，DK可以追溯到最早的SK。
            
            ![https://api2.mubu.com/v3/document_image/8cb5d63d-1f39-40b2-8e4e-0a140ccf38ee-14086676.jpg](https://api2.mubu.com/v3/document_image/8cb5d63d-1f39-40b2-8e4e-0a140ccf38ee-14086676.jpg)
            
        - super nature key （durable key）,老师没怎么用过，因为对系统的计算要求高，每次insert update都要计算最初的sk, 更新到dk 中
    - 4. Drilling down
        - 向下钻取，挖掘更细节的信息，group by 通过增加column来获取更佳细节的信息
            
            ![https://api2.mubu.com/v3/document_image/0684954e-22ea-4d45-8938-999bfe24ab09-14086676.jpg](https://api2.mubu.com/v3/document_image/0684954e-22ea-4d45-8938-999bfe24ab09-14086676.jpg)
            
    - 5. Degenerate Dimensions
        - 不需要原子化的信息，放到同一个dimension中去，减少join，减少ETL
            
            ![https://api2.mubu.com/v3/document_image/8fc718f5-594a-44a4-8321-b85077d20799-14086676.jpg](https://api2.mubu.com/v3/document_image/8fc718f5-594a-44a4-8321-b85077d20799-14086676.jpg)
            
        - 没有附加描述性信息 no description info，就不要再normalize 了，给Pipline ingestion 增加复杂度，还要再多join一次。这就需要一个Degeneration technique，将过度generated 的信息， degenerate
            
            ![https://api2.mubu.com/v3/document_image/e0b08ff8-0558-4adb-bc2b-83fc91a29d3c-14086676.jpg](https://api2.mubu.com/v3/document_image/e0b08ff8-0558-4adb-bc2b-83fc91a29d3c-14086676.jpg)
            
            - 如，issue number只有一个attribute，直接存在issue fact table中，可以normalize 但是我们不normalize ，因为没有必要，增加复杂度了
                
                ![https://api2.mubu.com/v3/document_image/be5f8457-69c8-440d-9dfc-1ad04f8b3f42-14086676.jpg](https://api2.mubu.com/v3/document_image/be5f8457-69c8-440d-9dfc-1ad04f8b3f42-14086676.jpg)
                
    - 6. Denormalized flattened dimensions
        - 
            
            ![https://api2.mubu.com/v3/document_image/5b524290-b74e-42f5-8ec2-504f57c066a3-14086676.jpg](https://api2.mubu.com/v3/document_image/5b524290-b74e-42f5-8ec2-504f57c066a3-14086676.jpg)
            
        - data warehouse 对于大类信息用一张表储存就可以了，不需要特别原子化。而transaction system，ETL需要将很细的原子化了的表格给denormalize 出来，方便用户select。data warehouse 和 transaction data system 是有很大的不同的。
            - 在transaction system可以，但在DW不合适
                
                ![https://api2.mubu.com/v3/document_image/d73156ae-8ee3-459e-ae74-447ee592a13e-14086676.jpg](https://api2.mubu.com/v3/document_image/d73156ae-8ee3-459e-ae74-447ee592a13e-14086676.jpg)
                
    - 7. multiple hierarchies in demensions
        - 
            
            ![https://api2.mubu.com/v3/document_image/2fff12aa-495e-4f47-837f-3d53bbea9ed2-14086676.jpg](https://api2.mubu.com/v3/document_image/2fff12aa-495e-4f47-837f-3d53bbea9ed2-14086676.jpg)
            
        - 有分叉的
            
            ![https://api2.mubu.com/v3/document_image/de8987b1-d452-40ef-b030-0dcfdff9f51f-14086676.jpg](https://api2.mubu.com/v3/document_image/de8987b1-d452-40ef-b030-0dcfdff9f51f-14086676.jpg)
            
        - 优点，可以对不同层次的信息进行统计，例如以年，月日统计
    - 8. Flags and indicators as dimension attributes
        - 用数字或字母描述大类，利于统计和趋势分析
            
            ![https://api2.mubu.com/v3/document_image/4dc60773-36c8-4a2b-a4db-0d6ea19b5d80-14086676.jpg](https://api2.mubu.com/v3/document_image/4dc60773-36c8-4a2b-a4db-0d6ea19b5d80-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/72096209-aac3-4278-9283-ac3517554c1e-14086676.jpg](https://api2.mubu.com/v3/document_image/72096209-aac3-4278-9283-ac3517554c1e-14086676.jpg)
            
    - 9. Null attributes in dimensions
        - dimension 中不要留NULL这样的形式，可以用Unk 或N/A 表示null
            
            ![https://api2.mubu.com/v3/document_image/b14e19ee-3e7e-4ace-8cd1-43c4c7a44c41-14086676.jpg](https://api2.mubu.com/v3/document_image/b14e19ee-3e7e-4ace-8cd1-43c4c7a44c41-14086676.jpg)
            
    - 10. Calendar Date Dimension
        - 它有自己的PK、 SK ，例如20220525
            
            ![https://api2.mubu.com/v3/document_image/8c815577-f864-471a-9eeb-d0f7545c1451-14086676.jpg](https://api2.mubu.com/v3/document_image/8c815577-f864-471a-9eeb-d0f7545c1451-14086676.jpg)
            
        - Calendar date dimension 是人工完成的，因为一些public holiday是会shift移动的，人工一次性做成一张大表是值得的。每个公司的Calendar dimension都不同，跟业务需求相关。
            
            ![https://api2.mubu.com/v3/document_image/92841f3c-0122-4efd-92ad-17d0f1e21f87-14086676.jpg](https://api2.mubu.com/v3/document_image/92841f3c-0122-4efd-92ad-17d0f1e21f87-14086676.jpg)
            
    - 11. Role playing dimensions
        - 在fact表格中，有不同的FK，对于到通一张dimension table中，同样的dimension 在不同的fact表中，表示的意义不同。例如fact table中不同的时间FK，对应到date dimension table中
            
            ![https://api2.mubu.com/v3/document_image/31185a9b-0fa0-416d-88c8-75f7b1bb7b8d-14086676.jpg](https://api2.mubu.com/v3/document_image/31185a9b-0fa0-416d-88c8-75f7b1bb7b8d-14086676.jpg)
            
        - A single physical dimension can be referenced multiple times in a fact table, with each reference linking to a logically distinct role for the dimension. For instance, a fact table can have several dates, each of which is represented by a foreign key to the date dimension. It is essential that each foreign key refers to a separate view of the date dimension so that the references are independent. These separate dimension views (with unique attribute column names) are called roles.
    - 12. Junk dimensions
        - 优化的结果，它可能是一些完全没有逻辑关系的组合，而出现的频率是相对固定的，把他集合起来，做junk dimension, 方便user 去 select . Junk dimension 是一个手动能控制的过程。
            
            ![https://api2.mubu.com/v3/document_image/e7a42e3e-5409-4f9c-8059-f754d204803f-14086676.jpg](https://api2.mubu.com/v3/document_image/e7a42e3e-5409-4f9c-8059-f754d204803f-14086676.jpg)
            
        - 例如，下面这三个很小的没有逻辑联系的dimension ，这里每个有3个cardinality, 有27种组合就可以用Junk Dimension 将它们组合起来放到一张dimension table 中，用Junk Key就能找到它们三个dimension的全部组合。这样只要join一次就可以了，不然要join三次，导致效率太低。这就是我们说的Data warehouse是存在一定的优化过程的。
            
            ![https://api2.mubu.com/v3/document_image/332da862-6935-4e9d-b52e-94925dcc2d9a-14086676.jpg](https://api2.mubu.com/v3/document_image/332da862-6935-4e9d-b52e-94925dcc2d9a-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/1d63cc54-29b1-489a-87c0-c484b1f7f1cc-14086676.jpg](https://api2.mubu.com/v3/document_image/1d63cc54-29b1-489a-87c0-c484b1f7f1cc-14086676.jpg)
            
        - 这种组合出现过一次就记录在在Junk dimension中，还是比较实用的
    - 13. Snowflaked dimensions
        - Snowflake 把dimension拆解到一种原子的状态，尤其是把heirachical
            
            ![https://api2.mubu.com/v3/document_image/36781624-044b-4f28-b475-4ba85bfcc2c4-14086676.jpg](https://api2.mubu.com/v3/document_image/36781624-044b-4f28-b475-4ba85bfcc2c4-14086676.jpg)
            
        - snowflake在工业中尽量不要用。分的太细，效率管理维护pipline都很麻烦。
            
            ![https://api2.mubu.com/v3/document_image/ba0ef895-a128-4b47-ac96-c620db4b8996-14086676.jpg](https://api2.mubu.com/v3/document_image/ba0ef895-a128-4b47-ac96-c620db4b8996-14086676.jpg)
            
    - 14. Outrigger dimensions
        - 与Junk dimension不一样，有点junk dimension 反过来 的意思。老师不推荐这种方式，因为要join回来，麻烦，尽量保持原有状态
        - 如果fact table中有一部分信息不是 static的，可以将它拽出来形成单独dimension，如变化的district , region. 有利于分析与预测，例如一个10年前没人的工业区，变成现在的居民社区，这种变迁对业务有比较大的影响，就要单独拉出来，map也会更好看，预测趋势也更准确。
            
            ![https://api2.mubu.com/v3/document_image/f88b466e-8455-49d3-bd6d-cda77faa4b2c-14086676.jpg](https://api2.mubu.com/v3/document_image/f88b466e-8455-49d3-bd6d-cda77faa4b2c-14086676.jpg)
            
        - 如果这些non static的信息（如地区）对业务没有那么强的影响，理论上不需要outrigger，保留在fact table中就可以了
- 3.Basic Fact Table Techniques
    - 1. Fact table structure
        - transaction system里面数据可能储存6个月，最多储存3年，而DW 可以储存n年
        - fact table 可以是原始的，也可以是经过处理的，取决于具体的诉求. 某些时候，measure 和fact可以分开，尤其是measure很长，更新fact不方便。大部分情况下，measure都会被放在fact table里面
            
            ![https://api2.mubu.com/v3/document_image/b0442ac2-bab1-4b0f-a136-276c51e433dd-14086676.jpg](https://api2.mubu.com/v3/document_image/b0442ac2-bab1-4b0f-a136-276c51e433dd-14086676.jpg)
            
        - fact table 里面还有其它的fact，fact 进行aggregation。fact table做计算做集合统计
            
            ![https://api2.mubu.com/v3/document_image/66bb9688-1463-4833-8c26-a9db02e04950-14086676.jpg](https://api2.mubu.com/v3/document_image/66bb9688-1463-4833-8c26-a9db02e04950-14086676.jpg)
            
        - 3种fact table：前两种不需要做refresh，可以做append，最后一种只能做refresh。
            
            ![https://api2.mubu.com/v3/document_image/9ee2df09-4ec1-405f-94b7-bcc9620fcc32-14086676.jpg](https://api2.mubu.com/v3/document_image/9ee2df09-4ec1-405f-94b7-bcc9620fcc32-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/fc7a1f8b-0696-4c13-9578-5c0341d3b494-14086676.jpg](https://api2.mubu.com/v3/document_image/fc7a1f8b-0696-4c13-9578-5c0341d3b494-14086676.jpg)
            
            - 1. Additive :累加，全部dimension能累加，例如昨天加今天的就可以计算的出来的fact，直接append
            - 2. Semi-additive : 部分dimension能累加，例如balance amount是semi-additive，它不能加time dimension。
            - 3. Non-additive : 不能通过累加计算出来，要全部重新计算一次的，例如ratio，profit margin, DE经常要用的表达。需要进行比较的，必须做join才能哪些信息是insert ， update， delete这三种状态。
            - 工业中，第一种第三种用的多，第三种refresh用的最多，refresh是fact table的常态
            - small to big: delta， 小比大，今天来了一小部分信息，要跟大的那部分比，今天新进的5百条和昨天的1万条比较
            - big to big : full compare , 昨天的snapshot与今天的snapshot比较，昨天1万条，今天1万5百条
                
                ![https://api2.mubu.com/v3/document_image/1629bef0-1007-4e8e-a853-cf6ed35a9b3d-14086676.jpg](https://api2.mubu.com/v3/document_image/1629bef0-1007-4e8e-a853-cf6ed35a9b3d-14086676.jpg)
                
    - 2.Null in fact tables
        - 与dimension一样，不能用null来表示空值
            
            ![https://api2.mubu.com/v3/document_image/d6eb5cf0-afe3-4017-b259-7f88460e0a2f-14086676.jpg](https://api2.mubu.com/v3/document_image/d6eb5cf0-afe3-4017-b259-7f88460e0a2f-14086676.jpg)
            
    - 3. Conformed facts
        - 共用，有交集的，
            
            ![https://api2.mubu.com/v3/document_image/bec10b97-8abe-4604-83a3-f0a52a95f326-14086676.jpg](https://api2.mubu.com/v3/document_image/bec10b97-8abe-4604-83a3-f0a52a95f326-14086676.jpg)
            
    - 4. Transaction fact table
        - 流水账。一般来讲，data warehouse 会产生一个T+1的效果。
            
            ![https://api2.mubu.com/v3/document_image/46c4c13d-4ae8-443a-bfc0-9d63640f6179-14086676.jpg](https://api2.mubu.com/v3/document_image/46c4c13d-4ae8-443a-bfc0-9d63640f6179-14086676.jpg)
            
        - transaction fact 没有summary，是一个Raw的处理
            
            ![https://api2.mubu.com/v3/document_image/51c935c1-0a74-484d-a71e-46c9a62a020c-14086676.jpg](https://api2.mubu.com/v3/document_image/51c935c1-0a74-484d-a71e-46c9a62a020c-14086676.jpg)
            
    - 5. Periodic snapshot fact tables
        - A row in a periodic snapshot fact table summarizes many measurement event soccurring over a standard period, such as a day, a week, or a month.
            
            ![https://api2.mubu.com/v3/document_image/b57de0f1-466e-4eb3-ae36-e885a0537fed-14086676.jpg](https://api2.mubu.com/v3/document_image/b57de0f1-466e-4eb3-ae36-e885a0537fed-14086676.jpg)
            
        - 需要aggregation达到的，这样的统计方式往往需要refresh
            
            ![https://api2.mubu.com/v3/document_image/74105540-2616-437f-8661-23cd887a17dc-14086676.jpg](https://api2.mubu.com/v3/document_image/74105540-2616-437f-8661-23cd887a17dc-14086676.jpg)
            
    - 6. Accumulating snapshot fact tables
        - 这个在工业中经常用到。表达格式和前两种不同，要用到partition by，研究某个特定行为的。例如，违约情况，状态1 违约，状态2 违约，状态3 不违约，进行回滚计算，得出结论这个人是否可靠，系统把他放到一个block list中
            
            ![https://api2.mubu.com/v3/document_image/bd2d14b6-7705-4e07-8209-8bc5caf03149-14086676.jpg](https://api2.mubu.com/v3/document_image/bd2d14b6-7705-4e07-8209-8bc5caf03149-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/58b0d4db-ee9f-4974-bd39-4fa4d0f539b6-14086676.jpg](https://api2.mubu.com/v3/document_image/58b0d4db-ee9f-4974-bd39-4fa4d0f539b6-14086676.jpg)
            
    - 7. Factless fact table
        - 通过summary，calculation 得到的信息录入到fact table，不是纯raw的，反向推导的，没有记录相关信息，推出某种信息。例如学生上课，attendance
            
            ![https://api2.mubu.com/v3/document_image/b88b8459-3974-407a-9478-2b0ef8f647e0-14086676.jpg](https://api2.mubu.com/v3/document_image/b88b8459-3974-407a-9478-2b0ef8f647e0-14086676.jpg)
            
        - DE基本用不到。
            
            ![https://api2.mubu.com/v3/document_image/71c2467a-1358-4bd1-8467-36518a142a72-14086676.jpg](https://api2.mubu.com/v3/document_image/71c2467a-1358-4bd1-8467-36518a142a72-14086676.jpg)
            
    - 8.Aggregated fact tables or cubes
        - 增加我们在使用时的效率，常用的信息直接在fact table中表现出来
            
            ![https://api2.mubu.com/v3/document_image/e44437dd-655c-4589-a896-f2a895ece706-14086676.jpg](https://api2.mubu.com/v3/document_image/e44437dd-655c-4589-a896-f2a895ece706-14086676.jpg)
            
        - Aggregation fact table 相当于给fact table 做 一个升级。对现在的fact table做一个summary，aggregate 一个table，是一对一的过程。
            
            ![https://api2.mubu.com/v3/document_image/49b996c4-6ead-406c-951f-cc366df8e4d2-14086676.jpg](https://api2.mubu.com/v3/document_image/49b996c4-6ead-406c-951f-cc366df8e4d2-14086676.jpg)
            
    - 9.Consolidated fact tables
        - 要先有Aggregation fact table。将n个fact table 合并到一张Fact table中，阐述一个完整的事实。做起来会比较复杂。是N到1的过程
            
            ![https://api2.mubu.com/v3/document_image/343ca266-897c-4625-a4c0-2a094209e3a8-14086676.jpg](https://api2.mubu.com/v3/document_image/343ca266-897c-4625-a4c0-2a094209e3a8-14086676.jpg)
            
        - campaign，比较没campaign的销售情况，campaign 的销售占比是不是有提高，有没有提升业绩
            
            ![https://api2.mubu.com/v3/document_image/607908b1-87bd-4cbe-8c8c-31d7e1ff1388-14086676.jpg](https://api2.mubu.com/v3/document_image/607908b1-87bd-4cbe-8c8c-31d7e1ff1388-14086676.jpg)
            
- 4.Integration via Conformed Dimensions
    - 1. Conformed dimensions
        - 两个不同的procedure中有重叠的dimension，有些dimension会被多个fact table重复用到
            
            ![https://api2.mubu.com/v3/document_image/ea0d4fd3-a1a7-499b-9d1b-39fbb6c2a591-14086676.jpg](https://api2.mubu.com/v3/document_image/ea0d4fd3-a1a7-499b-9d1b-39fbb6c2a591-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/83258f93-0ded-4d77-a021-0e9e5b4d5111-14086676.jpg](https://api2.mubu.com/v3/document_image/83258f93-0ded-4d77-a021-0e9e5b4d5111-14086676.jpg)
            
    - 2. Shrunken rollup dimensions
        - Shrunken dimensions are conformed dimensions that are a subset of rows and /or columns of a base dimension. 减少duplication。dimension特别繁杂，可能把dimension分出来，做subdimension，
            
            ![https://api2.mubu.com/v3/document_image/37d7cbba-051b-4639-ba94-0bb621c84eb7-14086676.jpg](https://api2.mubu.com/v3/document_image/37d7cbba-051b-4639-ba94-0bb621c84eb7-14086676.jpg)
            
        - 不是特别多，直接用复杂的就可以了，因为现在的计算能力提升
            
            ![https://api2.mubu.com/v3/document_image/39497688-5d9e-45e2-b503-ddc25e0bbd87-14086676.jpg](https://api2.mubu.com/v3/document_image/39497688-5d9e-45e2-b503-ddc25e0bbd87-14086676.jpg)
            
    - 3. Drilling across
        - 依靠BI的能力，一个表达方式
            
            ![https://api2.mubu.com/v3/document_image/e5bfa779-7ad9-46f0-ad3b-93a714450c89-14086676.jpg](https://api2.mubu.com/v3/document_image/e5bfa779-7ad9-46f0-ad3b-93a714450c89-14086676.jpg)
            
1. SCD techniques
    - 0. 此技术可以增加记录的保有量，可以记录更多有效的信息，避免信息丢失。
        - 
            
            ![https://api2.mubu.com/v3/document_image/8ae45e32-d400-4105-a7b2-863eaac96e0a-14086676.jpg](https://api2.mubu.com/v3/document_image/8ae45e32-d400-4105-a7b2-863eaac96e0a-14086676.jpg)
            
    - Type 1: Sometimes
        - Not exist. 过去的历史信息完全不保留（小作坊公司用的）会复写之前的记录，不保留China了。
            
            ![https://api2.mubu.com/v3/document_image/b7531e03-57be-4038-a07d-ff0b10317a93-14086676.jpg](https://api2.mubu.com/v3/document_image/b7531e03-57be-4038-a07d-ff0b10317a93-14086676.jpg)
            
    - Type 2: Frequently （业界公认标准）
        - 用SK 来保留历史信息，新进来的信息不删除掉，只是对expiry date 进行修改，将新进来的信息的date减去1就是 expiry date.
            
            ![https://api2.mubu.com/v3/document_image/bb913b17-4d33-43ea-81e5-f62cb8d8b495-14086676.jpg](https://api2.mubu.com/v3/document_image/bb913b17-4d33-43ea-81e5-f62cb8d8b495-14086676.jpg)
            
        - dummy record： 9999， bash information，
        - 区间，可以得到比较精致的报表
        - type 2 大多数公司使用的原因：既记录了历史信息的同时，又使用了最少的系统消耗。
    - Type 3 : Rarely
        - Type 1 与 type 2的结合体
        - 在实际中的工作中不推荐这种做法，因为计算量会比较大，对录入的performance是有影响的。记type 2 Frequently 就可以了。
            
            ![https://api2.mubu.com/v3/document_image/fcb35b77-0874-459c-9669-bfa139aebc8a-14086676.jpg](https://api2.mubu.com/v3/document_image/fcb35b77-0874-459c-9669-bfa139aebc8a-14086676.jpg)