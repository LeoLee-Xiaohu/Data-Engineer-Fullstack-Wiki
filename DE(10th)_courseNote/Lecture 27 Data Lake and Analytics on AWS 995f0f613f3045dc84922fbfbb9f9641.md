# Lecture 27 Data Lake and Analytics on AWS

- 0. 导读
    - 
        
        ![https://api2.mubu.com/v3/document_image/fad03188-056a-447a-8b02-3d561aec6549-14086676.jpg](https://api2.mubu.com/v3/document_image/fad03188-056a-447a-8b02-3d561aec6549-14086676.jpg)
        
    - 把数据当product来看，business oriented
        
        ![https://api2.mubu.com/v3/document_image/6f01ab3c-41d9-4724-b080-f29c960429ca-14086676.jpg](https://api2.mubu.com/v3/document_image/6f01ab3c-41d9-4724-b080-f29c960429ca-14086676.jpg)
        
- 1. Data lake process
    - 1.skills covered
        - 
            
            ![https://api2.mubu.com/v3/document_image/c3ccec30-2901-411e-b54d-a81d473fdfa3-14086676.jpg](https://api2.mubu.com/v3/document_image/c3ccec30-2901-411e-b54d-a81d473fdfa3-14086676.jpg)
            
    - 2.data lake overview
        - data lake 需要2节课时间理解和消化，data lake架构理解非常重要，如果理解不到位，很容易做成data swamp
            
            ![https://api2.mubu.com/v3/document_image/6aa1f9cb-86f5-4ff8-a1e7-f549173813f4-14086676.jpg](https://api2.mubu.com/v3/document_image/6aa1f9cb-86f5-4ff8-a1e7-f549173813f4-14086676.jpg)
            
        - 公司越来越需要实时分析real-time analytics
        - Data science
            - 1.
                
                ![https://api2.mubu.com/v3/document_image/bfa3e027-94c6-49e5-ba7d-a743757f8cab-14086676.jpg](https://api2.mubu.com/v3/document_image/bfa3e027-94c6-49e5-ba7d-a743757f8cab-14086676.jpg)
                
            - 2. data science lifecycle
                - step1， bussiness understanding. 进入到工业中，最早需要问的问题是：解决什么商业问题。拿到数据不要先想数据做什么，而是想商业问题。
                    
                    ![https://api2.mubu.com/v3/document_image/17104e31-7ebd-48d8-9ee0-f3bd92b698fa-14086676.jpg](https://api2.mubu.com/v3/document_image/17104e31-7ebd-48d8-9ee0-f3bd92b698fa-14086676.jpg)
                    
                - step 2. data acquisition and understanding (DE 的主要工作）
- 2.Data lake architecture （需要着重掌握）
    - 0. data warehouse + Data lake （为什么要用DW、DL？）
    - 1.DW优缺点
        - 优点：star schema, snowflake schema 非常简单，使用友好
            
            ![https://api2.mubu.com/v3/document_image/cfa4ba6c-1a14-4190-b721-dc7c23a069eb-14086676.jpg](https://api2.mubu.com/v3/document_image/cfa4ba6c-1a14-4190-b721-dc7c23a069eb-14086676.jpg)
            
        - 缺点：加column很麻烦，
        - 总结：公司业务变化不大的话比较适合data warehouse，但在发展中业务经常需要加一些新的表格column就不太适合data warehouse了。
    - 2.data warehouse 的目的
        - 主要用于分析数据
            
            ![https://api2.mubu.com/v3/document_image/dae37bbc-c4c9-4e6f-8b77-4ec4b9190c48-14086676.jpg](https://api2.mubu.com/v3/document_image/dae37bbc-c4c9-4e6f-8b77-4ec4b9190c48-14086676.jpg)
            
    - 3.传统数据仓库
        - 
            
            ![https://api2.mubu.com/v3/document_image/c0716998-cea2-4952-9330-42bedb830d83-14086676.jpg](https://api2.mubu.com/v3/document_image/c0716998-cea2-4952-9330-42bedb830d83-14086676.jpg)
            
    - 4.modernizing an existing DW
        - 1.为什么要modernize DW?
            - 1.数据源更多了， volume, velocity, variety 都变的更多了， device & sensors 都是以Terabyte 来计算的
            - 2. Data warehouse基本都是batch的处理方式，无法实时处理数据T
            - 3. data lake 和 data warehouse 相辅相成，有些数据经过data lake处理后放到data warehouse。data lake优点： raw data 也可以放在data lake中进行real time处理和使用，这些数据可以更加容易的被使用，不需要太多的transformation，更快的产生business value。
                
                ![https://api2.mubu.com/v3/document_image/08e17394-6c64-4e46-9ff5-1b86c474171c-14086676.jpg](https://api2.mubu.com/v3/document_image/08e17394-6c64-4e46-9ff5-1b86c474171c-14086676.jpg)
                
    - 5. Ways to approach data warehousing
        - Hadoop现在用的越来越少，了解即可
            
            ![https://api2.mubu.com/v3/document_image/e3bbdd3c-17be-4caf-9dcb-89473f3133dc-14086676.jpg](https://api2.mubu.com/v3/document_image/e3bbdd3c-17be-4caf-9dcb-89473f3133dc-14086676.jpg)
            
    - 6. Growing an existing DW Environment
        - MPP现在很流行的DW 处理方法
            
            ![https://api2.mubu.com/v3/document_image/b57a3938-991e-4c82-850b-afc2c20f9638-14086676.jpg](https://api2.mubu.com/v3/document_image/b57a3938-991e-4c82-850b-afc2c20f9638-14086676.jpg)
            
        - 2、MPP
            
            ![https://api2.mubu.com/v3/document_image/f7a2d686-259c-4b41-ad10-6b073568cea2-14086676.jpg](https://api2.mubu.com/v3/document_image/f7a2d686-259c-4b41-ad10-6b073568cea2-14086676.jpg)
            
            - 疑问MPP 与 map reduce 有什么区别？
                - MPP代表的是大规模并行处理，而MPP数据库也就是大规模并行处理的数据库，例如：Vertica、Greenplum都是。MPP数据库的架构肯定和传统的MySQL之类的数据库架构是不一样的，它采用的是非单机架构。这说到分布架构，就要聊聊网格计算（Grid Computing）和集群计算（Cluster Computing）。
                - 网格计算其实还是一个分布式系统，由很多的异构计算机组成一个“超级计算机”，它将分布在网络中的计算机共同来实现数据处理。它可以利用系统空闲的计算资源来执行处理任务。网格计算资源管理是非常重要的。它可以控制提交的任务请求，将任务请求调度到选定的服务器上。这些选定的服务器组成一个网格。任务可以在网格中独立执行。
                - Grid Computing指的是异构网络、不同硬件、不同操作系统在网格中连接在一起。而Cluster Computing指的是同构的快速局域网、相同硬件设备、相同操作系统连接在一起组成一个集群，集群计算中的每个计算机称为一个节点，每个节点都具备相同的硬件架构和相同的操作系统。所以，我们一般都说Hadoop集群。
                - Grid Computing是一个更大的概念。你可以把Grid Computing理解为一个超算中心。Cluster Compting一般用于解决数据库、或者是Web应用服务器中的问题。而Grid Computing用于遗传学建模、工程设计、甚至是成吉思汗墓搜索、搜索外星智慧等，有一些工作必须要通过异构系统来解决。例如：一个物联网网格架构中包含了各种传感器系统、数据存储/计算系统、图像/音频处理系统、雷达信号分析系统，这些系统可能分布在不同的网络中，可能一个在香港、一个在多伦多、一个在北京等等。所以，网格计算核心强调的是异构，而集群计算强调的是同构。Cluster Computing可以是Grid Computing的一部分。
                - Grid Computing的两个关键字：空闲资源、异构。基于这种架构的MPP可以将分布在网络中的计算机都利用起来，但因为它要根据可用性机会性的使用资源，这肯定会提高资源利用率，但这就会限制在处理高峰时期能够使用的资源，无法保证稳定的带宽、资源来应对。Cloud Computing就是由Grid Computing发展过来的，云计算侧重于提供资源的抽象和服务。
                - 而另一种流行的架构就是Cluster Computing了，它可以将特定的节点连接在一起，提供稳定的资源服务。
                - 从概念来说，我认为，绝大多数的MPP都是Cluster Computing。
                - MPP虽然快，效率特别高。但任何东西都不是绝对的。MapReduce一个阶段一个阶段地执行，非常稳定，每个任务都可以看到非常详细的执行日志，方便排错。而MPP我们能看到的就是物理执行计划了，它不是按阶段执行地，所以有时候调试错误会很麻烦。资源不利于管控。因为MPP任务和执行器是绑定的，所以，假设有个节点处理慢就会导致整个作业性能变慢，短板效应非常明显。另外，MPP的节点越多，出现问题的概率越大。一旦节点出问题，会导致整个集群性能受限。所以，一般MPP集群规模不会太大。但Hadoop集群可以非常大，上万个节点也是没有问题的。
                - MapReduce的并行度确实不是最大化的。写过MapReduce都知道，程序主要包含了Mapper和Reducer两部分。而Hive做的事情是将SQL解析为命令式的Java MapReduce，本质上还是MapReduce。如果程序里面有一些聚合计算，是必须要等到Mapper任务都执行完才能继续往下执行。它在资源有限的场景比较适合。还有，现阶段的Hive还是有很多地方和传统的SQL不兼容的，写法上也是要做一些调整的。
                - MapReduce是能够将数据集分成一个个的批次，然后分别启动任务来处理。而MPP肯定也是有机制能够让大数据集分成一部分一部分来处理的。分布式计算基本上都是这个套路。我们用MapReduce的时候，因为数据大都是存储在HDFS这种分布式数据集上，这种存储成本较低，很稳定。但要知道，它就是一个文件系统，它对数据本身的了解一定是有限的。所以查询计划对依赖的处理可能那么准确，甚至是基于成本的执行计划也是难搞出来的。MPP数据库的优势在这里就比较明显了，数据依赖很容易识别，而且MPP数据库一般都是单独部署的，并行处理能够最大化地发挥出来。
                - MPP数据库也是分布式并行计算，它会根据数据分布，将处理分成一小队一小队的，然后每个小队都放在计算节点去执行，计算完成后再将结果合并在一起。在效率上MPP数据库肯定是有优势的，但对计算资源的要求也很高。
                - 资料来源：[https://www.modb.pro/db/106683](https://www.modb.pro/db/106683)
            - compute node 是 类似MapReduce hadoop name node 吗？
            - Hadoop是HDFS 文件，那MMP的数据格式是什么样的呢？
        - 3.user 只access 一个layer就能获取DW 或Data lake 中的数据
            
            ![https://api2.mubu.com/v3/document_image/5c139627-7d9b-443c-930c-dc88c6f585b9-14086676.jpg](https://api2.mubu.com/v3/document_image/5c139627-7d9b-443c-930c-dc88c6f585b9-14086676.jpg)
            
    - 7.Multi-Strucured Data
        - 
            
            ![https://api2.mubu.com/v3/document_image/ee62cc92-a924-4709-9e07-61558762a2e1-14086676.jpg](https://api2.mubu.com/v3/document_image/ee62cc92-a924-4709-9e07-61558762a2e1-14086676.jpg)
            
    - 8. Lambda Architecture
        - Speed Layer(streaming) + Batch Layer + Serving Layer
        - The Lambda Architecture contains both a traditional batch data pipeline and a fast streaming pipeline for real-time data, as well as a serving layer for responding to queries.
        - DE 中最常用的Architecture，面试中会问。
        - Speed Layer不走batch layer 直接实时出数据, 对历史性数据做分析时，主要还是用Batch Layer（因为Batch更稳定可靠）
            
            ![https://api2.mubu.com/v3/document_image/2b7dd16c-741e-42b7-a83e-fad6fc7e873b-14086676.jpg](https://api2.mubu.com/v3/document_image/2b7dd16c-741e-42b7-a83e-fad6fc7e873b-14086676.jpg)
            
        - benefits:
            - The Lambda Architecture attempts to balance concerns around latency, data consistency, scalability, fault tolerance, and human fault tolerance. Let’s look at each of these elements.
            - Latency. Raw data is indexed in the serving layer so that end users can query and analyze all historical data. Since batch indexing takes a bit of time, there tends to be a relatively large time window of data that is temporarily not available to end users for analysis. The speed layer uses stream processing technologies to immediately index recent data that is currently not queryable in the batch/serving layers, thus narrowing the time window of unanalyzable data. This helps to reduce the latency (i.e., the wait time for making data available for analysis) that is inherent in the batch/serving layers.
            - Data consistency. One key idea behind the Lambda Architecture is that it eliminates the risk of data inconsistency that is often seen in distributed systems. In a distributed database where data might not be delivered to all replicas due to node or network failures, there is a chance for inconsistent data. In other words, one copy of the data might reflect the up-to-date value, but another copy might still have the previous value. In the Lambda Architecture, since the data is processed sequentially (and not in parallel with overlap, which may be the case for operations on a distributed database), the indexing process can ensure the data reflects the latest state in both the batch and speed layers.
            - Scalability. The Lambda Architecture does not specify the exact technologies to use, but is based on distributed, scale-out technologies that can be expanded by simply adding more nodes. This can be done at the data source, in the batch layer, in the serving layer, and in the speed layer. This lets you use the Lambda Architecture no matter how much data you need to process.
            - Fault tolerance. As above, the Lambda Architecture is based on distributed systems that support fault tolerance, so should a hardware failure occur, other nodes are available to continue the workload. In addition, since all data is stored in the batch layer, any failures during indexing either in the serving layer or the speed layer can be overcome by simply rerunning the indexing job at the batch/serving layers, and letting the speed layer continue indexing the most recent data.
            - Human fault tolerance. Since raw data is saved for indexing, it acts as a system of record for your analyzable data, and all indexes can be recreated from this data set. This means that if there are any bugs in the indexing code or any omissions, the code can be updated and then rerun to reindex all data.
            - The Lambda Architecture has sometimes been criticized as being overly complex. Each pipeline requires its own code base, and the code bases must be kept in sync to ensure consistent, accurate results when queries touch both pipelines.
            - 资料来源：[https://hazelcast.com/glossary/lambda-architecture/](https://hazelcast.com/glossary/lambda-architecture/)
    - 9. Hybrid Architecture
        - 既有Cloud 也有On-premises, 有些公司没有办法全用cloud ，如银行
            
            ![https://api2.mubu.com/v3/document_image/635ff248-47fc-4a49-9dac-1b9e5b4e7aed-14086676.jpg](https://api2.mubu.com/v3/document_image/635ff248-47fc-4a49-9dac-1b9e5b4e7aed-14086676.jpg)
            
- 3.Data Lake Demo (00:59)
    - 1.在Datalake 中建立storage layer.
    - 2. AWS Glue
        - 1. add crawler
            - 1.choose data store
                
                ![https://api2.mubu.com/v3/document_image/8a7e69d4-8167-4a94-b0b0-8686c61eb759-14086676.jpg](https://api2.mubu.com/v3/document_image/8a7e69d4-8167-4a94-b0b0-8686c61eb759-14086676.jpg)
                
            - 2. 设置include path
                
                ![https://api2.mubu.com/v3/document_image/b12ee200-0bfd-4a38-8309-3d9a78f2985c-14086676.jpg](https://api2.mubu.com/v3/document_image/b12ee200-0bfd-4a38-8309-3d9a78f2985c-14086676.jpg)
                
            - 设置IAM role
                
                ![https://api2.mubu.com/v3/document_image/3440810d-d287-4413-a026-4f96cb02adb0-14086676.jpg](https://api2.mubu.com/v3/document_image/3440810d-d287-4413-a026-4f96cb02adb0-14086676.jpg)
                
            - 设置frequency，选run on demand
                
                ![https://api2.mubu.com/v3/document_image/01c8f3e1-6fc9-41eb-a5b8-a072283160e2-14086676.jpg](https://api2.mubu.com/v3/document_image/01c8f3e1-6fc9-41eb-a5b8-a072283160e2-14086676.jpg)
                
            - 建立database
                
                ![https://api2.mubu.com/v3/document_image/5728bc2e-2bb0-4819-818c-9fad456d7d9c-14086676.jpg](https://api2.mubu.com/v3/document_image/5728bc2e-2bb0-4819-818c-9fad456d7d9c-14086676.jpg)
                
        - 2. run crawler
            - 点击对应的crawler，run crawler
                
                ![https://api2.mubu.com/v3/document_image/b6638f02-586a-4fd6-8518-16990cbf945f-14086676.jpg](https://api2.mubu.com/v3/document_image/b6638f02-586a-4fd6-8518-16990cbf945f-14086676.jpg)
                
        - 
    - 3. AWS Athena
        - 第一次可能要search query editor
            
            ![https://api2.mubu.com/v3/document_image/93b9c5ff-31bd-42ca-9987-0bfa98bd533e-14086676.jpg](https://api2.mubu.com/v3/document_image/93b9c5ff-31bd-42ca-9987-0bfa98bd533e-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/86bd2027-b963-4ef9-9d37-a2ee48c77fa3-14086676.jpg](https://api2.mubu.com/v3/document_image/86bd2027-b963-4ef9-9d37-a2ee48c77fa3-14086676.jpg)
            
        - run 完Glue之后，选择对应的database，就会出现tables
            
            ![https://api2.mubu.com/v3/document_image/66ed2815-c3a4-43cb-84fb-4ea0ef3ef112-14086676.jpg](https://api2.mubu.com/v3/document_image/66ed2815-c3a4-43cb-84fb-4ea0ef3ef112-14086676.jpg)
            
        - 写完query一定要加一个limit
            
            ![https://api2.mubu.com/v3/document_image/7773454c-712d-47db-836f-7ee345f06ccc-14086676.jpg](https://api2.mubu.com/v3/document_image/7773454c-712d-47db-836f-7ee345f06ccc-14086676.jpg)
            
        - 
- 4.R Programming Language
    - 1.基本的R 操作
        - 建立data frame，详细见老师PPT
            
            ![https://api2.mubu.com/v3/document_image/9ded7967-5c88-4588-af2f-c4ea56dbd3bb-14086676.jpg](https://api2.mubu.com/v3/document_image/9ded7967-5c88-4588-af2f-c4ea56dbd3bb-14086676.jpg)
            
    - 2. RStudio 介绍
    - 自己练
- 5. Introduction to modelling for data science
    - 什么是统计？等等统计知识复习
        - 
            
            ![https://api2.mubu.com/v3/document_image/c617b484-3aaa-4da1-b4dc-03bef8dfe64b-14086676.jpg](https://api2.mubu.com/v3/document_image/c617b484-3aaa-4da1-b4dc-03bef8dfe64b-14086676.jpg)
            
    - DE 需要做data quality checking，所以需要统计学知识
    - 方差--》离散程度
    - 协方差covariance --》 两者相关性
        - 1
            
            ![https://api2.mubu.com/v3/document_image/4fc3909c-9145-4b8e-9b96-6167a413341a-14086676.jpg](https://api2.mubu.com/v3/document_image/4fc3909c-9145-4b8e-9b96-6167a413341a-14086676.jpg)
            
        - 2.Corr(X,Y): 范围取到-1到1, 便于比较
            
            ![https://api2.mubu.com/v3/document_image/cbd78135-8be3-407b-b682-66f5904cd319-14086676.jpg](https://api2.mubu.com/v3/document_image/cbd78135-8be3-407b-b682-66f5904cd319-14086676.jpg)
            
            4.random variables - 概览分布
            
            - 1
                
                ![https://api2.mubu.com/v3/document_image/799c2ba5-ea77-4ac2-a18d-8564e9af991d-14086676.jpg](https://api2.mubu.com/v3/document_image/799c2ba5-ea77-4ac2-a18d-8564e9af991d-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/12383b08-a1d8-42cb-a298-c976f5ebf853-14086676.jpg](https://api2.mubu.com/v3/document_image/12383b08-a1d8-42cb-a298-c976f5ebf853-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/f25536b6-e744-4850-9fb6-de8863b7751a-14086676.jpg](https://api2.mubu.com/v3/document_image/f25536b6-e744-4850-9fb6-de8863b7751a-14086676.jpg)
                
            - central limit theorem: 重要统计学经常用的。 不管原来的分布，只每次从中抽样，抽样样本的平均值，就符合高斯分布。如，测一个国家的平均身高
                
                ![https://api2.mubu.com/v3/document_image/a3b310c6-750c-4e17-8299-481bc6826a74-14086676.jpg](https://api2.mubu.com/v3/document_image/a3b310c6-750c-4e17-8299-481bc6826a74-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/089eaa0f-6217-4953-b184-8bab9c17bc43-14086676.jpg](https://api2.mubu.com/v3/document_image/089eaa0f-6217-4953-b184-8bab9c17bc43-14086676.jpg)