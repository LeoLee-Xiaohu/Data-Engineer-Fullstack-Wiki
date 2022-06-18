# Lecture05 SQL Part 2

- 0.导读
    - 
        
        ![https://api2.mubu.com/v3/document_image/28bfe0d1-2244-4960-9463-7eeb10240760-14086676.jpg](https://api2.mubu.com/v3/document_image/28bfe0d1-2244-4960-9463-7eeb10240760-14086676.jpg)
        
- 1. SQL case study
    - 但凡遇到有歧义的SQL题目时，可以向面试官提出来，阐述清楚。
    - 上机要求要100%做对
    - 面试白板95%正确度以上，重思路逻辑
- 2. SQL Table VS View
    - view 解决security 问题, 在database 中原始table不让一般人看到，例如batch input，账户余额
        
        ![https://api2.mubu.com/v3/document_image/2737105f-6b39-4c08-82e7-1cde7376f798-14086676.jpg](https://api2.mubu.com/v3/document_image/2737105f-6b39-4c08-82e7-1cde7376f798-14086676.jpg)
        
        - create or replace view XXX as (sql query)
            
            ![https://api2.mubu.com/v3/document_image/7c9db770-7495-46e0-ad83-23718b105f70-14086676.jpg](https://api2.mubu.com/v3/document_image/7c9db770-7495-46e0-ad83-23718b105f70-14086676.jpg)
            
    - view 减少常用的statement 写SQL的工作量
- 3.Tuning & Index
    - Tuning , 优化代码，要防止分布式计算时数据倾斜
        - 
            
            ![https://api2.mubu.com/v3/document_image/9f75d902-0c40-44cd-83ca-3646b475fa53-14086676.jpg](https://api2.mubu.com/v3/document_image/9f75d902-0c40-44cd-83ca-3646b475fa53-14086676.jpg)
            
    - index ，相当于做个目录，不需要遍历整张表，遍历速度更快，缺点是占用物理储存空间。在数据量非常大的时候，至少Tera data级别，用index 可以提升data retrieve的效率。
        - 有primary index 和second index。
            
            ![https://api2.mubu.com/v3/document_image/9647a89e-6ab5-4667-ab09-6e54c3f4f051-14086676.jpg](https://api2.mubu.com/v3/document_image/9647a89e-6ab5-4667-ab09-6e54c3f4f051-14086676.jpg)
            
        - index与primary key不冲突
        - index放在重复记录比较多的column上是不合适的
        - 现在DW 用index用的越来越少了。
- 4.Window analytic function -- rank
    - SQL运行先后顺序
        
        ![https://api2.mubu.com/v3/document_image/fed28539-98dc-4756-9ccd-4e0512d3a5da-14086676.jpg](https://api2.mubu.com/v3/document_image/fed28539-98dc-4756-9ccd-4e0512d3a5da-14086676.jpg)
        
    - DENSE_RANK
        - 1,1,2,2,3
    - RANK
        - 1,1,3,4
    - ROW_NUMBER
        - 1,2,3,4,5
    - 三者图例
        
        ![https://api2.mubu.com/v3/document_image/b4dd4a97-6383-4377-b24d-f2e3ccd9a665-14086676.jpg](https://api2.mubu.com/v3/document_image/b4dd4a97-6383-4377-b24d-f2e3ccd9a665-14086676.jpg)
        
    - partition by
        
        ![https://api2.mubu.com/v3/document_image/89959277-833d-48ee-8203-5deddbe3b0a0-14086676.jpg](https://api2.mubu.com/v3/document_image/89959277-833d-48ee-8203-5deddbe3b0a0-14086676.jpg)
        
- 5.Window function -- lead & leg
    - LEAD
        
        ![https://api2.mubu.com/v3/document_image/d0cb9506-c91c-442e-b53b-c65ed0062c3f-14086676.jpg](https://api2.mubu.com/v3/document_image/d0cb9506-c91c-442e-b53b-c65ed0062c3f-14086676.jpg)
        
    - LAG, 不是所有的RDBMS都有的
- 6.Load Data into Snowflake (local) -- Manual process
    - 0. snowflake本地安装及配置（Mac）
        - 视频教程： [https://www.youtube.com/watch?v=N0fGpsmCI_E](https://www.youtube.com/watch?v=N0fGpsmCI_E)
    - 1. snowflake 上传数据流程图
        - 1. local 传到snowflake （这节课用的就是local方式）
            - 先put到一个internal named stage中，然后再copy到database 中。copy非常快
                
                ![https://api2.mubu.com/v3/document_image/e4350640-b5f7-4dae-9e55-fdf4df884bba-14086676.jpg](https://api2.mubu.com/v3/document_image/e4350640-b5f7-4dae-9e55-fdf4df884bba-14086676.jpg)
                
        - 2. S3 Bucket 传到snowflake
            - 只是put的地址不同，是cloud的
                
                ![https://api2.mubu.com/v3/document_image/df55a044-7b0b-4971-b1cf-afc399d421da-14086676.jpg](https://api2.mubu.com/v3/document_image/df55a044-7b0b-4971-b1cf-afc399d421da-14086676.jpg)
                
    - 2. snowflake 上传步骤操作
        - 
            
            ![https://api2.mubu.com/v3/document_image/8d575872-bfee-421d-8ac5-98fdf4f5845f-14086676.jpg](https://api2.mubu.com/v3/document_image/8d575872-bfee-421d-8ac5-98fdf4f5845f-14086676.jpg)
            
    - 第一步，Data Profiling （check the input source, 是什么文件，CSV，还是JSON等等）很重要！( 3: 00)
        - 先看看数据格式，数据长什么样。有无“”内的逗号。等等
            
            ![https://api2.mubu.com/v3/document_image/d399be37-2211-4c9d-a1a0-ea3376b6926b-14086676.jpg](https://api2.mubu.com/v3/document_image/d399be37-2211-4c9d-a1a0-ea3376b6926b-14086676.jpg)
            
        - 如果head里有column name我们需要跳过去
        - 分隔符不同，有“,” 有tab，我们需要转换成file format标准表达式
        - 如果单元格中有逗号，我们可以用“”包起来，避免错误识别column分隔了如红圈地方
    - 第二步， create & run target table SQL
        - snowflake可以定义一个比较宽的区间，允许不用定义到很窄，比较方便。
            
            ![https://api2.mubu.com/v3/document_image/26b99827-7360-4252-92f0-e726cfd7efe6-14086676.jpg](https://api2.mubu.com/v3/document_image/26b99827-7360-4252-92f0-e726cfd7efe6-14086676.jpg)
            
    - 第三步，open CLI interface
        - 登入terminal , 输入account name , user_name, warehouse name, database name, schema
            
            ![https://api2.mubu.com/v3/document_image/27f42d1e-fe07-4e94-991c-fe4b38632b6d-14086676.jpg](https://api2.mubu.com/v3/document_image/27f42d1e-fe07-4e94-991c-fe4b38632b6d-14086676.jpg)
            
        - warehouse name, database name, schema 在snowflake 界面中的Content中可以找到
            
            ![https://api2.mubu.com/v3/document_image/46add077-943f-4178-94f6-9cdcb7a8cd8b-14086676.jpg](https://api2.mubu.com/v3/document_image/46add077-943f-4178-94f6-9cdcb7a8cd8b-14086676.jpg)
            
        - 在导航条中找account name
            
            ![https://api2.mubu.com/v3/document_image/96df3249-1f94-47c9-991f-e70463e24c93-14086676.jpg](https://api2.mubu.com/v3/document_image/96df3249-1f94-47c9-991f-e70463e24c93-14086676.jpg)
            
        - show data
            
            ![https://api2.mubu.com/v3/document_image/fb877da3-0a68-4e05-9468-da8b4d7a86cd-14086676.jpg](https://api2.mubu.com/v3/document_image/fb877da3-0a68-4e05-9468-da8b4d7a86cd-14086676.jpg)
            
    - 第四步，select database & table
    - 第五步，create file format
        - 创建文件储存格式, 告诉Snowflake上传的格式，以解析正确，例如逗号分隔符
            
            ![https://api2.mubu.com/v3/document_image/7dfc265f-222d-4b6c-a515-75f83d005e5a-14086676.jpg](https://api2.mubu.com/v3/document_image/7dfc265f-222d-4b6c-a515-75f83d005e5a-14086676.jpg)
            
    - 第六步，create stage
        - 其实就是一个Snowflake path
            
            ![https://api2.mubu.com/v3/document_image/f7539c08-5413-47f5-bbb6-dc58c0832ace-14086676.jpg](https://api2.mubu.com/v3/document_image/f7539c08-5413-47f5-bbb6-dc58c0832ace-14086676.jpg)
            
    - 第七步，put the file into stage
        - 上传是，注意文件地址更改put file:///mnt/CSV本地文件路径
            
            ![https://api2.mubu.com/v3/document_image/cb3cfb73-8af9-420c-97b5-9a3f2e8d01af-14086676.jpg](https://api2.mubu.com/v3/document_image/cb3cfb73-8af9-420c-97b5-9a3f2e8d01af-14086676.jpg)
            
    - 第八步，copy data into table
        - 
            
            ![https://api2.mubu.com/v3/document_image/35577139-f4c4-4953-99c5-3420d63b16a2-14086676.jpg](https://api2.mubu.com/v3/document_image/35577139-f4c4-4953-99c5-3420d63b16a2-14086676.jpg)
            
- 7. 高阶SQL
    - 1. Cumulative sum & Moving average
        - 类似 阶段性累加，平滑均线, 股票中的5日均线
            
            ![https://api2.mubu.com/v3/document_image/a8e04c49-21d9-400a-9e2d-13115cba6f5b-14086676.jpg](https://api2.mubu.com/v3/document_image/a8e04c49-21d9-400a-9e2d-13115cba6f5b-14086676.jpg)
            
        - 用SQL Frame Clause 完成
            - N PRECEDING 向上 N rows， M FOLLWOING 向下 M rows
            - 或上下无限行，不能完全使用Unbounded preceding, 会非常消耗资源，特别是共有云计算，特别耗钱
            - 实例，current row 向下平滑计算7行之后，reset，又以reset 行向下平滑7行计算
                
                ![https://api2.mubu.com/v3/document_image/c587f5f1-d4bf-43a7-ba3c-ea00dc3d2544-14086676.jpg](https://api2.mubu.com/v3/document_image/c587f5f1-d4bf-43a7-ba3c-ea00dc3d2544-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/402e1b61-f4fe-4fd5-a26f-64c2596f806c-14086676.jpg](https://api2.mubu.com/v3/document_image/402e1b61-f4fe-4fd5-a26f-64c2596f806c-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/db3c038b-3dc9-428f-a235-1c83948e8b4c-14086676.jpg](https://api2.mubu.com/v3/document_image/db3c038b-3dc9-428f-a235-1c83948e8b4c-14086676.jpg)
                
        - SQL 代码
            
            ![https://api2.mubu.com/v3/document_image/4aeef500-201a-4eb8-a25c-9d3270c9381f-14086676.jpg](https://api2.mubu.com/v3/document_image/4aeef500-201a-4eb8-a25c-9d3270c9381f-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/033f2c91-351e-4866-a94d-88a8e949d72e-14086676.jpg](https://api2.mubu.com/v3/document_image/033f2c91-351e-4866-a94d-88a8e949d72e-14086676.jpg)
            
    - 2. NTILE
        - 对数据划分N分，当原始数据无法整分时，会在第一层多划分一个出来，例如，9分成4份，就需要讲第一份划分到第一层中，后面的就可以整分了。
            
            ![https://api2.mubu.com/v3/document_image/b9b14b55-e81a-4e41-b815-1a0a6fb6153f-14086676.jpg](https://api2.mubu.com/v3/document_image/b9b14b55-e81a-4e41-b815-1a0a6fb6153f-14086676.jpg)
            
        - SQL code （曾经有同学面试被问到，所有的SQL语法必须全部熟练掌握）
            
            ![https://api2.mubu.com/v3/document_image/0a3ac5be-bcb6-4a67-8fcc-9a2d7d47655c-14086676.jpg](https://api2.mubu.com/v3/document_image/0a3ac5be-bcb6-4a67-8fcc-9a2d7d47655c-14086676.jpg)
            
            - 结果
                
                ![https://api2.mubu.com/v3/document_image/a8213b79-a465-4a64-8824-b5411da2049d-14086676.jpg](https://api2.mubu.com/v3/document_image/a8213b79-a465-4a64-8824-b5411da2049d-14086676.jpg)
                
    - 3. Common Table Expression (CTE)
        - 将（）里的select操作，命名，并之后直接调出来
            
            ![https://api2.mubu.com/v3/document_image/12e0ee8b-c7f6-4bcf-9cf8-57592358b8f9-14086676.jpg](https://api2.mubu.com/v3/document_image/12e0ee8b-c7f6-4bcf-9cf8-57592358b8f9-14086676.jpg)
            
        - CTE can be self-referencing, 一个抽象表达，Recursion 递归CTE
            - recursion, SQL只会做第一种。
                
                ![https://api2.mubu.com/v3/document_image/1f48821a-f33d-434c-b057-455376e61f4b-14086676.jpg](https://api2.mubu.com/v3/document_image/1f48821a-f33d-434c-b057-455376e61f4b-14086676.jpg)
                
            - CTE加了Recursive 就完全不一样了，不仅循环一次。没有recursive 的CTE就执行一次
                
                ![https://api2.mubu.com/v3/document_image/08dea8e7-e7a2-4d86-b84e-a0f6d912ffe6-14086676.jpg](https://api2.mubu.com/v3/document_image/08dea8e7-e7a2-4d86-b84e-a0f6d912ffe6-14086676.jpg)
                
                - 上面的anchor member 是初始表达，UNION ALL下面的是递归表达
                - 结果
                    
                    ![https://api2.mubu.com/v3/document_image/e3bc9957-82ab-4c54-917d-04bbb7a44d12-14086676.jpg](https://api2.mubu.com/v3/document_image/e3bc9957-82ab-4c54-917d-04bbb7a44d12-14086676.jpg)
                    
                - 曾经有学员考到了这个。老师认为工作中，recursive CTE 表达用的少，效率不高，但是在这种层进式的场景下可以考虑recurive CTE.