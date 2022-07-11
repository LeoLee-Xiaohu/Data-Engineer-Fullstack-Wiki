# Lecture 29 AWS data platform and serverless part 1

- 1. Serverless Introduction
    - 1. what is Serverless
        - 云计算的延伸，服务商可以动态的管理你的机器资源分配
            
            ![https://api2.mubu.com/v3/document_image/6dce1b54-6ea9-4ade-a520-507262b66c74-14086676.jpg](https://api2.mubu.com/v3/document_image/6dce1b54-6ea9-4ade-a520-507262b66c74-14086676.jpg)
            
        - pay as you go
        - 简化一些deploying code的步骤
        - 和传统的deploy的形式相结合
        - AWS definition：一个云架构，能提高敏捷性，能够更快的将产品开发出来
            
            ![https://api2.mubu.com/v3/document_image/04a2de27-b1d0-4c7f-9480-89f8a2078e43-14086676.jpg](https://api2.mubu.com/v3/document_image/04a2de27-b1d0-4c7f-9480-89f8a2078e43-14086676.jpg)
            
    - 2. Why would we use serverless?
        - 不用考虑server，不用担心operation，很容易做scale up/down, scale out/in, 可以把精力放在production上
            
            ![https://api2.mubu.com/v3/document_image/d00258d6-66bc-4084-9147-4422da6a24c6-14086676.jpg](https://api2.mubu.com/v3/document_image/d00258d6-66bc-4084-9147-4422da6a24c6-14086676.jpg)
            
    - 3. Some serverless services on AWS
        - 
            
            ![https://api2.mubu.com/v3/document_image/421bf9c3-486c-49f8-ac81-adeefdb38a40-14086676.jpg](https://api2.mubu.com/v3/document_image/421bf9c3-486c-49f8-ac81-adeefdb38a40-14086676.jpg)
            
- 2. Serverless Framework
    - 1. what is serverless framework?
        - 
            
            ![https://api2.mubu.com/v3/document_image/ddb73587-e196-4a88-9f96-78ff9addb9ee-14086676.jpg](https://api2.mubu.com/v3/document_image/ddb73587-e196-4a88-9f96-78ff9addb9ee-14086676.jpg)
            
    - 2. serverless Framework installation （sample）
        - 
            
            ![https://api2.mubu.com/v3/document_image/bed9df5c-fe50-4fd8-bd9d-fe7d507cd13c-14086676.jpg](https://api2.mubu.com/v3/document_image/bed9df5c-fe50-4fd8-bd9d-fe7d507cd13c-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/6020ed81-4e13-4fd6-8e31-2eeebb929648-14086676.jpg](https://api2.mubu.com/v3/document_image/6020ed81-4e13-4fd6-8e31-2eeebb929648-14086676.jpg)
            
- 3.CloudFormation introduction
    - 1.what is AWS CloudFormation
        - 
            
            ![https://api2.mubu.com/v3/document_image/a99b2673-3122-4502-91b1-41e828769e2c-14086676.jpg](https://api2.mubu.com/v3/document_image/a99b2673-3122-4502-91b1-41e828769e2c-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/3f2e258b-0422-4b88-9e5d-111957af3af2-14086676.jpg](https://api2.mubu.com/v3/document_image/3f2e258b-0422-4b88-9e5d-111957af3af2-14086676.jpg)
            
    - 2. 可以针对性给permission
        - 
            
            ![https://api2.mubu.com/v3/document_image/d3433e3a-7271-4b6e-882e-b1191577835f-14086676.jpg](https://api2.mubu.com/v3/document_image/d3433e3a-7271-4b6e-882e-b1191577835f-14086676.jpg)
            
- 4. serverless 相关操作
    - 1. serverless framework 安装
        - 
            
            ![https://api2.mubu.com/v3/document_image/41c0fb07-4afd-403f-b215-5e4d13ef3562-14086676.jpg](https://api2.mubu.com/v3/document_image/41c0fb07-4afd-403f-b215-5e4d13ef3562-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/b8b7e86f-5b09-41bf-8162-000b45298011-14086676.jpg](https://api2.mubu.com/v3/document_image/b8b7e86f-5b09-41bf-8162-000b45298011-14086676.jpg)
            
    - 2. 认识 serverless framework 以aws-python-http-api-project 为例
        - 操作重点回看视频 1:05:00
        - 在aws-python-http-api-project 文件夹中启动serverless
            - 
                
                ![https://api2.mubu.com/v3/document_image/b5bcf4b8-81b9-410d-81a7-703eebf799d6-14086676.jpg](https://api2.mubu.com/v3/document_image/b5bcf4b8-81b9-410d-81a7-703eebf799d6-14086676.jpg)
                
        - 本地测试serverlesss.yml中的function
            - 
                
                ![https://api2.mubu.com/v3/document_image/ba5ec60c-db7e-4ecb-9374-d6a408ec827d-14086676.jpg](https://api2.mubu.com/v3/document_image/ba5ec60c-db7e-4ecb-9374-d6a408ec827d-14086676.jpg)
                
        - 清除serverless 项目
            - 
                
                ![https://api2.mubu.com/v3/document_image/e17ff96e-51cd-4f56-a59d-ef7285afad66-14086676.jpg](https://api2.mubu.com/v3/document_image/e17ff96e-51cd-4f56-a59d-ef7285afad66-14086676.jpg)
                
    - 3. Lab: Build Data Pipeline in AWS
        - 0.
            
            ![https://api2.mubu.com/v3/document_image/f5cd848a-5a76-41fa-bcb0-e327b427706c-14086676.jpg](https://api2.mubu.com/v3/document_image/f5cd848a-5a76-41fa-bcb0-e327b427706c-14086676.jpg)
            
- 5.Lab: Deploy Data Pipeline in AWS using Serverless Framework
    - 0.
        
        ![https://api2.mubu.com/v3/document_image/4db6577c-11c8-43e0-a324-2ffabbfc7bdb-14086676.jpg](https://api2.mubu.com/v3/document_image/4db6577c-11c8-43e0-a324-2ffabbfc7bdb-14086676.jpg)
        
    - 1 initialize
        - 
            
            ![https://api2.mubu.com/v3/document_image/c264b605-da1b-47de-8723-36706a86d8e7-14086676.jpg](https://api2.mubu.com/v3/document_image/c264b605-da1b-47de-8723-36706a86d8e7-14086676.jpg)
            
    - 2.详细介绍serverless.yml 代码（2:35:00)
        - 
            
            ![https://api2.mubu.com/v3/document_image/3ffcf178-77f6-4d44-b501-3c6beaf78dbe-14086676.jpg](https://api2.mubu.com/v3/document_image/3ffcf178-77f6-4d44-b501-3c6beaf78dbe-14086676.jpg)
            
    - 3. serverless framework code
        - 
            
            ![https://api2.mubu.com/v3/document_image/03a850fb-32f0-4e20-9e63-8c1fc94911d5-14086676.jpg](https://api2.mubu.com/v3/document_image/03a850fb-32f0-4e20-9e63-8c1fc94911d5-14086676.jpg)
            
    - 4. my data pipeline 代码讲解 （2:45）
        - Makefile（3:00:00) ：wrapped shell command 不想写很繁琐的shell command，就可以用makefile， 直接在shell中 make deploy 就可以运行deploy的全部代码
            
            ![https://api2.mubu.com/v3/document_image/862154cd-b512-4e4f-ba8d-cfd082e5801c-14086676.jpg](https://api2.mubu.com/v3/document_image/862154cd-b512-4e4f-ba8d-cfd082e5801c-14086676.jpg)
            
            - make package ，打包看下size有多大
        - serverless.yml (3:05:00)
            
            ![https://api2.mubu.com/v3/document_image/fdcf9bec-8a58-4bdd-a9c6-dd1fb603b2da-14086676.jpg](https://api2.mubu.com/v3/document_image/fdcf9bec-8a58-4bdd-a9c6-dd1fb603b2da-14086676.jpg)
            
            - custom: 定义自己的variable。 dotenv: 将env里面的variable变成lambda中的variable
        - data_pipeline.py 讲解（2:52:00）
            
            ![https://api2.mubu.com/v3/document_image/e870f4b2-d7da-4692-979b-3363d9809b63-14086676.jpg](https://api2.mubu.com/v3/document_image/e870f4b2-d7da-4692-979b-3363d9809b63-14086676.jpg)
            
        - requirements.txt 安装所依存的包
        - plugin 需要先comment掉，第一次安装成功后，才能release出来。

salary 给出一个确切的值，不要给范围，高于市场价一些。