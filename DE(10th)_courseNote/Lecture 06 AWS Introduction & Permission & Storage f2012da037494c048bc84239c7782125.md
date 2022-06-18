# Lecture 6 AWS Introduction & Permission & Storage

- 0. 导读
    - 
        
        ![https://api2.mubu.com/v3/document_image/951e7223-c3eb-48a1-9354-ee5f7cc45e56-14086676.jpg](https://api2.mubu.com/v3/document_image/951e7223-c3eb-48a1-9354-ee5f7cc45e56-14086676.jpg)
        
- 1. Introduction
    - 1. Why Learn AWS?
        - 最大的云服务商，客户占比最多
            
            ![https://api2.mubu.com/v3/document_image/ca5d8558-f3eb-47b9-8ca9-d83c6c521c24-14086676.jpg](https://api2.mubu.com/v3/document_image/ca5d8558-f3eb-47b9-8ca9-d83c6c521c24-14086676.jpg)
            
    - 2. Why Is AWS So Powerful?
        - “Invention requires two things:
            - 1. The ability to try a lot of experiments and
            - 2. not having to live with the collateral damage of failed experiments.”
        - Easy to provision virtual machine in the cloud
        - Not locked in any long-term contact
        - Experiment or design different apps
        - If you don’t want to do that, you can just terminate instances
        - Free-tier services
        - 在有AWS之前，很麻烦，需要购买Physical services 等等
            - 
                
                ![https://api2.mubu.com/v3/document_image/3cda8eb2-7af7-4aa1-bb2d-16e27b9394e0-14086676.jpg](https://api2.mubu.com/v3/document_image/3cda8eb2-7af7-4aa1-bb2d-16e27b9394e0-14086676.jpg)
                
    - 3. AWS的服务分类
        - 
            
            ![https://api2.mubu.com/v3/document_image/9847739c-96fb-4a79-94c3-def33c213e0f-14086676.jpg](https://api2.mubu.com/v3/document_image/9847739c-96fb-4a79-94c3-def33c213e0f-14086676.jpg)
            
    - 4. AWS Global Infrastructure
        - 
            
            ![https://api2.mubu.com/v3/document_image/ab74dba1-ad95-4f95-a6e2-98cf126c6a78-14086676.jpg](https://api2.mubu.com/v3/document_image/ab74dba1-ad95-4f95-a6e2-98cf126c6a78-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/564a1cff-bfce-41ab-adce-4ccb3340e4ab-14086676.jpg](https://api2.mubu.com/v3/document_image/564a1cff-bfce-41ab-adce-4ccb3340e4ab-14086676.jpg)
            
    - 5. What is IAM?
        - IAM allows you to manage users and their level of access to the AWS Console. It is important to understand IAM and how it works, both for the exam and for administrating a company’s AWS account in real life.
    - 6. Key Features of IAM
        - global based service
        - Identity Access Management (IAM) offers the following features
        - Centralized control of your AWS account
        - Share Access to your AWS account
        - Granular Permissions ：允许什么使用什么，不允许什么做什么
        - Identity Federation (including Active Directory, Facebook, Linkedin etc)
        - Multifactor Authentication (MFA, 多渠道验证，eg.密码+短信动态口令)
        - Provide temporary access for users/devices and services where necessary，给用户提供一定时间的权限使用服务
        - Allows you to set up your own password rotation policy
        - Integrates with many different AWS services
        - Supports PCI DSS Compliance
    - 7. Key Terminology For IAM
        - 
            
            ![https://api2.mubu.com/v3/document_image/9d2a14f9-6aaf-451a-8fea-554141a6f78f-14086676.jpg](https://api2.mubu.com/v3/document_image/9d2a14f9-6aaf-451a-8fea-554141a6f78f-14086676.jpg)
            
    - Summary
        - IAM is universal. It does not apply to regions at this time.
        - The “root account” is simply the account created when first setup your AWS
        - account. It has complete Admin access.
        - New Users have NO permissions when first created.
        - New Users are assigned Access Key ID & Secret Access Keys when first created.
        - These are not the same as a password. You cannot use the Access key ID & Secret
        - Access Key to Login in to the console. You can use this to access AWS via the APIs
        - and Command Line, however.
        - You only get to view these once. If you lose them, you have to regenerate them.
        - So, save them in a secure location.
        - Always setup Multifactor Authentication on your root account.
        - You can create and customize your own password rotation policies.
- 2. MFA lab (实验操作请跳到 1:13:00 回看视频 )
- 3. Create A Billing Alarm- LAB （1:50）
    - Use your AWS account email address and password to sign in to the AWS Management Console as the AWS account root user.
    - On the navigation bar, choose your account name, and then choose MyAccount.
    - Next to IAM User and Role Access to Billing Information, choose Edit.
    - Then select the check box to Activate IAM Access and choose Update.
    - Open the Billing and Cost Management console
    - at https://console.aws.amazon.com/billing/.
    - In the navigation pane, choose Billing Preferences. Check if Receive Billing
    - Alerts is ticked.If not, tick it and choose Save preferences.
    - Sign out of the console.
- 4. S3 (2:30)
    - 1. 类似网盘，但功能更多. region based service.
        - 非常安全，object based storage, 但不是disk.
            
            ![https://api2.mubu.com/v3/document_image/4c50fc97-8462-4bbc-afa3-fdd9e2015a41-14086676.jpg](https://api2.mubu.com/v3/document_image/4c50fc97-8462-4bbc-afa3-fdd9e2015a41-14086676.jpg)
            
        - S3 basics
            
            ![https://api2.mubu.com/v3/document_image/8636d282-3323-48d9-b6d0-aaad046c1d8b-14086676.jpg](https://api2.mubu.com/v3/document_image/8636d282-3323-48d9-b6d0-aaad046c1d8b-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/472867ed-9805-4b4e-bd7a-ae4cfbf7f305-14086676.jpg](https://api2.mubu.com/v3/document_image/472867ed-9805-4b4e-bd7a-ae4cfbf7f305-14086676.jpg)
            
            - S3 名字必须是universal unique的
            - 11x9s 面试可能会问，就是99.999999999%的durability
            - encryption --》KMS对数据进行加密和解密，有两种：
                - aws 建好的
                - 自己建的
        - S3 standard
            - 
                
                ![https://api2.mubu.com/v3/document_image/a980cde4-76c9-49a1-a0c6-141cb9075d89-14086676.jpg](https://api2.mubu.com/v3/document_image/a980cde4-76c9-49a1-a0c6-141cb9075d89-14086676.jpg)
                
        - Tier and cost
            - 把数据储存成不同的种类，收不同的费用。S3 OneZone-IA （infrequently access) 适合容易再次生成的数据。Glacier : 适用于不怎么用于分析的数据，但是又必须要备份的数据。eg.政府强制备份的4-5年前不怎么用于分析的数据
                
                ![https://api2.mubu.com/v3/document_image/8d08d9c5-2190-4c83-9615-069ae1203621-14086676.jpg](https://api2.mubu.com/v3/document_image/8d08d9c5-2190-4c83-9615-069ae1203621-14086676.jpg)
                
        - S3 基本花费
            - 
                
                ![https://api2.mubu.com/v3/document_image/d6db1f79-a6cf-445d-8b0e-d337dee1b607-14086676.jpg](https://api2.mubu.com/v3/document_image/d6db1f79-a6cf-445d-8b0e-d337dee1b607-14086676.jpg)
                
        - 加速Transfer
            - 
                
                ![https://api2.mubu.com/v3/document_image/321d4d8e-3c4a-47d1-a576-de7d2d705afe-14086676.jpg](https://api2.mubu.com/v3/document_image/321d4d8e-3c4a-47d1-a576-de7d2d705afe-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/8b6cf9ed-e86f-473c-8178-79fd827b0f23-14086676.jpg](https://api2.mubu.com/v3/document_image/8b6cf9ed-e86f-473c-8178-79fd827b0f23-14086676.jpg)
                
        - 
    - 2. Data Consistency Model
        - 1. Strong Read-After-Write Consistency
            - 写入的时候就可以直接读它
            - After a successful write of a new object, or an overwrite or delete of an existing object, any subsequent read request immediately receives the latest version of the object. S3 also provides strong consistency for list operations, so after a write, you can immediately perform a listing of the objects in a bucket with any changes reflected.
        - 2. Eventual Consistency for overwrite PUTS and DELETS
            - 对于PUTS和DELETS，会稍微花点时间保持一致性，有可能读到的是旧的object。
    - 3. object based storage（不可以在S3 上装application/operation system/database）
        - value： 数据， key ：name
            
            ![https://api2.mubu.com/v3/document_image/1fa970ae-6c1c-4f34-8cbd-842a8af9ecee-14086676.jpg](https://api2.mubu.com/v3/document_image/1fa970ae-6c1c-4f34-8cbd-842a8af9ecee-14086676.jpg)
            
        - 需要做life cycle management
    - 4. lifecycle management, 管理S3 数据储存的周期，在哪段时间内存在哪个空间中
        - 
            
            ![https://api2.mubu.com/v3/document_image/b9cad561-f22f-4e1b-b03a-bf824b7013a2-14086676.jpg](https://api2.mubu.com/v3/document_image/b9cad561-f22f-4e1b-b03a-bf824b7013a2-14086676.jpg)
            
    - summary （需要记）
        - 
            
            ![https://api2.mubu.com/v3/document_image/afd9084b-64dd-4987-8b1d-04f43980b3d0-14086676.jpg](https://api2.mubu.com/v3/document_image/afd9084b-64dd-4987-8b1d-04f43980b3d0-14086676.jpg)
            
- 5. s3 lab （2：54）
    - create bucket
        - 
            
            ![https://api2.mubu.com/v3/document_image/24d45085-8227-4b35-94f6-78b72155d3a8-14086676.jpg](https://api2.mubu.com/v3/document_image/24d45085-8227-4b35-94f6-78b72155d3a8-14086676.jpg)
            
    - public bucket
        - 1.disable public access
            
            ![https://api2.mubu.com/v3/document_image/1d816ac6-25d0-4e6d-8e27-81163ec14127-14086676.jpg](https://api2.mubu.com/v3/document_image/1d816ac6-25d0-4e6d-8e27-81163ec14127-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/76caae0f-70df-4f0f-9ee5-9659ea287f7e-14086676.jpg](https://api2.mubu.com/v3/document_image/76caae0f-70df-4f0f-9ee5-9659ea287f7e-14086676.jpg)
            
        - 2.give ownership, 3.give ACL
            - 1.
                
                ![https://api2.mubu.com/v3/document_image/fba5e6b7-9422-4087-8f24-de7e071ab750-14086676.jpg](https://api2.mubu.com/v3/document_image/fba5e6b7-9422-4087-8f24-de7e071ab750-14086676.jpg)
                
        - 4.make public using ACL
            
            ![https://api2.mubu.com/v3/document_image/519a9768-68e9-4015-ba87-3d984eb3d316-14086676.jpg](https://api2.mubu.com/v3/document_image/519a9768-68e9-4015-ba87-3d984eb3d316-14086676.jpg)