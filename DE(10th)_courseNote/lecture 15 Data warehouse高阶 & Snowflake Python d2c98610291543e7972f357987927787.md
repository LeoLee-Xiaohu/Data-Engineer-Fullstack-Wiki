# C6 lecture15 Data warehouse高阶 & Snowflake Python

- 1.Advanced Fact Table Techniques
    - 1. Fact table surrogate key（SK）
        - SK internal，想要表达的是唯一性，用SK
            
            ![https://api2.mubu.com/v3/document_image/538360d4-43fc-4891-bcd3-08ff5294d9c5-14086676.jpg](https://api2.mubu.com/v3/document_image/538360d4-43fc-4891-bcd3-08ff5294d9c5-14086676.jpg)
            
        - fact table 要么是add 要么是refresh，加SK之后，开发成本或定义会变得更复杂，某些程度上还不如做一次refresh。所以听起来很好的功能，不见到值得开发，除了add或refresh的fact table，其它的都不采用SK。不用特别考虑Fact table 要做SK。
        - fact table 只要记住append 和refresh 就好了
    - 2. Centipede fact table
        - 比较完美的状况，不建议这么原子化的结构
            
            ![https://api2.mubu.com/v3/document_image/603824d9-9bd2-4162-9d0c-e332a5296d6b-14086676.jpg](https://api2.mubu.com/v3/document_image/603824d9-9bd2-4162-9d0c-e332a5296d6b-14086676.jpg)
            
        - 我们要解决的是grain这个topic，在能完整表达grain意思时就不要把table继续拆开了。
    - 3. Numeric values as attributes or facts
        - numeric 表达的颗粒度太广了，分级做range处理到fact table 会好点。例如，price区间设置成0-50， 50-100， ......
            
            ![https://api2.mubu.com/v3/document_image/7e0a4dde-51d6-46e9-805f-254b9504a302-14086676.jpg](https://api2.mubu.com/v3/document_image/7e0a4dde-51d6-46e9-805f-254b9504a302-14086676.jpg)
            
    - 4.Lag/duration facts
        - 很常见的业务需求，客户在某个特定时段是什么状态，为了ML的铺垫
            
            ![https://api2.mubu.com/v3/document_image/99ee84ed-fd68-438d-b548-b418cd0a3701-14086676.jpg](https://api2.mubu.com/v3/document_image/99ee84ed-fd68-438d-b548-b418cd0a3701-14086676.jpg)
            
    - 5.Header/line fact tables
        - 非常重要的fact table，有一个母系的entity有很多的子系，跟交易有关的都用这种方式， 例如超市的账单，order 是parent，巧克力，面包等等东西就是order details
            
            ![https://api2.mubu.com/v3/document_image/238ca1b2-664b-4854-b1c8-cd437fb2faac-14086676.jpg](https://api2.mubu.com/v3/document_image/238ca1b2-664b-4854-b1c8-cd437fb2faac-14086676.jpg)
            
        - 错误表达，不要分两个表，只要分开处理header和line就是不对的，要将可能对应的纹理降到最低，有一些duplication没有关系。transaction 是一个nature fact
            
            ![https://api2.mubu.com/v3/document_image/dac076ac-bad4-48ee-b596-854b47ec199b-14086676.jpg](https://api2.mubu.com/v3/document_image/dac076ac-bad4-48ee-b596-854b47ec199b-14086676.jpg)
            
        - transaction header 和 transaction line 从transaction来的时候是两个input，两个table，但DW正确表达要放到一个fact table中
        - 正确表达，header 和line放在一个fact table中，不要拆开。dimension 颗粒度一定要最低。可以接受适度的重复，重复主要是在header中的，很少。
            
            ![https://api2.mubu.com/v3/document_image/86adb142-7b50-4515-8656-1231925fdcd5-14086676.jpg](https://api2.mubu.com/v3/document_image/86adb142-7b50-4515-8656-1231925fdcd5-14086676.jpg)
            
        - 可以将Oder ID information重复，储存在header/line fact table 里面去
    - 6.Allocated facts
        - 与header与line 差不多一回事
        - 原本product的信息是missing的，order和product整合在一起，成一个table。这样相对来说就更靠谱一些
            
            ![https://api2.mubu.com/v3/document_image/ab1de402-723b-4b6a-9571-500f4b59bac2-14086676.jpg](https://api2.mubu.com/v3/document_image/ab1de402-723b-4b6a-9571-500f4b59bac2-14086676.jpg)
            
    - 7.Profit and loss fact tables using allocations
        - 一个hyposes的，很困难，部门之间实际中很难操作，politic issue多，实际中很难实现
            
            ![https://api2.mubu.com/v3/document_image/cec18755-aabe-4c4a-b56f-a567978f1717-14086676.jpg](https://api2.mubu.com/v3/document_image/cec18755-aabe-4c4a-b56f-a567978f1717-14086676.jpg)
            
    - 8.Multiple currency facts
        - 多币种结算，跟multi-time zone相似，以何种参照为标准
            
            ![https://api2.mubu.com/v3/document_image/f889069a-1ad8-4807-9129-7f9fe35a9710-14086676.jpg](https://api2.mubu.com/v3/document_image/f889069a-1ad8-4807-9129-7f9fe35a9710-14086676.jpg)
            
    - 9.Multiple units of measure
        - 很多计算型的描述，所有的measures是单独存在一个表里面，是stand alone的
        - 例如loan ，LVR, LMI , REPAYMENT, INTEREST这些指标都是measure，他们在不断的变
            
            ![https://api2.mubu.com/v3/document_image/bb637643-c590-4180-971b-76173647d54b-14086676.jpg](https://api2.mubu.com/v3/document_image/bb637643-c590-4180-971b-76173647d54b-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/56c1d54f-2786-4552-9465-cbd952e75fc6-14086676.jpg](https://api2.mubu.com/v3/document_image/56c1d54f-2786-4552-9465-cbd952e75fc6-14086676.jpg)
            
        - 所有通过aggregation得到的结果基本都是measure
    - 10.Year-to-date facts
        - 多年的销售记录，能不能展开，给end user表达更多细节的信息。drill down/cross都包括。
            
            ![https://api2.mubu.com/v3/document_image/9676d64c-577c-4482-bd06-a05f62530e5a-14086676.jpg](https://api2.mubu.com/v3/document_image/9676d64c-577c-4482-bd06-a05f62530e5a-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/66c17a80-e42a-4e6b-81b0-898f4d2bedb5-14086676.jpg](https://api2.mubu.com/v3/document_image/66c17a80-e42a-4e6b-81b0-898f4d2bedb5-14086676.jpg)
            
        - group by column update (eg.year-->month)
    - 11.Multipass SQL to avoid fact-to-fact table joins
        - 千万不要用fact table去join fact table，很可能造成歧义，logical上面抵触。下面的操作很如出现表达上的分歧
            
            ![https://api2.mubu.com/v3/document_image/40c7b0d2-bd1d-493e-ae09-efd1f537d518-14086676.jpg](https://api2.mubu.com/v3/document_image/40c7b0d2-bd1d-493e-ae09-efd1f537d518-14086676.jpg)
            
        - 正确的方法是这样用，要把所有对应的信息用dimension全部找到之后，所有的dimension都统一，使得所有的fact有一个统一的dimension参照系。但是如果先join 参照系很容易出现偏差。两个fact table找到相同的dimension，通过相同的这个dimension，join fact tables会更佳准确
            
            ![https://api2.mubu.com/v3/document_image/5ee62806-4abe-4aeb-8566-1516de30bb2a-14086676.jpg](https://api2.mubu.com/v3/document_image/5ee62806-4abe-4aeb-8566-1516de30bb2a-14086676.jpg)
            
        - fact join fact回溯错误是很困难的。
        - 
            
            ![https://api2.mubu.com/v3/document_image/8d526237-3d80-4556-966e-0a45150fe00b-14086676.jpg](https://api2.mubu.com/v3/document_image/8d526237-3d80-4556-966e-0a45150fe00b-14086676.jpg)
            
    - 12.Timespan tracking in fact tables
        - 使用SCDII 可以很准确的拿出来
            
            ![https://api2.mubu.com/v3/document_image/f477ba9e-37b3-43ce-b09e-fcf7cd01044d-14086676.jpg](https://api2.mubu.com/v3/document_image/f477ba9e-37b3-43ce-b09e-fcf7cd01044d-14086676.jpg)
            
    - 13.Late arriving facts
        - 常见的异常处理，dimension信息缺失了怎么办。大部分缺失的信息在dimension table中
        - 系统录入有一些不可抗力，一些信息没有在dimension table中update，但是信息已经传到fact table中，又不能把对应信息删掉，比较通用的处理是，假设product dimension中找不到，用-1 来处理
            
            ![https://api2.mubu.com/v3/document_image/51e8d616-a151-4757-a997-9bf2c9c78f76-14086676.jpg](https://api2.mubu.com/v3/document_image/51e8d616-a151-4757-a997-9bf2c9c78f76-14086676.jpg)
            
        - unmatched/ matched information
        - refresh fact table（最保守最保险的方式）
- 2.Advanced Dimension Table Techniques
    - 1. 不建议Dimension-to-dimension table joins
        - 不要Dimension to dimension join
            
            ![https://api2.mubu.com/v3/document_image/33bc15e8-fd26-4b0a-af81-9f713ca8cffb-14086676.jpg](https://api2.mubu.com/v3/document_image/33bc15e8-fd26-4b0a-af81-9f713ca8cffb-14086676.jpg)
            
    - 2. Multivalued dimensions and bridge tables
        - 美国药监局，混合性的treatment，就符合Multivalued dimension and bridge tables。如果一个病人，病情有不同的诊疗方法措施，一个start schema解决不了。这种many to many的情况怎么办，我们需要bridge table
            
            ![https://api2.mubu.com/v3/document_image/ac3dc95f-5fb9-43f7-a8b3-688139e55383-14086676.jpg](https://api2.mubu.com/v3/document_image/ac3dc95f-5fb9-43f7-a8b3-688139e55383-14086676.jpg)
            
        - 优化处理，举例批发sales的case，一个group里面有3个sales person，order table要看sales person的信息，就可以通过sales group bridge到得到sales person 的信息。
            
            ![https://api2.mubu.com/v3/document_image/c8c4591c-cdb0-4396-8504-2417b54f4944-14086676.jpg](https://api2.mubu.com/v3/document_image/c8c4591c-cdb0-4396-8504-2417b54f4944-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/c570b57d-1759-4fa9-adbe-5d8731559248-14086676.jpg](https://api2.mubu.com/v3/document_image/c570b57d-1759-4fa9-adbe-5d8731559248-14086676.jpg)
            
    - 3.Behavior tag time series
        - 
            
            ![https://api2.mubu.com/v3/document_image/dc36a888-fe79-414e-a237-645223c1ad0b-14086676.jpg](https://api2.mubu.com/v3/document_image/dc36a888-fe79-414e-a237-645223c1ad0b-14086676.jpg)
            
    - 4.Behavior study group
        - 研究客户行为，专项个人化订制的table
            
            ![https://api2.mubu.com/v3/document_image/879a3081-00cd-45de-8a9b-811ce157f903-14086676.jpg](https://api2.mubu.com/v3/document_image/879a3081-00cd-45de-8a9b-811ce157f903-14086676.jpg)
            
        - 用durable key，嵌入到我们未来的模型中。它有一个变迁的过程，我们可以追溯到最早的产品，中间发生的变化
            
            ![https://api2.mubu.com/v3/document_image/45765d47-4bf1-45ea-875d-85b5f4cbac06-14086676.jpg](https://api2.mubu.com/v3/document_image/45765d47-4bf1-45ea-875d-85b5f4cbac06-14086676.jpg)
            
    - 5.Aggregated facts as dimension attributes
        - 老师个人不太建议使用。因为最初录入最好是以raw的方式录入
            
            ![https://api2.mubu.com/v3/document_image/180190b3-0956-4084-8881-2d22c9316ff8-14086676.jpg](https://api2.mubu.com/v3/document_image/180190b3-0956-4084-8881-2d22c9316ff8-14086676.jpg)
            
        - 简单的aggregation直接可以用view来表示, 不用dimension
            
            ![https://api2.mubu.com/v3/document_image/e1f25dc1-d863-491a-adf6-cadb79d6d6a5-14086676.jpg](https://api2.mubu.com/v3/document_image/e1f25dc1-d863-491a-adf6-cadb79d6d6a5-14086676.jpg)
            
    - 6.Dynamic value banding
        - 分区间，在区间每天都在变化的情况下，用的Dynamic value banding
            
            ![https://api2.mubu.com/v3/document_image/60331596-6e87-452a-ab0a-35b3f0d7116a-14086676.jpg](https://api2.mubu.com/v3/document_image/60331596-6e87-452a-ab0a-35b3f0d7116a-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/a0ed97ef-7763-4536-aa5e-c7c43929c257-14086676.jpg](https://api2.mubu.com/v3/document_image/a0ed97ef-7763-4536-aa5e-c7c43929c257-14086676.jpg)
            
    - 7.Text comments
        - text 过长，用简写表示并用reference table来解释
            
            ![https://api2.mubu.com/v3/document_image/3c2046ab-f9a1-4442-b4b3-14e753d0a5c9-14086676.jpg](https://api2.mubu.com/v3/document_image/3c2046ab-f9a1-4442-b4b3-14e753d0a5c9-14086676.jpg)
            
    - 8.Multiple time zones
        - 尽量使用UTC （例如如果用local time zone，澳洲一年要调两次时间，增加复杂度）
            
            ![https://api2.mubu.com/v3/document_image/6706d509-7bf6-4e51-bd66-16fee0c43ee2-14086676.jpg](https://api2.mubu.com/v3/document_image/6706d509-7bf6-4e51-bd66-16fee0c43ee2-14086676.jpg)
            
    - 9. Measure type dimensions
        - 这种非常不好用，可以不用管， dimension table里面尽量录入raw data
            
            ![https://api2.mubu.com/v3/document_image/34e6a0db-3538-49e6-945a-73be78e79efb-14086676.jpg](https://api2.mubu.com/v3/document_image/34e6a0db-3538-49e6-945a-73be78e79efb-14086676.jpg)
            
    - 10. Step dimensions
        - 把用户的行为分为多少个steps，具体到什么step，用户做出什么反应
            
            ![https://api2.mubu.com/v3/document_image/7c5831c5-2c59-4a2d-a348-67ff876ae071-14086676.jpg](https://api2.mubu.com/v3/document_image/7c5831c5-2c59-4a2d-a348-67ff876ae071-14086676.jpg)
            
        - 现在基本已经实时化了，这是比较老派的做法
            
            ![https://api2.mubu.com/v3/document_image/6c90df89-0cf0-4d48-9a84-12eb0b8f5743-14086676.jpg](https://api2.mubu.com/v3/document_image/6c90df89-0cf0-4d48-9a84-12eb0b8f5743-14086676.jpg)
            
    - 11. Hot swappable dimensions
        - Hot swappable 其实就是sub category
        - supertype与subtype, 大类与小类的区别,在一个大类的Dimension里可以切换到小类
            
            ![https://api2.mubu.com/v3/document_image/d6d4b1be-7c62-46c6-acd1-0e9cad4506c9-14086676.jpg](https://api2.mubu.com/v3/document_image/d6d4b1be-7c62-46c6-acd1-0e9cad4506c9-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/d8191e1d-7526-477d-ba4c-271a842ff471-14086676.jpg](https://api2.mubu.com/v3/document_image/d8191e1d-7526-477d-ba4c-271a842ff471-14086676.jpg)
            
        - 例如，customer 就是super type， direct consumer/ business consumer 就是sub type
    - 12. Abstract generic dimensions
        - subtype 全部对应到supertype里面去
            
            ![https://api2.mubu.com/v3/document_image/0d113900-e913-46e2-a2a8-8828f3a4023b-14086676.jpg](https://api2.mubu.com/v3/document_image/0d113900-e913-46e2-a2a8-8828f3a4023b-14086676.jpg)
            
    - 13. Late arriving dimensions
        - 数据Dimension 录的比较晚，类似late arriving facts
            
            ![https://api2.mubu.com/v3/document_image/15a7c91c-18cf-4e8f-9de2-84ca0dec6343-14086676.jpg](https://api2.mubu.com/v3/document_image/15a7c91c-18cf-4e8f-9de2-84ca0dec6343-14086676.jpg)
            
- 3.Special Purpose Schemas
    - 1. Supertype and subtype schemas for heterogeneous products
        - 用supertype subtype，从大类就可以寻找一个小类
            
            ![https://api2.mubu.com/v3/document_image/f8abd42c-b309-4932-bfe2-a2faf69a807d-14086676.jpg](https://api2.mubu.com/v3/document_image/f8abd42c-b309-4932-bfe2-a2faf69a807d-14086676.jpg)
            
    - 2. Real-time fact tables
        - 分步处理，DB达不到realtime的，再快也有delay，nearly realtime
            
            ![https://api2.mubu.com/v3/document_image/4a7984b6-8c84-4575-ae14-c9c9039486fb-14086676.jpg](https://api2.mubu.com/v3/document_image/4a7984b6-8c84-4575-ae14-c9c9039486fb-14086676.jpg)
            
        - 直观的告诉当下业务状况如何，eg, 淘宝的双十一实时销售金额
            
            ![https://api2.mubu.com/v3/document_image/694172cc-f902-4178-b4f1-85ff29a33c76-14086676.jpg](https://api2.mubu.com/v3/document_image/694172cc-f902-4178-b4f1-85ff29a33c76-14086676.jpg)
            
    - 3. Error event schemas
        - 记录error的信息，upper stream 到 down stream， dimension table数据先录入再录入fact table。
            
            ![https://api2.mubu.com/v3/document_image/b16e14aa-dff1-4796-b895-9511360a8e27-14086676.jpg](https://api2.mubu.com/v3/document_image/b16e14aa-dff1-4796-b895-9511360a8e27-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/fbdc2862-9fdf-4f16-a076-054dbb9e5834-14086676.jpg](https://api2.mubu.com/v3/document_image/fbdc2862-9fdf-4f16-a076-054dbb9e5834-14086676.jpg)
            
        - 与Audit dimensions整合在一起
            - 记录bash中的信息
                
                ![https://api2.mubu.com/v3/document_image/e8003992-606d-46a2-a092-88a1448b9e87-14086676.jpg](https://api2.mubu.com/v3/document_image/e8003992-606d-46a2-a092-88a1448b9e87-14086676.jpg)
                
- 2:30 python pipeline code 讲解
    - 用Python跑Snowflake对应的data pipeline process。ad hoc pipeline(如下), 大多数公司用的方式
        
        ![https://api2.mubu.com/v3/document_image/70c427fa-501d-4d50-8934-fa8e7cbbef42-14086676.jpg](https://api2.mubu.com/v3/document_image/70c427fa-501d-4d50-8934-fa8e7cbbef42-14086676.jpg)
        
        ![https://api2.mubu.com/v3/document_image/39997e51-1ef1-4f91-88f6-0ed4e2da84b3-14086676.jpg](https://api2.mubu.com/v3/document_image/39997e51-1ef1-4f91-88f6-0ed4e2da84b3-14086676.jpg)
        
    - 要pip install snowflake.connecter
    - 大公司会用更general 的pipeline, 构建很大很宽的pipeline， 业务更大，如果每次都用特设的pipeline就会很耗时耗力，所以如何选择pipeline需要根据业务和技术情况而定。