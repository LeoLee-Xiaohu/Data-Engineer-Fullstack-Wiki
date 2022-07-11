# Lecture 26 C1 Project bootcamp

- 1. Infrastructure as Code
    - 公司是以一种code的方式建立infrastructure
    - 用code去define我们的infrastructure，而不是去console里建立infras
        - 优点，不用手动建立infrastructure
            
            ![https://api2.mubu.com/v3/document_image/ce8ea002-d49e-420c-8309-7373b896ca5d-14086676.jpg](https://api2.mubu.com/v3/document_image/ce8ea002-d49e-420c-8309-7373b896ca5d-14086676.jpg)
            
    - 建立infrastructure的形式
        - CloudFormation最常用
            
            ![https://api2.mubu.com/v3/document_image/76633f35-c226-453c-be7f-39a2aeecb88d-14086676.jpg](https://api2.mubu.com/v3/document_image/76633f35-c226-453c-be7f-39a2aeecb88d-14086676.jpg)
            
    - 什么是cloudFormation
        - 用template 写需要的资源，如EC2， s3
            
            ![https://api2.mubu.com/v3/document_image/5f9501b6-c88a-4705-9261-b36b741f7171-14086676.jpg](https://api2.mubu.com/v3/document_image/5f9501b6-c88a-4705-9261-b36b741f7171-14086676.jpg)
            
        - stack ： a group of resources
    - couldformation deployed 的流程lifecycle
        - 最主要的是template
            
            ![https://api2.mubu.com/v3/document_image/8c48a9fa-040c-4f8f-ad7c-cf548cc79ea0-14086676.jpg](https://api2.mubu.com/v3/document_image/8c48a9fa-040c-4f8f-ad7c-cf548cc79ea0-14086676.jpg)
            
    - increment changes
        - 每建一个template，会建一个stack
            
            ![https://api2.mubu.com/v3/document_image/11dec338-eba0-407d-8889-ca81984c3c2a-14086676.jpg](https://api2.mubu.com/v3/document_image/11dec338-eba0-407d-8889-ca81984c3c2a-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/144b8416-f4c6-4957-994a-90a8f7857ea0-14086676.jpg](https://api2.mubu.com/v3/document_image/144b8416-f4c6-4957-994a-90a8f7857ea0-14086676.jpg)
            
- 2. CI/CD Pipeline
    - 概念
        - 
            
            ![https://api2.mubu.com/v3/document_image/e1ed7bdd-f2af-42cc-b463-8e3f8bdeaaab-14086676.jpg](https://api2.mubu.com/v3/document_image/e1ed7bdd-f2af-42cc-b463-8e3f8bdeaaab-14086676.jpg)
            
    - CICD步骤
        - source code， build（把code package化）， test， deploy
            
            ![https://api2.mubu.com/v3/document_image/f31e03fb-b682-415b-a92b-08e444e8f1f2-14086676.jpg](https://api2.mubu.com/v3/document_image/f31e03fb-b682-415b-a92b-08e444e8f1f2-14086676.jpg)
            
    - CICD目的
        - 不需要很多manual work，快，高效
            
            ![https://api2.mubu.com/v3/document_image/df58c670-e25a-4593-9aaf-e7ece1ffab23-14086676.jpg](https://api2.mubu.com/v3/document_image/df58c670-e25a-4593-9aaf-e7ece1ffab23-14086676.jpg)
            
- 3. Github Actions
    - 概念
        - 
            
            ![https://api2.mubu.com/v3/document_image/7d09144c-d626-4435-bcdc-261965ae75f1-14086676.jpg](https://api2.mubu.com/v3/document_image/7d09144c-d626-4435-bcdc-261965ae75f1-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/a56cb5bd-f112-4ec3-80c8-0593b6ca2771-14086676.jpg](https://api2.mubu.com/v3/document_image/a56cb5bd-f112-4ec3-80c8-0593b6ca2771-14086676.jpg)
            
    - create a workflow
        - workflow结构
            
            ![https://api2.mubu.com/v3/document_image/1100ef93-c913-417c-bd63-c42014da6302-14086676.jpg](https://api2.mubu.com/v3/document_image/1100ef93-c913-417c-bd63-c42014da6302-14086676.jpg)
            
        - git action yaml 文件重要的概念：
            - name
                
                ![https://api2.mubu.com/v3/document_image/4177aa8a-24de-4166-ab1d-d4f4b5ebf82e-14086676.jpg](https://api2.mubu.com/v3/document_image/4177aa8a-24de-4166-ab1d-d4f4b5ebf82e-14086676.jpg)
                
            - on: push。 define 的event
            - jobs：触发了event，git actions 要跑的东西
                
                ![https://api2.mubu.com/v3/document_image/a3c1bbce-0878-4325-9cff-21c31ce7cf06-14086676.jpg](https://api2.mubu.com/v3/document_image/a3c1bbce-0878-4325-9cff-21c31ce7cf06-14086676.jpg)
                
            - Env ， 是自定义的变量，让jobs运行
                
                ![https://api2.mubu.com/v3/document_image/59769681-ebfd-4864-9f48-c49bb77ff7c4-14086676.jpg](https://api2.mubu.com/v3/document_image/59769681-ebfd-4864-9f48-c49bb77ff7c4-14086676.jpg)
                
- 4. Project initiate
- 5. infrastructure as code 实验git action
    - Cloud formation template
        - 
            
            ![https://api2.mubu.com/v3/document_image/37c147ee-2230-4e4d-9446-63744144674b-14086676.jpg](https://api2.mubu.com/v3/document_image/37c147ee-2230-4e4d-9446-63744144674b-14086676.jpg)
            
    - 1:50:00 main.yaml讲解