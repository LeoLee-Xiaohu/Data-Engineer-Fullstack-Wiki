# Lecture 21 Data Analytics -Hu Ke

- 1. data analytics
    - 数据建模怎么做？
        - 1.
            
            ![https://api2.mubu.com/v3/document_image/926f25fd-c7da-4b28-b416-cde66b732e2c-14086676.jpg](https://api2.mubu.com/v3/document_image/926f25fd-c7da-4b28-b416-cde66b732e2c-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/fb6b0909-a69c-4fdf-8c74-5fa6c7a0691b-14086676.jpg](https://api2.mubu.com/v3/document_image/fb6b0909-a69c-4fdf-8c74-5fa6c7a0691b-14086676.jpg)
            
        - sas面试时说不会没关系，sas 是简单的编程语言，会Python，sas基本研究会
            
            ![https://api2.mubu.com/v3/document_image/7df5d84f-7edc-4339-8213-00646b79c910-14086676.jpg](https://api2.mubu.com/v3/document_image/7df5d84f-7edc-4339-8213-00646b79c910-14086676.jpg)
            
        - DA 的数据清理与DE的数据清理是不同的。DA 在data cleaning上花费的时间最多，有时要DE来协助
            
            ![https://api2.mubu.com/v3/document_image/dfa50749-879b-4aea-a518-98f6ecdf1d86-14086676.jpg](https://api2.mubu.com/v3/document_image/dfa50749-879b-4aea-a518-98f6ecdf1d86-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/1700d4dd-67d9-4720-a077-22e2d0a5851d-14086676.jpg](https://api2.mubu.com/v3/document_image/1700d4dd-67d9-4720-a077-22e2d0a5851d-14086676.jpg)
            
        - 
- 2. Docker （1:30）
    - 1. 什么是docker？
        - 0.给coworker完全一致的环境，相同的文件使用
        - 1 .docker 四个关键的feature
            - 
                
                ![https://api2.mubu.com/v3/document_image/e1be4494-4e3e-4f86-b69f-dada5e9018cd-14086676.jpg](https://api2.mubu.com/v3/document_image/e1be4494-4e3e-4f86-b69f-dada5e9018cd-14086676.jpg)
                
            - docker image: 一个含有所有需要的操作系统，比如Ubuntu系统里装好Python等等
            - docker container在docker image 基础上建立读写
                - 不能再image文件上run，可以在container中run
                    
                    ![https://api2.mubu.com/v3/document_image/e66d67ac-e17a-4e87-9d34-f291f050faaa-14086676.jpg](https://api2.mubu.com/v3/document_image/e66d67ac-e17a-4e87-9d34-f291f050faaa-14086676.jpg)
                    
                - 不同的container，包含适用不同的环境
                    
                    ![https://api2.mubu.com/v3/document_image/d02dc1ca-73ba-496f-bab7-f7c0633cad9a-14086676.jpg](https://api2.mubu.com/v3/document_image/d02dc1ca-73ba-496f-bab7-f7c0633cad9a-14086676.jpg)
                    
            - docker engine: 就是我们装的docker客户端
            - docker registry service: 类似github, 可以让上传和下载docker image给别人
        - 2. Devops , DE 用的多
            - docker可以防止环境的不同导致开放测试到部署应用出现问题
                
                ![https://api2.mubu.com/v3/document_image/979a7ce6-17d1-44c5-8fb1-6b892c6e93f0-14086676.jpg](https://api2.mubu.com/v3/document_image/979a7ce6-17d1-44c5-8fb1-6b892c6e93f0-14086676.jpg)
                
        - 3. 与VM概念相似，但实际不同
            - vm 的开销很大，guest OS和Hypervisor 都需要占几十个G的内存， docker只需要装需要APP 的bins和libs 就行了，系统开销会小很多
                
                ![https://api2.mubu.com/v3/document_image/c2787d0c-c2c5-4f42-bb32-121308d19f61-14086676.jpg](https://api2.mubu.com/v3/document_image/c2787d0c-c2c5-4f42-bb32-121308d19f61-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/a7b912d8-8c68-4d64-8867-6cd7d575620f-14086676.jpg](https://api2.mubu.com/v3/document_image/a7b912d8-8c68-4d64-8867-6cd7d575620f-14086676.jpg)
                
            - 我们下载community版本就可以了
                
                ![https://api2.mubu.com/v3/document_image/27678c9f-ccc0-4252-bdc8-e0e6e6db6891-14086676.jpg](https://api2.mubu.com/v3/document_image/27678c9f-ccc0-4252-bdc8-e0e6e6db6891-14086676.jpg)
                
    - 2. docker实际操作
        - 与git语法是很相似的
        - 回看老师PDF 课件图文步骤解释很详细
- 3. Dockerfile
    - 进行版本控制,保证环境的一致性
        
        ![https://api2.mubu.com/v3/document_image/59caad93-de8b-466e-bff1-05ab1284b868-14086676.jpg](https://api2.mubu.com/v3/document_image/59caad93-de8b-466e-bff1-05ab1284b868-14086676.jpg)
        
    - 可以写的非常复杂， FROM等命令一定要大写
        
        ![https://api2.mubu.com/v3/document_image/be833e3f-b8d1-41bd-bae6-9c4381a9dc56-14086676.jpg](https://api2.mubu.com/v3/document_image/be833e3f-b8d1-41bd-bae6-9c4381a9dc56-14086676.jpg)
        
    - example
        
        ![https://api2.mubu.com/v3/document_image/f126efbb-d44e-4933-acdc-12077759db6f-14086676.jpg](https://api2.mubu.com/v3/document_image/f126efbb-d44e-4933-acdc-12077759db6f-14086676.jpg)
        
        ![https://api2.mubu.com/v3/document_image/7965588d-53b0-4b90-9125-7f1c488d6f14-14086676.jpg](https://api2.mubu.com/v3/document_image/7965588d-53b0-4b90-9125-7f1c488d6f14-14086676.jpg)
        
        - 工业中不会用$ path 本地路径,将requirements.txt cp到docker container路径中
        - apt-get is for installing, upgrading, and cleaning packages, [https://itsfoss.com/apt-get-linux-guide/](https://itsfoss.com/apt-get-linux-guide/)
        - APT (advanced package tool) :[https://wiki.debian.org/Apt](https://wiki.debian.org/Apt)
        - apt-transport-https - APT transport for downloading via the HTTP Secure protocol (HTTPS)
- 4. Repository
    - 1. UI create repository
        - 
            
            ![https://api2.mubu.com/v3/document_image/6a058b57-b323-4db8-a0b6-c5e3c6fd5c1c-14086676.jpg](https://api2.mubu.com/v3/document_image/6a058b57-b323-4db8-a0b6-c5e3c6fd5c1c-14086676.jpg)
            
    - 2. local docker login and push
        - 上传到repo
            
            ![https://api2.mubu.com/v3/document_image/0c42c0ca-94ce-4b8e-aad5-fab37c5b29ee-14086676.jpg](https://api2.mubu.com/v3/document_image/0c42c0ca-94ce-4b8e-aad5-fab37c5b29ee-14086676.jpg)
            
    - 3. 从docker中cp 文件到本地
        - 
            
            ![https://api2.mubu.com/v3/document_image/feeaf98c-8001-42d2-bc06-5ace39ce3e37-14086676.jpg](https://api2.mubu.com/v3/document_image/feeaf98c-8001-42d2-bc06-5ace39ce3e37-14086676.jpg)
            
- 5. docker完整代码 [https://www.notion.so/docker-9e5410a0c25d4518af0a3144d5b14514](https://www.notion.so/docker-9e5410a0c25d4518af0a3144d5b14514)